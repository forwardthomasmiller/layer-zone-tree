# Chapter 3: You Need an Organization System

---

Last month I visited the city library.

Not to borrow books, but to help a friend find an out-of-print photography collection. It was an old library with perhaps several hundred thousand volumes. Walking in, I honestly didn't feel confident—hundreds of thousands of books, finding one specific title, sounded like finding a needle in a haystack.

Found it in three minutes.

Entered, checked the directory board: Photography on third floor. Went to third floor, checked area signs: Art photography in section C. Walked to section C, read shelf labels: Arranged alphabetically by author surname. Finger traced spines, ten seconds, got it.

Hundreds of thousands of books. Three minutes.

Walking out of the library, I suddenly thought of an uncomfortable comparison: my project has only sixty thousand lines of code, why does "finding things" in it take so much longer?

The library's hundreds of thousands of books—I could locate any one in three minutes. My sixty thousand lines of code—I wanted to find "timer pause state saving logic," had to flip through the file list, open three or four files to confirm, sometimes still got it wrong.

What's the difference?

Not quantity. The library has far more books than my code. The difference is the library has a classification system—floors, areas, shelves, alphabetical order—and my code doesn't.

---

## Quantity Isn't the Problem, Lack of Classification Is

This discovery made me re-examine that "asymmetric race" from Chapter 2.

I'd always thought the problem was "too much code." Sixty thousand lines, too big, brain can't hold it, so I fell behind. This diagnosis sounds reasonable, but it implies a despairing conclusion—if the problem is too much code, what do you do? Delete code? Stop adding features? Doesn't that mean stopping product development?

But the library gave me a completely different perspective: **Hundreds of thousands of books isn't the problem. Hundreds of thousands of unclassified books is the problem.**

If you dumped the library's hundreds of thousands of volumes on the ground in a pile, forget finding a specific book, you'd have trouble even walking in. But those same hundreds of thousands, arranged by floor, area, category, alphabet—anyone can precisely locate a book in minutes.

Still the same books. Quantity unchanged. What changed is their **organization method**.

Back to code: GetDone Timer's sixty thousand lines, if each line is in its proper place with clear classification and ownership, then sixty thousand and six thousand don't fundamentally differ in "comprehensibility." You don't need to remember every line of code—just like you don't need to remember every book's content in the library—you just need to know "where to look."

**My project isn't too big, it lacks classification.**

This cognitive shift is important, because it transforms a despairing problem ("what do I do with too much code") into a solvable problem ("how do I classify code"). The former makes you want to quit, the latter makes you want to act.

---

## You Do This Every Day

Speaking of classification, I suddenly realized something pretty ironic.

Everyone who's written code has learned data structures. You know that searching for an element in an unsorted array has O(n) time complexity—scan from start to end, worst case you scan the entire array. You also know that switching to a binary search tree drops complexity to O(log n)—each comparison cuts the search space in half. You further know that red-black trees through self-balancing rules guarantee O(log n) lookup even in worst cases.

These are basics of basics. Every programmer can recite them.

But have you considered: **The action of "finding code" in your own project follows exactly the same rules?**

A project without architecture is an unsorted array. You want to find "timer pause state saving logic," you can only open file after file, linear scan, until you happen to find it. More files, slower search. O(n).

A project with layered architecture is like having one index layer. "State saving is logic layer's job, not UI layer, not data layer." One judgment, cut two-thirds of search space. Then continue searching within logic layer—still quite a few files, but at least the scope narrowed.

A project with finer classification—we'll get to this—is like having several index layers. "Logic layer → Timer-related → State management → Pause handling." Each classification layer narrows search range, a few steps to precise location.

You spent tons of time learning data structures to optimize your program's data lookup efficiency. But your code itself—**it's also a kind of data**. You "query" it, "search" it, "locate" it every day. You build indexes for databases, you sort user data, you use hash tables for O(1) lookup—but your code? Your code still lies in an "unsorted array."

You build classification systems for other people's data every day, but forgot to build one for your own code.

---

## First Storage Cabinet: Layers

After figuring this out, I started working.

The first step was intuitive: create broad categories for code. Like the library's first classification level is "floors"—first floor periodicals, second floor literature, third floor science—I also needed to divide code into a few major categories.

How to divide? Actually the standard is simple. My code is basically doing three things: interacting with users (UI), processing business rules (Logic), accessing data (Data). These three things are completely different in nature. Separating them is the most natural first cut.

This is "layered architecture." Divide code by technical responsibility into several layers:

UI layer on top, responsible for everything users see—windows, buttons, cards, animations. It only cares about "what it looks like" and "what the user clicked," not the underlying business rules.

Logic layer in the middle, responsible for all business rules—how tasks are created, how timers run, what triggers when Pomodoro time's up. It's the application's brain, but it doesn't directly interact with users or touch the database.

Data layer at bottom, responsible for data access—where task data is stored, how to read it out, how to write it in. It only cares about "how data persists," doesn't care what the data is used for.

The rule between the three layers is also simple: **Only depend downward**. UI layer can call Logic layer, Logic layer can call Data layer, but not the reverse. Data layer doesn't know Logic layer exists, Logic layer doesn't know UI layer exists. Like the library's first floor doesn't need to know what books are on the third floor, but the third floor directory will tell you where the first floor is.

This was my first classification for code. First storage cabinet.

How effective? Actually quite good.

The most obvious change: many previously invisible problems suddenly surfaced. When I tried classifying code into three layers, I found two files clearly doing UI rendering, yet mixed among logic-related code. Also a database operation snippet, somehow written inside a UI component. These "misplaced" codes were completely unnoticeable when everything was jumbled together. Classification exposed them.

**Classification's value isn't just "finding things faster," but also "making errors visible."**

Instructions to AI also got more precise. Previously I'd say "help me modify timer logic," AI had to first figure out which files held timer logic. Now I say "in the Logic layer, timer-related code, help me modify pause behavior"—at least AI knows it doesn't need to search UI and Data layers.

---

## But the Shelves Are Still Messy

After layering, I was happy for about a week.

Then problems came.

Logic layer. This layer contains all of GetDone Timer's business logic—task creation, editing, deletion, sorting, filtering; Pomodoro start, pause, completion, statistics; free timer countdown, count-up, time adjustment; task scheduling execution order, time planning; state management, data validation, notification triggers...

All piled in one category: "Logic layer."

It's like the library's third floor labeled "Science"—you go up and look—tens of thousands of books densely packed across the entire floor, no further subdivision. Computer books next to physics, physics beside biology, biology followed suddenly by mechanical engineering. You know the book you want is on the third floor, but the third floor itself is an ocean.

Storage cabinet exists. Three-layer shelves arranged. But stuff on each shelf still scattered randomly.

I had "floor" level indexing, search efficiency progressed from O(n) to "somewhat better"—but far from O(log n). I still needed further subdivision within each floor: areas, shelves, labels.

In code language: I had Layers, but inside each Layer I still needed further classification units.

What's missing on each shelf?

**Storage boxes. Labeled storage boxes.**

---

**Chapter Summary**

> Sixty thousand lines of code isn't the problem. Sixty thousand lines of unclassified code is the problem.
>
> Layered architecture is your first storage cabinet—dividing code into three shelf layers: UI, Logic, Data. It makes errors visible, makes instructions to AI more precise, makes "finding things" efficiency shift from random scanning to at least having direction.
>
> But stuff on each shelf is still scattered. In Logic layer, task management, timers, state management all piled together. You know "it's on the third floor," but the third floor itself is a tangled mess.
>
> You still need storage boxes—the labeled kind. Next chapter, let's solve this problem.
