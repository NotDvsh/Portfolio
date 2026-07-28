# 🏋️ Gym Management System

> **One system, three kinds of user.** A database-backed management application handling gym members, staff, classes, and training schedules from a single terminal interface.

<div align="center">

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square&logo=python&logoColor=white)
![Interface](https://img.shields.io/badge/Interface-CLI-4B5563?style=flat-square)

</div>

---

## Overview

A complete management system for a gym, built around a relational database and driven
entirely from the terminal.

The system serves **three distinct roles** — administrators, staff, and members — each
with its own entry point, its own permissions, and its own set of things it can do. A
member extends a membership and books a session; a trainer creates classes; an
administrator sees and manages everything.

**Why it's interesting:** it's a genuine multi-user application rather than a script
with a menu. Data is persistent and relational, every role has a different view of it,
and the interesting work is in the parts most beginner projects skip — validating
input before it reaches the database, calculating membership periods correctly, and
keeping the whole thing usable for someone who isn't a programmer.

> 🔒 Source is kept private — this is coursework, and publishing a working solution
> isn't fair to anyone still doing it. Happy to walk through the design in an interview.

---

## ✨ Capabilities

### 👤 Members

| Capability | Description |
| :--- | :--- |
| **Registration & Sign-In** | Self-service account creation with plan selection, plus returning-member login. |
| **Membership Plans** | Seven tiers from a single day to two years, with pricing and automatic end-date calculation from the chosen start date. |
| **Plan Extension** | Extend an active membership; the new expiry is computed from the existing one rather than from today, so time already paid for isn't lost. |
| **Plan Overview** | View current membership start and end dates at a glance. |
| **Training Sessions** | Browse available trainers and book a personal session at a chosen date and time. |
| **BMI Calculator** | Calculate BMI, classify it into a standard category, and view the result plotted against category ranges. |
| **Profile Management** | Update email and password with validation applied. |
| **Feedback** | Submit feedback, logged to a persistent file. |

### 🧑‍🏫 Staff

| Capability | Description |
| :--- | :--- |
| **Registration & Sign-In** | Staff onboarding with hire-date capture, plus returning-staff login. |
| **Class Creation** | Create classes with name, timing, and duration — including a review-and-amend step before anything is committed. |
| **Profile Management** | Update personal details with the same validation members get. |
| **Feedback** | Submit feedback through the same channel. |

### 🛠 Administration

| Capability | Description |
| :--- | :--- |
| **Full Record Access** | Browse all members, staff, and classes as formatted tables. |
| **Record Updates** | Field-level editing across all three record types, each with its own validation rules. |
| **Record Removal** | Field-level clearing of records, with confirmation of whether anything actually matched. |
| **Protected Entry** | Administration is gated behind a separate credential check from the member and staff flows. |

### ✅ Validation & Experience

| Capability | Description |
| :--- | :--- |
| **Input Validation** | Identifiers, dates, times, durations, and menu selections are all checked and re-prompted until valid — bad input never reaches the database. |
| **Email Rules** | Addresses are validated against a set of accepted providers before acceptance. |
| **Password Policy** | Enforced minimum and maximum length plus required character classes, checked on every password entry. |
| **Formatted Output** | All records and menus render as aligned tables rather than raw output. |
| **Guided Navigation** | Nested, numbered menus with consistent "back" options at every level. |

---

## 🛠 Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Language** | Python 3 |
| **Database** | MySQL |
| **DB Connectivity** | `mysql-connector-python` |
| **Visualisation** | Matplotlib |
| **CLI Presentation** | PrettyTable |
| **Imaging** | Pillow |
| **Data Export** | CSV (standard library) |
| **Date & Time** | `datetime` (standard library) |

---

## 🏗 Architecture

```
        ┌───────────────────────────────┐
        │        Main Menu (CLI)        │
        └───────────────┬───────────────┘
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
   ┌─────────┐    ┌──────────┐    ┌──────────┐
   │  Admin  │    │  Staff   │    │  Member  │
   └────┬────┘    └────┬─────┘    └────┬─────┘
        │              │                │
        └──────────────┼────────────────┘
                       ▼
            ┌──────────────────────┐
            │   Validation Layer   │
            └──────────┬───────────┘
                       ▼
            ┌──────────────────────┐
            │        MySQL         │
            │ members · staff ·    │
            │ classes · sessions   │
            └──────────────────────┘
```

**Guiding rules**

- **Validate before you write.** Every input passes a check before it reaches a query, so the database never has to defend itself against the interface.
- **Parameterised queries throughout.** User input is bound as parameters rather than concatenated into SQL — the correct habit, applied consistently.
- **Role-shaped access.** Each role has its own menu tree and its own set of operations; capabilities aren't shared by accident.
- **Confirm before committing.** Destructive and creative actions surface what's about to happen and report what actually changed.

---

## 👤 My Contributions

I built the entire system — database design, all three role flows, validation, and the
interface.

| Area | What I built |
| :--- | :--- |
| **Data Model** | The relational schema covering members, staff, classes, and training sessions, and the relationships between them. |
| **Role Flows** | Three separate application paths — administrator, staff, and member — each with its own menu tree and permitted operations. |
| **Membership Logic** | Plan tiers, pricing, duration handling, end-date calculation, and extension that builds on an existing expiry. |
| **Booking** | Trainer listing and the session-scheduling flow with date and time validation. |
| **Validation Layer** | Reusable checks for identifiers, dates, times, email addresses, and password strength, applied consistently across every flow. |
| **Admin Tooling** | Full view, update, and clear operations across all record types. |
| **Extras** | BMI calculation with a plotted result, a persistent feedback log, and formatted table output throughout. |

---

## 🧩 Challenges Solved

<details open>
<summary><b>One application, three different users</b></summary>
<br/>

A member, a trainer, and an administrator want completely different things from the
same data. Collapsing them into one menu makes the tool confusing and gives everyone
access to everything.

**Outcome:** three distinct entry points with separate menu trees and operation sets,
so each role sees only what's relevant to it.

</details>

<details open>
<summary><b>Dates that behave correctly</b></summary>
<br/>

Membership periods are the core of a gym's business, and they're easy to get subtly
wrong — especially extensions, where naively adding time to *today* silently discards
whatever the member had left.

**Outcome:** plan durations, expiry dates, and extensions all compute from the correct
anchor, so a member never loses time they've already paid for.

</details>

<details open>
<summary><b>Keeping bad data out</b></summary>
<br/>

A terminal application accepts anything the user types. Without checks, a mistyped
date or an empty identifier becomes a corrupt row or a crash mid-operation.

**Outcome:** a validation layer covering identifiers, dates, times, durations, emails,
and passwords — applied at every entry point, with clear messages and re-prompting
rather than failure.

</details>

<details open>
<summary><b>Making a terminal app usable</b></summary>
<br/>

CLI tools are typically written for their author. This one had to be operable by gym
staff who won't read documentation.

**Outcome:** numbered menus with consistent navigation, aligned table output, review
steps before commitment, and confirmation messages that say what actually happened.

</details>

---

## 🎯 Key Takeaways

- **Database-backed application design.** Schema design, relationships, and persistent multi-user state — not a script holding data in memory.
- **Safe query habits.** Parameterised queries used consistently, which is the single most important thing to get right when user input meets SQL.
- **Domain logic is where the bugs live.** The hard part wasn't the CRUD; it was making membership periods behave correctly in every path.
- **Defensive input handling.** Validation treated as a shared, reusable layer rather than scattered one-off checks.
- **Users first, even in a terminal.** Menus, formatting, and confirmations are product decisions.

---

## 🔭 Future Improvements

- **Hashed credentials** and externalised configuration in place of stored secrets
- **Attendance tracking** and class enrolment for members
- **Reporting** — revenue, retention, and class popularity over time
- **A web or desktop front end** over the same data model
- **Automated tests** covering membership and booking logic

---

<div align="center">
<sub><a href="../../README.md">← Back to portfolio</a></sub>
</div>
