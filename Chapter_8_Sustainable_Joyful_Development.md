# Chapter 8: Vibe Coding + Panoramic Photo = Sustainable Joyful Development

---

The first seven chapters walked a complete path: starting from Vibe Coding's honeymoon phase, experiencing the black box predicament, learned layering (Layer) and zoning (Zone), then used Layer-Zone Tree to take a panoramic photo of the project, also learned to have AI help you photograph.

Tools complete. Methods in hand.

This chapter answers the final question: **How do these things integrate into your daily development?**

Not saying starting tomorrow spend two hours daily on architecture—that wouldn't be Vibe Coding anymore. But finding a rhythm that lets you enjoy Vibe Coding's speed and excitement while not losing direction when the project swells.

---

## Sustainable Workflow

Condensing the entire book into one workflow, it's two things alternating:

**Daily: Vibe Coding.**

Think of what feature, build it. AI helps you write code. Rapid iteration. Don't need to stop and check architecture every time you write a code segment—that would completely disrupt your rhythm. Vibe Coding's core is "follow intuition," don't change this.

**Periodically: Take a panoramic photo.**

Every interval (2-4 weeks, or after a major feature completes), have AI re-analyze code once, output new Tree and Visuals. Then compare with last photo—see what changed in the project.

Just these two things. Daily Vibe Coding, periodic photo comparison.

Specifically, after periodically photographing you'll do three actions:

**First, see changes.**

New Tree and old Tree placed together, differences at a glance. What new Zones added? Which Zones' file counts growing? Any new dependency violations? Most changes are normal—you added new features, naturally more Zones and files. What you watch for are abnormal signals.

**Second, mark problems.**

Discovered abnormality then mark it down. Some Zone swelled from 8 files to 15—mark "consider splitting next time." Appeared a new 🟡 dependency—mark "handle during next refactor." A file ran to wrong Layer—mark "move back when there's opportunity."

Note: marking problems doesn't equal immediately fixing. Most problems can accumulate, handled together when the time's right. Only 🔴 level violations (reverse dependencies, circular dependencies) need prompt handling, because they make Zone boundaries fail, harder to fix the longer you drag.

**Third, continue Vibe Coding.**

Finished looking at photo, finished marking problems, close Tree file, continue your daily development. Should add features add features, should fix bugs fix bugs. Next periodic photo, come back to see whether those marked problems worsened.

```
Daily                      Periodic
┌─────────────┐            ┌───────────────┐
│  Vibe Coding │   Every   │  AI takes      │
│  AI crushing │  2-4 wks  │  panoramic     │
│  it          │ ──────→   │  photo         │
│  Rapid       │           │  New/old Tree  │
│  iteration   │           │  compare       │
│  Follow      │    ←────── │  Mark abnormal │
│  intuition   │           │  signals       │
│              │           │  🟢🟡 note first│
│  Continue    │           │  🔴 handle soon│
│  developing  │           │                │
└─────────────┘            └───────────────┘
```

This loop's core principle: **Panoramic photo is background-running architecture guardian, not foreground process approval.**

You don't need to check Tree before modifying code each time, don't need to update Zone mapping every time adding a file, don't need to draw architecture diagrams before starting to write code. These things would kill Vibe Coding's rhythm.

What you need to do is just periodically step back, glance at the big picture. Like driving long distance—you don't need to check navigation every second, but you need to occasionally glance, confirm you're still on the right road.

---

## New Projects: Have Panoramic Photo from Day 1

If you're about to start a completely new project, you have a huge advantage: you can establish panoramic photo from day one.

Last chapter covered three photography methods, among them Top-down is prepared for new projects. Before writing the first line of code, plan Layer-Zone structure first.

**How specifically?**

**First step: List core features.**

Don't need to list very detailed, just list project's main feature modules. Like you're making a task management app:

- Task creation and management
- Timer (Pomodoro + free timer)
- Schedule planning
- Data persistence
- User settings

**Second step: Determine Layer structure.**

Most projects three layers suffice—UI, Logic, Data. If you expect fairly complex ViewModel logic (like needing lots of data transformation between UI and Logic), can add a Glue layer. If there's quite a few cross-layer shared pure data models, can add a Models layer.

If uncertain, start with three layers. Later discover not enough then add, better than over-designing from the start.

**Third step: Plan initial Zones for each feature.**

Each core feature has one Zone in corresponding Layer:

```
UI Layer:    TaskUIZone, TimerUIZone, ScheduleUIZone, SettingsUIZone
Logic Layer: TaskZone, TimerZone, ScheduleZone, SettingsZone
Data Layer:  PersistenceZone
```

This is your blueprint version Tree. Very rough, very simple—but it's enough.

**Fourth step: Give blueprint to AI, have AI write code by Zone.**

You tell AI: "Now implementing task creation feature, code goes in TaskZone (Logic layer) and TaskUIZone (UI layer)." AI from the start writes code in correct Zones, not randomly finding a place to stuff.

**Benefit of having panoramic photo from Day 1**: You won't accumulate black boxes. Each line of new code when written, it's already in correct position. During project growth process, you always see clearly what it looks like.

Don't need to wait until "project messy" then organize—because it never got messy from the start.

Of course, blueprint can't stay unchanged. As development progresses, you'll discover need for new Zones, need to split certain Zones, need to adjust dependency relationships. This is all normal. Blueprint is starting point, not endpoint. Periodically use Calibration to photograph and compare, see deviation between actual code and blueprint, adjust when should adjust.

---

## Existing Projects: Progressive Transformation

More common situation: your project already Vibe Coded for a while, code already swelled, you now want to introduce panoramic photo.

Good news: **Don't need to tear down and rebuild.**

You don't need to stop development, spend a week reorganizing project structure. You also don't need to move any files, change any directories. Remember Chapter 4's conclusion—Zone is logical concept, not physical folder. Introducing Zone has zero cost.

Progressive transformation four steps:

**First step: Have AI do Bottom-up analysis once.**

Throw AI Playbook and project source code to AI, have it output Tree and Visuals. This is your first panoramic photo—a current status photo. No matter how messy the project, photograph it first, see clearly then talk.

**Second step: Review photo, find biggest pain points.**

After you get Tree, first don't try to fix all problems. Look at a few key indicators:

- Any 🔴 level dependency violations? (reverse dependencies, circular dependencies)
- Any severely swelling Zones? (exceeding 15 files)
- Any files obviously misplaced? (UI components mixed in Logic layer and such)

Find the most painful one or two points.

**Third step: Start fixing from the most painful place.**

Only handle one problem at a time. Like you discovered Logic layer has a reverse dependency—a logic file directly references UI component. Tell AI: "This file shouldn't depend on UI layer, help me decouple through callback or protocol." AI fixes, this 🔴 eliminated.

Or like you discovered TaskZone has 18 files, obviously too big. Tell AI: "Help me analyze TaskZone whether it can split." AI might suggest extracting "task sorting" related files into a TaskSortingZone, or extracting "task state transitions" into a TaskStateZone. You look at proposal, judge reasonable or not, make call.

**Fourth step: Periodically photograph, continuously iterate.**

After fixing the most painful problems, return to daily Vibe Coding. Wait until next periodic photo, you'll discover: last marked 🔴 disappeared, some 🟡 might have improved or worsened, might have new problems appeared.

This is progressive transformation's rhythm: **Don't pursue one-step perfection, each time only handle the most painful one or two problems.** Several rounds down, project's architecture health will continuously improve—and you never stopped developing for this.

Use a timeline to see GetDone Timer's transformation process:

```
1st photo (current status photo):
  160 files, 33 Zones
  🔴 0  🟡 1  🟢 2
  2 files clearly misplaced
  → Mark problems, continue developing

2nd photo (4 weeks later):
  Added 2 Zones (StatisticsZone, StatisticsUIZone)
  That 🟡 dependency hasn't worsened, leave it for now
  ScheduleUIZone grew from 16 files to 19 → mark "consider splitting"
  → Continue developing

3rd photo (another 4 weeks later):
  ScheduleUIZone continued swelling to 22 files → decide to split
  Have AI split ScheduleUIZone into ScheduleDayUIZone and ScheduleWeekUIZone
  After splitting rephotograph to confirm: structure clear, continue developing
```

Each photo a few minutes, looking at photo ten-some minutes, handling problems maybe half hour to an hour. This is all the extra investment. In exchange you always see clearly what project looks like.

---

## Practical Advice

Several experiences accumulated in practice, help you avoid detours.

### Give AI Complete Source Code, Not Just Directory Structure

When having AI do Bottom-up analysis, must give complete source code files. Only giving filenames and directory tree isn't enough—AI needs to read code content to judge what a file is actually doing.

Filenames can deceive. A file called `GoogleSignInWindow.swift` placed in Logic directory, looking at name and location seems like Logic layer authentication code. But AI reads code discovers—it's a WKWebView popup, pure UI component, should belong to UI layer. If AI only looks at filename and path, will classify wrong.

### First Handle 🔴, 🟢 and 🟡 Can Wait

Dependency violation's three-level classification isn't decoration. 🔴 means Zone boundaries are failing—two Zones mutually depend, changing one might cascade break another, AI's isolation during work also decreases. This kind of problem drags longer harder to fix.

🟢 and 🟡 usually controllable. A simple scenario jumped a layer (🟢), or some direct connection temporarily doesn't affect functionality (🟡), these can accumulate to appropriate time to handle together. Don't interrupt your development rhythm because pursuing "all green."

### Swelling Zones Must Split

A Zone exceeds 10-15 files, should consider splitting. Not splitting's consequence is what? You tell AI "modify Week view in ScheduleUIZone," AI needs to read 19 files to understand this Zone's full picture—half of which are Day view code completely unrelated to Week view. Context window wasted, AI's attention diluted.

After splitting, you say "modify date switching in ScheduleWeekUIZone," AI only needs to read 8 files, all related to Week view, attention one hundred percent concentrated.

Splitting judgment doesn't need you to do yourself—tell AI "this Zone too big, help me analyze how to split," AI will give you proposal, you make call.

### Physical Location and Logical Zone Inconsistent? Mark First, No Rush

Tree might tell you some files' physical directory and logical ownership inconsistent. Like a UI component placed in Logic directory.

This inconsistency isn't urgent. Where file is in which folder doesn't affect code running, also doesn't affect AI analysis (because AI judges ownership by code content, not folder path). First mark it in Tree.

If someday you decide to do a round of directory refactoring—move files to directories consistent with logical ownership—handle it then. But this is completely optional. Many projects carry this inconsistency and run fine.

### Don't Let Panoramic Photo Become Process Approval

This is the most important point.

Panoramic photo's value lies in "making you see." But if you turn it into an approval process—check Tree before adding features each time, immediately update Zone mapping after modifying code each time, validate whether conforms to Zone boundaries before AI outputs code—then you've turned a lightweight cognitive tool into a heavy process burden.

**Panoramic photo is background guardian, not foreground approver.**

Should add features add features, should iterate iterate. Only look at Tree when periodically photographing. Like car navigation—it runs quietly in background, you occasionally glance to confirm direction, but you won't stop to look at navigation every time you press the gas pedal.

If you discover yourself starting to slow down development speed for "keeping Tree perfect," indicates you over-used it. Back up, return to "daily Vibe Coding + periodic photographing" rhythm.

---

## From Black Box to Panoramic Photo

Look back at the path we walked.

Preface's predicament was: project getting bigger, you can't see what it looks like anymore. You're guessing, not judging. AI gets stronger, you get more lost easier.

Chapters 1 to 2 established the problem's essence: not that there's too much code, but you lack a method to organize code. Commander lost the map, elite troops no matter how strong are useless.

Chapters 3 to 5 gave you classification tools: Layer (storage cabinet) divides code by technical responsibility into layers, Zone (storage boxes) divides by business responsibility within each layer into partitions, every file has clear ownership. Classification system built.

Chapters 6 to 7 turned classification system into a visible map: Layer-Zone Tree is your project's panoramic photo, AI helps you photograph, you look. Periodically rephotograph, new/old compare, changes at a glance.

This chapter strings everything into a sustainable workflow: daily Vibe Coding unchanged, periodically photograph to see big picture. New projects have blueprint from Day 1, existing projects progressively transform.

**One line walked through: from "can't see" to "see clearly."**

This isn't some profound methodology. At its root just a simple idea:

Classify code properly (Layer + Zone), then take a panoramic photo (Layer-Zone Tree).

Classification gives each file ownership. Panoramic photo lets you see the big picture. Seeing it, your instructions to AI become precise. Instructions precise, AI's execution won't deviate. Won't deviate, project won't lose control.

This is Vibe Coding's truly sustainable way—not relying on "writing code faster" to solve problems, but relying on "seeing clearer" to maintain control.

---

## Commander's Map

Finally, a feeling to share.

My experience building GetDone Timer, the biggest lesson wasn't technical, but cognitive.

For AI-era developers, the scarcest capability isn't writing code—AI writes better, faster than you. The scarcest capability is **understanding the big picture**. Knowing what the project looks like, knowing where to add things, knowing changing one place affects which places.

This capability won't become obsolete as AI gets stronger. On the contrary, the stronger AI becomes, the more code it produces, the faster projects swell, the more you need a map to maintain sense of direction.

Layer-Zone Tree is this map.

It doesn't help you write code—AI writes better than you.
It doesn't help you fix bugs—AI fixes faster than you.
It only does one thing: **makes you see.**

See project's full picture, see where each file is, see dependency relationships between Zones, see where's swelling, see where's violations.

A commander who sees the big picture clearly, plus an AI force with maxed execution—this combination is truly unstoppable.

AI will get stronger and stronger. Code will get more and more. Projects will get more and more complex.

But as long as you hold a panoramic photo in hand—you won't get lost.

---

**Chapter Summary**

> Sustainable workflow: daily Vibe Coding (follow intuition, AI crushing it) + periodic panoramic photo (every 2-4 weeks, AI analyzes code, new/old Tree compare).
>
> New projects can have panoramic photo from Day 1—Top-down plan initial Zones, AI writes code by Zone, won't accumulate black boxes.
>
> Existing projects don't need tearing down and rebuilding—Bottom-up first take current status photo, find most painful problems, fix one or two at a time, progressively improve.
>
> Panoramic photo is background architecture guardian, not foreground process approval. Don't let it drag down your Vibe Coding rhythm.
>
> A commander who sees the big picture clearly + an AI force with maxed execution = unstoppable.
