<div align="center">

# Devashya Solanki

### Software Engineer · Mobile & Full-Stack

Building production-quality applications with an obsession for user experience,
security, and code that stays maintainable after the first thousand commits.

<a href="https://github.com/NotDvsh"><img src="https://img.shields.io/badge/GitHub-NotDvsh-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"></a>
<a href="mailto:devashyasolanki1234@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
<a href="#"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>

<br/>

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=flat-square&logo=dart&logoColor=white)
![Swift](https://img.shields.io/badge/Swift-F05138?style=flat-square&logo=swift&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=firebase&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

</div>

---

## 📌 Projects

| Project | What it is | Stack | Status |
| :--- | :--- | :--- | :---: |
| **[Focal ↗](projects/focal/README.md)** | Cross-platform focus & study app with real-time multiplayer study rooms | Flutter · Firebase · Swift | ✅ Built |
| **[Journal.IO ↗](projects/journal-io/README.md)** | Privacy-conscious journaling app with AI-assisted pattern insights | React Native · Node · MongoDB · OpenAI | ✅ Built |
| **[Metro Simulator ↗](projects/metro-simulator/README.md)** | Multi-line transit simulator with journey planning, scheduling, and fares | Python | ✅ Built |
| **[Assembler & Simulator ↗](projects/simulator-assembler/README.md)** | RISC-V toolchain — assembles source to machine code and executes it | Python · RISC-V | ✅ Built |
| **[AI Game Replay Analyzer ↗](projects/ai-game-replay-analyzer/README.md)** | _Coming soon_ | — | 🚧 In progress |

---

<br/>

## 🌌 Focal

> **Focus on what matters.** A goal-driven focus companion that turns study intentions into tracked, shared, and rewarded sessions.

Most productivity apps stop at a timer. Focal closes the whole loop — set a goal,
schedule it, focus on it in a distraction-shielded session, watch the progress
accumulate, and when motivation runs thin, do it alongside other people in a
synchronized study room.

**Highlights**

- Real-time multiplayer study rooms where every device stays in perfect agreement, including late joiners
- Distraction blocking through native iOS Screen Time, behind a platform-agnostic interface
- Eight full visual environments that animate a recolor of the entire application
- Authorization enforced at the database layer, so a tampered client can't escalate privileges
- Invite deep links that survive a cold start and an unauthenticated recipient
- Recurring goals, achievements, streaks, and focus analytics

<sub>Flutter · Dart · Firebase · Swift · ~47,000 lines of Dart · 30+ screens</sub>

<div align="left"><b><a href="projects/focal/README.md">Read the full Focal case study →</a></b></div>

---

<br/>

## 📓 Journal.IO

> **Reflection that adds up.** A privacy-conscious journaling app that turns private writing into understandable trends and practical next steps.

Most journals store thoughts and do nothing with them. Journal.IO reads back what
you've written and surfaces the recurring themes, mood shifts, and habits sitting in
your own words — framed as supportive observations, never clinical claims.

**Highlights**

- AI-assisted weekly insights, behavioral trends, and an interactive reflection Mind Map
- Structured, non-blocking analysis — writing never waits on a model call
- Privacy as architecture: full AI opt-out, biometric lock, hidden entries, export and deletion
- Mood check-ins, tags, calendar history, and search across every entry
- Goals, streaks, achievements, and on-device daily reminders
- iOS home-screen widgets for one-tap capture, plus RevenueCat subscriptions

<sub>React Native · TypeScript · Express · MongoDB · OpenAI · SwiftUI/WidgetKit</sub>

<div align="left"><b><a href="projects/journal-io/README.md">Read the full Journal.IO case study →</a></b> · <b><a href="https://journalio.app">journalio.app ↗</a></b></div>

---

<br/>

## 🚇 Metro Route & Schedule Simulator

> **Real transit, modelled honestly.** A multi-line metro simulator that plans journeys, times trains, and prices fares against a real-world network.

A transit network is a graph with awkward real-world constraints bolted on. Trains only
run during service hours, frequency changes at peak times, and switching lines costs
minutes that appear on no map — so the shortest route by stops isn't the fastest by clock.

**Highlights**

- Multi-line journey planning with interchange detection and real clock-time itineraries
- Next-train lookup with peak/off-peak frequency and service-hour awareness
- Fare calculation, per-line station browsing, and a forgiving menu-driven CLI
- Data-driven network model — scaled from the two required lines to four without a rewrite
- Built on real published network data, with assumptions documented where sources were ambiguous
- Zero third-party dependencies

<sub>Python 3 · standard library only</sub>

<div align="left"><b><a href="projects/metro-simulator/README.md">Read the full case study →</a></b></div>

---

<br/>

## ⚙️ Assembler & Simulator

> **From assembly source to executed instruction.** A two-stage RISC-V toolchain that assembles source into machine code and executes it on a virtual processor.

Most software sits on top of abstractions like these. Building both ends means
understanding what actually happens between a line of source and a value landing in a
register — encoding, addressing, control flow, and termination, with nothing hand-waved.

**Highlights**

- Full instruction-format coverage, symbolic label resolution, and ABI register naming
- A layered validation system that reports precisely what's wrong instead of emitting bad machine code
- A processor model with a complete register file, memory regions, and correct signed/unsigned semantics
- Per-instruction state tracing, verified against reference output across easy and hard cases
- Zero third-party dependencies

<sub>Python 3 · RISC-V (32-bit integer subset) · standard library only</sub>

<div align="left"><b><a href="projects/simulator-assembler/README.md">Read the full case study →</a></b></div>

---

<br/>

## 🎮 AI Game Replay Analyzer

> 🚧 **In progress** — case study coming soon.

<div align="left"><b><a href="projects/ai-game-replay-analyzer/README.md">View project →</a></b></div>

---

<br/>

## 📁 Repository Structure

```
.
├── README.md                          ← you are here
└── projects/
    ├── focal/
    │   └── README.md                  ← full case study
    ├── journal-io/
    ├── simulator-assembler/
    ├── metro-simulator/
    └── ai-game-replay-analyzer/
```

Every project follows the same layout: **Overview · Features · Tech Stack ·
Architecture · My Contributions · Challenges Solved · Key Takeaways.**

---

<div align="center">

### Let's build something

<a href="mailto:devashyasolanki1234@gmail.com"><img src="https://img.shields.io/badge/Email-devashyasolanki1234%40gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
<a href="https://github.com/NotDvsh"><img src="https://img.shields.io/badge/GitHub-NotDvsh-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"></a>

<sub>Open to software engineering internship and new-grad opportunities.</sub>

</div>
