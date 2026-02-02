# Chapter 7: Let AI Take the Photo

---

Last chapter looked at what's in the panoramic photo. This chapter covers how to take it.

Three photography methods, suitable for three different scenarios. After reading you'll know when to take photos, how to take them, how to use them after taking.

---

## Three Photography Methods

### Bottom-up: Photographing Existing Projects

**Scenario**: Your project already has a bunch of code, you want to see what it looks like now.

This is the most common method. Project has Vibe Coded to a certain stage, code swelled beyond what your brain can hold, you need a current status photo.

Method is simple: throw AI Playbook and project source code to AI together. AI starts from code, reverse-engineers the entire Layer-Zone structure, outputs Tree and Visuals.

Just "push open the door, take a current status photo of the room." No matter how messy the room, photograph it first, see clearly then talk.

### Top-down: Drawing Blueprint for New Projects

**Scenario**: You're starting a new project, want to plan the organization system before writing code.

At this point there's no code yet, can't reverse-engineer from code. Direction reverses—start from requirements, design Layer-Zone Tree first, then have AI write code according to Tree.

Method: list project's core features (like: task management, timing, notifications, data storage), each feature corresponds to an initial Zone, determine Layer division, plan dependency relationships, output a design version Tree.

This is like "drawing design drawings before renovation." From day one you have a panoramic photo, code grows according to blueprint, won't accumulate black boxes.

### Calibration: Comparing Two Photos

**Scenario**: You already have a Tree (whether Bottom-up photographed or Top-down designed), continued Vibe Coding for a while, want to see how much the project changed.

This is the most valuable method.

Method: Have AI redo Bottom-up analysis once, get a new Tree. Then put new and old Trees together for comparison, AI outputs a diff report.

See an example. Suppose GetDone Timer took a photo in January, another in March:

```
January photo:
  Logic Layer: 5 Zones, largest Zone has 8 files
  Dependency violations: 0

March photo:
  Logic Layer: 7 Zones, largest Zone has 14 files
  Dependency violations: 2

Comparison finds:
  ✅ Added AIZone and StatisticsZone — feature growth, normal
  🟡 TaskZone swelled from 8 files to 14 — consider splitting
  🔴 Appeared one Logic → UI reverse dependency — must fix
  ⚠️ Two utility files ran to Logic layer — should mark as Non-Zone
```

Put two photos together, changes at a glance. What's normal growth, what's noteworthy swelling, what's must-handle problems—all visible.

**This is the rhythm Vibe Coding most needs**: not stopping to check architecture after adding each feature, but regularly taking a photo, comparing with last time, seeing which direction the project is going. Doesn't interrupt your flow, but keeps you continuously controlling the big picture.

---

## Bottom-up: How AI Takes This Photo

Among three methods Bottom-up is most common, let's expand on what AI specifically does.

What you throw to AI is AI Playbook + source code. After AI receives it, following rules defined in Playbook, walks eight steps:

**Step 1: Scan all source files**

AI lists name and path of every code file in the project. This step is pure inventory—first see how much stuff is actually in the room.

**Step 2: Judge Layer structure**

Start from basic three layers (UI / Logic / Data), AI sees if project has signals needing extension layers: independent ViewModels directory with enough files? Add Glue layer. Independent startup / DI container code? Add Core layer. Large amount of cross-layer shared pure data models? Add Models layer.

**Step 3: Assign each file to a Layer**

Key point: **Assign by code content, not folder location.** AI reads file's actual code, judges what it's doing—UI rendering? Business logic? Data storage?—then assigns to corresponding Layer.

This is why Tree can discover "lost files"—an NSWindowController placed in Logic directory, AI reads code finds it's UI component, will mark this deviation.

**Step 4: Cluster into Zones within each Layer**

AI within each layer, groups by "what problem do these files jointly solve." The answer becomes Zone's name and responsibility description. Grouping basis is code's actual functionality, not filename prefix or folder name.

**Step 5: Fill in Zone detailed information**

Each Zone's name, belonging Layer, type (execution/organization), responsibility description, contained file list, depended other Zones.

**Step 6: Mark Non-Zone code**

Utility functions, constants, extension methods not belonging to any Zone, listed in corresponding Layer's "Non-Zone code" inventory. AI will use the four judgment criteria from last chapter to confirm they indeed don't need Zone creation.

**Step 7: Analyze dependency relationships**

This step is Tree's diagnostic value location. AI checks which other Zones each Zone depends on, method is scanning in code for:

- Constructor injection (`init(persistence: PersistenceProtocol)`)
- Singleton references (`AccountManager.shared`)
- Protocol implementations
- Combine subscriptions
- Notifications and callbacks

Especially watch `.shared` singletons—they hide dependency relationships. A file writes `AccountManager.shared.state`, means it depends on AccountZone, even without constructor injection.

After scanning, AI makes compliance judgment for each dependency: is direction correct? Any layer-jumping? Any reverse dependencies? Violations marked with 🟢🟡🔴 three levels.

**Step 8: Output Tree + Visuals**

All analysis compiled, outputs two files. All those seen last chapter—structure overview, Zone details table, dependency compliance table, statistics summary, lost files list, ownership pending table—all generated in this step.

Eight steps, start to finish all done by AI. What you need to do is throw Playbook and source code to it, then wait for results to come out for review.

---

## How to Do Calibration

Calibration operation also very simple:

**First step**: Have AI re-analyze current code in Bottom-up method once, get new Tree.

**Second step**: Throw new Tree and old Tree to AI together, have it compare item by item.

**Third step**: AI outputs diff report, content includes:

- New Zones (feature growth)
- Disappeared Zones (feature deletion or merging)
- Zone internal file count changes (which are swelling)
- New dependency relationships (any new violations)
- New deviations of physical location and logical ownership

You look at diff report, judge which changes are normal, which need handling. Most changes are normal—you added new features, naturally more Zones appear. What you watch for are abnormal signals: Zone swelling, new violations, file misplacement.

---

## When to Take Photos

Don't need to photograph every time after writing code. Too frequent becomes burden, too sparse loses control.

**Recommended rhythm**:

- **Every 2-4 weeks once**, or
- **After completing each major feature once**

Specifically depends on your Vibe Coding intensity. If you added three new features in a week, photographing once every two weeks is appropriate. If you're slowly polishing details, once every four weeks suffices.

**Several good photo timing moments**:

- You just finished adding a major feature (schedule module, AI assistant, payment system), want to see its impact on overall architecture
- You feel project "starting to get messy"—this intuition is usually right, take a photo to confirm
- Before you're about to start a major refactor or new feature development round, first take a current status photo for archiving
- You need to explain project structure to others (collaborators, investors, or future self)

**Timing that doesn't need photographing**:

- Fixed a bug
- Adjusted a color
- Added a button

These small changes won't affect architecture. Wait for them to accumulate to a certain amount, next regular photo will naturally reflect them.

Core principle: **Panoramic photo is background-running architecture guardian, not foreground process approval.** It shouldn't drag down your Vibe Coding rhythm. You should add features add features, should iterate iterate—just periodically stop to take a photo, confirm you haven't deviated from course.

---

## Choosing Among Three Methods

| Method | Applicable Scenario | Operation |
|:---|:---|:---|
| **Bottom-up** | Existing project, want to see current status | Playbook + source → AI analyzes → Tree + Visuals |
| **Top-down** | New project, want structure from day one | Requirements list → design Zones → output blueprint Tree |
| **Calibration** | Ongoing development, want to see changes | Redo Bottom-up → new/old Tree compare → diff report |

Most Vibe Coders' first photo is Bottom-up—project already wrote a bunch, want to see what it actually looks like.

After that is Calibration's cycle—regularly rephotograph, compare with last time.

Top-down suitable when you start a completely new project, or about to add a large new module.

Three methods aren't mutually exclusive, they're the same tool's usage at different stages.

---

**Chapter Summary**

> Three photography methods: Bottom-up (photograph existing code's current status), Top-down (draw blueprint for new project), Calibration (compare new/old photos to see changes).
>
> Bottom-up is most common—AI's eight steps: scan files → judge Layers → assign files → cluster Zones → fill details → mark Non-Zone → analyze dependencies → output Tree + Visuals. Entire process AI completes, you review results.
>
> Calibration is most valuable—regularly rephotograph, new/old compare, changes at a glance. Recommend every 2-4 weeks or after each major feature completes once.
>
> Panoramic photo is background architecture guardian, not foreground process approval. Doesn't interrupt your Vibe Coding rhythm, but keeps you continuously controlling the big picture.
