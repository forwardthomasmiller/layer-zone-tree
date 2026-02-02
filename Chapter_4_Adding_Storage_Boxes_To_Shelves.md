# Chapter 4: Adding Storage Boxes to Shelves

---

Last chapter ended in a somewhat awkward position.

Storage cabinet bought. Three-layer shelves arranged—UI, Logic, Data, each in place. Results were real: finding things had direction, instructions to AI more precise than before.

But stuff on each shelf still scattered.

Especially Logic layer. Task management, timer service, Pomodoro logic, schedule planning, state management, notification triggers... a dozen files piled in this big category "Logic layer." You know what you're looking for is on the third floor, but the third floor itself is an ocean.

This chapter solves this problem: how to group and classify stuff on the shelves.

---

## Zone: Labeled Storage Boxes

Layering solved "how many layers," but didn't solve "who belongs with whom inside each layer." A dozen files piled in Logic layer—you know what you want is on the third floor, but the third floor itself is a tangled mess.

I needed something to group files on the shelves. I call it **Zone**.

One-sentence definition: **Zone is a functional partition within a Layer, clustering by responsibility.**

Sounds a bit abstract. The storage box analogy makes it intuitive:

Layer is one shelf in the storage cabinet. Zone is a storage box placed on the shelf—the labeled kind.

- **Label** = responsibility definition. Like "Task Management" "Timer Service" "Schedule Planning." The label says what the box holds, not which files it contains.
- **Put in** = Files matching this responsibility go inside. CardManager.swift handles task CRUD? Goes in the "Task Management" box. TimerService.swift handles countdown? Goes in the "Timer Service" box.
- **Won't fit** = If a file doesn't match any existing box labels, either it belongs to another existing box (you mislabeled it), or you need a new box.
- **Scattered items on the shelf** = Utility functions, constants, extension methods—things not belonging to any specific business responsibility don't need to be forced into boxes. They're like loose items on the shelf—leave them there, no need to specially box them.

Back to GetDone Timer's Logic layer, once those dozen files are boxed:

- `TaskZone`: CardManager, CardGroup, state transitions—all logic related to the "task" concept
- `TimerZone`: TimerService, PomodoroService—all logic related to "timing"
- `ScheduleZone`: ScheduleManager, time planning, conflict detection—all logic related to "scheduling"
- `AIZone`: AIService, AIAPIClient, PromptAssembly—all logic related to "AI assistant"

A dozen files scattered on the shelf makes your head spin. Four labeled boxes arranged on the shelf, clear at a glance.

Content unchanged. Not a single file moved. What changed is how you view them.

---

## Zone Is a Label, Not a Move

This point is critical, worth pulling out separately.

**Zone is a logical concept, it doesn't correspond to physical folders.**

You don't need to create a folder called `TaskZone` in Xcode and drag files into it. You don't need to change any directory structure. You don't need to move any files.

You just need to know—"CardManager.swift belongs to TaskZone, TimerService.swift belongs to TimerZone"—like putting an invisible label on each file.

This distinction is important because it determines Zone's adoption cost.

If Zone meant you had to reorganize your project's folder structure, move files, modify import paths, deal with compile errors—that cost would be too high. For a rapidly iterating Vibe Coding project, you can't possibly stop and spend a whole day refactoring directories.

But Zone doesn't require you to do these things. It's a purely cognitive tool. Files stay in their original locations, not a line of code needs changing, the compiler doesn't need to know Zones exist. Zones exist in your mind—or more precisely, in a document you and AI share.

**Adoption cost: zero.**

You're just labeling existing files. Like you don't need to move library books to new shelves—you just need to put a small label on each book, indicating which category it belongs to. Books stay in their original positions, but you know what category they are now.

For Vibe Coders, this means you can introduce Zones anytime, no need to pause development, no need to refactor code, won't disrupt your rhythm. Today you realize Logic layer needs classification, today you can start labeling. Tomorrow continue Vibe Coding, add features as needed.

---

## Changes After Labeling

Zone looks like just "grouping files," a very light action. But this light action's impact in actual development is transformative.

Let me illustrate with two specific scenarios.

**Scenario 1: AI's Working Scope**

Suppose you want to modify "pause logic"—timer running, user clicked pause, how should state be saved and restored.

Without Zones, how do you tell AI? "Help me modify pause-related code in Logic layer." How many files in Logic layer? A dozen. AI needs to read all dozen files, understand their relationships, judge which relate to "pause" and which don't—then finally start modifying.

Context window is only so big. Stuff a dozen files in, most space gets occupied by files "completely unrelated to pause." TaskZone's task sorting logic, ScheduleZone's conflict detection code, AIZone's prompt assembly methods—these things occupy AI's attention but contribute nothing to the "modify pause logic" task.

With Zones, you say: "In TimerZone, modify state saving logic when pausing." How many files in TimerZone? Four. AI reads all four files thoroughly, understands every line carefully, attention one hundred percent focused on timer-related code.

Same context window. First approach, AI's attention diluted across a dozen files. Second approach, AI's full attention focused on four files.

**Different instruction precision means different AI comprehension depth, which means different output quality.**

It's not that AI got smarter—it's that the context you gave it got cleaner.

**Scenario 2: Changed A, Accidentally Touched B**

You asked AI to modify task sorting logic. AI finished, sorting works fine. But the next day you discover schedule display broke—time blocks completely disordered.

What happened? Because without classification, task sorting and schedule query code might be squeezed in the same file (casually written back then, everything stuffed in one place). When AI modified sorting logic, it incidentally touched schedule-related parts in the same file—not intentionally, it just thought that code "looked related."

With Zones, task sorting code is in TaskZone, schedule display code is in ScheduleZone. You say "modify sorting logic in TaskZone," AI's activity scope is limited to those few files in TaskZone, won't even touch ScheduleZone's stuff.

**Zone draws boundaries: you can touch stuff in this box, don't touch other boxes.** Change A only changes A, B won't get accidentally hit.

---

## Stand Back and Look

At this point, we have two things:

**Storage Cabinet** (Layer)—dividing code into three shelf layers: UI, Logic, Data.

**Storage Boxes** (Zone)—on each shelf layer, grouping files into labeled boxes by responsibility.

Classification system complete. Every file now has clear ownership: which layer it's in, which box it belongs to. No longer a pile of scattered files, but an orderly structure with hierarchy, grouping, labels.

But one problem remains unsolved.

Can you see at a glance what the whole room looks like?

Three shelf layers, several boxes per layer, several files per box, relationships between boxes, any files in wrong boxes, any boxes overstuffed about to overflow—can you see all this information in one picture?

Not yet. You know which Zone each file belongs to, but you don't have a complete "panoramic view" in your mind. Like you've organized every storage box in the room, but you haven't stood at the doorway to look back at the room's entirety.

You need to stand back, take a panoramic photo of the whole room.

---

**Chapter Summary**

> Layering tells you "divide into three layers," but inside each layer which dozen files belong together? Zone solves this.
>
> Zone is a functional partition within a Layer clustering by responsibility—just labeled storage boxes.
>
> Zone is a logical concept, not a physical folder. You don't need to move any files, change any directory structure. Adoption cost is zero, but effect is transformative: context for AI changes from scattered files across an entire layer to a few precise files in one box.
>
> Storage cabinet + storage boxes = classification system complete. But you're still missing a panoramic photo—stand back, see what the whole room looks like.
