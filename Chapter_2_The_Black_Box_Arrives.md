# Chapter 2: The Black Box Arrives

---

One day I needed to make a product decision.

GetDone Timer supports two timer modes—Pomodoro and free timer. I wanted to add task scheduling functionality, letting users plan execution order and time allocation in advance. The question was: should scheduling bind directly to task management, or become an independent module?

This wasn't a technical question, it was a product design question. The answer depended on the current project structure—what does the task management module currently connect to? How does its data flow? If I stuff scheduling into it, would it become too bloated? If I make it independent, how many existing modules need new connections?

I should have been able to answer these questions. Three months earlier I definitely could have. But that day I stared at the screen for a long time and realized my mind held only vague impressions—"probably like this, I guess."

I couldn't make the decision. Not because the decision was particularly hard, but because I lacked the information needed to make it. That information existed in my project, in those sixty thousand lines of code, but I couldn't see it.

The preface covered my experience of falling behind. This chapter I want to discuss something different—not "how I fell behind" but **why falling behind is inevitable**. Understanding this mechanism matters, because it's not just my problem, it's a problem every Vibe Coder will eventually face.

---

## An Asymmetric Race

Vibe Coding is essentially an asymmetric race.

As project scale grows larger, code structure more complex, two lines move in opposite directions.

One is AI's capability. The bigger the project, the more complex the structure, the more AI's advantages shine—its capacity to handle large-scale code keeps strengthening, models iterate, context windows expand, reasoning improves. Code swelling from a thousand to sixty thousand lines doesn't weaken AI. Thanks to evolving tools and models, it gets stronger. This line trends upward.

The other is your comprehension. This line trends downward. When the project has a thousand lines, your brain easily holds the entire thing. At ten thousand lines, you need to deliberately memorize and organize. At thirty thousand lines, your brain can't hold it anymore—you start forgetting certain modules exist, start confusing feature locations, start making false assumptions about dependencies.

One line rising, one falling. As project scale grows, these two lines inevitably cross.

Before the intersection, you're lucid, AI is strong, everything's smooth.

After the intersection is where the real anxiety begins—the project keeps swelling, AI's capability keeps rising, and your comprehension keeps declining. **The scissors gap widens.** AI can handle ever-increasing complexity, while what you can see clearly keeps shrinking. The chasm between you isn't static, it accelerates with project growth.

**This intersection point won't "possibly" arrive—it will "definitely" arrive.** As long as you keep using Vibe Coding to add to your project, code volume will keep growing, but your brain capacity won't. This is a math problem, not a capability problem.

---

## What AI Can't See Either

Here I want to say something fair about AI—and point out its real boundaries.

AI genuinely crushes it at writing code, I've said that repeatedly. But AI isn't omnipotent. It has a frequently overlooked limitation: **context windows**.

What does this mean? Every time AI talks with you, the information it can "see" is limited. It can't read all sixty thousand lines of your code at once. It sees the portion you give it—maybe a few files, maybe a description, maybe an error message. It makes judgments based on what it sees.

When the project is small, this isn't a problem. You can throw the whole project at it, it sees everything. But after the project grows, AI can only see fragments each time. Its judgment within that fragment might be correct, but it doesn't necessarily know what exists outside the fragment.

Another issue: **AI has no natural cross-session memory**. This conversation you tell it "TaskManager handles all task-related logic," next conversation it won't remember. You need to tell it again, or show it relevant code.

What does this mean?

It means when a project swells beyond a certain point, **neither you nor AI can see the whole picture**. You can't see it because your brain can't hold it. AI can't see it because its context window can't hold it. You each see part of the project, but no one—including AI—has complete cognition of the entire thing.

This doesn't affect AI's ability to execute specific tasks. You ask it to change a button color, it does great. You ask it to add a data field, no problem either. But when it comes to cross-module decisions, global adjustments, architectural tradeoffs—AI's judgment quality directly depends on the context quality you provide.

**The more precise your instructions, the better AI performs. The vaguer your instructions, the easier AI drifts.**

So the problem returns to you: when you yourself can't see the big picture, how do you provide AI with precise context?

---

## Three Signals You're Falling Behind

This state of "can't see the big picture" manifests as three specific signals in daily development. If you find yourself experiencing two or more during Vibe Coding, you've probably fallen behind.

**First signal: Decision paralysis.**

You want to add a new feature, but you don't know where it should go. Not "torn between two options," but "can't even list the options." You're unclear what the current project structure looks like, so you can't judge which module the new feature should attach to. Eventually you either randomly pick a location and make do, or throw the decision to AI—"where do you think it should go?"

**Second signal: Blind commands.**

You tell AI "help me modify this feature," but the location you give is wrong, or you missed a related module. AI changes what you said to change, then something else breaks. You ask AI to fix that broken thing, triggering a third problem. After several rounds, you discover the root cause was actually in a place you completely didn't consider.

This chain reaction of "changed A, broke B, fixed B, crashed C" isn't an AI execution problem. It's your command direction problem.

**Third signal: Repetitive churn.**

The same feature gets changed, reverted, changed again, repeated three or four times. Each time you think "this time should be right," but the result always falls a bit short. Not because AI implemented it poorly, but because each requirement description you gave was incomplete—you missed a constraint, forgot an edge case, didn't consider a module dependency. The root of these omissions is the same: you can't see the big picture.

If these three scenarios sound familiar, don't panic. It's not your fault.

---

## Vicious Cycle

These three signals aren't isolated. They stack on each other, forming a vicious cycle.

You can't see the project landscape, so your instructions to AI aren't precise enough. AI faithfully executes the imprecise instructions, code deforms through repeated imprecise modifications—things that should be together get split apart, modules that shouldn't couple get bound together, temporary workarounds become permanent technical debt.

After the project structure deforms, you see even less clearly. Seeing less clearly makes instructions even less precise. Less precise makes the project deform worse.

This is a self-reinforcing downward spiral. And it has a despairing characteristic: **the harder you try, the faster it spins.** Because trying harder means adding more to the project, and each addition dilutes your global understanding a bit more.

Vibe Coding's speed becomes a double-edged sword here. If you code slowly—traditional hand-coding—then code swells slowly too, your brain at least has time to gradually digest. But Vibe Coding is too fast, so fast you haven't finished digesting the last feature before the next one's already added.

As the project grows larger, code structure more complex, AI handles it with increasing ease, while you get more lost.

**This is Vibe Coding's paradox: the more capable AI becomes, the easier you get lost.**

---

## This Isn't Your Problem

It took me a long time to accept one thing: falling behind isn't because I wasn't smart enough, hardworking enough, or experienced enough.

Falling behind is Vibe Coding's **structural flaw**.

Vibe Coding optimizes for "rapid output"—think of something, build it, features launch quickly. It achieves this to the extreme. But it has no built-in mechanism to help you maintain "global understanding." Nothing forces you to pause and think "what does my project look like right now." No tool helps you redraw that increasingly blurry map in your mind.

Traditional software engineering has all sorts of ritualistic practices to combat this—code reviews, architecture docs, design discussions. You might find them tedious, but they at least force you to periodically think globally. Vibe Coding skips all of that—along with the tiny bit of "global lucidity" they provide.

So this isn't a problem solvable through "trying harder." You can't compensate for the global understanding loss caused by Vibe Coding by doing more Vibe Coding. That only makes the problem worse.

You need something different.

You need a method that lets you continue enjoying Vibe Coding's speed and excitement while periodically "seeing clearly" your project. Not understanding every line of code—you don't need to. But seeing the big picture: what's in the project, how it's organized, what connects to what.

In other words, you need an organization system. A method that can restore order to a room stuffed full of things.

That's what the next chapter is about.

---

**Chapter Summary**

> The black box isn't because you're not smart enough—it's Vibe Coding's structural flaw.
>
> As project scale swells, AI's capability rises while your comprehension falls. These two lines inevitably cross, and after crossing the scissors gap widens—AI gets stronger and stronger, you get more and more lost.
>
> Signals of falling behind: can't make decisions, commands go wrong direction, repeatedly churning the same feature. These three signals form a vicious cycle, and the harder you try the faster it spins.
>
> You don't need to run faster than AI. You need an organization system—one that lets you always see your project clearly while AI blazes ahead.
