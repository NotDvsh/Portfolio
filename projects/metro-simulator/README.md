# 🚇 Metro Route & Schedule Simulator

> **Real transit, modelled honestly.** A command-line simulator for a multi-line metro network that plans journeys, times trains, and prices fares against a real-world timetable.

<div align="center">

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Dependencies](https://img.shields.io/badge/Dependencies-none-success?style=flat-square)
![Interface](https://img.shields.io/badge/Interface-CLI-4B5563?style=flat-square)
![Data](https://img.shields.io/badge/Data-Real%20Network-0EA5E9?style=flat-square)

</div>

---

## Overview

A simulator for a real metro system — modelled on the Delhi Metro's actual station
order, travel times, and interchange points — that answers the questions a rider
actually has: *when is my next train, how do I get there, how long will it take, and
what will it cost?*

**Why it's interesting:** a transit network is a graph with awkward real-world
constraints bolted on. Trains only run during service hours. Frequency changes at peak
times. Switching lines costs you minutes that don't appear on any map. The shortest
route by stops isn't always the fastest by clock. Getting a believable answer means
modelling all of that, not just running a pathfinder over a graph.

**Scope note:** the assignment called for two lines. I built it as a general
multi-line network and modelled four.

> 🔒 Source is kept private — this is coursework, and publishing a working solution
> isn't fair to anyone still doing it. Happy to walk through the design in an interview.

---

## ✨ Capabilities

### Journey Planning

| Capability | Description |
| :--- | :--- |
| **Route Finding** | Computes a route between any two stations across the network, including journeys that span multiple lines. |
| **Interchange Handling** | Line changes are detected, surfaced to the user, and costed in time rather than treated as free. |
| **Time-Aware Results** | Plans are anchored to a departure time, so boarding and arrival times are real clock times, not abstract durations. |
| **Structured Itinerary** | Output reads as a usable set of directions — where to board, where to switch, and when you arrive. |

### Scheduling

| Capability | Description |
| :--- | :--- |
| **Next Train Lookup** | Reports upcoming departures from any station on any line at a given time. |
| **Peak & Off-Peak Frequency** | Service intervals shift with time of day, matching how the network actually runs. |
| **Service Hours** | Queries outside operating hours are recognised and handled, rather than silently returning impossible trains. |

### Network & Usability

| Capability | Description |
| :--- | :--- |
| **Multi-Line Network** | Four lines modelled with full station ordering and interchange relationships. |
| **External Data** | The network is defined in a data file rather than hardcoded, so lines and stations can be added without touching program logic. |
| **Fare Calculation** | Journey cost derived from travel time, with a minimum-fare floor. |
| **Line Browsing** | Full station listings per line, for orientation before planning. |
| **Forgiving Input** | Station and line names are accepted in any casing. |
| **Menu-Driven CLI** | A guided prompt-based interface — no flags or syntax to memorise. |

---

## 🛠 Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Language** | Python 3 |
| **Dependencies** | None — standard library only |
| **Data Source** | Real published network data, structured manually into a delimited data file |
| **Interface** | Interactive command-line menu |

---

## 🏗 Architecture

```
 Network data file
        │
        ▼
┌────────────────┐   stations · connections · interchanges
│  Data Loader   │
└───────┬────────┘
        │
        ├──────────────┬──────────────────┐
        ▼              ▼                  ▼
┌──────────────┐ ┌────────────┐  ┌────────────────┐
│ Route Finder │ │ Scheduling │  │ Fare Calculation│
└──────┬───────┘ └─────┬──────┘  └────────┬───────┘
       │               │                   │
       └───────────────┴───────────────────┘
                       │
                       ▼
             Journey plan / timings
```

**Guiding rules**

- **Data out of code.** The network lives in a data file, so extending it is a data change rather than a code change — which is exactly why going from two lines to four was straightforward.
- **Model reality, not the happy path.** Service hours, peak frequency shifts, and interchange penalties are part of the model, not caveats in a comment.
- **Composable pieces.** Routing, scheduling, and fare logic are independent, so each can be reasoned about and corrected on its own.
- **The user is not a programmer.** Input is forgiving and output is written to be read.

---

## 👤 My Contributions

I built the entire simulator, sourced and structured the network data, and extended it
beyond the required scope.

| Area | What I built |
| :--- | :--- |
| **Network Model** | Sourced real station ordering, travel times, and interchange points, and structured them into a loadable data format. |
| **Route Finding** | The pathfinding layer that connects any two stations, including multi-line journeys. |
| **Scheduling** | Next-train logic with peak/off-peak frequency variation and service-hour awareness. |
| **Journey Planning** | The layer that combines route, timing, and interchange cost into a real itinerary with clock times. |
| **Fare Logic** | Cost calculation with a minimum-fare rule. |
| **Interface** | The menu-driven CLI, forgiving input handling, and readable output formatting. |
| **Scope Extension** | Doubled the network beyond the two required lines, which the data-driven design absorbed without a rewrite. |

---

## 🧩 Challenges Solved

<details open>
<summary><b>The shortest route isn't the fastest one</b></summary>
<br/>

Fewest stations and least time are different answers once interchanges carry a real
penalty. A route with one fewer stop but an extra line change can be slower.

**Outcome:** interchange cost is part of the model, so planned journeys reflect actual
travel time rather than a naive hop count.

</details>

<details open>
<summary><b>Time that behaves like time</b></summary>
<br/>

Train frequency isn't constant, service stops overnight, and a journey that starts at
one frequency can finish under another. Treating time as a plain number breaks all of
this.

**Outcome:** departures, waits, and arrivals are computed against real clock times with
correct peak/off-peak behaviour, and out-of-service queries are handled rather than
producing nonsense.

</details>

<details open>
<summary><b>Turning a paper map into a usable data model</b></summary>
<br/>

Published network information is designed for humans reading a poster — station order,
travel times, and interchanges are scattered across sources and inconsistently
presented.

**Outcome:** a clean, consistent data representation that the program loads directly,
with documented assumptions where source data was ambiguous.

</details>

<details open>
<summary><b>Building for a scope larger than the brief</b></summary>
<br/>

Hardcoding two lines would have been faster and would have met the requirement.

**Outcome:** a data-driven design that scaled to four lines without restructuring —
the difference between solving the assignment and building the system the assignment
described.

</details>

---

## 🎯 Key Takeaways

- **Modelling judgment.** The engineering here isn't the pathfinding, it's deciding which real-world constraints matter and how faithfully to represent them.
- **Design for the requirement you'll get next.** Separating data from logic turned a scope increase into a data-entry task.
- **Honest assumptions.** Where source data was incomplete, defaults were chosen deliberately and documented rather than quietly guessed.
- **Usability counts, even in a terminal.** Forgiving input and readable output are product decisions, not polish.
- **No-dependency discipline.** Built entirely on the standard library.

---

## 🔭 Future Improvements

- **Full network coverage** beyond the current four lines
- **Live timetable data** in place of modelled frequencies
- **Route alternatives** — fastest versus fewest-interchange options side by side
- **Distance-based fares** matching real fare tables more closely
- **A visual or web front end** for the network map and planned route

---

<div align="center">
<sub><a href="../../README.md">← Back to portfolio</a></sub>
</div>
