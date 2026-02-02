# 第五章：Zone 设计实战

---

上一章讲了 Zone 是什么——贴好标签的收纳箱，Layer 内部按职责归类的功能分区。概念清楚了。

这一章要回答下一个问题：Zone 具体长什么样？怎么建？

先把结论说在前面：**Zone 不需要你手动去规划。** 你不用自己翻文件、读代码、一个个分组。这件事让 AI 来做——它读得懂代码，分得比你快。你要做的是理解 Zone 的设计原则，这样当 AI 给你一份分组方案的时候，你能看懂、能判断、能提出调整意见。

所以这一章的目的不是教你"动手归类"，而是让你**看懂 Zone 是怎么回事**。

---

## Zone 的完整定义

上一章用类比快速引出了 Zone。这里给一个更完整的定义。

**Zone 是 Layer 内部按业务职责聚类的功能分区。**

拆开来看，Zone 有五个关键特征：

**一、Zone 属于某个 Layer。** 每个 Zone 都挂在一个特定的 Layer 下面。TaskZone 在逻辑层，TaskUIZone 在界面层。不存在"跨层的 Zone"。

**二、Zone 按业务职责划分，不按技术类型。** "任务管理"是一个 Zone，"计时服务"是一个 Zone。但"所有 Manager 放一个 Zone"不是——"Manager"是技术命名习惯，不是业务职责。

**三、Zone 有清晰的标签。** 每个 Zone 的职责应该能用一句话说清楚。如果你需要用"以及""还有""同时负责"来描述一个 Zone 的职责，那它可能太大了，需要拆。

**四、Zone 是逻辑概念，不是物理文件夹。** 上一章重点强调过这一点：你不需要在项目里创建对应的文件夹。Zone 存在于你和 AI 共享的一份文档里——一张"哪个文件属于哪个 Zone"的映射表。

**五、Zone 有边界。** 一个文件只属于一个 Zone。如果一个文件"好像哪个 Zone 都能放"，说明要么 Zone 的标签不够清晰，要么这个文件承担了太多职责（它本身应该被拆分）。

---

## 让 AI 帮你建 Zone

理解了 Zone 的定义之后，来看实际操作。

你不需要自己打开每个文件去读代码。Zone 的创建和组织，从头到尾都可以让 AI 来做。

但 AI 不能凭空干活，它需要一份"说明书"——告诉它 Zone 是什么、怎么分、分完输出什么格式。这份说明书已经写好了，叫 **AI Playbook**。顾名思义，它是一份给 AI 看的剧本——里面定义了 Layer 和 Zone 的所有规则、判定标准、输出格式。你不需要自己写这份剧本——直接用现成的就行。

操作流程是这样的：

**第一步**：把 AI Playbook 和你的项目源码一起丢给 AI。

**第二步**：AI 读完所有源码，按照 Playbook 里的规则，自动完成分析：判断项目有几个 Layer，每个 Layer 里有哪些 Zone，每个 Zone 包含哪些文件，Zone 之间有什么依赖关系。

**第三步**：AI 输出两份文件——

- **Layer-Zone Tree**：文字版全景照。用结构化的格式列出所有 Layer、所有 Zone、每个 Zone 的职责和文件清单、Zone 之间的依赖关系。这是数据源，是你审核和查阅的主文件。

- **Layer-Zone Visuals**：图表版全景照。用 Mermaid 图表把 Tree 里的信息可视化——层级结构图、依赖关系图、Zone 大小分布图。一眼就能看到全局。

以 GetDone Timer 为例。我把 160 个 Swift 文件和 AI Playbook 丢给 AI，它输出的 Tree 里，逻辑层长这样：

```
💼 Logic Layer
│
├─ TaskZone [执行型]  — L.Z1
│  "任务的创建、管理、状态流转"
│  包含：CardManager, CardManagerProtocol
│
├─ TimingZone [执行型]  — L.Z2
│  "计时器倒计时与番茄钟 Focus/Break 阶段管理"
│  包含：TimerService, PomodoroService
│
├─ ScheduleZone [执行型]  — L.Z3
│  "日程时间槽管理、冲突检测、定时任务启动"
│  包含：ScheduleManager, ScheduledStartManager
│
├─ AccountZone [执行型]  — L.Z4
│  "用户认证、Session 管理、邀请码"
│  包含：AccountManager, AuthService, InviteManager
│
├─ AIZone [执行型]  — L.Z5
│  "AI 多 Provider 调用、提示词组装、任务生成"
│  包含：AIService, AIAPIClient, AICardGenerator
│
├─ ...（还有 PaymentZone、SettingsZone、PermissionZone 等）
│
└─ 非Zone代码：DeviceInfo, TimezoneHelper, ThemeManager
```

每个 Zone 有编号（L.Z1、L.Z2...），有类型标注（执行型/组织型），有一句话职责描述，有文件清单，有依赖关系。AI 连"哪些文件不属于任何 Zone"都帮你标出来了。

对应的 Visuals 文件里，同样的信息变成了可视化图表——层级总览图、依赖关系图，在 Obsidian 或 GitHub 里直接渲染，一张图看清整个项目。

你拿到这两份文件之后要做什么？**审核。** 不是每一行都审，而是看几个关键点：

- **标签是否清晰？** 每个 Zone 的职责能一句话说清楚吗？"任务的创建、管理、状态流转"——清楚。如果有一个 Zone 叫"杂项"——不清楚，让 AI 重新分。
- **分组是否合理？** PermissionManager 被 AI 单独列为 PermissionZone 了——合适吗？它管的是权限（Free/Pro），跟账户有关系，要不要合进 AccountZone？这种边界上的判断，你来做。
- **有没有遗漏？** DeviceInfo、TimezoneHelper 被标为"非 Zone 代码"——对不对？对的，它们是工具函数，不需要装箱。后面会解释这一类东西。

AI 负责干活（读代码、分析、输出 Tree 和 Visuals），你负责决策（这个分法好不好、要不要调整）。**你是审稿人，不是作者。**

三个工具各自的角色：

| 工具 | 是什么 | 给谁看 |
|:---|:---|:---|
| **AI Playbook** | AI 的剧本——怎么分析、怎么分组、怎么输出 | 给 AI 看 |
| **Layer-Zone Tree** | 文字版全景照——结构化的 Zone 清单和依赖关系 | 给你看（审核用） |
| **Layer-Zone Visuals** | 图表版全景照——Mermaid 可视化图表 | 给你看（一眼全局） |

你不需要读懂 AI Playbook 的每一条规则——那是 AI 的剧本，不是你的。你只需要看懂 Tree 和 Visuals 的输出，能判断"这个分组合不合理"就行。

---

## 哪些东西不用装箱

AI 给的分组方案里，一定会有几个文件没有被归入任何 Zone。

比如 GetDone Timer 逻辑层的 DeviceInfo（获取设备信息的工具方法）和 TimezoneHelper（时区转换）。它们不属于任何特定的业务领域——谁都可能调用，但它们自身不代表一个"功能"。

**这些东西不需要装箱。** 它们就像架子上放着的剪刀和胶带——随手取用的工具，不值得专门弄一个收纳箱。

在 Zone 体系里，这一类叫 **Non-Zone**。

怎么判断一个东西是应该归入 Zone 还是当作 Non-Zone？当 AI 给的分组方案里有些文件你拿不准的时候，可以用这四个问题快速判断：

1. **有独立的业务职责吗？**（不只是工具函数）
2. **管理自己的状态吗？**（有独立的生命周期）
3. **被其他 Zone 依赖吗？**（改了会影响别人）
4. **会独立演化吗？**（未来会变复杂）

四条里中了两条以上 → 应该归入某个 Zone（或者单独建一个 Zone）。
不到两条 → Non-Zone，散放在架子上就行。

TimezoneHelper？没有业务职责，不管理状态，改了不影响别人，未来也不会变复杂。四条全没中。Non-Zone。

PermissionManager？有独立职责（管理权限级别），管理自己的状态（当前用户是 Free 还是 Pro），其他 Zone 依赖它（很多功能要检查权限），未来会变复杂（新增套餐类型）。四条全中。应该归入 Zone。

这个判断标准你不需要自己去执行——你可以直接告诉 AI："这几个文件帮我判断一下，是应该归入 Zone 还是当 Non-Zone？" AI 会给你分析，你来拍板。

---

## Zone 的两种角色

AI 分出来的 Zone 里，你会发现它们干的事情不太一样。有些 Zone 在"做事"，有些 Zone 在"调度"。

**执行型 Zone：直接做事。**

TaskZone 里的 CardManager 在创建任务、删除任务。TimerZone 里的 TimerService 在倒计时、暂停、恢复。这些 Zone 有具体的业务逻辑——你让 AI 改一个功能，改的就是这些 Zone 里的代码。

**组织型 Zone：只协调，不做事。**

GetDone Timer 的 Core 层有一个 AppZone.swift。它是整个应用的协调中心——创建所有的 Manager 和 Service，把它们连接起来。但它自己**不包含任何业务逻辑**。它不知道任务怎么排序，不知道计时器怎么暂停。它只负责"把合适的零件组装在一起"。

判定很简单：有具体的业务实现 → 执行型。只调度其他 Zone → 组织型。

这个区分的价值在于：**它告诉你去哪里找代码。** 要改业务逻辑，去执行型 Zone。要改启动流程或页面导航，去组织型 Zone。告诉 AI 的时候也一样——"AppZone 里加一个新 Manager 的初始化"和"TaskZone 里改任务排序"，AI 立刻知道该打开哪些文件。

---

## 大箱子套小箱子

有些 Zone 会很大。

GetDone Timer 的界面层（UI Layer），MainWindow 目录下有七十多个 Swift 文件。如果 AI 把这些全归进一个"MainWindowUIZone"——那等于没分。

这时候你让 AI 继续往下分。AI 会在大 Zone 里面再分出小 Zone：

```
MainWindowUIZone（大箱子）
├── CardViewUIZone      → 任务卡片渲染（14个文件）
├── ScheduleUIZone      → 日程规划界面（16个文件）
├── AccountUIZone       → 账户页面（9个文件）
├── AIAssistantUIZone   → AI 助手界面（15个文件）
├── SettingsUIZone      → 设置页面（4个文件）
├── DialogsUIZone       → 各种对话框（9个文件）
├── SidebarUIZone       → 侧边栏（1个文件）
└── MainContentUIZone   → 主内容网格（1个文件）
```

七十多个文件，一分就清楚了。你要改日程界面的 Week 视图？去 ScheduleUIZone。要改任务卡片的 Footer 按钮？去 CardViewUIZone。

这就是 **Zone 嵌套**：大箱子里面放小箱子。

层级建议不超过三层：Layer → Zone → Sub-Zone。再往下拆就过度设计了。大多数项目两层就够。只有当某个 Zone 大到十几个文件的时候，才让 AI 往下再分一层。

判断标准很直觉：**一个 Zone 超过 10-15 个文件，就该拆了。**

---

## 同一个功能，不同层的箱子

"任务"这个功能，在不同层都有代码：

- **数据层**：TaskDataZone — 任务数据怎么存
- **逻辑层**：TaskZone — 任务的业务规则
- **Glue 层**：TaskGlueZone — 连接界面和逻辑
- **界面层**：TaskUIZone — 任务卡片长什么样

怎么让它们一眼就能对上？**命名规范**：

| Layer | 命名格式 | 示例 |
|:---|:---|:---|
| Data | [Feature]**Data**Zone | TaskDataZone |
| Logic | [Feature]Zone（无后缀） | TaskZone |
| Glue | [Feature]**Glue**Zone | TaskGlueZone |
| UI | [Feature]**UI**Zone | TaskUIZone |

逻辑层是主 Zone，不加后缀——因为业务逻辑是一个功能的核心。其他层加后缀标明角色。

名字本身就是地图。你说"改 TaskZone 的排序逻辑"，AI 知道去逻辑层。你说"改 TaskUIZone 的卡片布局"，AI 知道去界面层。不需要额外解释。

这套命名规范你不需要自己去想——让 AI 建 Zone 的时候告诉它："同一功能在不同层的 Zone，按这个命名规则来。" AI 会自动对齐。

---

## 依赖规则：箱子之间怎么打交道

Zone 之间不是孤立的。任务开始运行时，TaskZone 要通知 TimerZone 启动计时。日程规划时，ScheduleZone 要从 TaskZone 获取任务列表。

这些关系是正常的。但需要有规则，你看到 AI 的分析结果时才知道哪些依赖是合理的、哪些有问题。

**跨层依赖：严格向下。**

界面层可以依赖逻辑层，逻辑层可以依赖数据层，反过来不行。如果 AI 的分析报告里出现"TaskZone → TaskUIZone"（逻辑层依赖了界面层）——这是反向依赖，有问题。

**同层依赖：允许，但越少越好。**

TaskZone 调用 TimerZone 启动计时——合理。但如果同一层的每个 Zone 都跟其他所有 Zone 有依赖——那就变成蜘蛛网了。理想状态是少数几条明确的连线。

**违规了怎么办？**

实际项目中依赖不可能完美。分三级管理就好：

- 🟢 **可接受**：偶尔跳一层，影响范围小，记下来就行。
- 🟡 **关注**：暂时可控，但在膨胀，下次重构时处理。
- 🔴 **必须修**：反向依赖或循环依赖（A 依赖 B，B 又依赖 A），Zone 边界会失效，尽快修。

这个分级的意义：**不要因为追求完美而停下来。** Vibe Coding 的节奏是快速迭代。分级让你知道哪些可以先放着，哪些必须现在处理。

当 AI 给你分析完 Zone 并标出依赖关系的时候，你要关注的主要就是有没有 🔴 级别的违规。🟢 和 🟡 先记着，不用立刻处理。

---

**本章小结**

> Zone 有五个特征：属于某个 Layer、按业务职责划分、标签清晰、是逻辑概念、有明确边界。
>
> Zone 不需要你手动建——让 AI 读代码、分组、贴标签，你来审核和决策。不属于任何业务职责的工具代码是 Non-Zone，不用装箱。
>
> Zone 分执行型（做事）和组织型（调度）。大 Zone 可以嵌套小 Zone，不超过三层。同一功能在不同层用命名规范对齐。
>
> 依赖违规分三级：🟢 先放着，🟡 下次处理，🔴 现在就修。
>
> 现在你理解了 Zone 的设计原则，也知道怎么让 AI 来做这件事。接下来，是时候站远一点，给整个项目拍一张全景照了。
