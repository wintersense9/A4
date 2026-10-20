# NBA 与市场营销方向毕业设计资料汇编

**主题定位：数据科学视角下的 NBA 市场营销研究**
**内容构成：研究背景 → 文献资料 → 数据集清单 → 研究计划与研究问题（多方向候选）→ 方向选择建议 → 链接汇总**

> 使用说明：本文件为"选题资料包"，不是最终开题报告。第四部分给出 4 个可选研究方向（A/B/C/D）加 1 个拓展方向，每个方向都配套了研究问题、假设、数据、方法与预期贡献，请先浏览第五部分的"方向选择对照表"，挑出你最终要做的方向，再据其展开正式开题报告。

---

## 目录

1. [第一部分　研究背景与选题定位](#第一部分研究背景与选题定位)
2. [第二部分　文献资料汇编](#第二部分文献资料汇编)
3. [第三部分　数据集清单（Kaggle 为主 + 外部补充源）](#第三部分数据集清单kaggle-为主--外部补充源)
4. [第四部分　研究计划与研究问题（多方向候选）](#第四部分研究计划与研究问题多方向候选)
5. [第五部分　方向选择建议与对照表](#第五部分方向选择建议与对照表)
6. [第六部分　参考文献与数据源链接汇总](#第六部分参考文献与数据源链接汇总)

---

## 第一部分　研究背景与选题定位

### 1.1 为什么"NBA + 市场营销 + 数据科学"是一个成立且好做的题目

NBA 是目前全球商业化程度最高、数据公开程度最好的职业体育联盟之一，三个条件同时具备，使它成为"体育营销 + 数据科学"交叉研究的理想样本：

1. **商业规模大、营销议题真实**。联盟与球队的收入来源覆盖门票（gate revenue）、转播版权、赞助、 merchandising（球衣/周边）、数字订阅、NFT 与社交媒体变现等。球队估值已达数十亿美元量级（2026 年 Sportico/Forbes 榜单中金州勇士估值约 145 亿美元居首），营销决策的"钱味"很浓，研究结论具备现实价值。
2. **数据可得性极好**。球员/球队逐场与赛季统计数据、投篮位置数据（shot chart）、上座率与球馆容量、薪资合同、伤病史、社交媒体热度等均有公开来源。Kaggle 上以 "nba" 为关键词可检索到 700+ 个数据集，Basketball-Reference、官方 `nba_api`、Sportradar 等提供补充。
3. **数据科学方法有充分的用武之地**。问题天然包含回归/分类/聚类/时间序列/文本情绪分析/NLP/因果推断等，既能做"预测任务"（predictive），也能做"归因解释"（explanatory），适合作为本科/硕士毕业设计的深度。

### 1.2 核心逻辑链条（可作为全文主线）

> **球迷参与（fandom & engagement）→ 需求（attendance / viewership / merchandise）→ 收入与品牌价值（revenue & franchise value）→ 营销策略（pricing / sponsorship / content / CRM）**

数据科学在这条链上的切入点是：**用可量化的行为与内容数据，去预测、解释、优化每一个环节的营销结果**。四个候选研究方向本质上都是这条主线在不同环节上的"切段"。

### 1.3 与本选题相关的现实趋势（可作为研究动机）

- NBA 已与 AWS、Microsoft 等合作建设 AI 驱动的实时数据与个性化内容平台（ticket/内容推荐、实时进阶数据），"数据驱动的球迷体验"成为联盟级战略。
- NBA 中国市场的数字化营销持续加码（赛事直播、短视频集锦、社媒互动、中国赛期间的 88VIP 会员权益、AI 篮球助手等），为"跨文化/跨市场"视角提供了独特话题。
- 学界近年热点集中在：球迷忠诚度与"bandwagon fans"预测、社交媒体情绪与收视/参与预测、动态票务定价、赞助 ROI 度量、生成式 AI 对体育营销的重塑。

---

## 第二部分　文献资料汇编

> 说明：以下按主题分组。每篇给出【标题】【来源/链接】【方法】【主要发现】【对本研究的可用之处】。标注为"（综述/概念性）"的文献偏理论框架，适合放进文献综述；标注"（实证/建模）"的适合作为方法学参照。

### 主题 A　球迷参与、上座率与收视率预测（对应方向 A）

**A1. Buzz to Broadcast: Predicting Sports Viewership Using Social Media Engagement**（实证/建模）
- 来源：arXiv，https://arxiv.org/pdf/2412.10298v1
- 方法：基于回归的方法，用社交媒体指标（发帖量、评论数、比赛比分、基于 TextBlob / VADER 的情绪得分）预测体育赛事收视人数。
- 主要发现：经迭代优化（聚焦主流体育板块、加入类别特征、按运动项目处理离群值）后，模型达到 R² ≈ 0.99、MAE ≈ 127 万人；但对小规模赛事表现有限，提示数据不平衡问题。
- 可用之处：**"社媒热度 → 收视/关注度"的典型建模范式**；可直接迁移到 NBA 场景，也是方向 A 的方法论基石。

**A2. Jump off the Bandwagon? Characterizing Bandwagon Fans' Future Loyalty in Online NBA Fan Communities**（实证/建模）
- 来源：arXiv，https://arxiv.org/html/2401.11629
- 方法：基于在线 NBA 球迷社区（论坛）数据，构造**活动特征（activity）与网络特征（network）**，预测"跟风球迷"下一个赛季是否继续保持忠诚。
- 主要发现：活动与网络特征能有效预测下一赛季忠诚状态，相比基线 **AUC 提升约 16%、F1 提升约 19%**；且活动特征的预测力强于网络特征。
- 可用之处：方向 A 中"球迷忠诚/流失预测"的现成标签定义与特征工程思路。

**A3. Cheering for your country: prediction of attendance at international football games using machine learning techniques**（实证/建模）
- 来源：Applied Economics（Taylor & Francis），https://www.tandfonline.com/doi/pdf/10.1080/00036846.2026.2618091
- 要点：文中综述并引用了体育上座率预测的关键结论——Şahin & Uçar (2022) 对 NBA、NFL、MLB 的研究发现**球队战绩与比赛重要性是最有影响力的上座率驱动因素，梯度提升（Gradient Boosting）预测最准**；King (2017) 对 NBA 的研究识别出**主队人气与比赛日因素**，随机森林精度最高。
- 可用之处：**直接证明"NBA 上座率预测"是一个已有方法学基础、可复现且有对比基准的问题**，非常适合毕业设计。

**A4. Quantifying Fan Engagement and Sentiment During Live Games Via Social Media Analytics**（应用/案例）
- 来源：Samford University, Center for Sports Analytics，https://www.samford.edu/sports-analytics/fans/2026/Quantifying-Fan-Engagement-and-Sentiment-During-Live-Games-Via-Social-Media-Analytics
- 要点：体育组织正在把"客户情绪预测"逻辑迁移到球迷数据上，用社媒分析在比赛中量化参与度与情绪。
- 可用之处：方向 A/E 的行业实践证据；情绪指标体系设计参考。

**A5. Evaluating Machine Learning Algorithms for Predictive Modeling of Large-scale Event Attendance**（实证/建模）
- 来源：International Journal of Computer and Information System (IJCIS)，https://www.ijcis.net/index.php/ijcis/article/view/249/211
- 要点：集成方法（Gradient Boosting Regressor、XGBoost）在大型活动上座率预测中取得最低 MAE、最高 R²，优于线性模型。
- 可用之处：算法选型与"线性 vs 集成"对比实验的参考文献。

### 主题 B　球队价值、营收与经营决策（对应方向 D）

**B1. Examination of National Basketball Association (NBA) Team Values Based on Dynamic Linear Mixed Models**（实证/建模）
- 来源：PLOS ONE（PMC），https://pmc.ncbi.nlm.nih.gov/articles/PMC8211228/
- 方法：先做相关分析，再用 K-means 与层次聚类识别球队相似性，最后用**动态线性混合模型（dynamic linear mixed models）**分析球队价值的决定因素，以 AIC 选模。
- 主要发现：球队价值的显著决定因素包括**收入（revenue）、GDP、夺冠（championship）、人口（population）、关键球员（key player）**；**失误总数对球队价值有负向影响**；模型 R² ≈ 0.974。
- 可用之处：方向 D 的**方法学核心参照**（面板/混合效应建模），变量体系可直接借鉴。

**B2. Run Up the Score, and the Profits: Analysis of NBA Revenue Using Gameplay Statistics as Predictors of Higher Revenue**（实证/建模）
- 来源：UNLV Spectra，https://oasis.library.unlv.edu/cgi/viewcontent.cgi?article=1038&context=spectra
- 方法：对 NBA 球队真实营收与比赛统计数据做**固定效应回归（fixed effect regression）**。
- 主要发现：以"Run and Gun"为代表的**快节奏打法与更高营收相关**，对球队前台（front office）有明确战略含义。
- 可用之处：**"打法风格 → 营销/商业结果"**的独特切入点，属方向 D 的创新变体。

**B3. A Rolling-Horizon Stochastic Optimization Framework for NBA Franchise Management with Distributionally Robust Risk Constraints**（方法学/前瞻）
- 来源：arXiv，https://arxiv.org/html/2604.06548
- 要点：构建**多层级（球员级、比赛级）多源数据集**，用滚动时域随机优化 + 分布鲁棒风险约束做球队管理决策（以纽约尼克斯为案例）。
- 可用之处：可作为"进阶/加分"方法方向；其**多源数据整合思路**对方向 A/D 的数据设计有启发。

**B4. The NBA's Revenue Sharing Scorecard: Determining Success for Small-Market Franchises**（实证/案例）
- 来源：Boston College，https://ur.bc.edu/system/files/2025-04/bc-ir102222.pdf
- 要点：使用**Ticket Price Model（也称 Revenue Model，票务价格/收入计量模型）**预测平均票价；指出**门票收入约占球队总收入的 30%–40%**。
- 可用之处：把"门票收入占比"这一量化事实写进研究背景；票务建模的经典做法。

### 主题 C　票务定价与动态定价（对应方向 C）

**C1. Dynamic Pricing for Sports Event Ticket**（实证/建模）
- 来源：ICDATA 2020（作者 Matthew A. Lanham 团队），https://matthewalanham.github.io//Students/2020/ICDATA20_Dynamic%20Pricing%20for%20Sports%20Event%20Ticket.pdf
- 方法：用**随机森林**建立票价/需求预测模型，再以迭代法对单张票在不同时点做价格优化（以期望收入最大化为目标）；配套 Tableau 看板。
- 可用之处：方向 C 的**完整"需求预测 + 价格优化"范式**，可 1:1 迁移到 NBA。

**C2. Dynamic Pricing Models for Ticket Sales Managers**（行业方法）
- 来源：DataCalculus，https://datacalculus.com/en/blog/spectator-sports/ticket-sales-manager/dynamic-pricing-models-for-ticket-sales-managers
- 要点：动态定价的实施流程——市场细分、需求预测建模、模拟环境测试、KPI 持续监测与参数调优。
- 可用之处：方向 C 的**落地流程与评价指标（KPI）设计**参考。

**C3. Analysis of the Tactics of NBA Pricing Tickets**（综述/分析）
- 来源：Semantic Scholar，https://pdfs.semanticscholar.org/cdde/6bfaf03ab522d296e075eaaec312666d57bf.pdf
- 要点：票价随"离球场中心的接近程度"上升；大城市市场球队定价高于小市场球队；梳理了 NBA 常见分级定价策略。
- 可用之处：定价策略背景与描述性分析素材。

**C4. What Variables Predict Ticket Prices of NBA Franchises? A Review**（综述）
- 来源：Semantic Scholar，https://pdfs.semanticscholar.org/3539/69e7dfb64dd09314323bec4b01d1eae5a14e.pdf
- 要点：从**需求侧**与**供给侧**两类因素梳理 NBA 票价预测变量，并映射球队可用的攫取消费者剩余的营销策略（动态定价/价格歧视/垄断利润）。
- 可用之处：方向 C 的**变量字典**（自变量清单）来源。

**C5. Examining the Effectiveness of Different Ticket Bundling Strategies: An Example of the NBA**（实证/博士论文）
- 来源：University of Georgia，https://openscholar.uga.edu/record/11763/files/chen_kuan-chou_201308_phd.pdf
- 要点：研究 NBA 套票/捆绑销售策略的效果，含历年平均票价变化数据（如 2009-10 赛季 $48.90，为 2001-02 以来首降）。
- 可用之处：方向 C 的"促销/捆绑"策略实验设计参考。

### 主题 D　赞助、消费者行为与营销效果（营销侧理论）

**D1. Searching for the "Holy Grail" of Sponsorship-Linked Marketing: A Generalizable Sponsorship ROI Model**（实证/建模）
- 来源：arXiv，https://arxiv.org/pdf/2305.09473v1
- 方法：用 **5,800+ 条赞助记录**构建模型，以**赞助方是否续约（renewal）作为正 ROI 的代理变量**。
- 可用之处：**赞助 ROI 度量的经典思路**——"用行为（续约）代理财务结果"，对缺乏公开财务数据的毕业设计极其实用。

**D2. Consumer Split Identification: The Case of Sponsorship**（实证）
- 来源：Journal of Sport Management, 40(4), 2026，https://journals.humankinetics.com/view/journals/jsm/40/4/article-p315.xml
- 要点：实验显示球迷对**带赞助商胸标（sponsor patch）球衣的购买意愿**显著受赞助品牌影响（如 Patagonia vs ExxonMobil 差异显著，t(288)=6.97, p<.001）。
- 可用之处：球衣赞助 → 购买意愿的实证证据，方向 B/D 的营销变量依据。

**D3. The Influence of the NBA Star Endorsers' Credibility and Brand Image on Purchase Intention（以林书豪为例）**（实证）
- 来源：European Journal of Management and Marketing Studies，https://oapub.org/soc/index.php/EJMMS/article/view/623
- 方法：描述统计、信度分析、独立样本 t 检验、Pearson 相关、回归分析。
- 主要发现：**球星代言人可信度显著影响购买意愿，其中"专业形象"影响大于"可靠性"；品牌形象显著影响购买意愿，其中"象征性"影响更大**。
- 可用之处：**"球星影响力（credibility）→ 消费者购买意愿"**的成熟量表与结论，是方向 B 的理论支点。

**D4. The Effect of Promotional Bundles on Purchase Intent for High/Medium/Low-Vested Sports Tourists（NBA 夏洛特黄蜂）**（实证）
- 来源：Longdom（Journal of Tourism & Hospitality 系列），https://www.longdom.org/open-access-pdfs/the-effect-of-promotional-bundles-on-purchase-intent-for-high-mediumand-low-vested-sports-tourists-segments-within-the-context-of-2167-0269-1000275.pdf
- 方法：现场问卷 + **MANOVA**。
- 主要发现：**狂热型与聚焦型体育游客最偏好"含游览/景点元素"的套票，社交型游客对任何套票购买意愿都低**——即**球迷细分（market segmentation）决定促销有效性**。
- 可用之处：**球迷分层（segmentation）**这一营销核心概念的操作化示例，是方向 A/D 的聚类分析动机。

**D5. Beyond Purchase Intention in Sports Sponsorship: Measuring Brand Equity Using Best-Worst Scaling**（实证）
- 来源：Macquarie University 研究库，https://researchers.mq.edu.au/en/publications/beyond-purchase-intention-in-sports-sponsorship-an-alternative-ap/
- 要点：用 **BWDCE（best-worst 离散选择实验）**测量赞助对品牌资产的影响，以**价格溢价（price premium）与市场份额**替代"购买意愿"作为结果变量。
- 可用之处：**如何在缺少一手问卷时，用行为/市场数据度量品牌资产**。

### 主题 E　数据科学/AI 在体育营销中的整体应用（综述，用于第一、二章背景）

**E1. AI-Powered Sports Marketing: Predictive Insights, Consumer Behavior, and Global Brand Strategy**（综述/概念）
- 来源：Semantic Scholar，https://pdfs.semanticscholar.org/39ab/1b8e0d887d3d26992383400663c6a30cd06b.pdf
- 要点：系统阐述 AI（机器学习、大数据、NLP）如何提升**营销效率、赞助估值、消费者定向**，实现实时球迷参与与表现分析；同时指出**数据隐私、算法偏见、透明度**等伦理问题。
- 可用之处：全文引言与文献综述的"宏观框架"来源；可作为"研究意义"的论据。

**E2. Algorithmic Fandom: How Generative AI Is Reshaping Sports Marketing, Fan Engagement, and the Integrity of Sport**（综述/概念）
- 来源：PMC，https://pmc.ncbi.nlm.nih.gov/articles/PMC12094936/
- 要点：生成式 AI 推动**超个性化球迷参与、实时内容分发、数据驱动商业战略**，并带来伦理、心理与竞技诚信层面的复杂问题。
- 可用之处：讨论"研究局限与伦理"章节的引用来源。

**E3. The Role of Digital Marketing in Promoting Sports Marketing: Taking the Changes in NBA Marketing Methods as An Example**（综述/案例）
- 来源：Semantic Scholar，https://pdfs.semanticscholar.org/113b/cb0784779c4775809fc8c59c86600aa65a8c.pdf
- 要点：以 NBA 为例分析数字营销如何推动体育营销；提及**约 87% 的 NBA 球员使用至少一个社交媒体、其中约 70% 使用 Twitter**，社媒把"观赛"变成"参与"。
- 可用之处：**直接以 NBA 为对象的数字营销文献**，方向 A/B 的背景引用首选。

**E4. Sports NFTs as Multidimensional Digital Assets: Online Public Discourse and Strategic Implications from NBA Social Big Data**（实证/文本分析）
- 来源：Taylor & Francis，https://www.tandfonline.com/doi/full/10.1080/2...（检索所得为摘要页）
- 要点：基于 NBA 社交大数据的公开话语分析，讨论体育 NFT 的多维数字资产属性与战略含义。
- 可用之处：**数字资产/新变现方式**这一前沿议题；文本分析方法的NBA案例。

### 主题 F　NBA 中国市场数字化营销（拓展方向，中文语境加分项）

**F1. NBA Red Card 2018（Mailman 集团）**（行业报告）
- 来源：https://380c1e7a-3488-40d2-83c6-698e99ba1c7d.filesusr.com/ugd/302453_631d7449d3574f349a5da058a9fd5cba.pdf
- 要点：用 5 个指标衡量 NBA 球队与球员在中国的线上影响力，并对两支球队的中英文渠道做内容分析，提炼中国社媒成功要素。
- 可用之处：**唯一一批"NBA 中国影响力指标"公开数据/框架**，中国市场方向的关键素材。

**F2. NBA 官方中国传播数据（NBA Communications / NBA China）**（一手资料）
- 来源：https://pr.nba.com/nba-aws-partnership/ ；https://pr.nba.com/first-ever-nba-chinese-new-year-celebration-builds-on-fan-interest-in-china-this-season/
- 要点：官方口径披露中国区数字化数据（如 NBA.com/中国与新浪 NBA 板块页面浏览量约 70 亿次、直播视频流约 70 亿次，同比大幅增长；NBA 是中国粉丝最多的体育联盟，社媒粉丝规模庞大）。
- 可用之处：中国市场的**规模性论据**（注意：用于论文需标注来源与年份）。

---

## 第三部分　数据集清单（Kaggle 为主 + 外部补充源）

> Kaggle 检索入口：https://www.kaggle.com/datasets?search=nba （返回 700+ 数据集）
> 许可提醒：Kaggle 数据集许可各异（CC0 / MIT / Unknown），**论文中务必注明数据集名称、作者、链接与许可**；商业敏感字段（薪资之外）多为公开数据。

### 3.1 Kaggle 核心数据集（推荐优先使用）

| # | 数据集 | 链接 | 内容要点 | 规模 / 口碑 | 适用方向 |
|---|---|---|---|---|---|
| 1 | **NBA Stats (1947–present)** | https://www.kaggle.com/datasets/sumitrodatta/nba-aba-baa-stats | NBA/ABA/BAA 三联盟；球员 12 类文件（总量、场均、每36分钟、每100回合、进阶、play-by-play 位置占比等）+ 球队与联盟统计 | 22 个 CSV，约 11 MB，下载 3.2 万+，可用性 10.0 | A / B / C / D（**主力底层数据**） |
| 2 | **NBA Database**（wyattowalsh） | https://www.kaggle.com/datasets/wyattowalsh/basketball | 综合型数据库，赛季中每日更新，含比赛、球员、阵容、投篮等；附 10 个官方 Notebook（MVP 预测、比赛结果建模、球员聚类、投篮图、阵容分析） | 大型，维护活跃 | A / B / C / D（**一站式+现成案例**） |
| 3 | **NBA data 1946–2026**（Deo Cheng） | https://www.kaggle.com/datasets （见 "nba" 标签页列表） | 覆盖 1946–2026 的长期历史数据 | 93 文件，约 899 MB，近 3 月更新 | A / D（长期时间序列） |
| 4 | **NBA Dataset: Box Scores and Stats (1947–Today)** | https://www.kaggle.com/datasets/eoinamoore/historical-nba-data-and-player-box-scores | 全历史比赛记录，**含主场/客场、赛果、球馆与上座率（attendance）字段**；含 2024–25、2025–26 赛程 | 持续更新 | **A / C（上座率与赛程核心）** |
| 5 | **Annual Attendance of all NBA Teams 2000–2015** | https://www.kaggle.com/datasets/rishidamarla/annual-attendance-of-all-nba-teams-from-20002015 | 30 支球队逐年上座人数（源自 data.world） | 1 个 Excel，轻量 | A（**上座率标签**） |
| 6 | **NBA Player Salaries 2000–2025** | https://www.kaggle.com/datasets/ratin21/nba-player-salaries-2000-2025 | 1999–00 至 2024–25 球员薪资；附爬取脚本 | CSV，CC0 | B / D（薪资因变量） |
| 7 | **NBA Player Stats and Salaries 2000–2025** | https://www.kaggle.com/datasets/ratin21/nba-player-stats-and-salaries-2000-2025 | **球员统计数据与薪资合并**，2000–2025 全量 | CSV | B（**性价比分析主力**） |
| 8 | **NBA Player Stats 2024-25** | https://www.kaggle.com/datasets/ratin21/nba-player-stats-2024-25-per-game | 2024–25 球员进阶/场均/总量三类统计 | CC0 | B（近期数据） |
| 9 | **NBA Player Stats (Season 24/25)** | https://www.kaggle.com/datasets/eduardopalmieri/nba-player-stats-season-2425 | 2024–25 球员逐场表现统计 | MIT | B |
| 10 | **NBA Shots**（mexwell） | https://www.kaggle.com/datasets/mexwell/nba-shots | 2003–04 至 2023–24 **常规赛投篮位置数据**（坐标、主客队、位置分组等） | 较大 | B / D（打法风格与空间分析） |
| 11 | **NBA shot logs**（DanB） | https://www.kaggle.com/datasets?search=nba （"NBA shot logs"） | 经典投篮日志，比赛时间、距离、结果等 | CSV，约 3 MB，下载近 2 万，Gold | B |
| 12 | **NBA & WNBA Play-by-Play and Shot Details (1996–2021)** | https://www.kaggle.com/datasets/brains14482/nba-playbyplay-and-shotdetails-data-19962021 | 逐回合事件 + 投篮细节（位置、距离、结果、助攻人） | 大型 | B / D（逐回合建模） |
| 13 | **NBA Injuries 2010–2020** | https://www.kaggle.com/datasets?search=nba （"NBA Injuries from 2010-2020"） | 球员伤病记录（日期、缺阵等） | 1 CSV，约 231 KB，下载 7000+，Silver | A / B（**可供性控制变量**） |
| 14 | **1991–2021 NBA Stats**（Vivo Vinco） | https://www.kaggle.com/datasets?search=nba+stats | 30 年球员赛季统计 | CSV | B / D |
| 15 | **NBA Social**（球员社媒数据） | https://www.kaggle.com/code/leimango/nba-social/input | 约 100 名球员的社交统计（PLAYER_ID、TEAM、AGE、社媒指标字段） | 小样本 | **A / B（社交影响力因子）** |
| 16 | **Top 100 Social Media Profiles** | https://www.kaggle.com/datasets/medaxone/top-100-social-media-profiles | Instagram/Twitter/YouTube/Twitch/TikTok 各前 100 账号粉丝量 | 小 | A（作为社媒体量参照） |

### 3.2 Kaggle 之外的补充数据源（强烈建议组合使用）

| 数据源 | 链接 | 提供什么 | 用途 |
|---|---|---|---|
| **Basketball-Reference** | https://www.basketball-reference.com/ | 球员/球队逐赛季与逐场统计、球馆、薪资、教练、交易 | 补齐与交叉校验 Kaggle 数据 |
| **nba_api**（Python 包） | https://github.com/swar/nba_api | 官方 stats.nba.com 接口封装：赛程、比分、play-by-play、投篮坐标、阵容 | 需要"最新/自定义"数据时自行抓取 |
| **NBA 官方统计** | https://www.nba.com/stats | 官方进阶数据、跟踪数据（player tracking） | 官方口径核验 |
| **Forbes / Sportico NBA 球队估值榜** | https://www.hoopsrumors.com/2026/10/warriors-knicks-top-2026-nba-franchise-valuations.html | 30 队**估值、收入、营业利润**年度榜单（2026 年勇士估值约 145 亿美元居首，同比 +28%） | **方向 D 的因变量来源** |
| **Team Marketing Report – Fan Cost Index** | 官网 / 行业报道 | 各队球迷消费成本指数、平均票价 | **方向 C 的票价与消费者成本来源** |
| **Statista** | https://www.statista.com/ | NBA 联盟收入、上座率、转播、赞助规模等汇总 | 背景数据与图表 |
| **data.world** | https://data.world/gmoney/nba-team-annual-attendance | 球队年度上座率（Kaggle 数据集 #5 的原始来源） | 上座率补充 |

### 3.3 数据整合的关键设计（无论做哪个方向都要先想清楚）

1. **唯一键（join key）**：以 `SEASON`（如 2023-24）+ `TEAM_ID/FRANCHISE` + `PLAYER_ID` 作为跨表连接键；注意球队迁移/更名（如 夏洛特山猫→黄蜂、新泽西→布鲁克林）需要映射表。
2. **时间对齐粒度**：逐场（game-level）适合上座率/观赛预测；逐赛季（season-level）适合营收/估值/薪资分析；逐回合（play-by-play）适合打法风格分析。
3. **外部变量的时间锚定**：估值、收入、GDP、人口等按对应年份匹配，避免"用未来信息预测过去"的数据泄漏。
4. **缺失与口径**：球馆容量、票价、GDP/人口、社媒数据常有缺失，需记录缺失率并说明插补或剔除策略（这是论文"数据预处理"章节的得分点）。

---

## 第四部分　研究计划与研究问题（多方向候选）

> 下列 4 个方向共享同一套"总目标 + 总技术路线"，差异在**研究问题、因变量与数据主表**。建议先读第五部分对照表再定。

### 4.0 总体研究计划框架（四大方向通用）

**总目标**：以多源公开数据为基础，构建"球迷参与/球队表现 → 营销结果（收视、上座、票价、收入、估值、品牌资产）"的可解释预测模型，识别关键驱动因素，并提出数据驱动的 NBA 营销策略建议。

**总技术路线（六阶段）**：

```
阶段 0  选题与文献综述  →  明确研究问题、假设、变量表
阶段 1  数据获取与整合  →  Kaggle 多表 + Basketball-Reference/nba_api/Forbes 补充，构建分析宽表
阶段 2  数据清洗与特征工程 →  缺失/异常处理、球队名称与赛季标准化、生成营销特征（战绩、星味、赛程强度、社媒热度、伤病）
阶段 3  探索性分析(EDA) →  分布、相关、时序趋势、聚类/细分（segmentation）
阶段 4  建模与验证    →  基线模型 → 集成模型 → 可解释性(SHAP/系数)；回归/分类/时间序列
阶段 5  营销策略推导与检验 →  情景分析/反事实模拟，形成策略建议
阶段 6  结论、局限与论文撰写 →  结果解释、伦理与局限、可视化（图表统一英文、学术风格）
```

**通用研究方法与工具**：Python（pandas / scikit-learn / XGBoost / LightGBM / statsmodels / SHAP）、可选 R（lme4 做混合效应）、SQLite、Tableau/PowerBI 或 Plotly 可视化。

**通用评价指标**：回归用 R²、MAE、RMSE；分类用 AUC、F1、Accuracy；聚类用轮廓系数、Calinski-Harabasz；解释性用 SHAP 值与特征重要性。

**通用可行性保障**：全部数据公开可得；算法均有成熟库；若某方向数据不足，可降级为"单赛季 + 简化特征"的可行性兜底方案。

---

### 方向 A（主推）：球迷参与驱动的 NBA 商业结果预测与归因研究

**A.1 一句话题目**
> 基于多源数据的 NBA 球迷参与度建模及其对收视/上座等营销结果的预测与归因研究

**A.2 研究背景与动机**
球迷参与是体育营销的核心资产，但"参与"难以直接量化，且与商业结果（上座、收视、周边）之间缺乏可验证的量化关系。本方向把"参与"操作化为**可观测的行为与内容指标**（社媒讨论量、情绪、话题热度、球队战绩与星味），并用机器学习预测商业结果。

**A.3 研究问题（RQ）**
- RQ1：哪些球迷参与特征（社媒活跃度、情绪得分、球星效应、战绩、赛程强度）对 NBA 比赛的**收视/上座**最具预测力？
- RQ2：社交媒体热度与比赛收视/上座之间是**相关**还是存在**领先—滞后（lead-lag）关系**？能否用赛前热度预测赛后关注度？
- RQ3：球队之间是否存在**球迷细分类型**（如狂热型/社交型/跟风型）？不同细分对营销指标的敏感度是否不同？
- RQ4：能否用球迷参与特征预测**球迷忠诚/流失（bandwagon 转化）**，并识别最有效的留存干预点？

**A.4 研究假设示例**
- H1：赛前社媒讨论量与情绪得分显著正向预测收视人数（借鉴 A1）。
- H2：队伍战绩与比赛重要性是上座率的最强驱动，集成模型显著优于线性模型（借鉴 A3、A5）。
- H3：活动类特征对球迷留存的预测力强于网络结构类特征（借鉴 A2）。
- H4：不同球迷细分群体的购买/到场意愿对促销敏感性存在显著差异（借鉴 D4）。

**A.5 数据方案**
- 主表：Kaggle #4（Box Scores + 球馆与上座率）、#5（年度上座）→ 得到"逐场上座/收视"标签。
- 特征表：Kaggle #1/#2（球队与球员战绩）、#13（伤病）、#15/#16（社媒体量）、可选 #14。
- 补充：Basketball-Reference 赛程与战绩、nba_api 抓取赛前话题/阵容、行业社媒报告。
- 关键构造变量：赛程强度（SOS）、背靠背、主客场、对阵明星球员数、球队连胜/连败、近 10 场胜率、社媒互动量、情绪极性。

**A.6 方法与模型**
- 探索性：相关分析、时序趋势、K-means/层次聚类做球迷或球队细分。
- 预测：线性回归（基线）→ 随机森林 → XGBoost/LightGBM（主模型），对比 A3/A5 结论。
- 归因：SHAP/排列重要性，输出"驱动因素排序"。
- 若引入文本：用 VADER/TextBlob（英文）或中文模型做情绪打分（参考 A1）。
- 进阶（可选）：用时间序列（ARIMA/Prophet）或面板模型处理赛季间趋势。

**A.7 预期产出与贡献**
- 一套可复现的"球迷参与→商业结果"预测流程与特征字典；
- NBA 场景下驱动因素的量化排序，验证/修正既有文献（A1–A3）结论；
- 面向球队市场部门的参与度提升与留存策略建议。

**A.8 难度与创新点**
- 难度：中；数据最全，方法最成熟，风险最低，**最适合作为稳妥的毕业设计主线**。
- 创新点：把"社交情绪"与"传统战绩/上座"整合到同一模型并做归因；引入球迷细分刻画异质性。

---

### 方向 B（可选）：NBA 球员商业价值与薪资评价的数据驱动研究

**B.1 一句话题目**
> 基于场上表现与社交影响力的 NBA 球员商业价值评估及薪资合理性建模研究

**B.2 研究动机**
球员既是竞技资产也是营销资产（代言、球衣、内容流量）。球队/品牌需要一个"性价比"标尺来判断薪资与市场价值是否匹配。可结合"代言可信度→购买意愿"理论（D3）与"球衣赞助→购买意愿"证据（D2）。

**B.3 研究问题**
- RQ1：球员的**场上表现指标**能在多大程度上解释其薪资？不同位置/年龄段的定价逻辑是否不同？
- RQ2：加入**社交影响力/曝光度**后，模型的解释力是否显著提升（即"流量溢价"是否存在）？
- RQ3：哪些球员存在明显的"高薪低能"或"低薪高能"（性价比异常）？可否用无监督方法识别？
- RQ4：球员商业价值能否用类别化评分（如 A/B/C 档）表达，并验证其与薪资、球队战绩的关联？

**B.4 研究假设**
- H1：基础与进阶统计对薪资有显著解释力，但存在随位置与年龄变化的**结构性差异**。
- H2：社交影响力对薪资具有显著**额外正向**贡献（流量溢价）。
- H3：以"表现—薪资残差"可有效识别薪资异常球员。

**B.5 数据方案**
- 主表：Kaggle #7（球员统计+薪资 2000–2025）、#6（薪资），补齐 #1/#8/#9（进阶统计）。
- 社交数据：Kaggle #15（球员社媒）、#16；必要时用 nba_api + 公开社媒榜单抓取。
- 控制变量：位置、年龄、出场数、伤病（#13）、球队战绩、工资帽年份。
- 目标变量：赛季薪资（连续）或薪资分档（分类），以及构造的"性价比"指标（表现/薪资）。

**B.6 方法与模型**
- 回归：多元线性回归、Lasso/Ridge、随机森林、XGBoost。
- 分类：薪资档位预测（逻辑回归/梯度提升）。
- 无监督：K-means 对球员画像聚类（"高流量低产出"等类型）。
- 解释：SHAP + 分位置/分年代的分组回归对比。

**B.7 预期产出与贡献**
- 球员薪资预测模型与"性价比"排行榜；
- "流量溢价"是否存在的量化证据，为球队签约与品牌代言选择提供参考；
- 可复用的球员价值评分体系。

**B.8 难度与创新点**
- 难度：中；数据可得性好（统计+薪资同表），但社交数据的覆盖率有限是主要风险。
- 创新点：把"营销端的社交影响力"作为额外解释变量注入薪资模型，形成"竞技 + 商业"双维评价。

---

### 方向 C（可选）：NBA 票务需求预测与动态定价策略研究

**C.1 一句话题目**
> 面向 NBA 赛事的票务需求预测与动态定价策略优化研究

**C.2 研究动机**
门票收入约占球队总收入 30%–40%（B4），且需求高度波动（对手、球星、天气、赛程、战绩）。动态定价是球队营收管理的核心工具（C1、C2）。

**C.3 研究问题**
- RQ1：哪些因素（对手吸引力、主场战绩、明星球员、比赛日、赛程位置、球馆容量）最能解释 NBA 单场**需求/上座率**？
- RQ2：能否构建**单场票务需求预测模型**，其精度是否优于单纯的历史均值/线性模型？
- RQ3：在给定需求模型的条件下，**如何为不同比赛设定差异化票价以最大化收入**？相比统一定价的收入提升幅度是多少？
- RQ4：不同球迷细分与分区（坐席等级）的最优定价弹性是否存在差异？

**C.4 研究假设**
- H1：对阵球队的"市场吸引力"与明星球员可用性是需求的强正向驱动。
- H2：动态定价相较单一票价策略可显著提升期望收入。
- H3：需求价格弹性在高端坐席与普通坐席间存在显著差异。

**C.5 数据方案**
- 主表：Kaggle #4（逐场含球馆与上座）、#5（年度上座）→ 得到"需求/上座"标签。
- 需求驱动变量：Kaggle #1/#2（球队战绩、对手强度）、#10/#11（打法观赏性，可构造"进攻节奏/三分占比"等风格变量）、#13（伤病影响明星可用性）。
- 价格/成本：Team Marketing Report 票价、球馆容量、分区价格（需外部补充）；若缺票价逐场数据，可用"上座率（相对容量）"作为需求的替代指标。
- 补充：Forbes/Sportico 营收数据用于校准。

**C.6 方法与模型**
- 需求模型：随机森林/XGBoost 做需求（或上座率）预测；对比线性与集成（参考 C1、A5）。
- 弹性估计：回归中的价格项系数/价格弹性建模（需票价数据）。
- 优化：在需求模型基础上做**迭代式价格搜索**（给定竞争对手与座位，按期望收入最大化的价格迭代，参考 C1）或情景模拟。
- 评估：收入提升百分比、命中率、鲁棒性（不同赛季/球队）。

**C.7 预期产出与贡献**
- 单场需求预测模型 + 动态定价策略原型（含收入提升量化）；
- 面向球队票务部门的分区定价与促销时机建议；
- 与 C1/C2 的 NFL/行业做法对比，给出 NBA 场景的差异结论。

**C.8 难度与创新点**
- 难度：中偏上；**主要风险是逐场票价数据难获取**，需以"上座率需求代理"或公开票价样本兜底。
- 创新点：把"比赛风格/观赏性"引入需求模型；区分坐席等级的需求弹性。

---

### 方向 D（可选）：NBA 球队品牌价值影响因素与营销绩效研究

**D.1 一句话题目**
> NBA 球队品牌/商业价值的影响因素分析与营销绩效计量研究

**D.2 研究动机**
球队估值与营收是营销绩效的最终财务体现，其驱动因素（战绩、市场、球星、打法、社区影响）具备明确的管理意义（B1、B2）。

**D.3 研究问题**
- RQ1：哪些因素（收入、夺冠、城市 GDP/人口、关键球员、打法风格、上座率）显著影响 NBA 球队**估值/收入**？
- RQ2：**打法风格（如快节奏/三分比重）**是否与更高收入相关？其效应在控制战绩后是否稳健？
- RQ3：大市场与小市场球队的价值驱动因素是否存在**异质性**？对小市场球队，哪些营销杠杆更有效？
- RQ4：球队价值的年度变化能否用营销与竞技指标预测？

**D.4 研究假设**
- H1：收入、夺冠、市场规模（GDP/人口）、关键球员是估值的显著正向驱动（复现并扩展 B1）。
- H2：以"Run and Gun"为代表的快节奏打法与更高收入相关（检验 B2）。
- H3：收入对估值的边际效应在小市场球队更大（异质性）。

**D.5 数据方案**
- 因变量：**球队估值/收入/营业利润**（Forbes 或 Sportico 年度榜单，逐年抓取/整理）。
- 主表：Kaggle #1/#2/#4（战绩、上座、比赛风格）、#5（上座率）。
- 宏观与市场：城市 GDP、人口、媒体市场规模（外部统计）。
- 风格变量：由 #10/#11 投篮数据构造节奏（pace）、三分出手占比、助攻率、快攻得分占比等。

**D.6 方法与模型**
- 计量：**面板回归 / 固定效应模型 / 动态线性混合模型**（直接对标 B1），以 AIC/BIC 选模。
- 稳健性：聚类标准误、异质性分组回归（大/小市场）、工具变量（若可行）。
- 补充机器学习：随机森林/XGBoost 做估值预测与非线性关系识别（GDP、人口可能存在非线性）。
- 解释：系数显著性 + SHAP 双通道解释。

**D.7 预期产出与贡献**
- 一份 NBA 球队价值驱动因素的量化证据与稳健性检验；
- 面向小市场球队的营销杠杆建议；
- 与 B1/B2 的结论对照（复现 → 扩展 → 更新年份）。

**D.8 难度与创新点**
- 难度：中；**核心难点在估值/收入数据的逐年整理**（样本为 30 队 × 若干年，属"小样本面板"，需谨慎处理）。
- 创新点：在经典"收入—估值"研究框架中**加入打法风格与上座率等营销变量**，并做市场异质性分析。

---

### 拓展方向 E（跨市场加分项）：NBA 中国市场的数字营销效果研究

> 定位：可作为上述任一方向的"第二案例"或单独的探索性章节，**不建议作为唯一主线**（原因见下）。

**可研究的问题**：NBA 在中国的社媒影响力指标如何构建（参考 F1 的 5 指标框架）？中国赛/春节活动的社媒声量与其商业转化（会员、周边、观赛）之间有什么关系？中外渠道内容策略差异如何影响互动率？

**数据现实**：Kaggle 上缺少系统性的 NBA 中国社媒数据集，需要**自行采集**（微博/抖音/小红书/虎扑等公开数据，注意平台条款与合规）或使用行业报告（F1、F2）。因此**数据获取成本高、可复现性弱**，适合有一定爬虫与中文 NLP 基础、且研究条件允许的同学。

**价值**：中文语境 + 跨文化营销视角，对中文论文的"研究意义"和答辩呈现有加分作用。

---

## 第五部分　方向选择建议与对照表

### 5.1 四方向对照表

| 维度 | A 球迷参与→商业结果预测 | B 球员商业价值与薪资 | C 票务需求与动态定价 | D 球队品牌价值影响因素 |
|---|---|---|---|---|
| 数据可得性 | ★★★★★ 最全 | ★★★★ 统计+薪资同表 | ★★★ 缺逐场票价 | ★★★ 估值需整理 |
| 方法成熟度 | ★★★★★ | ★★★★ | ★★★★ | ★★★★（计量） |
| 建模主任务 | 回归/分类/聚类/文本 | 回归/分类/聚类 | 回归+最优化 | 面板/混合效应回归 |
| 营销味 | ★★★★★ | ★★★★ | ★★★★★ | ★★★★ |
| 创新空间 | 中高 | 高（流量溢价） | 高（风格→需求） | 中高（风格→估值） |
| 主要风险 | 社媒数据覆盖不足 | 社交数据覆盖不足 | 票价数据缺失 | 估值样本量小 |
| 适合人群 | 求稳、想要完整流程 | 对球员/代言感兴趣 | 喜欢优化与定价 | 喜欢计量经济学 |
| 论文主线契合度 | 最贴合"市场营销" | 偏"人力资源/价值评估" | 偏"收益管理" | 偏"品牌/财务" |

### 5.2 选择建议（按你的偏好）

- **想要最稳妥、最容易做出完整结果** → 选 **方向 A**，可把 B/C/D 的变量作为特征纳入。
- **对"球星经济/代言价值"最感兴趣** → 选 **方向 B**。
- **喜欢定价、优化、收益管理** → 选 **方向 C**（注意提前确认票价数据获取方案）。
- **擅长计量经济学、喜欢做实证归因** → 选 **方向 D**（建议以 B1 为方法蓝本做"复现+扩展"）。
- **想要差异化与中文特色、且能接受自采数据** → 在主线基础上加 **拓展方向 E** 作为一章。

### 5.3 推荐组合打法（两种常见结构）

- **稳妥型**：主线 = 方向 A；辅 = 方向 B 的一节（球员特征如何影响上座/收视）。
- **进取型**：主线 = 方向 C 或 D（营销结果更"硬"）；辅 = 方向 A 的社交情绪特征作为解释变量。

---

## 第六部分　参考文献与数据源链接汇总

### 6.1 学术文献（可下载链接）

- Buzz to Broadcast: Predicting Sports Viewership Using Social Media Engagement — https://arxiv.org/pdf/2412.10298v1
- Jump off the Bandwagon? Characterizing Bandwagon Fans' Future Loyalty in Online NBA Fan Communities — https://arxiv.org/html/2401.11629
- Cheering for your country: prediction of attendance at international football games using ML — https://www.tandfonline.com/doi/pdf/10.1080/00036846.2026.2618091
- Evaluating Machine Learning Algorithms for Predictive Modeling of Large-scale Event Attendance — https://www.ijcis.net/index.php/ijcis/article/view/249/211
- Quantifying Fan Engagement and Sentiment During Live Games Via Social Media Analytics — https://www.samford.edu/sports-analytics/fans/2026/Quantifying-Fan-Engagement-and-Sentiment-During-Live-Games-Via-Social-Media-Analytics
- Examination of NBA Team Values Based on Dynamic Linear Mixed Models — https://pmc.ncbi.nlm.nih.gov/articles/PMC8211228/
- Run Up the Score, and the Profits: NBA Revenue Using Gameplay Statistics — https://oasis.library.unlv.edu/cgi/viewcontent.cgi?article=1038&context=spectra
- A Rolling-Horizon Stochastic Optimization Framework for NBA Franchise Management — https://arxiv.org/html/2604.06548
- The NBA's Revenue Sharing Scorecard — https://ur.bc.edu/system/files/2025-04/bc-ir102222.pdf
- Dynamic Pricing for Sports Event Ticket (ICDATA 2020) — https://matthewalanham.github.io//Students/2020/ICDATA20_Dynamic%20Pricing%20for%20Sports%20Event%20Ticket.pdf
- Dynamic Pricing Models for Ticket Sales Managers — https://datacalculus.com/en/blog/spectator-sports/ticket-sales-manager/dynamic-pricing-models-for-ticket-sales-managers
- Analysis of the Tactics of NBA Pricing Tickets — https://pdfs.semanticscholar.org/cdde/6bfaf03ab522d296e075eaaec312666d57bf.pdf
- What Variables Predict Ticket Prices of NBA Franchises? A Review — https://pdfs.semanticscholar.org/3539/69e7dfb64dd09314323bec4b01d1eae5a14e.pdf
- Examining the Effectiveness of Different Ticket Bundling Strategies (NBA) — https://openscholar.uga.edu/record/11763/files/chen_kuan-chou_201308_phd.pdf
- Searching for the "Holy Grail" of Sponsorship-Linked Marketing: A Generalizable Sponsorship ROI Model — https://arxiv.org/pdf/2305.09473v1
- Consumer Split Identification: The Case of Sponsorship (JSM 40(4), 2026) — https://journals.humankinetics.com/view/journals/jsm/40/4/article-p315.xml
- The Influence of NBA Star Endorsers' Credibility and Brand Image on Purchase Intention — https://oapub.org/soc/index.php/EJMMS/article/view/623
- The Effect of Promotional Bundles on Purchase Intent (Charlotte Hornets) — https://www.longdom.org/open-access-pdfs/the-effect-of-promotional-bundles-on-purchase-intent-for-high-mediumand-low-vested-sports-tourists-segments-within-the-context-of-2167-0269-1000275.pdf
- Beyond Purchase Intention in Sports Sponsorship: Best-Worst Scaling — https://researchers.mq.edu.au/en/publications/beyond-purchase-intention-in-sports-sponsorship-an-alternative-ap/
- AI-Powered Sports Marketing: Predictive Insights, Consumer Behavior, and Global Brand Strategy — https://pdfs.semanticscholar.org/39ab/1b8e0d887d3d26992383400663c6a30cd06b.pdf
- Algorithmic Fandom: How Generative AI Is Reshaping Sports Marketing — https://pmc.ncbi.nlm.nih.gov/articles/PMC12094936/
- The Role of Digital Marketing in Promoting Sports Marketing: NBA as an Example — https://pdfs.semanticscholar.org/113b/cb0784779c4775809fc8c59c86600aa65a8c.pdf
- Sports NFTs as Multidimensional Digital Assets: NBA Social Big Data — https://www.tandfonline.com/doi/full/10.1080/2...
- NBA Red Card 2018 (Mailman, 中国市场报告) — https://380c1e7a-3488-40d2-83c6-698e99ba1c7d.filesusr.com/ugd/302453_631d7449d3574f349a5da058a9fd5cba.pdf

### 6.2 数据集链接

- Kaggle NBA 数据集检索 — https://www.kaggle.com/datasets?search=nba
- NBA Stats (1947–present) — https://www.kaggle.com/datasets/sumitrodatta/nba-aba-baa-stats
- NBA Database (wyattowalsh) — https://www.kaggle.com/datasets/wyattowalsh/basketball
- NBA Dataset: Box Scores and Stats (1947–Today) — https://www.kaggle.com/datasets/eoinamoore/historical-nba-data-and-player-box-scores
- Annual Attendance of all NBA Teams 2000–2015 — https://www.kaggle.com/datasets/rishidamarla/annual-attendance-of-all-nba-teams-from-20002015
- NBA Player Salaries 2000–2025 — https://www.kaggle.com/datasets/ratin21/nba-player-salaries-2000-2025
- NBA Player Stats and Salaries 2000–2025 — https://www.kaggle.com/datasets/ratin21/nba-player-stats-and-salaries-2000-2025
- NBA Player Stats 2024-25 — https://www.kaggle.com/datasets/ratin21/nba-player-stats-2024-25-per-game
- NBA Player Stats (Season 24/25) — https://www.kaggle.com/datasets/eduardopalmieri/nba-player-stats-season-2425
- NBA Shots (mexwell) — https://www.kaggle.com/datasets/mexwell/nba-shots
- NBA & WNBA Play-by-Play and Shot Details (1996–2021) — https://www.kaggle.com/datasets/brains14482/nba-playbyplay-and-shotdetails-data-19962021
- Top 100 Social Media Profiles — https://www.kaggle.com/datasets/medaxone/top-100-social-media-profiles

### 6.3 补充数据源

- Basketball-Reference — https://www.basketball-reference.com/
- nba_api (Python) — https://github.com/swar/nba_api
- NBA 官方统计 — https://www.nba.com/stats
- Forbes / Sportico NBA 球队估值榜（2026） — https://www.hoopsrumors.com/2026/10/warriors-knicks-top-2026-nba-franchise-valuations.html
- Statista — https://www.statista.com/
- data.world NBA 上座率 — https://data.world/gmoney/nba-team-annual-attendance

---

### 附：写作与论文呈现建议（可选）

- 图表尽量使用**英文标签、学术黑白配色、去除冗余元素**，保持版面整洁；
- 每张关键图都要能回答一个研究问题（RQ），避免"为画图而画图"；
- 报告中明确标注**数据来源、年份与许可**，并在"研究局限"中说明数据缺失、样本量与外部效度问题；
- 若研究涉及社媒文本，需在方法章节说明隐私与合规处理（匿名化/仅公开数据/平台条款）。

> 下一步建议：先确定方向（A/B/C/D + 是否加 E），我可以据此进一步产出**正式开题报告**（含研究背景、文献综述、研究方法、技术路线图、创新点、进度安排与参考文献表）。
