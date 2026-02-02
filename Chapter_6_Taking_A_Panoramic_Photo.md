# Chapter 6: Taking a Panoramic Photo of Your Project

---

This chapter does exactly that: **Stand back, take a panoramic photo of the whole room.**

---

## What Is Layer-Zone Tree

Layer-Zone Tree is your project's panoramic photo.

It's a document—gathering all Layers, all Zones, each Zone's responsibility, contained files, dependency relationships between Zones, all compiled together. One document, answers six questions:

1. How many Layers does the project have?
2. What Zones exist in each Layer?
3. What is each Zone responsible for?
4. Which files belong to each Zone?
5. What dependency relationships exist between Zones?
6. Are there files not belonging to any Zone?

Answer all six questions, your global cognition of the project is rebuilt. Not "vaguely know," but "see crystal clearly."

Last chapter said, this document doesn't need manual writing—throw AI Playbook and source code to AI, AI will automatically output two files:

- **Layer-Zone Tree**: Text version panoramic photo, structured data.
- **Layer-Zone Visuals**: Chart version panoramic photo, Mermaid visualization.

This chapter we'll see what's actually in these two files.

---

## What Tree Looks Like

Look directly at GetDone Timer's real Tree. After AI analyzed 160 Swift files, the output structure overview looks like this:

```
GetDoneTimerV1 — Layer-Zone Tree

🚀 Core Layer
├─ BootstrapZone [organization]  — Core.Z1
│  "Application startup, DI container assembly, lifecycle management"
│  Contains: main, AppDelegate, AppZone, AppSecrets

📱 UI Layer
├─ MainWindowZone [organization]  — UI.Z1
├─ SidebarUIZone [execution]      — UI.Z2
├─ CardUIZone [execution]         — UI.Z3    (15 files)
├─ ScheduleUIZone [execution]     — UI.Z4    (19 files)
├─ AIAssistantUIZone [execution]  — UI.Z5    (14 files)
├─ AccountUIZone [execution]      — UI.Z6    (9 files)
├─ SettingsUIZone [execution]     — UI.Z7
├─ DialogUIZone [execution]       — UI.Z8    (11 files)
├─ GroupUIZone [execution]        — UI.Z9
├─ MenuBarUIZone [execution]      — UI.Z10
└─ StatisticsUIZone [execution]   — UI.Z11   (10 files)

🔗 Glue Layer
├─ TaskGlueZone       — G.Z1
├─ ScheduleGlueZone   — G.Z2
├─ AIGlueZone         — G.Z3
├─ AccountGlueZone    — G.Z4
└─ StatisticsGlueZone — G.Z5

💼 Logic Layer
├─ TaskZone          — L.Z1
├─ TimingZone        — L.Z2
├─ ScheduleZone      — L.Z3
├─ AccountZone       — L.Z4
├─ AIZone            — L.Z5
├─ GroupZone         — L.Z6
├─ SettingsZone      — L.Z7
├─ StatisticsZone    — L.Z8
├─ PaymentZone       — L.Z9
├─ PermissionZone    — L.Z10
├─ NotificationZone  — L.Z11
└─ HotkeyZone        — L.Z12

💾 Data Layer
├─ PersistenceZone     — D.Z1
├─ UserDataZone        — D.Z2
├─ AIDataZone          — D.Z3
└─ ScheduleDataZone    — D.Z4

📦 Models (cross-layer shared, 24 files)
└─ All pure value types, no Zones
```

160 files. 6 Layers. 33 Zones. All unfolded on one page.

Notice each Zone's ID: UI.Z3, L.Z1, D.Z2... Prefix is Layer abbreviation, followed by sequence number. One look at the ID, you know which layer this Zone is in. In all subsequent dependency analysis and violation reports, the ID is the location coordinate.

---

## What Can Be Seen in the Photo

Tree isn't just an inventory. It's a diagnostic report.

After AI finishes analysis, besides structure overview, it also outputs several specific "check-up tables." Let's see what Tree discovered in GetDone Timer.

### Dependency Relationships: Who Relates to Whom

Tree contains a complete dependency compliance table. Every dependency between Zones is listed and marked whether compliant:

```
✅ Compliant: UI.Z3 CardUIZone → G.Z1 TaskGlueZone
✅ Compliant: G.Z1 TaskGlueZone → L.Z1 TaskZone, L.Z2 TimingZone
✅ Compliant: L.Z1 TaskZone → D.Z1 PersistenceZone
```

UI layer depends on Glue layer, Glue layer depends on Logic layer, Logic layer depends on Data layer—all directions downward, compliant.

But there are also non-compliant ones:

```
🟢 Acceptable: UI.Z7 SettingsUIZone → L.Z7 SettingsZone
   (Settings UI directly reads SettingsManager, skipped Glue layer, but scenario simple, doesn't need ViewModel)

🟡 Watch: G.Z3 AIGlueZone → D.Z3 AIDataZone
   (Glue layer directly accesses Data layer, skipped Logic layer. Currently pure CRUD, risk controllable,
    but if later conversation history needs complex business logic, should add Logic layer intermediary)
```

GetDone Timer's 160 files, 27 dependency relationships: 24 compliant, 2 🟢, 1 🟡, 0 🔴. Architecture overall healthy.

**Could you see this information before?** Couldn't. They're hidden in code, hidden in import statements between files. You couldn't possibly memorize 27 dependency relationships' compliance status in your brain. But Tree looked for you, marked for you, graded for you.

### Swelling Zones: Which Box Too Full

Tree comes with a Zone details table, listing each Zone's file count:

| Zone | File Count |
|:---|---:|
| UI.Z4 ScheduleUIZone | 19 |
| UI.Z3 CardUIZone | 15 |
| UI.Z5 AIAssistantUIZone | 14 |
| UI.Z8 DialogUIZone | 11 |
| UI.Z11 StatisticsUIZone | 10 |

ScheduleUIZone has 19 files—the largest Zone in the entire project. Last chapter said, exceeding 10-15 files should consider splitting. Here you can see at a glance which boxes are swelling.

### Lost Files: Misplaced Things

This is the most interesting part. AI doesn't classify by folder—it reads code content, judges ownership based on what the code actually does. This means it can discover **files where physical location and logical ownership are inconsistent**.

GetDone Timer's Tree marked several deviations:

| Physical Location | Logical Ownership | What Happened |
|:---|:---|:---|
| Logic/GoogleSignInWindow | UI.Z6 AccountUIZone | A UI component placed in Logic directory—it's WKWebView OAuth window, pure UI code |
| MainWindow/Schedule/ScheduleCoordinator | G.Z2 ScheduleGlueZone | A Glue layer Coordinator placed in UI directory |
| MainWindow/AIAssistant/.../ConversationRecord | Models Layer | A pure data model placed in UI directory |

Did you know about these "lost files" before? Probably not. They won't cause compile errors, won't crash the app, but they're quietly polluting your architecture—a UI component mixed in Logic layer, next time you tell AI "modify Logic layer authentication flow," AI might modify this UI file too.

**Tree makes these hidden problems visible.** Only when seen can you decide whether to handle them.

### Ownership Pending: Files AI Also Uncertain About

Some files, after AI analysis, feel "any Zone would make sense"—it won't force them—instead lists candidate proposals, lets you decide:

| File | Candidate A | Candidate B | Reason |
|:---|:---|:---|:---|
| GoogleSignInWindow | L.Z4 AccountZone | UI.Z6 AccountUIZone | Physical in Logic but content is UI component |
| ConversationRecord | UI.Z5 AIAssistantUIZone | Models Layer | Physical in UI but essence is pure data model |

AI does analysis, you make decisions. This division of labor is consistent in every link of Tree.

---

## Visuals: Chart Version Panoramic Photo

Tree is the text version panoramic photo—detailed, complete, suitable for review and reference. But sometimes what you need isn't details, but seeing the whole at a glance.

This is Visuals file's purpose. It transforms Tree's information into Mermaid charts, rendered directly in Obsidian, GitHub, VS Code.

GetDone Timer's Visuals has several key diagrams.

**Hierarchy Overview Diagram**: One diagram shows all Layers and all Zones' distribution. Core layer 1 Zone, UI layer 11 Zones, Glue layer 5 Zones, Logic layer 12 Zones, Data layer 4 Zones. The project's "skeleton" at a glance.

**Dependency Graph**: All dependency connections between Zones drawn out, compliant ones use solid lines, violations use dashed lines with color markers. You don't need to read the compliance table line by line—glance at the diagram, where the dashed lines are, that's where problems are.

**Feature Slice Diagram**: Pick a feature (like "task management"), see how it penetrates from UI to Data:

```
UI.Z3 CardUIZone (15) → G.Z1 TaskGlueZone (4) → L.Z1 TaskZone (2) → D.Z1 PersistenceZone (2)
```

How many files a feature has in four layers, how they connect—one line makes it clear.

**File Distribution Pie Chart**: 160 files' distribution across layers—UI layer 89 (56%), Logic layer 30, Models 24, Glue layer 14, Data layer 7. If a layer's proportion is abnormally large, indicates that layer might need finer Zone splitting.

Tree and Visuals are two presentations of the same photo. Tree is data source, you use it for reviewing details. Visuals is visualization, you use it for seeing the big picture.

---

## Statistics Summary: A Photo's Data Fingerprint

Tree's end also has a statistics summary—using a few numbers to summarize the photo's key information:

```
Layer count: 6 (Core + UI + Glue + Logic + Data + Models)
Zone total: 33 (execution 31 + organization 2)

File total: ~160
  In Zones: ~148
  Non-Zone: ~7
  Models (cross-layer shared): 24
  Ownership pending: 2

Dependency count: 27
  ✅ Compliant: 24
  🟢 Acceptable: 2
  🟡 Watch: 1
  🔴 Must fix: 0
```

These numbers are your project's "check-up report summary." Next time AI retakes the photo, you compare two summaries—Zone count changed? Violations increased? Any new 🔴?—changes at a glance.

---

## Seeing Is Half the Solution

Back to the predicament mentioned in the preface: project getting bigger, you can't see what it looks like anymore.

Layer-Zone Tree is the answer. It doesn't help you write code, doesn't help you fix bugs, doesn't help you add features—it only does one thing: **makes you see.**

See how many layers the project has, what Zones exist in each layer. See dependency relationships between Zones, which are compliant, which violated. See which Zone is swelling, which file is misplaced. See the entire project transform from 160 scattered files into a structured, labeled, relationship-mapped panoramic view.

You don't need to remember every line of code—AI remembers.

You just need to see the big picture clearly—Tree helps you see.

**Commander with a map, elite troops can exert maximum combat power.**

---

**Chapter Summary**

> Layer-Zone Tree is your project's panoramic photo. It answers six questions: how many layers, how many Zones, each responsible for what, contains which files, dependency relationships, any omissions.
>
> Tree isn't just an inventory, it's a diagnostic report: compliant/violated dependencies, swelling Zones, lost files, ownership pending edge cases—all visible.
>
> Visuals file turns Tree's information into charts: hierarchy overview, dependency graph, feature slice, file distribution—see the whole at a glance.
>
> But the coolest part is—you don't need to take this photo yourself. Last chapter already said, throw AI Playbook + source code to AI, Tree and Visuals come out. Next chapter, let's see how to make AI help you regularly take photos, continuously maintain control of project changes.
