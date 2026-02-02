# Epilogue: A Vibe Coder's Architecture Reflections

---

Having finished writing this book, I want to say a few heartfelt words.

---

## I'm Not an Architecture Expert

I want to make this clear.

I'm not from a computer science background, haven't systematically studied software engineering, hadn't even written macOS code before building GetDone Timer. Layered architecture, design patterns—these concepts I learned while stumbling through the project process, can't claim systematic mastery.

I'm a Vibe Coder. Someone who relies on AI to write code, relies on intuition to build products.

Layer-Zone Tree isn't some carefully designed architecture theory. It was forced out of me in real combat—project swelled beyond visibility, I had no choice but to find a method to see the big picture again. Tried various approaches, finally discovered the most useful was this simple idea: classify code properly, then take a photo.

If you're an experienced programmer, you might find what this book covers very basic. Layered architecture? Module division? Dependency management? Aren't these software engineering common sense?

Yes. For professional developers, these indeed are common sense.

But for Vibe Coders, this "common sense" is brand new knowledge. We didn't come from computer classrooms, we started from the point of "AI help me implement an idea." We skipped those foundational cognitions traditional developers spend years accumulating, jumped straight into product development.

This is why Vibe Coding hits walls at a certain stage—not because we're dumb, but because we lack some basic tools. Layer-Zone Tree is such a basic tool. It transforms "how to organize code" from professional developers' tacit knowledge into an explicit method Vibe Coders can also understand and use.

I won't claim this method is the best. But I can say it works for me—a project with over sixty thousand lines of code, I still see the big picture clearly, still can precisely command AI to work.

---

## About CLVZ

This book focused on explaining Layer-Zone Tree—how to classify code, how to take panoramic photos. But Layer-Zone Tree is actually part of a larger framework.

This framework is called **CLVZ**—Contract-first, Layered, Validated, Zoned. Four letters, four dimensions:

**C — Contract-first**

Before starting to write code, first define collaboration interfaces between Zones. What does A Zone need B Zone to provide? What's the data format? What's the calling method? Write the "contract" clearly first, then have AI implement according to contract. This solves the problem of "how to make collaboration between Zones error-free."

**L — Layered**

Divide code by technical responsibility into layers—UI, Logic, Data. This book's Chapter 3 content.

**V — Validated**

How to ensure code indeed runs according to layering and zoning rules? How to detect whether Zone boundaries were breached? How to automatically validate compliance after AI writes code? This solves the problem of "how to ensure correct classification."

**Z — Zoned**

Divide Zones by business responsibility within each layer. This book's Chapters 4 and 5 content.

Among four dimensions, this book's focus is **L and Z**—layering and zoning. And Layer-Zone Tree is the tool that makes you **see** L and Z. It visualizes layering and zoning results into a panoramic photo, letting you see at a glance what the project looks like.

C (Contract) and V (Validation) are two other dimensions, they solve problems different from Tree. Contracts solve "how Zones collaborate," validation solves "how to ensure rules are followed." Both topics are very important, but they're not within this book's scope—if there's opportunity in the future will discuss separately.

**If you only learn one thing—learning Layer-Zone Tree is enough.**

Because all problems start from "can't see." You can't see project structure, so you give wrong commands. You can't see dependency relationships, so you change A break B. You can't see which Zone is swelling, so you wait until it explodes to discover.

Tree solves the most fundamental problem: makes you see.

Once seen, you naturally know what to do. See 🔴 violations, you know to decouple. See swelling Zones, you know to split. See lost files, you know to reposition.

**Seeing is half the solution.**

---

## GetDone Timer Still Evolving

When writing this book, GetDone Timer was already a macOS application with over sixty thousand lines of code. Task management, Pomodoro timing, schedule planning, AI assistant, statistics analysis, account system, payment system—quite a few features.

It's still continuing to grow.

But different from half a year ago, I'm no longer afraid of it growing.

Previously every time adding a major feature, I felt a bit unsure—"After adding will the project get messier? Can I still see clearly?" Now this anxiety is basically gone. Because I know, no matter how big the project grows, I can anytime have AI take a panoramic photo, see the big picture within a few minutes.

New feature added? Take a photo. Everything normal in photo? Continue. Some Zone starting to swell? Split it. New dependency violation appeared? Handle it.

Just this simple.

Vibe Coding's joy hasn't decreased one bit. But anxiety much less.

---

## To All Vibe Coders

If you read to here, I guess you're most likely a Vibe Coder—or at least someone interested in Vibe Coding.

Whether you're a newcomer just starting to use AI to write code, or already Vibe Coded for several months with project swelling to the point of panic "veteran," I want to say the same thing:

**You don't need to become an architecture expert.**

You don't need to finish reading Clean Architecture, don't need to understand every principle of SOLID, don't need to know the difference between hexagonal architecture and onion architecture. This knowledge is useful, but not essential.

What you need is just a panoramic photo.

Take a photo of your project. See what it looks like. How many layers, what Zones in each layer, what relationships between Zones, is anything wrong somewhere.

Just this much.

AI will get stronger and stronger. It will write code faster and faster, quality higher and higher, tasks it can handle more and more complex. This means your project will swell at faster speed.

But as long as you hold a panoramic photo in hand—you'll never get lost.

**Periodically take a photo of your project. That photo is your most important navigation device in the AI era.**

---

*Cowboy salute.*
