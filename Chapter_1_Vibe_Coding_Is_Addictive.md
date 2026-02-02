# Chapter 1: Vibe Coding Is Addictive

---

Do you remember how it felt the first time you saw your idea become a working application?

I remember. It was a weekend evening. I told Claude Code something like "build me a task list, sidebar on the left for categories, task cards on the right." Then I went to get some water. When I came back, a decent-looking interface had appeared on screen—sidebar, card layout, click interactions, all working.

I stared at the screen for about ten seconds, one thought running through my mind: **This actually works?**

Not the rational realization of "wow, technology is so advanced." More a primal shock—like you'd always thought there was a wall between ideas and products, then someone opened a door in that wall and said "go ahead, just walk through."

That evening I added three more features. Each addition layered on another level of excitement.

---

## What Is Vibe Coding

I mentioned this term in the preface, but I want to explain it seriously here, because it's more than just "coding by feel."

The core of Vibe Coding is a loop: **Think of it → Describe it → AI implements → See the result → Adjust → Continue**.

Notice what's missing from this loop—**no "write code" step**.

The traditional programming loop is: Think of it → Look up docs → Write code → Debug → Fix bugs → Debug again. Between "thinking of it" and "seeing results," you spend enormous time wrestling with the programming language. Syntax errors, API calls, type conversions, memory management—none of this relates to your product idea, but you must solve it all before seeing what your idea looks like.

Vibe Coding skips all of that.

You don't need to know how to write a for-loop in Swift, don't need to know how to initialize AppKit's NSViewController, don't need to know how to construct a CoreData Fetch Request. You just need to clearly describe what you want, and AI handles all the technical details.

This isn't "lowering the programming barrier." This is **removing the barrier entirely**.

It fundamentally changes role allocation in "making software." The traditional model: you're both designer and laborer—you draw the blueprints and lay the bricks yourself. Vibe Coding hands the "laborer" role to AI. You just be the designer. More precisely, you're the director—AI is the entire crew. You say "push this shot from left to right," the crew handles lighting, camera, props. You don't carry the camera yourself.

So Vibe Coding's essence isn't "a new way to write code." It's **a new way to build products**. You describe the product in natural language, AI turns it into code. That giant chasm between "idea" and "implementation" gets filled by AI.

---

## Why It's So Addictive

Once you understand what Vibe Coding is, why it's addictive becomes clear: **instant feedback**.

Traditional programming has feedback cycles of hours or even days. You might spend a whole day setting up environment, writing boilerplate code, only to see a Hello World by evening. Vibe Coding's feedback cycle is minutes. Say something, see results minutes later. Not satisfied? Say something else, iterate again.

It feels a lot like gaming. Each interaction produces visible output. Each session ends with the product having more than when it started. You can literally watch it grow—yesterday just an empty shell, today it displays task lists, tomorrow the timer works. This continuous, visible, cumulative sense of progress is addictive.

And this isn't fake progress. Each new feature is genuinely usable. You can open the app, click buttons, see the timer counting down, see task status changing. It's not a PowerPoint, not a concept mockup, it's an actual working product.

I remember during the first two weeks of building GetDone Timer, I couldn't resist adding features almost every night. "Just one more and I'll sleep"—then added three more. Not from deadline pressure, purely because it felt so good. Each "add XX feature" → seeing it appear on screen created a small sense of achievement that stacked up. After two weeks, the product evolved from an empty-interface prototype to a complete application with over twenty feature points.

This speed is unimaginable in traditional programming.

---

## More Than Just Fast

But Vibe Coding is addictive not just because it's fast. There's a deeper reason: **it lets you focus on the product itself**.

Traditional programming spends tons of time on things unrelated to the product. Environment setup, dependency management, build systems, version conflicts. Your mind wants to think about "how to improve user experience," but your hands are dealing with "why does this library conflict with that one."

Vibe Coding eliminates all that noise. Your attention is one hundred percent on the product—where should this button go for better UX? Is this interaction flow too long? What's the user's first reaction seeing this interface?

This feeling is hard to describe. It's like—you can finally build products the way a "product person" should. No need to spend three months learning Swift syntax first, no need to figure out Xcode's build system first, no need to understand macOS sandboxing mechanisms first. Your mind thinks product, your words describe features, AI translates these product ideas into code.

For someone like me who can't code, this is liberation. But even for programmers who can code, this experience is completely new. I later chatted with programmer friends. They said Vibe Coding's biggest change isn't "not having to write code," but "finally not being interrupted from product thinking by technical details."

---

## The Hidden Premise of the Honeymoon

At this point, you might think Vibe Coding is perfect. Fast, efficient, keeps you focused on product, lowers barriers. Any downsides?

In early project stages—genuinely, no.

But there's a trap: the lack of downsides exists precisely because there's a premise you haven't noticed quietly supporting everything.

That premise is: **The project is small enough to fit in your brain.**

Think about it—why did everything go so smoothly the first two weeks? You told AI to add a feature, it added it, results perfectly matched expectations. You told AI to modify an interaction, it modified it, no unexpected consequences. Why?

Because back then the entire project had just a dozen files, a few thousand lines of code. Your brain held the complete map—which feature in which file, which button triggered which logic, how data flowed from here to there. You didn't need to deliberately memorize it. With so little content, you naturally remembered it.

So every instruction you gave AI was precise. "Add a deadline field to TaskManager"—you clearly knew what TaskManager was, where it lived, what it managed. Of course AI executed quickly and accurately.

This is the honeymoon's secret: **It's not that AI was smarter in the early stages. You were more lucid.**

You were lucid, so your instructions were precise. Instructions precise, so AI's execution perfect. AI's execution perfect, so everything felt smooth.

It's a virtuous cycle. But it has an expiration date.

The expiration depends on your brain's capacity. When the project swells beyond what your brain can hold—can't hold all file locations, can't hold all module relationships, can't hold all feature dependencies—the virtuous cycle starts loosening.

And Vibe Coding's speed makes that day arrive faster than you expect.

---

**Chapter Summary**

> Vibe Coding is genuinely amazing. It lets you skip technical details and build products with pure product thinking. Instant feedback, continuous output, design focus—in early project stages, it has almost no downsides.
>
> But everything going smoothly has a premise: your brain can still hold the entire project.
>
> AI is rapidly stuffing things into the room, and you haven't realized the room is filling up.
>
> Next chapter, let's see what happens when the room gets full.
