<div align="center">

# Devashya Solanki

### Software Engineer · Mobile & Full-Stack

Building production-quality applications with an obsession for user experience,
security, and code that stays maintainable after the first thousand commits.

<a href="https://github.com/NotDvsh"><img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"></a>
<a href="https://www.linkedin.com/in/devashya-solanki"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="mailto:solankidevashya@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
<a href="tel:+916354068612"><img src="https://img.shields.io/badge/Contact-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="Contact"></a>

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

| Project | What it is | Stack |
| :--- | :--- | :--- |
| **[Focal ↗](projects/focal/README.md)** | Cross-platform focus & study app with real-time multiplayer study rooms | Flutter · Firebase · Swift |
| **[Journal.IO ↗](projects/journal-io/README.md)** | Privacy-conscious journaling app with AI-assisted pattern insights | React Native · Node · MongoDB · OpenAI |
| **[NSS IIIT Delhi ↗](projects/nss-iiitd/README.md)** | Official site for IIIT Delhi's NSS unit — static, dependency-free, with a build that fails on insecure markup | Vite · Vanilla JS · CSS · sharp |
| **[Metro Simulator ↗](projects/metro-simulator/README.md)** | Multi-line transit simulator with journey planning, scheduling, and fares | Python |
| **[Assembler & Simulator ↗](projects/simulator-assembler/README.md)** | RISC-V toolchain — assembles source to machine code and executes it | Python · RISC-V |
| **[Gym Management System ↗](projects/gym-management-system/README.md)** | Multi-role, database-backed management system for members, staff, and classes | Python · MySQL |

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

## 🤝 NSS IIIT Delhi — Unit Website

> **A public record, not a brochure.** The official site for IIIT Delhi's National Service Scheme unit, built so that every fact on it can be traced to a source and the build refuses to ship an insecure page.

The unit's previous site advertised invented statistics, a placeholder team and stock
photography. This one states only what the unit can prove: twenty events re-derived
from its own reports and photograph EXIF, rendered from a single chronology file so the
count, the timeline, the year chart and the front page can never disagree.

**Highlights**

- One chronology file renders the Events page, the home rail, the year chart and every count at build time
- A build-time security audit that **fails the build** on an inline handler, style attribute, form, iframe or undeclared origin
- Hash-pinned Content-Security-Policy with `default-src 'none'` and Trusted Types, shipped as headers for any host plus a meta fallback
- Six static pages, no framework, no runtime dependencies, zero third-party requests
- ~12 KB of JavaScript, all of it additive — every page is complete before a module boots
- AVIF/WebP/JPEG responsive ladder across seven widths, and a post-build crawler that fails on a dead link or anchor

<sub>Vite 5 · Vanilla JS · CSS · sharp · Built as Web Development Lead, NSS IIIT Delhi core team 2026–27</sub>

<div align="left"><b><a href="projects/nss-iiitd/README.md">Read the full case study →</a></b></div>

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

## 🏋️ Gym Management System

> **One system, three kinds of user.** A database-backed management application handling gym members, staff, classes, and training schedules from a single terminal interface.

A genuine multi-user application rather than a script with a menu — persistent
relational data, three roles with different views of it, and the interesting work in
the parts most projects skip: validating input before it reaches the database and
getting membership periods right in every path.

**Highlights**

- Three distinct role flows — administrator, staff, and member — each with its own permissions
- Seven membership tiers with automatic expiry calculation, and extensions that build on existing time rather than discarding it
- Trainer browsing and personal session booking
- A reusable validation layer covering identifiers, dates, times, emails, and password strength
- Parameterised queries used consistently throughout
- BMI calculation with plotted results, formatted table output, and a persistent feedback log

<sub>Python 3 · MySQL · Matplotlib · PrettyTable</sub>

<div align="left"><b><a href="projects/gym-management-system/README.md">Read the full case study →</a></b></div>

---

<br/>

## 📁 Repository Structure

```
.
├── README.md                    ← you are here
└── projects/
    ├── focal/
    ├── journal-io/
    ├── nss-iiitd/
    ├── metro-simulator/
    ├── simulator-assembler/
    └── gym-management-system/   ← each contains a full case study README
```

Every project follows the same layout: **Overview · Features · Tech Stack ·
Architecture · My Contributions · Challenges Solved · Key Takeaways.**

---

<div align="center">

### Let's build something

<a href="https://github.com/NotDvsh"><img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"></a>
<a href="https://www.linkedin.com/in/devashya-solanki"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="mailto:solankidevashya@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
<a href="tel:+916354068612"><img src="https://img.shields.io/badge/Contact-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="Contact"></a>

<sub>Open to software engineering internship and new-grad opportunities.</sub>

</div>
