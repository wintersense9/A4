# 实验网络基础搭建（最简教学版）

> 与 `factory_network/lab/` 的区别：那里是完整版（netplan 持久化 + systemd 服务）；
> **这里是最小教学版**——只用最基础的 `ip` / `sysctl` / `iptables` 命令，配好马上生效，
> 目的是让你看懂**每一条命令在干什么**。重启后配置会丢，重新跑一遍脚本即可（这也正好练手）。

## 0. 这套实验只用到 5 类基本操作

| # | 操作 | 命令族 | 在哪台机器上用 |
|---|---|---|---|
| 1 | 查看网卡 | `ip -br link` | 每台 |
| 2 | 给网卡配 IP | `ip addr add` | 每台 |
| 3 | 配默认网关 | `ip route replace default via` | 普通主机 |
| 4 | 开启转发 | `sysctl -w net.ipv4.ip_forward=1` | 只有路由器 |
| 5 | 防火墙规则 | `iptables` | 只有路由器 |
| 6 | 验证连通 | `ping` / `curl` | 每台 |

## 1. 拓扑（4 台虚拟机）

VirtualBox 的**"内部网络"**相当于一根只存在于虚拟世界的网线：网卡接到**同一个名字**的内部网络，
就在同一个二层广播域里。我们建 3 个内部网络，一台 4 网卡（实际用 3 块）的 VM 当路由器：

```
                 +----------------------------+
                 |  router（Ubuntu，3块网卡）  |
                 |  10.0.10.1  10.0.30.1  10.0.40.1
                 +------+----------+---------+
        lab-robot      |          |         |  lab-office
        (机器人网段)     |          |         |  (办公网段)
   +---------+---------+  lab-server     +--+----------+
   | robot1                 (服务器网段) | office-pc   |
   | 10.0.10.101           +------------+ 10.0.40.100  |
   +-----------------------+ dispatch    +-------------+
                           | 10.0.30.10  |
                           +-------------+
```

**VirtualBox 设置**（每台 VM：设置 → 网络 → 网卡 → 连接方式选"内部网络"→ 界面名称照抄）：

| VM | 网卡1 | 网卡2 | 网卡3 | 装好后跑 |
|---|---|---|---|---|
| router | lab-robot | lab-server | lab-office | `sudo bash router.sh` |
| dispatch | lab-server | — | — | `sudo bash dispatch.sh` |
| robot1 | lab-robot | — | — | `sudo bash robot.sh` |
| office-pc | lab-office | — | — | `sudo bash office.sh` |

系统装 Ubuntu Server 22.04/24.04 最小安装（勾选 OpenSSH Server）即可。

---

## 2. 每台机器的 Ubuntu 操作 + 含义

### 2.1 第一步（每台都要）：确认网卡叫什么名

```bash
ip -br link
```

**含义**：`ip` 是 Linux 管网络的总工具；`link` 指网卡这一层（二层）；`-br` 是 brief 精简输出。
你会看到类似：

```
enp0s3    UP
enp0s8    UP
enp0s9    UP
```

`enp0s3` 就是网卡名（en=以太网，p0s3=主板第 0 总线第 3 槽位——正好对应 VirtualBox 的"网卡1"）。
**如果你的名字不一样，把脚本里的 `enp0s3` 等改成你实际看到的名字。**

> 怎么知道哪块网卡接了哪个内部网络？按添加顺序：网卡1=enp0s3、网卡2=enp0s8、网卡3=enp0s9。
> 拿不准就在 router 上 `ip link set enp0s3 down` 再 `up`，看 VirtualBox 里哪块网卡断了线。

### 2.2 router（路由器）—— `router.sh` 逐条解释

```bash
ip addr flush dev enp0s3
ip addr add 10.0.10.1/24 dev enp0s3
ip link set enp0s3 up
```

| 命令 | 含义 |
|---|---|
| `ip addr flush dev enp0s3` | 把这块网卡上**已有的 IP 全部清掉**（防止旧配置干扰） |
| `ip addr add 10.0.10.1/24 dev enp0s3` | 给网卡配上 IP `10.0.10.1`。`/24` 表示掩码前 24 位是网络位（=255.255.255.0），即这台机器认为 `10.0.10.x` 都是"本段邻居"，直接发；别的网段才找网关 |
| `ip link set enp0s3 up` | **启用**这块网卡（相当于插上网线打开开关） |

三块网卡重复三次，分别配 `10.0.10.1/24`（lab-robot）、`10.0.30.1/24`（lab-server）、`10.0.40.1/24`（lab-office）。
**配完后这台机器就是三个网段共同的网关。**

```bash
sysctl -w net.ipv4.ip_forward=1
```

**含义**：这是本实验最关键的一条。Linux 默认收到"目的地不是自己"的包会直接扔掉（它默认是主机，不是路由器）。
`sysctl` 是改内核运行参数的工具；`net.ipv4.ip_forward=1` 打开 IPv4 转发开关——**从此这台机器收到别人的包会帮忙转发，它就变成了路由器**。

```bash
iptables -F FORWARD
iptables -P FORWARD DROP
iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -i enp0s3 -o enp0s8 -p tcp -d 10.0.30.10 --dport 8080 -j ACCEPT
iptables -A FORWARD -i enp0s3 -o enp0s8 -p icmp -j ACCEPT
```

| 命令 | 含义 |
|---|---|
| `iptables -F FORWARD` | 清空"转发链"（FORWARD = 经过本机转发的包）上的旧规则 |
| `iptables -P FORWARD DROP` | 转发链**默认策略 = 丢弃**。默认全不通，再逐条放行——这就是 ACL 的思想 |
| `-m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT` | 放行**已建立连接的返程包**。没有这条，机器人发出的请求能到服务器，但回复回不来（防火墙是有方向的） |
| `-i enp0s3 -o enp0s8 -p tcp -d 10.0.30.10 --dport 8080 -j ACCEPT` | 只放行：从机器人网卡进、从服务器网卡出、目标是调度服务器 8080 端口的 TCP（机器人上报心跳的通道） |
| `... -p icmp -j ACCEPT` | 再放行 ICMP（ping），方便排查 |

**注意没有给 office 网卡写任何 ACCEPT** → 办公网段发的包全部命中默认 DROP，被隔离。这就是 Goal 2 的最小实现。

### 2.3 dispatch（服务器）—— `dispatch.sh` 逐条解释

```bash
ip addr flush dev enp0s3
ip addr add 10.0.30.10/24 dev enp0s3
ip link set enp0s3 up
ip route replace default via 10.0.30.1
```

前三条同 router（配 IP、启用网卡）。第四条是新操作：

| 命令 | 含义 |
|---|---|
| `ip route replace default via 10.0.30.1` | 设**默认路由**：凡是目的地不在本段（不是 10.0.30.x）的包，都交给网关 10.0.30.1（router）去转。`replace` = 有就改、没有就加。普通主机只需要这一条路由 |

**普通主机和路由器的区别就在这两条**：主机要"默认网关"，不开转发；路由器不开默认网关（它自己就是网关），要开转发。

然后跑调度服务器（脚本在 `factory_network/dispatch/dispatch_server.py`，先用共享文件夹或 scp 拷过来）：

```bash
python3 dispatch_server.py --host 0.0.0.0 --port 8080
```

`--host 0.0.0.0` 的含义：监听本机**所有**网卡（不写就只监听 127.0.0.1，别的机器连不上）。

### 2.4 robot1（机器人）—— `robot.sh`

```bash
sudo bash robot.sh        # 配 10.0.10.101，网关 10.0.10.1，最后自动 ping 服务器验证
sudo bash robot.sh 102    # 第二台机器人传 102，自动配成 10.0.10.102
```

命令和 dispatch 完全一样（配 IP + 网关），只是地址在机器人网段。脚本最后自动执行：

```bash
ping -c3 -W2 10.0.30.10
```

`-c3` = 发 3 个包；`-W2` = 每个最多等 2 秒。**通了说明：网卡配对了、网关配对了、router 的转发和 ACL 都工作了**——一条 ping 验证了四层配置。

### 2.5 office-pc（办公机）—— `office.sh`

同样只配 IP + 网关（10.0.40.100，网关 10.0.40.1）。然后**故意验证"不通"**：

```bash
ping -c3 -W2 10.0.10.101          # 期望：超时（不通）——被 router 的默认 DROP 拦下
ping -c3 -W2 10.0.40.1            # 期望：通（自己网段的网关是通的）
curl -m3 http://10.0.30.10:8080/health   # 期望：超时
```

**"不通"就是这个演示要的结果**：证明办公网络碰不到机器人（Goal 2）。对比实验：在 router 上把默认策略临时改成放行 `sudo iptables -P FORWARD ACCEPT`，office 立刻就能 ping 通机器人——改回来又断。这个开/关对比非常有说服力。

---

## 3. 验证清单

| # | 在哪 | 命令 | 期望 |
|---|---|---|---|
| 1 | router | `ip -br addr` | 看到三个 10.0.x.1 |
| 2 | router | `sysctl net.ipv4.ip_forward` | 输出 `= 1` |
| 3 | router | `iptables -L FORWARD -n -v` | 看到规则列表，DROP/ACCEPT 计数在涨 |
| 4 | dispatch | `ss -lntp \| grep 8080` | python3 在监听 0.0.0.0:8080 |
| 5 | robot1 | `ping -c3 10.0.30.10` | 通 |
| 6 | robot1 | `curl http://10.0.30.10:8080/health` | 返回 JSON |
| 7 | office | `ping -c3 10.0.10.101` | **不通**（隔离生效） |
| 8 | office | `ping -c3 10.0.40.1` | 通 |

## 4. 命令含义速查表（背这 12 条就够）

| 命令 | 一句话含义 |
|---|---|
| `ip -br link` | 看有哪些网卡、开没开 |
| `ip -br addr` | 看网卡上配了什么 IP |
| `ip route` | 看路由表（包会往哪走） |
| `ip addr add <IP/掩码> dev <网卡>` | 配 IP |
| `ip link set <网卡> up` | 启用网卡 |
| `ip route replace default via <网关>` | 设默认网关 |
| `sysctl -w net.ipv4.ip_forward=1` | 开启转发（变路由器） |
| `iptables -F FORWARD` | 清空转发规则 |
| `iptables -P FORWARD DROP` | 转发默认丢弃 |
| `iptables -A FORWARD ... -j ACCEPT` | 加一条放行规则 |
| `ping -c3 <IP>` | 测连通（3 个包） |
| `ss -lntp` | 看本机开了哪些监听端口 |

## 5. 弄乱了怎么办

```bash
ip addr flush dev enp0s3      # 清掉这块网卡的 IP，重配
sudo iptables -P FORWARD ACCEPT && sudo iptables -F FORWARD   # 防火墙全放开（排查时用）
reboot                         # 终极办法：重启后本套配置全部消失，从头再来
```

## 6. 下一步

理解这批命令后，再看 `factory_network/lab/`（netplan 持久化版）和
`factory_network/configs/`（真实设备语法版）就会发现：**做的事情一模一样，只是写法更工程化**。
