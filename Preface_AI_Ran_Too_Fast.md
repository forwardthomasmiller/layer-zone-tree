# Preface: AI Ran Too Fast, and I Got Left Behind

---

It was an ordinary Wednesday afternoon.

I wanted to remove a feature. GetDone Timer had this rarely-used capability, and as the product grew more complex, I felt it was time to simplify. But I stared at the screen for twenty minutes, afraid to touch anything. Because I had no idea if this feature was connected to others—would removing it break something else?

This project, GetDone Timer, is a macOS Pomodoro app I built. Task management plus Pomodoro timers. Not particularly complex.

To be honest, this feeling of "not knowing where things are" didn't just appear that day. It grew gradually as the project progressed—features piling up, code expanding line by line. Like a room that slowly fills with stuff. You don't suddenly realize it's messy one day. Instead, one day you need to find something, you search for half an hour and can't locate it, and that's when it hits you: **I no longer know what's actually in my own project.**

I couldn't read the code anyway—I'll get to this later, but I genuinely don't know how to write macOS code. But previously, this wasn't a problem. Because even though I couldn't understand the code details, I at least had a clear picture of the project's landscape: which features were where, what files to touch when changing something, where to add a new requirement. This "common sense" let me give AI precise instructions.

But at some point, that common sense started getting fuzzy.

And what really hit me was this—AI knew.

I threw the problem at Claude Code. Three minutes later, it located the bug, modified two files, tests passed. Clean, effortless.

That moment, I realized: **It's not that AI can't handle the code. I can't keep up with AI.**

---

## The Honeymoon Phase of a Vibe Coder

I need to give you some context first.

I'm an indie developer. Notice I didn't say I'm a programmer—because I genuinely can't write code. At least not macOS code. Swift? AppKit? CoreData? Before I started building GetDone Timer, these words meant nothing to me.

GetDone Timer is a macOS Pomodoro app with task management and timer features. I started in August-September 2025. The entire project—from initial UI mockups to final production code—was built by AI. Claude web version helped with design and architecture discussions. Claude Code handled coding, debugging, testing. What did I do? I thought, I observed, I said "no, try again" or "yes, that's exactly it."

This development approach now has a cool name: **Vibe Coding**.

Building products by feel. No need to write code yourself, no need to master any programming language. You just need to know what you want, know what good products look like, and AI does the rest.

In the beginning, it felt like magic.

"Add a Pomodoro timer for me." —Thirty minutes later, a fully functional Pomodoro feature appeared.

"Create a menubar quick entry." —Two hours later, the menubar component was ready.

"Persist task data to CoreData." —Half a day later, the data layer was built.

I didn't even need to know what the CoreData API looked like. AI handled everything.

New features launched every day. Visible progress every day. Lines of code grew from hundreds to thousands, then to ten thousand, twenty thousand. My product evolved from a crude prototype into a fully-featured application. Someone who couldn't write macOS code built an actual working macOS app, powered by AI.

AI was crushing it, and I was loving it.

**This was the honeymoon phase—everything looked so beautiful.**

---

## How I Fell Behind

The code kept growing, but my understanding didn't keep pace.

This didn't happen overnight. It crept up slowly, like a frog in boiling water. Every time I asked AI to add a new feature, it delivered beautifully. But after each completion, the project gained a few more files, a few hundred more lines of code, and my understanding of these additions was limited to "it works."

A month later, the code went from two thousand to ten thousand lines. I still felt in control.

Two months later, it hit twenty thousand lines. I started needing to search to find where certain features lived.

Three months later, approaching thirty thousand lines. I noticed that when making product decisions, I was increasingly **guessing**—guessing this change wouldn't affect other features, guessing this module should be in that folder, guessing adding this feature would probably require touching these files.

**I was guessing, not judging.**

That's where the real danger lay. Not that AI wrote wrong code, but that I gave imprecise instructions. AI is too obedient—you tell it to go east, it goes precisely east, even if there's a cliff to the east. If you say "add a scheduled reminder feature to TaskManager," it dutifully adds it. Whether TaskManager is the right place for this feature, whether it makes the file bloated, whether it creates weird coupling with other modules—AI won't question your decisions.

You're the commander, AI is the elite force. The troops execute flawlessly. The problem is the commander is losing sight of the battlefield.

**AI was accelerating forward, and I was losing the big picture.**

---

## The Price of "Going by Feel"

The project kept growing. By sixty thousand lines, the problems were impossible to ignore.

Fix one bug, unsure if it would trigger new bugs. Add a feature, uncertain where it should go. Want to refactor a section, but afraid to touch it because I didn't know how many things depended on it. Every change felt like walking through a minefield—maybe fine, maybe boom.

I started doing something frequently: throwing the entire problem at AI, letting AI make the judgment.

"Where do you think this feature should go?"

"Can you check if changing this will affect other modules?"

"Can you sort out the dependency relationships between these Managers?"

AI always provided answers. But I knew deep down this wasn't sustainable. **A developer who can't understand their own project has fundamentally lost control of the product.** No matter how powerful AI is, final product decisions, architectural tradeoffs, priority sequencing—all require a human who understands the big picture.

If I can't even articulate "what the project looks like now," how can I decide "where to go next"?

---

## Not About Running Faster, But About Having a Map

I stopped and thought for a long time.

What was the problem? Not that AI wasn't good enough—AI was too good. Not that I wasn't working hard—I pushed forward every day. The problem was that from the beginning, I never had a **method for organizing code**. No architecture, no planning, no structure that let me quickly see the big picture. Code was just piled up feature by feature, like constantly stuffing things into a room without ever buying a storage cabinet.

The room filled with more and more stuff, until eventually you couldn't even push the door open.

I decided to systematically learn software architecture. Not to become an architecture expert, not to write papers. Just to find a method that would let me see clearly what my project looks like while AI blazes ahead.

**I didn't need to run faster than AI. I needed a map.**

---

## What This Book Is

This book is my study notes.

Starting from a complete architecture novice as a Vibe Coder, I explored my way through learning about layered architecture, interface contracts, module separation—all this "serious" knowledge—then discovered in practice what traditional architecture was missing. I call it **Zone**.

Zone isn't some profound theoretical invention. It's a simple idea: **Categorize code, label it clearly, so AI can take a group and complete work independently.** This idea gradually grew into a methodology: **CLVZ**—Contract-first, Layered, Validated, Zoned.

Sounds formal, but it's really just "clearly define what to do, layer the code properly, ensure it's done right, organize within each layer."

I used this approach to reorganize GetDone Timer, extracting clear structure from over sixty thousand lines of chaotic code. Not a complete rewrite, but progressive organization. After reorganizing, I could finally paint a mental picture of the project landscape—where's the UI, where's the business logic, where's the data layer, what Zones exist within each layer, what each is responsible for.

**Map in hand, the commander is back online.**

If you're also using AI to write code—whether you can code but want better efficiency, or like me, can't code at all but want to build products—if you vaguely feel "the project's getting bigger, I'm losing clarity," this book might help. This isn't a textbook. It won't use academic language to complicate simple things. These are just study notes from an ordinary developer, sharing how I went from falling behind to catching up, from confusion to clarity.

If you learn something from this, or even just get a bit of "oh, I'm not alone in this struggle" resonance, then these notes were worth writing.

Alright, turn the page. Let's start from the most exhilarating moment of Vibe Coding.
