# Layer-Zone Tree
### A Navigation System for AI-Generated Code

> **Keep Your Map While AI Draws the Territory**
> A Practical Vibe Coding Guide • AI Coding Architecture • Claude Code Best Practices

---

## The Problem

You're building with AI. Claude writes your code, Cursor autocompletes your functions, GitHub Copilot suggests your implementations. Development is **fast**—faster than ever.

But at 10,000 lines... 20,000 lines... 60,000 lines...

**You start to lose track.**

- "Where did I put that timer logic?"
- "If I change this, what else breaks?"
- "Which files depend on which?"

You're no longer directing AI—you're **guessing**.

---

## The Solution

**Layer-Zone Tree** is a simple AI coding architecture system for organizing AI-generated code. This guide shows you how to organize AI-generated code and maintain clarity as your project scales:

1. **Layer** — Divide code by technical role (UI / Logic / Data)
2. **Zone** — Group files by business responsibility within each layer
3. **Tree** — Take a "panoramic photo" of your entire project

**Result:** You see your whole codebase at a glance. No matter how big it grows.

---

## What You'll Learn

This **Vibe Coding guide** teaches practical **Claude Code best practices** for real-world projects:

- Why Vibe Coding inevitably leads to a "black box" (and how to prevent it)
- **How to organize AI-generated code** at scale (60k+ lines)
- The "panoramic photo" method: see structure, dependencies, violations at a glance
- Progressive transformation: improve existing projects without stopping development
- Sustainable workflow: rapid AI development + architectural clarity

---

## Who This Is For

✅ **Vibe Coders** — You build with AI but the project's getting messy
✅ **Indie Developers** — Fast iteration without losing control
✅ **Non-Programmers** — Building products with Claude/Cursor/Copilot
✅ **Traditional Devs** — Curious about AI-era architecture

---

## Quick Start

**Read the Book:**
- [📖 English: Preface - AI Ran Too Fast](./Preface_AI_Ran_Too_Fast.md)
- [🇨🇳 中文版：前言 - AI跑太快我掉队了](./前言_AI跑太快我掉队了.md)

**Get Your First Panoramic Photo:**
1. Read [Chapter 7: Let AI Take the Photo](./Chapter_7_Let_AI_Take_The_Photo.md)
2. Use the AI Playbook (coming soon)
3. Have AI analyze your project
4. See your structure clearly

---

## Real-World Example

This method was developed while building **GetDone Timer** — a 60,000-line macOS Pomodoro app built entirely with AI.

**Before Layer-Zone Tree:**
- 160 scattered files
- Lost track at 30k lines
- Afraid to refactor anything

**After Layer-Zone Tree:**
- 6 Layers, 33 Zones
- Clear structure visible in one document
- Confident to keep building

---

## Table of Contents

### 📚 English Version

#### Part I: The Problem
- [Preface: AI Ran Too Fast, and I Got Left Behind](./Preface_AI_Ran_Too_Fast.md)
- [Chapter 1: Vibe Coding Is Addictive](./Chapter_1_Vibe_Coding_Is_Addictive.md)
- [Chapter 2: The Black Box Arrives](./Chapter_2_The_Black_Box_Arrives.md)

#### Part II: The Solution
- [Chapter 3: You Need an Organization System](./Chapter_3_You_Need_An_Organization_System.md)
- [Chapter 4: Adding Storage Boxes to Shelves](./Chapter_4_Adding_Storage_Boxes_To_Shelves.md)
- [Chapter 5: Zone Design in Practice](./Chapter_5_Zone_Design_In_Practice.md)

#### Part III: The Practice
- [Chapter 6: Taking a Panoramic Photo of Your Project](./Chapter_6_Taking_A_Panoramic_Photo.md)
- [Chapter 7: Let AI Take the Photo](./Chapter_7_Let_AI_Take_The_Photo.md)
- [Chapter 8: Sustainable Joyful Development](./Chapter_8_Sustainable_Joyful_Development.md)

#### Appendix
- [Epilogue: A Vibe Coder's Architecture Reflections](./Epilogue_A_Vibe_Coders_Architecture_Reflections.md)

---

### 🇨🇳 中文版

#### 第一部分：问题
- [前言：AI跑太快，我掉队了](./前言_AI跑太快我掉队了.md)
- [第一章：Vibe Coding真香](./第一章_Vibe_Coding真香.md)
- [第二章：黑箱来了](./第二章_黑箱来了.md)

#### 第二部分：解决方案
- [第三章：你需要一个收纳系统](./第三章_你需要一个收纳系统.md)
- [第四章：给架子配上收纳箱](./第四章_给架子配上收纳箱.md)
- [第五章：Zone设计实战](./第五章_Zone设计实战.md)

#### 第三部分：实践
- [第六章：给项目拍一张全景照片](./第六章_给项目拍一张全景照片.md)
- [第七章：让AI帮你拍照](./第七章_让AI帮你拍照.md)
- [第八章：可持续的快乐开发](./第八章_可持续的快乐开发.md)

#### 附录
- [后记：一个Vibe Coder的架构感悟](./后记_一个Vibe_Coder的架构感悟.md)

---

## Key Concepts

### Layer (层)
Divide code by **technical responsibility**:
- **UI Layer** — Everything users see and interact with
- **Logic Layer** — Business rules and domain logic
- **Data Layer** — Data persistence and access

### Zone (区)
Group files by **business responsibility** within each layer:
- **TaskZone** — All task-related logic
- **TimerZone** — All timing functionality
- **ScheduleZone** — All scheduling features

### Tree (树)
A "panoramic photo" of your entire project:
- Shows all Layers and Zones
- Maps file ownership
- Reveals dependencies
- Spots violations

---

## The CLVZ Framework

**Layer-Zone Tree** is part of the larger **CLVZ** framework:

- **C** — Contract-first (define interfaces between Zones)
- **L** — Layered (organize by technical responsibility)
- **V** — Validated (ensure rules are followed)
- **Z** — Zoned (organize within layers by business domain)

This book focuses on **L** and **Z**. The Tree makes them visible.

---

## Contributing

Found a typo? Have a suggestion? Want to share your Layer-Zone Tree?

- 💬 [Start a Discussion](https://github.com/forwardthomasmiller/layer-zone-tree/discussions)
- 🐛 [Report an Issue](https://github.com/forwardthomasmiller/layer-zone-tree/issues)
- 🌟 Star this repo if it helped you!

---

## Keywords & Topics

`AI coding architecture` • `Vibe Coding guide` • `Claude Code best practices` • `How to organize AI-generated code` • `AI development workflow` • `Code organization system` • `Architecture for non-programmers` • `Claude AI` • `Cursor AI` • `GitHub Copilot` • `Software architecture` • `Project structure`

---

## About the Author

**Thomas** — A Vibe Coder who learned architecture the hard way. Built GetDone Timer (60k lines) with AI while figuring out how not to get lost.

Not a computer science graduate. Not an architecture expert. Just someone who needed a map.

- 🐦 Twitter: [@hithomasmiller](https://twitter.com/hithomasmiller)
- 📧 Email: forwardthomasmiller@icloud.com

---

## License

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a>

This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).

**You are free to:**
- Share — copy and redistribute
- Adapt — remix and build upon

**Under these terms:**
- Attribution — give appropriate credit
- NonCommercial — not for commercial use
- ShareAlike — distribute under same license

---

## Acknowledgments

- **Claude (Anthropic)** — For making Vibe Coding possible
- **GetDone Timer users** — For being patient during the messy phases
- **Every Vibe Coder who felt lost** — This guide is for you

---

**⭐ If this guide helped you see your project more clearly, star the repo!**

It helps other developers discover it.
