# 🌌 Focal

> **Focus on what matters.** A goal-driven focus companion that turns study intentions into tracked, shared, and rewarded sessions.

<div align="center">

![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20Android-black?style=flat-square)
![Flutter](https://img.shields.io/badge/Flutter-3.12+-02569B?style=flat-square&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-3.12-0175C2?style=flat-square&logo=dart&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-Auth%20%7C%20Firestore-FFCA28?style=flat-square&logo=firebase&logoColor=black)
![Swift](https://img.shields.io/badge/Native-Swift-F05138?style=flat-square&logo=swift&logoColor=white)
![Code](https://img.shields.io/badge/Dart%20LOC-47k+-blueviolet?style=flat-square)
![Screens](https://img.shields.io/badge/Screens-30+-9146FF?style=flat-square)

</div>

---

## Overview

**Focal** is a mobile application for people who want to actually finish what they sit down to do.

Most productivity apps stop at a timer. Focal connects the whole loop: you set a goal,
schedule it, focus on it in a distraction-shielded session, watch the progress accumulate,
and — when motivation runs thin — do it alongside other people in a synchronized study room.

**Who it's for:** students, self-learners, and anyone whose hardest problem is not
knowing what to do, but staying with it.

**The problem it solves:** intention decays. Focal closes the gap between planning
and doing by making the plan visible, the session frictionless, the distractions
physically unavailable, and the progress worth coming back for.

---

## ✨ Features

### 🎯 Goals & Planning

| Feature | Description |
| :--- | :--- |
| **Goal Management** | Create, schedule, edit, complete, reschedule, and archive goals with categories, descriptions, and session targets. |
| **Recurring Goals** | Daily, weekday, weekend, weekly, monthly, and yearly repetition with custom intervals, weekday selection, end dates, and occurrence limits — individual occurrences can be edited without disturbing the series. |
| **Calendar View** | A month-at-a-glance planner that surfaces what's scheduled on any day and lets goals be actioned directly from the date. |
| **Smart Reminders** | Per-goal reminders set either relative to the start time or at an exact moment, with multiple reminders per goal. |
| **Session Targets** | Each goal carries an estimated number of focus sessions, so completion progress is measurable rather than binary. |

### ⏱️ Focus Sessions

| Feature | Description |
| :--- | :--- |
| **Configurable Sessions** | Focus length, break length, and session count are all tunable, with a live summary of total commitment before starting. |
| **Focus Modes** | Pomodoro, Deep Work, and Flexible presets chosen during onboarding set sensible defaults from day one. |
| **App Blocking** | Distracting apps and whole categories are shielded for the duration of a session and released the moment it ends. |
| **Focus Alarms** | Seven selectable sounds mark the end of a focus block or break, so the timer works without the screen. |
| **Goal-Linked Sessions** | Sessions launched from a goal count toward that goal's progress automatically. |
| **Honest Accounting** | Only completed focus time counts toward statistics — abandoning a session early logs nothing, which keeps the numbers meaningful. |

### 👥 Multiplayer Study Rooms

| Feature | Description |
| :--- | :--- |
| **Real-Time Rooms** | Create or join a study room and see every member's live state — waiting, ready, studying — as it changes. |
| **Synchronized Timers** | Every device in a room shows the same phase, session number, and time remaining, including for people who join partway through. |
| **Invite Codes & Deep Links** | Rooms are shared with a short code or a tappable link that drops the recipient straight into the join flow — even if the app was closed or they weren't signed in yet. |
| **Join Previews** | An invite resolves to a safe preview of the room before committing, so nobody joins blind. |
| **Late Join** | Hosts can allow members to enter after a session has already begun. |
| **Session Summaries** | A shareable recap of who attended, how long they stayed, and what the room actually accomplished. |
| **Host Controls** | Ready checks, session start/end, and invite-link regeneration, with graceful host handover when the host leaves. |

### 🏆 Progress & Motivation

| Feature | Description |
| :--- | :--- |
| **Achievements** | A milestone system spanning five categories — Getting Started, Streaks, Monthly Focus Hours, Sessions Completed, and Multiplayer — presented as an explorable achievement wheel. |
| **Streaks** | Daily streaks that advance when the day's goals are cleared, with milestone tiers at 3, 7, 30, 100, and 365 days. |
| **Focus Analytics** | Weekly and monthly focus totals, time-of-day distribution, productivity trends, and consistency tracking. |
| **Session History** | A complete, endlessly scrollable record of past sessions with per-session detail. |
| **Daily Insights** | Contextual prompts derived from actual usage rather than generic encouragement. |

### 🎨 Personalization

| Feature | Description |
| :--- | :--- |
| **Focus Environments** | Eight full visual environments — Midnight, Ocean, Aurora, Sakura, Ember, Noir, Alpine, Clouds — each with its own animated ambience. |
| **App-Wide Recoloring** | Choosing an environment doesn't just change a background; it re-tints the entire application, and the transition is animated rather than abrupt. |
| **Theme Modes** | Light, Dark, and System, with the environment palette resolving correctly in each. |
| **Persistent Preferences** | The app always reopens exactly the way it was left. |

### 🔐 Account, Privacy & Notifications

| Feature | Description |
| :--- | :--- |
| **Social Sign-In** | Google authentication with a guided, resumable account creation flow (Apple sign-in surface is in place, pending enablement). |
| **Granular Notifications** | Independent toggles for focus sessions, break reminders, daily goals, and weekly summaries — switching a category off cancels anything already pending. |
| **Local-Only Reminders** | Reminders are scheduled on the device rather than pushed from a server, and this is stated plainly to the user during onboarding. |
| **Permission Transparency** | Every permission request is preceded by an explanation of what it's for and an option to decline without losing the app. |
| **Account Control** | Profile management, sign-out, and full self-service account deletion. |
| **Subscription Tier** | Focal Pro gates advanced analytics, premium environments, app blocking, unlimited history, and higher goal/room limits. |

---

## 🛠 Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Framework** | Flutter 3.12+ |
| **Language** | Dart 3.12 · Swift (native iOS modules) · JavaScript (Node.js 20) |
| **Platforms** | iOS · Android |
| **Backend** | Firebase |
| **Database** | Cloud Firestore (real-time listeners) |
| **Authentication** | Firebase Auth · Google Sign-In |
| **Server Logic** | Firebase Cloud Functions (Node.js) |
| **Authorization** | Firestore Security Rules |
| **State Management** | Streams · `ChangeNotifier` · Repository pattern |
| **Local Storage** | SharedPreferences |
| **Notifications** | `flutter_local_notifications` · `timezone` |
| **Payments** | RevenueCat (`purchases_flutter`) |
| **Audio** | `audioplayers` |
| **Deep Linking** | `app_links` (custom scheme + universal links) |
| **Native iOS** | FamilyControls · ManagedSettings · DeviceActivity (Screen Time) |
| **Sharing** | `share_plus` · `url_launcher` · `in_app_review` |
| **UI & Motion** | Material Design · `flutter_animate` · `google_fonts` · `skeletonizer` |
| **Testing** | `flutter_test` · `flutter_lints` |

---

## 🏗 Architecture

Focal follows a strict layered architecture. Every screen talks to a repository;
no screen touches the database directly.

```
┌──────────────────────────────────────────────────────────┐
│                      UI Layer                            │
│   Home · Calendar · Goals · Focus · Rooms · Profile      │
└────────────────────────┬─────────────────────────────────┘
                         │
┌────────────────────────▼─────────────────────────────────┐
│                  Repository Layer                        │
│   Goal · Auth · User · Statistics · Focus · Room         │
│        (single source of truth, stream-based)            │
└────────────────────────┬─────────────────────────────────┘
                         │
┌────────────────────────▼─────────────────────────────────┐
│                   Service Layer                          │
│  Notifications · Streaks · Achievements · Migration      │
│  Deep Links · Alarms · App Blocking · Subscriptions      │
└────────────────────────┬─────────────────────────────────┘
                         │
┌────────────────────────▼─────────────────────────────────┐
│      Firebase (Auth · Firestore · Cloud Functions)       │
│      + Native iOS Screen Time modules (Swift)            │
└──────────────────────────────────────────────────────────┘
```

**Guiding rules**

- **Unidirectional data access** — UI → Repository → Firebase. No shortcuts, no scattered queries.
- **Streams over polling** — repositories expose real-time streams, so multiplayer state and personal progress update without manual refresh.
- **Immutable models** — data classes with explicit serialization boundaries, keeping storage format decoupled from UI.
- **Fail-open startup** — only authentication is treated as critical; every other subsystem can fail at launch without preventing the app from opening.
- **Defense at the database** — security rules independently validate every write, so client bugs cannot become data corruption.

---

## 👤 My Contributions

I designed and built Focal end to end. The areas below represent the work I own most
directly.

| Area | What I built |
| :--- | :--- |
| **Onboarding** | The complete first-run experience — an eight-step guided intro covering personalization, daily target setting, focus-mode selection, privacy disclosure, and permission priming, followed by the analytics preview that shows new users what they're working toward. |
| **Authentication** | The full account lifecycle: Google sign-in, a resumable multi-step sign-up flow, distinct paths for new versus returning users, session handling, and self-service account deletion. |
| **Security & Validation** | The application's entire authorization model — ownership boundaries, write validation, immutability guarantees, anti-enumeration protections, and abuse-resistant invite handling — plus the prepared server-authoritative layer for the risks a client cannot close alone. |
| **Multiplayer** | The whole study-room feature: room creation, invite codes, join previews, ready checks, synchronized sessions, late join, host controls and handover, and post-session summaries. |
| **Deep Linking** | Invite links that work from a cold start, a warm app, or a signed-out state, preserving the user's intent through authentication. |
| **Theme System** | Eight complete visual environments, the light/dark/system mode system, and the app-wide animated recoloring that ties them together. |
| **App Blocking** | The distraction-shielding feature, its native platform integration, its permission flow, and its clean degradation on unsupported platforms. |
| **Permissions Handling** | Every permission touchpoint — priming, requesting, honoring refusal, and recovering when a permission is revoked later. |
| **Progress Systems** | The achievements engine, streak logic, statistics, analytics views, and session history. |
| **UI & UX Polish** | The shared component library, skeleton loading states, animated navigation, coach marks, empty states, and destructive-action safeguards. |
| **Reliability** | The fail-open startup sequence, the data migration system, and the backward-compatibility strategy that kept existing users whole through schema renames. |

---

## 🌟 Project Highlights

**Real-time state without real-time bugs.**
Multiplayer sessions stay in agreement across devices because every client derives
its view from the same shared anchor rather than its own local clock. A member who
joins ten minutes late sees exactly the same countdown as the host — no drift, no
resynchronization step, no per-device timer to go wrong.

**Security treated as a first-class feature.**
Authorization is enforced at the database layer, not just in the UI. Ownership
boundaries, value ranges, immutable fields, append-only membership, and
anti-enumeration protections are all specified declaratively and independently of
client code. The result is that a tampered or outdated client cannot escalate
privileges, hijack a room, inflate its own statistics, or scrape other users.

**Anti-abuse baked into the social layer.**
Invite codes resolve through a purpose-built preview surface that exposes only
non-sensitive information, so possessing a link never leaks a room's member list
or settings. Codes cannot be enumerated, cannot be re-pointed at a different room,
and cannot be used to forge a host.

**A theme system, not a color switch.**
Eight environments each define a complete palette that every surface in the app reads
from. Switching environments animates the entire interface as one continuous
interpolation rather than a jarring repaint, and the choice resolves correctly across
light, dark, and system modes.

**Deep links that survive reality.**
A shared invite works whether the app is running, backgrounded, or not yet launched —
and if the recipient isn't signed in, the intent is preserved through the entire
authentication flow and resumed on the other side.

**Native capability behind a portable interface.**
App blocking uses iOS Screen Time APIs through a native Swift module, but the rest of
the app never knows that. The capability is expressed through a platform-agnostic
contract that degrades cleanly to unavailable elsewhere, so no feature code is
littered with platform checks.

**Backward compatibility as a discipline.**
The project has been through schema and naming migrations without stranding existing
users. Legacy data paths are retained and migrated transparently on startup, and
migrations are additive so an older build still finds its data.

**Performance-conscious data access.**
History is paginated with cursor-based loading and in-flight guards rather than
downloading everything; date-scoped queries narrow reads to the relevant day instead
of pulling full histories on every interaction.

**Genuinely polished, not just styled.**
Skeleton loading states, animated route transitions, contextual coach marks that
correctly tear themselves down on navigation, empty states written as guidance rather
than apology, and destructive actions guarded by deliberate confirmation.

---

## 🧩 Challenges Solved

<details open>
<summary><b>Keeping multiple devices in perfect agreement</b></summary>
<br/>

A shared study timer has to look identical on every screen, including for people who
arrive after it started and people whose app was briefly backgrounded. Independent
per-device countdowns drift and diverge immediately.

**Outcome:** all members — early, late, or returning — see the same phase, session
index, and remaining time, with no reconciliation logic and no visible correction.

</details>

<details open>
<summary><b>Making a shared feature safe to open to strangers</b></summary>
<br/>

The moment a feature lets one user affect another's experience, every client becomes
untrusted. Someone could try to remove members, seize the host role, tamper with
timing, spoof what an invite claims to be, or crawl for active rooms.

**Outcome:** each of those attacks is closed at the database layer, and the remaining
theoretical risks were identified, documented, and addressed by a prepared
server-authoritative path — an honest accounting of what a client-side model can and
cannot guarantee.

</details>

<details open>
<summary><b>Statistics that can't be gamed</b></summary>
<br/>

Progress, streaks, and achievements are only motivating if they're truthful. A client
that writes its own numbers can trivially fabricate them.

**Outcome:** every progress counter is range-validated server-side against
physically possible bounds, achievements are evaluated in exactly one place so they
can never double-fire, and abandoning a session logs nothing at all.

</details>

<details open>
<summary><b>Recurring goals that behave the way people expect</b></summary>
<br/>

"Every weekday until December" is easy to store and hard to get right. Users edit a
single occurrence, reschedule another, complete a third, and expect the rest of the
series to stay untouched.

**Outcome:** a recurrence system covering six frequency patterns with custom
intervals, weekday selection, end dates, and occurrence limits — where per-occurrence
edits, completions, and reschedules coexist with the underlying series.

</details>

<details open>
<summary><b>Renaming core concepts on a live app</b></summary>
<br/>

Domain vocabulary changed mid-project, touching stored records, local preference keys,
and database collections. Users with existing data — and users who hadn't updated
yet — could not be broken.

**Outcome:** a transparent startup migration that copies rather than destroys, keeps
old paths readable, and lets old and new builds coexist during rollout.

</details>

<details open>
<summary><b>Asking for invasive permissions without losing the user</b></summary>
<br/>

Notifications and Screen Time access are both high-friction prompts, and Screen Time
in particular is one users are rightly suspicious of.

**Outcome:** every request is preceded by a plain-language explanation of what it
enables, an explicit statement that data stays on-device, and a genuine option to
decline — declining degrades the feature rather than blocking the app.

</details>

<details open>
<summary><b>Making a startup sequence that can't white-screen</b></summary>
<br/>

An app that initializes notifications, alarms, blocking, theming, migrations, deep
links, and billing before its first frame has many ways to fail on someone else's
device.

**Outcome:** non-critical subsystems fail independently and silently, and the one
genuinely critical dependency fails into a recoverable, retryable error screen
instead of a blank one.

</details>

---

## 🎯 Key Takeaways

- **Production thinking.** Failure handling, migrations, permission UX, account deletion, and billing are treated as core work rather than afterthoughts.
- **Security-conscious engineering.** Trust boundaries are identified explicitly, enforced where they can't be bypassed, and the residual risks are documented honestly instead of hidden.
- **Distributed systems intuition.** Shared real-time state is designed to be correct by construction rather than patched with synchronization workarounds.
- **Architectural discipline.** A consistent layered structure held across ~47,000 lines of Dart, 30+ screens, and a native platform integration.
- **Cross-platform and native fluency.** Flutter for reach, Swift where the platform demands it, with a clean seam between the two.
- **Product judgment.** Features exist because they close a real gap in the user's loop — the onboarding personalizes, the blocking removes temptation, the multiplayer supplies accountability.
- **Design craft.** A cohesive visual language, a real theme system, and interaction polish that holds up under scrutiny.
- **Maintainability.** Single-responsibility files, documented reasoning at every non-obvious decision, and testable business logic separated from UI.

---

## 🔭 Future Improvements

- **Server-authoritative multiplayer** — promote the prepared Cloud Functions to production so every room mutation is validated server-side.
- **Android app blocking** — extend the platform-agnostic blocking contract with an Android backend.
- **Push notifications** — cross-device room and social notifications alongside the current on-device scheduling.
- **Expanded test coverage** — grow beyond the current goal-lifecycle and recurrence suites into integration and multiplayer scenarios.
- **Larger rooms & social graph** — friends, persistent study groups, and higher member ceilings.
- **Web & tablet layouts** — responsive breakpoints for the existing Flutter web target.
- **Offline-first sync** — queued local writes that reconcile when connectivity returns.
- **Accessibility audit** — formal screen-reader, contrast, and dynamic-type verification.
- **Localization** — the language setting is in place; content translation is the next step.

---

## 🎨 Design Philosophy

Focal's interface is built on the idea that a focus app should itself be calm.

**Restraint over decoration.** The visual language is deep, low-contrast ambience with
a single accent that carries all emphasis. Nothing on screen competes for attention
with the thing the user came to do.

**Consistency by construction.** Every surface reads from a shared palette and a shared
component library — cards, buttons, badges, empty states, and sheets are defined once.
This is why eight entirely different environments can recolor the whole application
without a single screen looking out of place.

**Motion with meaning.** Animation is used to explain state, not to perform. Environment
changes interpolate so the user perceives one continuous world; skeleton loaders
preserve layout so content arrives instead of appearing.

**Honest empty states.** A screen with nothing in it tells the user what to do next
rather than apologizing for being empty.

**Guidance, not gatekeeping.** Onboarding personalizes rather than instructs, coach
marks appear once and disappear cleanly, and every permission is explained before it
is requested.

**Respect for the user's data and attention.** Privacy is stated plainly in the
product, not buried in a policy. Blocking releases the moment a session ends.
Account deletion is a first-class action, not a support ticket.

---

<div align="center">
<sub><b>Focal</b> — Flutter · Firebase · Swift · ~47,000 lines of Dart</sub>
</div>

<div align="center">
<sub><a href="../../README.md">← Back to portfolio</a></sub>
</div>
