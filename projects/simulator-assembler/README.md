# ⚙️ Assembler & Simulator

> **From assembly source to executed instruction.** A two-stage toolchain that assembles RISC-V assembly into machine code and executes it on a cycle-accurate virtual processor.

<div align="center">

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![RISC--V](https://img.shields.io/badge/ISA-RISC--V-283272?style=flat-square&logo=riscv&logoColor=white)
![Dependencies](https://img.shields.io/badge/Dependencies-none-success?style=flat-square)
![Tests](https://img.shields.io/badge/Tested-Automated%20Harness-6E56CF?style=flat-square)

</div>

---

## Overview

A complete low-level toolchain built in two halves that fit together:

**The Assembler** takes human-readable assembly and translates it into the exact binary
encoding a processor expects — resolving symbolic references, validating every
instruction, and reporting precisely what's wrong when the source isn't valid.

**The Simulator** takes that machine code and executes it, modelling the processor's
registers and memory faithfully enough that the state after every instruction can be
inspected and verified.

**Why it's interesting:** most software is written on top of abstractions like these.
Building both ends means understanding what actually happens between a line of source
and a value landing in a register — instruction encoding, addressing, control flow,
and program termination, with nothing hand-waved.

> 🔒 Source is kept private — this is coursework, and publishing a working solution
> isn't fair to anyone still doing it. Happy to walk through the design in an interview.

---

## ✨ Capabilities

### Assembler

| Capability | Description |
| :--- | :--- |
| **Full Instruction Coverage** | Supports every instruction format in the target ISA — arithmetic, logical, memory, branching, jumps, and upper-immediate. |
| **Symbolic Labels** | Named jump and branch targets are resolved automatically, including forward references. |
| **Register Naming** | Both numeric and conventional ABI register names are accepted interchangeably. |
| **Comprehensive Validation** | Unknown instructions, malformed operands, bad register names, out-of-range values, undefined labels, and duplicate labels are all caught before output is produced. |
| **Precise Diagnostics** | Errors identify what is wrong and where, rather than failing silently or producing incorrect machine code. |
| **Readable Output Mode** | An optional human-inspectable encoding alongside the raw binary, for verification and debugging. |

### Simulator

| Capability | Description |
| :--- | :--- |
| **Instruction Execution** | Decodes and executes machine code across the full supported instruction set. |
| **Register & Memory Model** | Maintains the complete register file and a memory model with separate instruction and data regions. |
| **Control Flow** | Branches and jumps drive execution exactly as the hardware would, including correct handling of the hardwired zero register. |
| **Signed & Unsigned Semantics** | Comparison and arithmetic behaviour matches the specification for both signed and unsigned interpretations. |
| **Execution Tracing** | Emits full processor state after every instruction, making execution auditable step by step. |
| **Clean Termination** | Detects the program-halt condition and stops deterministically rather than running off the end of memory. |

---

## 🛠 Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Language** | Python 3 |
| **Target ISA** | RISC-V (32-bit integer subset) |
| **Dependencies** | None — standard library only |
| **Interface** | Command line, file in / file out |
| **Testing** | Automated harness comparing output against reference results |

---

## 🏗 Architecture

```
Assembly source
      │
      ▼
┌──────────────┐   symbol resolution + validation
│  Assembler   │
└──────┬───────┘
       │  machine code
       ▼
┌──────────────┐   decode → execute → update state
│  Simulator   │   (registers · memory · control flow)
└──────┬───────┘
       │
       ▼
 Execution trace
```

**Guiding rules**

- **Two independent stages.** Each half is usable on its own, and each is verified on its own — a bug in one can't be masked by the other.
- **Separation of data and logic.** The instruction set is expressed as data rather than baked into control flow, so extending it doesn't mean rewriting the translator.
- **Fail loudly, fail early.** Invalid input is rejected with a specific reason before any output is written; producing wrong machine code silently is the worst possible outcome.
- **Verifiable by construction.** Every stage emits inspectable output, so correctness is demonstrated rather than assumed.

---

## 👤 My Contributions

I built both halves of the toolchain and the supporting test material.

| Area | What I built |
| :--- | :--- |
| **Assembler** | The full translation pipeline — parsing, symbol resolution, encoding across every instruction format, and output generation. |
| **Validation Layer** | The error-handling system covering instruction, operand, register, immediate, and label correctness, with targeted messages. |
| **Simulator** | Instruction decoding, the execution engine, the register and memory model, control-flow handling, and termination detection. |
| **Tracing** | Full per-instruction state output, which doubles as the verification mechanism. |
| **Testing** | Test programs spanning straightforward and complex cases, validated against reference output. |

---

## 🧩 Challenges Solved

<details open>
<summary><b>Getting the encoding exactly right</b></summary>
<br/>

Machine code is unforgiving — a single misplaced bit produces a valid-looking
instruction that does something entirely different. Several instruction formats scatter
their fields in non-obvious ways specifically to simplify hardware, not humans.

**Outcome:** every supported format encodes correctly and byte-matches reference
output across the full test suite.

</details>

<details open>
<summary><b>Resolving references that don't exist yet</b></summary>
<br/>

Programs routinely jump forward to a label defined later in the file, so a single
straight-through read of the source can't resolve them.

**Outcome:** all symbolic references resolve correctly regardless of order, with
undefined and duplicate labels reported as clear errors instead of bad output.

</details>

<details open>
<summary><b>Error messages that actually help</b></summary>
<br/>

A translator that only says "invalid input" is nearly useless to the person writing
the assembly.

**Outcome:** a layered validation system where each class of mistake — wrong operand
count, unknown register, out-of-range value, undefined label — is detected
independently and reported specifically.

</details>

<details open>
<summary><b>Proving the thing is correct</b></summary>
<br/>

"It runs" is not evidence. A processor model can produce plausible output while being
subtly wrong in ways that only surface on specific programs.

**Outcome:** full state tracing after every instruction, checked against reference
results across easy and hard cases, so correctness is verified rather than assumed.

</details>

---

## 🎯 Key Takeaways

- **Systems-level understanding.** Instruction encoding, register conventions, memory layout, and control flow — worked out at the bit level, not read about.
- **Correctness as the primary requirement.** In a translator, "mostly right" is indistinguishable from broken; the work was structured around proving output, not producing it.
- **Design for extension.** Treating the instruction set as data rather than logic keeps the system open to growth without rewrites.
- **Empathy for the user.** Even a command-line tool has a user, and diagnostics are a feature.
- **No-dependency discipline.** Built entirely on the standard library, so nothing is delegated to a package that hides the interesting part.

---

## 🔭 Future Improvements

- **Extended instruction support** beyond the current subset
- **Interactive debugging** — breakpoints and step-through execution
- **Performance modelling** such as pipeline and cycle-count simulation
- **A visual front end** for watching register and memory state evolve

---

<div align="center">
<sub><a href="../../README.md">← Back to portfolio</a></sub>
</div>
