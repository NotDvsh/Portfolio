# 🎨 Canvas Studio

> **A design tool that never leaves your machine.** A local-first, desktop-class vector canvas that runs entirely in the browser — infinite canvas, undo for everything, vector PDF export, and an AI layout assistant whose suggestions are validated before they touch the document.

<div align="center">

![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Konva](https://img.shields.io/badge/Konva-0D83CD?style=flat-square)
![Zustand](https://img.shields.io/badge/Zustand-433E38?style=flat-square)
![Backend](https://img.shields.io/badge/Backend-none-success?style=flat-square)

</div>

---

## Overview

Canvas Studio is a Figma-style design tool built to answer one question: how much of a
real editor can you build with **no server at all**? No accounts, no cloud, no upload
step — projects, pages, layers and image blobs persist to IndexedDB on the user's own
machine, and the whole thing ships as static files.

It opens on a projects dashboard (grid and list views, search, sort, starring, soft-delete
trash, a storage meter computed from the real documents), and a project opens into an
infinite canvas with a layers panel, an inspector, smart guides and a bottom-floating tool
switcher. An AI panel sits alongside, able to read the canvas — including the images on
it — and propose edits.

**Why it's interesting:** an editor is a pile of state that has to stay consistent under
a lot of pressure — sixty-frame-per-second dragging, undo that must never lie, images
that must survive being deleted and restored, and now a language model proposing
changes. The design problem wasn't drawing rectangles; it was deciding **what is allowed
to mutate the document, and making that list very short.**

> 📄 The repository is private; happy to walk through the code in an interview.

---

## ✨ Capabilities

### Canvas & Editing

| Capability | Description |
| :--- | :--- |
| **Infinite canvas** | Dotted backdrop with adaptive spacing; wheel/trackpad pan, pinch and ⌘-wheel zoom pivoting on the cursor (1%–800%), Space or **H** to drag-pan, zoom-to-fit. Opening a project frames its page automatically. |
| **Drawing tools** | Rectangle and arrow tools. Arrows have draggable endpoint handles, per-end arrowheads, and endpoints that snap to object centres, edge midpoints and corners. |
| **Selection & transform** | Click, shift-click, marquee, resize and rotate handles, multi-object drag. Pressing anywhere inside a selection's bounding box — gaps included — moves the whole selection. |
| **Groups** | Group / ungroup with nested hierarchy. A selected group is marked in violet, distinct from a plain multi-selection, so a container reads differently at a glance. |
| **Smart guides** | Edge and centre alignment with snapping while dragging, a configurable threshold, and grid snapping. |
| **Non-destructive crop** | The discarded region stays visible as a dimmed ghost, with rule-of-thirds guides. Reset always restores the full picture, and crops survive export. |
| **Images** | Paste from the system clipboard or drag-and-drop files; the blobs persist to IndexedDB. |
| **Undo / redo for everything** | Every document operation — including deleting a page — is an undoable command. |

### Workspace

| Capability | Description |
| :--- | :--- |
| **Layers panel** | Nested group tree with collapse, rename, hide, lock, and stacking-order controls. |
| **Inspector** | Edits the selection *box*: position, size, rotation, opacity, corner radius, arrowheads, fill, stroke and canvas settings. |
| **Pages** | Create, rename, switch and delete (undoably) pages within a project. |
| **Resizable panels** | Left and right panels collapse with animation and remember their widths across sessions. |
| **Autosave** | Debounced writes to IndexedDB; the last project reopens on launch. |
| **Vector PDF export** | Exports the current page as a real vector PDF sized to its content — written by a small hand-rolled PDF writer, not a library. |

### AI Assistant

| Capability | Description |
| :--- | :--- |
| **Natural-language editing** | "Organize this canvas", "align selected objects", "group related items", "convert this into a flowchart", "color-code sections". A selection scopes the request automatically. |
| **Swappable backends** | A built-in **offline** layout engine (instant, private, no key), **Claude**, or any **OpenAI-compatible** endpoint — switchable at runtime from the panel header. |
| **Sees the canvas** | With Claude, selected images are downscaled, cropped to their visible region and sent as vision input (up to five per request), each tagged with its object id so the model's operations map back to real objects. |
| **One suggestion, one undo** | However many operations a suggestion contains, accepting it is a single ⌘Z. |

---

## 🛠 Tech Stack

| Layer | Technology |
| :--- | :--- |
| **UI** | React 18, TypeScript (strict), Tailwind CSS 4 |
| **Canvas** | Konva via `react-konva` |
| **State** | Zustand 5 — a root store composed from slices, plus a separate transient interaction store |
| **Persistence** | IndexedDB through a small typed wrapper (projects, settings, image assets) |
| **Motion & input** | Framer Motion, `react-hotkeys-hook`, hand-written gesture hooks |
| **AI** | Provider interface with offline, Anthropic and OpenAI-compatible implementations |
| **Build** | Vite 6, `tsc --noEmit`, and a custom build-time check script |
| **Backend** | None. Seven runtime dependencies in total; ~13,500 lines of TypeScript across ~125 files. |

---

## 🏗 Architecture

```
src/
  types/       Domain model — objects (discriminated union), project, settings
  models/      Factories, hierarchy, crop maths, undoable commands
  store/       Zustand root store (slices) + interaction store + actions
  services/
    storage/       Typed IndexedDB wrapper — projects, settings, assets
    smart-guides/  Pure snapping engines
    export/        Hand-rolled vector PDF writer + page renderer
    ai/            Operation model · canvas snapshot · validator · applier
      providers/   offline · Claude · OpenAI-compatible
  components/  dashboard · canvas · toolbar · sidebar · inspector · ai · ui
  hooks/       bootstrap · autosave · shortcuts · gestures · assets
```

```
   user intent / gesture                        AI provider (offline | Claude | OpenAI)
          │                                                   │
          │                                      structured operations only
          ▼                                                   ▼
   ┌─────────────┐                                  ┌───────────────────┐
   │ store/      │                                  │  ai/validate.ts   │ drops unknown ids,
   │ actions.ts  │◄──── one CompositeCommand ◄──────│  ai/apply.ts      │ NaN, bad colours,
   └──────┬──────┘                                  └───────────────────┘ oversized plans
          │ executes
          ▼
   ┌─────────────┐   history   ┌──────────────┐  debounced  ┌───────────┐
   │  Commands   │────────────►│ document     │────────────►│ IndexedDB │
   │ (undoable)  │             │ slice (Zustand)           └───────────┘
   └─────────────┘             └──────┬───────┘
                                      │ reference-stable selectors only
                                      ▼
                              Konva stage + React panels
```

**Guiding rules**

- **All document mutations are commands.** The store's raw insert/remove/patch mutators are history-free primitives used only by commands and live drag previews. If it isn't a command, it can't change the document — which is what makes undo trustworthy.
- **The AI proposes; the app decides.** A provider returns declarative operations and nothing else. They are validated as hostile input, then compiled into a single command. Geometry-heavy intents like align and distribute are expressed as *goals*, so exact numbers come from real bounds, not from a language model.
- **Groups are logical.** Children keep world coordinates and point back via `parentId`; one module is the only place that walks that relation, so selection, dragging, transforms, delete and clone can't disagree.
- **Crops are fractions, never pixels.** An image's frame is its position and size; the crop says which fraction of the source that frame shows. The ghost, the commit and the PDF placement all derive from those two facts.
- **Transient state lives elsewhere.** Guides, marquees and drafts update every frame in their own store, so 60 fps interaction never wakes document subscribers.

---

## 👤 My Contributions

Solo project — designed and built end to end.

| Area | What I built |
| :--- | :--- |
| **Architecture** | The domain model, slice-based store, command layer, and the separation between document state and transient interaction state. |
| **Canvas engine** | Pan/zoom maths, the pointer-interaction state machine, selection and transform, arrow editing, snapping and smart-guide engines. |
| **Editing model** | Undoable commands for every operation, the group hierarchy, page-scoped history, and the non-destructive crop model. |
| **Persistence** | The typed IndexedDB layer, debounced autosave, soft-delete trash, and blob lifecycle for pasted and dropped images. |
| **Export** | A vector PDF writer and the page-to-PDF renderer, including cropped images. |
| **AI assistant** | The provider abstraction, canvas snapshot and scoping, the operation vocabulary, the validator and the applier — plus the offline layout engine that makes the feature useful without a key. |
| **Interface** | The projects dashboard, resizable panels, layers tree, inspector, toolbar and keyboard shortcuts. |
| **Guardrails** | A build-time check that fails on the subscription pattern that crashes the tab (see below). |

---

## 🧩 Challenges Solved

<details open>
<summary><b>A bug with no stack trace, caught by the build</b></summary>
<br/>

Zustand 5 reads through `useSyncExternalStore`, which compares snapshots by identity.
A selector that allocates a new array or object on every call makes React believe the
store changed on every render — it loops until the tab dies, and the error points at
nothing useful.

**Outcome:** selectors are split into reference-stable ones and a clearly marked
"derived (allocating)" section, and `npm run check` — wired into `npm run build` — fails
if a derived selector is passed to `useStore` or an inline selector allocates. A mistake
that would crash a user's tab is now a failed build with a file and line.

</details>

<details open>
<summary><b>Letting a language model near the document</b></summary>
<br/>

A model that edits the canvas directly can invent object ids, return `NaN` coordinates,
emit colours that aren't colours, or propose a thousand operations — and a half-applied
suggestion is worse than none.

**Outcome:** providers can only return declarative operations. A validator treats the
response as hostile — unknown ids, bad numbers and oversized plans are dropped and
*reported* to the user — and the survivors compile into one composite command. A
suggestion applies whole or not at all, and undoes in one keystroke.

</details>

<details open>
<summary><b>Undo that can never replay against the wrong thing</b></summary>
<br/>

Object edits live in a history; pages come and go. An undo after switching pages could
replay an edit against a page it was never made on. And a deleted image has to stay
restorable for as long as its delete sits on the undo stack — but orphaned blobs shouldn't
accumulate forever.

**Outcome:** page-level commands reset the object history first, so history never spans
a page boundary. Unreferenced image blobs are collected only at startup, the one moment
history is empty and an unreferenced blob is provably unreachable.

</details>

<details open>
<summary><b>Editing a crop without ever drifting</b></summary>
<br/>

Cropping an image repeatedly in pixel space accumulates rounding error, and breaks the
moment the source is re-encoded at a different size.

**Outcome:** crops are stored as normalized fractions of the source. Everything else —
the dimmed ghost, the commit, the PDF placement — is derived from the frame plus that
fraction, so cropping again and again doesn't drift and a crop stays valid across
re-encoding.

</details>

<details open>
<summary><b>Sixty frames a second without waking the whole app</b></summary>
<br/>

Wheel, trackpad and drag events arrive faster than frames, and every smart guide, marquee
and draft shape changes on every move. Pushed through the document store, that re-renders
every panel on every pixel.

**Outcome:** navigation input is coalesced to one viewport write per animation frame,
and transient visuals live in a separate interaction store that document subscribers never
see.

</details>

<details open>
<summary><b>Leaving a project without losing the last edit</b></summary>
<br/>

Autosave is debounced, so the editor can hold edits the dashboard's index hasn't seen yet.
Navigate away at the wrong moment and reopening loads a stale snapshot over live work.

**Outcome:** navigation flushes the open project into the index and to disk before it
happens, so the dashboard and the editor can't disagree about what's saved.

</details>

---

## 🎯 Key Takeaways

- **Shrink the set of things that can change state.** Routing every edit through commands is what made undo, autosave and AI suggestions all cheap to get right.
- **Treat model output as untrusted input.** Validating and compiling a suggestion into one command is the same discipline as validating a form submission — the model just writes in a friendlier format.
- **Enforce what you'd otherwise document.** A footgun that crashes the tab with no stack trace is better as a failing build than as a paragraph in a README.
- **Store the relationship, not the result.** Crops as fractions and groups as `parentId` links mean derived values can't drift out of sync with the thing they derive from.
- **No backend is a real design constraint.** Local-first meant thinking hard about blob lifetime, persistence timing and what "saved" means — questions a server would have answered for me.

---

## 🔭 Future Improvements

- **More drawing tools** — frames, circles, text and lines
- **Frames and nesting**, then components and auto-layout
- **Drag-to-reorder layers** and copy-as-PNG
- **Spacing and size smart guides**, plus rulers
- **Code-splitting** — the production bundle is a single ~726 KB chunk and the build warns about it
- **Realtime collaboration**, which the command layer is deliberately shaped to allow

---

<div align="center">
<sub><a href="../../README.md">← Back to portfolio</a></sub>
</div>
