# Chapter 5: Zone Design in Practice

---

Last chapter covered what Zone is—labeled storage boxes, functional partitions within a Layer clustering by responsibility. Concept clear.

This chapter answers the next question: What does Zone actually look like? How to build it?

Conclusion up front: **You don't need to manually plan Zones.** You don't have to flip through files, read code, group things yourself. Let AI do this—it reads code, groups faster than you. What you need is to understand Zone design principles, so when AI gives you a grouping proposal, you can comprehend it, judge it, suggest adjustments.

So this chapter's purpose isn't teaching you to "do the classification yourself," but helping you **understand how Zones work**.

---

## Complete Definition of Zone

Last chapter used analogies to quickly introduce Zone. Here's a more complete definition.

**Zone is a functional partition within a Layer, clustering by business responsibility.**

Breaking it down, Zones have five key characteristics:

**One, Zones belong to a specific Layer.** Each Zone sits under a specific Layer. TaskZone in Logic layer, TaskUIZone in UI layer. No such thing as "cross-layer Zones."

**Two, Zones divide by business responsibility, not technical type.** "Task Management" is a Zone, "Timer Service" is a Zone. But "all Managers in one Zone" isn't—"Manager" is a technical naming convention, not a business responsibility.

**Three, Zones have clear labels.** Each Zone's responsibility should be expressible in one sentence. If you need "and" "also" "simultaneously responsible for" to describe a Zone's responsibility, it's probably too big, needs splitting.

**Four, Zone is a logical concept, not a physical folder.** Emphasized heavily last chapter: you don't need to create corresponding folders in your project. Zones exist in a document shared between you and AI—a mapping of "which file belongs to which Zone."

**Five, Zones have boundaries.** A file belongs to only one Zone. If a file "could fit in any Zone," it means either Zone labels aren't clear enough, or the file has too many responsibilities (should itself be split).

---

## Let AI Build Zones

After understanding Zone's definition, let's look at actual operation.

You don't need to open each file and read code yourself. Zone creation and organization can all be done by AI from start to finish.

But AI can't work from nothing—it needs an "instruction manual" telling it what Zones are, how to divide them, what format to output. This manual is already written, called **AI Playbook**. As the name suggests, it's a script for AI—defining all rules, judgment criteria, output formats for Layers and Zones. You don't need to write this script yourself—use the ready-made one.

The workflow looks like this:

**Step One**: Throw AI Playbook and your project source code to AI together.

**Step Two**: AI reads all source code, following Playbook rules, automatically completes analysis: judges how many Layers the project has, what Zones exist in each Layer, what files each Zone contains, what dependency relationships exist between Zones.

**Step Three**: AI outputs two files—

- **Layer-Zone Tree**: Text version panoramic photo. Uses structured format to list all Layers, all Zones, each Zone's responsibility and file inventory, dependency relationships between Zones. This is the data source, your main file for review and reference.

- **Layer-Zone Visuals**: Chart version panoramic photo. Uses Mermaid diagrams to visualize Tree information—hierarchy diagrams, dependency graphs, Zone size distribution charts. See the big picture at a glance.

Take GetDone Timer as example. I threw 160 Swift files and AI Playbook to AI. In the output Tree, Logic layer looks like this:

```
💼 Logic Layer
│
├─ TaskZone [execution]  — L.Z1
│  "Task creation, management, state transitions"
│  Contains: CardManager, CardManagerProtocol
│
├─ TimingZone [execution]  — L.Z2
│  "Timer countdown and Pomodoro Focus/Break phase management"
│  Contains: TimerService, PomodoroService
│
├─ ScheduleZone [execution]  — L.Z3
│  "Schedule time slot management, conflict detection, scheduled task launch"
│  Contains: ScheduleManager, ScheduledStartManager
│
├─ AccountZone [execution]  — L.Z4
│  "User authentication, Session management, invite codes"
│  Contains: AccountManager, AuthService, InviteManager
│
├─ AIZone [execution]  — L.Z5
│  "AI multi-Provider calling, prompt assembly, task generation"
│  Contains: AIService, AIAPIClient, AICardGenerator
│
├─ ...(plus PaymentZone, SettingsZone, PermissionZone, etc.)
│
└─ Non-Zone code: DeviceInfo, TimezoneHelper, ThemeManager
```

Each Zone has an ID (L.Z1, L.Z2...), type annotation (execution/organization), one-sentence responsibility description, file inventory, dependency relationships. AI even marks out "which files don't belong to any Zone."

In the corresponding Visuals file, the same information becomes visualization charts—hierarchy overview diagram, dependency graph, rendered directly in Obsidian or GitHub, one chart shows the entire project.

After you get these two files, what should you do? **Review.** Not every line, but check a few key points:

- **Are labels clear?** Can each Zone's responsibility be stated in one sentence? "Task creation, management, state transitions"—clear. If there's a Zone called "Miscellaneous"—unclear, make AI re-divide.
- **Is grouping reasonable?** AI listed PermissionManager as independent PermissionZone—appropriate? It manages permissions (Free/Pro), relates to accounts, should it merge into AccountZone? You make these boundary judgments.
- **Any omissions?** DeviceInfo, TimezoneHelper marked as "non-Zone code"—correct? Yes, they're utility functions, don't need boxing. We'll explain this category later.

AI handles the work (reading code, analyzing, outputting Tree and Visuals), you handle decisions (is this division good, should it be adjusted). **You're the editor, not the author.**

Roles of three tools:

| Tool | What It Is | For Whom |
|:---|:---|:---|
| **AI Playbook** | AI's script—how to analyze, how to group, how to output | For AI |
| **Layer-Zone Tree** | Text panoramic photo—structured Zone inventory and dependencies | For you (review use) |
| **Layer-Zone Visuals** | Chart panoramic photo—Mermaid visualization diagrams | For you (global view) |

You don't need to read every rule in AI Playbook—that's AI's script, not yours. You just need to understand Tree and Visuals output, be able to judge "is this grouping reasonable."

---

## What Doesn't Need Boxing

In AI's grouping proposal, there will definitely be a few files not categorized into any Zone.

Like GetDone Timer's Logic layer's DeviceInfo (device info utility methods) and TimezoneHelper (timezone conversion). They don't belong to any specific business domain—anyone might call them, but they themselves don't represent a "feature."

**These things don't need boxing.** They're like scissors and tape lying on the shelf—grab-and-use tools, not worth a dedicated storage box.

In the Zone system, this category is called **Non-Zone**.

How to judge whether something should be categorized into a Zone or treated as Non-Zone? When AI's grouping proposal has files you're uncertain about, use these four questions for quick judgment:

1. **Has independent business responsibility?** (not just utility functions)
2. **Manages its own state?** (has independent lifecycle)
3. **Depended on by other Zones?** (changing it affects others)
4. **Will evolve independently?** (will grow more complex in the future)

Hit two or more of four → should be categorized into a Zone (or create separate Zone).
Fewer than two → Non-Zone, leave scattered on shelf.

TimezoneHelper? No business responsibility, doesn't manage state, changing it doesn't affect others, won't grow complex. Hit none of four. Non-Zone.

PermissionManager? Has independent responsibility (manages permission levels), manages own state (current user is Free or Pro), other Zones depend on it (many features check permissions), will grow complex (new subscription tiers added). Hits all four. Should be categorized into Zone.

You don't need to execute this judgment standard yourself—you can directly tell AI: "Help me judge these files, should they be categorized into Zones or be Non-Zone?" AI will analyze, you make the call.

---

## Two Roles of Zones

In AI's divided Zones, you'll notice they do different things. Some Zones "do work," some Zones "coordinate."

**Execution Zones: directly do work.**

CardManager in TaskZone creates tasks, deletes tasks. TimerService in TimerZone counts down, pauses, resumes. These Zones have concrete business logic—you ask AI to modify a feature, you're modifying code in these Zones.

**Organization Zones: only coordinate, don't do work.**

GetDone Timer's Core layer has an AppZone.swift. It's the coordination center for the entire application—creates all Managers and Services, connects them together. But it itself **contains no business logic**. It doesn't know how tasks sort, doesn't know how timers pause. It only handles "assembling the right parts together."

Judgment simple: has concrete business implementation → execution type. Only coordinates other Zones → organization type.

This distinction's value: **it tells you where to find code.** Want to modify business logic, go to execution Zones. Want to modify startup flow or page navigation, go to organization Zones. Telling AI is the same—"add a new Manager initialization in AppZone" and "modify task sorting in TaskZone," AI immediately knows which files to open.

---

## Big Boxes Containing Small Boxes

Some Zones will be large.

GetDone Timer's UI Layer, MainWindow directory has over seventy Swift files. If AI groups all these into one "MainWindowUIZone"—that's like not dividing at all.

At this point you tell AI to continue subdividing. AI will further divide within the big Zone into small Zones:

```
MainWindowUIZone (big box)
├── CardViewUIZone      → Task card rendering (14 files)
├── ScheduleUIZone      → Schedule planning interface (16 files)
├── AccountUIZone       → Account page (9 files)
├── AIAssistantUIZone   → AI assistant interface (15 files)
├── SettingsUIZone      → Settings page (4 files)
├── DialogsUIZone       → Various dialogs (9 files)
├── SidebarUIZone       → Sidebar (1 file)
└── MainContentUIZone   → Main content grid (1 file)
```

Over seventy files, one division makes it clear. Want to modify schedule interface's Week view? Go to ScheduleUIZone. Want to modify task card Footer buttons? Go to CardViewUIZone.

This is **Zone nesting**: big boxes containing small boxes.

Hierarchy suggestion no more than three levels: Layer → Zone → Sub-Zone. Further splitting is over-design. Most projects two levels suffice. Only when a Zone grows to over a dozen files, let AI subdivide one more level.

Judgment standard very intuitive: **A Zone exceeds 10-15 files, should split.**

---

## Same Feature, Different Layer Boxes

The "task" feature has code in different layers:

- **Data layer**: TaskDataZone — how task data is stored
- **Logic layer**: TaskZone — task business rules
- **Glue layer**: TaskGlueZone — connects UI and Logic
- **UI layer**: TaskUIZone — what task cards look like

How to make them align at a glance? **Naming convention**:

| Layer | Naming Format | Example |
|:---|:---|:---|
| Data | [Feature]**Data**Zone | TaskDataZone |
| Logic | [Feature]Zone (no suffix) | TaskZone |
| Glue | [Feature]**Glue**Zone | TaskGlueZone |
| UI | [Feature]**UI**Zone | TaskUIZone |

Logic layer is the main Zone, no suffix—because business logic is a feature's core. Other layers add suffixes marking their role.

The name itself is a map. You say "modify TaskZone's sorting logic," AI knows to go to Logic layer. You say "modify TaskUIZone's card layout," AI knows to go to UI layer. No extra explanation needed.

You don't need to invent this naming convention yourself—when telling AI to build Zones, tell it: "For same feature's Zones in different layers, follow this naming rule." AI will automatically align.

---

## Dependency Rules: How Boxes Interact

Zones aren't isolated. When task starts running, TaskZone needs to notify TimerZone to start timing. When schedule planning, ScheduleZone needs to get task list from TaskZone.

These relationships are normal. But rules are needed, so when you see AI's analysis results you know which dependencies are reasonable, which are problematic.

**Cross-layer dependencies: strictly downward.**

UI layer can depend on Logic layer, Logic layer can depend on Data layer, not the reverse. If AI's analysis report shows "TaskZone → TaskUIZone" (Logic layer depending on UI layer)—this is reverse dependency, problematic.

**Same-layer dependencies: allowed, but fewer the better.**

TaskZone calling TimerZone to start timing—reasonable. But if every Zone in the same layer has dependencies on all other Zones—it becomes a spider web. Ideal state is a few clear connections.

**What if violated?**

In real projects dependencies can't be perfect. Manage with three levels:

- 🟢 **Acceptable**: Occasionally jumps a layer, small impact, just note it.
- 🟡 **Watch**: Currently controllable but growing, handle during next refactor.
- 🔴 **Must fix**: Reverse dependency or circular dependency (A depends on B, B also depends on A), Zone boundaries will fail, fix soon.

This grading's significance: **Don't stop because pursuing perfection.** Vibe Coding's rhythm is rapid iteration. Grading lets you know what can wait, what must be handled now.

When AI finishes analyzing Zones and marks dependency relationships, what you mainly watch for is any 🔴 level violations. 🟢 and 🟡 note them first, no need to handle immediately.

---

**Chapter Summary**

> Zone has five characteristics: belongs to a Layer, divides by business responsibility, clear labels, is logical concept, has clear boundaries.
>
> Zone doesn't need manual building—let AI read code, group, label, you review and decide. Utility code not belonging to any business responsibility is Non-Zone, doesn't need boxing.
>
> Zones divide into execution (doing work) and organization (coordinating). Big Zones can nest small Zones, no more than three levels. Same feature in different layers uses naming convention to align.
>
> Dependency violations grade three levels: 🟢 let it go, 🟡 handle next time, 🔴 fix now.
>
> Now you understand Zone design principles, and know how to let AI do this. Next, it's time to stand back, take a panoramic photo of the entire project.
