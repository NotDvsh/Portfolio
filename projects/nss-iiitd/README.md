# 🤝 NSS IIIT Delhi — Unit Website

> **A public record, not a brochure.** The official site for IIIT Delhi's National Service Scheme unit: six static pages that state only what the unit can prove, built so the facts live in one file and the build refuses to ship an insecure page.

<div align="center">

![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)
![JavaScript](https://img.shields.io/badge/Vanilla%20JS-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![Runtime Dependencies](https://img.shields.io/badge/Runtime%20dependencies-none-success?style=flat-square)
![CSP](https://img.shields.io/badge/CSP-default--src%20'none'-0EA5E9?style=flat-square)

</div>

---

## Overview

The National Service Scheme unit at IIIT Delhi runs blood drives, teaching
programmes, cleanliness drives, heritage festivals and first-aid training. What it
did not have was a site that told the truth about any of it — the previous attempt
was a React app carrying invented statistics, placeholder people and stock
photography of a campus that wasn't ours.

This is the replacement, built as **Web Development Lead** for the 2026–27 core team:
six static documents — Home, About, What we do, Events, Gallery, How to join — plus a
real 404. No framework. No runtime dependencies. Nothing fetched at page load. Every
photograph on it was taken by a volunteer at one of the unit's own events.

**Why it's interesting:** a student-body site fails in a specific way. Counts get
hand-typed into four pages, three of them drift, and a year later nobody can say which
number is right. So the design problem wasn't visual — it was building a site where a
fact *cannot* be stated twice, where a date without a source *cannot* be added
casually, and where a well-meaning future edit that pastes in a tracking script or an
embedded form **fails the build instead of shipping**.

> 📄 Built for `nss.iiitd.ac.in`. The repository stays private until the unit's
> deploy is signed off by the institute; happy to walk through the code in an interview.

---

## ✨ Capabilities

### Content Integrity

| Capability | Description |
| :--- | :--- |
| **One source of truth** | A single chronology file holds every event the unit has run. The Events page, the front-page rail, the events-per-year chart and every count on the site are rendered from it at build time — add an entry and the whole site updates, or nothing does. |
| **Sourced dates only** | Each entry carries a precision-tagged date — a full day where a report or a photograph's EXIF establishes one, a month where only the month is on record — plus a `source` field naming the report it came from. No date is entered from memory. |
| **Honest photography** | A photograph taken at the event is shown as itself. Where a day left none, a picture of the same kind of work stands in and is flagged `representative`, which the page prints on the image rather than hiding. |
| **No invented figures** | The inherited site's "150+ volunteers / 5000+ lives" numbers were dropped outright rather than carried forward. Every figure on the page traces to the unit's own records. |

### The Build

| Capability | Description |
| :--- | :--- |
| **Route table drives everything** | One ordered list of routes generates the build inputs, the sitemap, the canonical URLs, the 301 redirects, the previous/next pager at the foot of every page and the 404's index. Reordering the site is a one-line edit. |
| **Partial expansion** | `<!--part:name-->` inlines the shared header, footer, utility strip and SVG sprite at build time — deliberately not a template language: no variables, no conditions, no loops. |
| **Build-time rendering** | Chronology markup, the year chart and responsive `<picture>` elements are all emitted during the build. The browser assembles nothing. |
| **Self-contained output** | Fonts are vendored locally, so the built site makes zero third-party requests. |

### Security (enforced, not documented)

| Capability | Description |
| :--- | :--- |
| **The build audits itself** | A custom Vite plugin reads the built output and **fails the build** on an inline event handler, a `javascript:` URL, an author-written `style` attribute, a plaintext `http` subresource, a `<form>`, an `<iframe>`, or a link to an origin nobody declared. |
| **Hash-pinned CSP** | Every inline script and style is hashed from the final bytes and named in the policy, so `script-src` needs no `unsafe-inline`. `default-src 'none'`, with each directive re-permitting exactly one thing. |
| **Trusted Types** | The policy requires Trusted Types for script, so an `innerHTML`-shaped assignment is refused by the browser rather than trusted to never be written. The source contains none — the lightbox and the sign-up block build DOM nodes instead. |
| **Host-agnostic headers** | The build writes `_headers`/`_redirects`, `.htaccess` and `nginx-headers.conf` — the institute's host wasn't known at build time — plus the same policy as a `<meta>` tag, so a host that ignores all three still enforces most of it. |
| **Full header set** | HSTS, `nosniff`, `X-Frame-Options: DENY`, a restrictive `Referrer-Policy` and `Permissions-Policy`, and the three cross-origin isolation headers. |
| **Link crawler** | A post-build crawler fails on an internal link to a page that doesn't exist, a `#fragment` with no matching element, or a `srcset` candidate that was never generated. |

### Interface & Motion

| Capability | Description |
| :--- | :--- |
| **Progressive enhancement throughout** | Roughly 12 KB of JavaScript, all of it additive. The gallery frames are frames, the event record is in the HTML, the rail scrolls on a trackpad — before a line of script runs. |
| **Linkable filtered views** | The Events category filter writes its state to the query string, so a filtered view can be linked and survives a reload — leaving the hash free for the anchors the front page points at. |
| **Native-dialog lightbox** | Arrow keys move between photographs, Escape closes, focus returns to the frame that was opened, and the enlarged view reuses the `srcset` the page already shipped. |
| **One motion authority** | A single module reads `prefers-reduced-motion`, re-reads it when it changes without a reload, and everything scroll-driven asks it before doing per-frame work. |
| **Responsive image ladder** | Curated masters emit AVIF, WebP and JPEG derivatives across seven widths, with intrinsic dimensions baked into the markup. No upscaling past a master's real size. |

---

## 🛠 Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Build** | Vite 5, multi-page, with four custom plugins (partials, chronology, responsive images, routing) and one security plugin |
| **Markup** | Static HTML, one document per route |
| **Styles** | Hand-written CSS — tokens and components, ~57 KB built |
| **Behaviour** | Vanilla ES modules, ~12 KB built, no framework |
| **Images** | `sharp` — AVIF / WebP / JPEG at seven widths |
| **Runtime dependencies** | None |
| **Output** | A static `dist/`. Nothing runs on a server. |

---

## 🏗 Architecture

```
  src/routes.js          src/data/events.js        assets/masters/
  (the site's shape)     (the chronology)          (curated photographs)
        │                        │                        │
        │                        │                        ▼
        │                        │              ┌───────────────────┐
        │                        │              │  image pipeline   │ AVIF · WebP · JPEG
        │                        │              │     (sharp)       │ × 7 widths
        │                        │              └─────────┬─────────┘
        ▼                        ▼                        ▼
┌──────────────────────────────────────────────────────────────────┐
│                        Vite build pipeline                       │
│  partials → chronology → responsive images → routing → security  │
└────────────────────────────────┬─────────────────────────────────┘
                                 │
                                 ▼
                        ┌────────────────┐
                        │ security audit │──► FAIL on inline handler, style attr,
                        │   + CSP hash   │     form, iframe, http subresource,
                        └───────┬────────┘     undeclared origin
                                │
                                ▼
                   dist/  (6 pages · 404 · header files
                           · sitemap · redirects)
                                │
                                ▼
                        link crawler ──► FAIL on a broken link,
                                          dead anchor or missing image
```

**Guiding rules**

- **A fact appears once.** If a number is stated in two places, one of them is already wrong. Counts, dates and the chronology are rendered from one file; page markup never types a figure.
- **The policy is the floor, not the ceiling.** Rather than documenting "don't add inline styles", the build fails on them. A rule nobody can quietly weaken is the only kind still standing a year later.
- **JavaScript is additive, always.** Every page is complete before a module boots. Script adds the lightbox, the filter, the drag-scroll and the reveals — it is never what makes the content readable.
- **Handed over, not abandoned.** Deploy notes name the file to edit for every kind of change, because the next Web Dev Lead is a student who has never seen this code.

---

## 👤 My Contributions

I built the site end to end as the unit's Web Development Lead — architecture, build
tooling, security, markup, styles, motion, the photo pipeline, and the verification
pass over the content itself.

| Area | What I built |
| :--- | :--- |
| **Architecture** | The route table, the six-page structure, the partials system, and the decision to drop the framework entirely. |
| **Build tooling** | Four custom Vite plugins — partial expansion, chronology rendering, responsive-image markup, and routing with dev/preview parity for redirects and the 404. |
| **Security** | The audit-and-fail plugin, the hash-pinned CSP with Trusted Types, the three host header files, and the meta-tag fallback. |
| **Content verification** | Cross-read the unit's reports, rosters and event forms against photo EXIF to date twenty entries; discarded every inherited claim that no source supported. |
| **Photo pipeline** | Master curation and alt text, the AVIF/WebP/JPEG derivative ladder, and the composited hero mural cut into the wordmark. |
| **Interface** | Styles and layout, the gallery lightbox, the linkable Events filter, the home-page rail, the count-up figures, and the reveal choreography. |
| **Accessibility & motion** | The reduced-motion authority, keyboard paths through the gallery and rail, focus return, and CSS-only reveals that never hide content from a reader without JavaScript. |
| **Handover** | Deploy documentation mapping each kind of content change to the one file that owns it, plus the link crawler that proves a build before it ships. |

---

## 🧩 Challenges Solved

<details open>
<summary><b>Inheriting a site built on numbers nobody could source</b></summary>
<br/>

The previous React site advertised "150+ volunteers" and "5000+ lives impacted",
a placeholder team, a fabricated volunteer table and stock photography. Carrying any
of it forward would have been faster, and would have made every real fact on the page
untrustworthy by association.

**Outcome:** none of it migrated. Twenty events were re-derived from the unit's own
reports, rosters and photograph EXIF — including two dates where the written overview
and the photographs disagreed, and the photographs won. Only structural ideas survived
the rewrite.

</details>

<details open>
<summary><b>A fact stated in four places drifts in three</b></summary>
<br/>

Event counts, the year chart, the front-page rail and the Events page all describe the
same record. Hand-maintained, they diverge on the first busy month — which is exactly
how the unit's earlier sites decayed.

**Outcome:** one chronology file, rendered into every one of those surfaces at build
time through placeholders. There is no path by which the count and the list can
disagree, because the count *is* the list.

</details>

<details open>
<summary><b>Security that survives the next maintainer</b></summary>
<br/>

This site will be handed to a student who has never seen it, under deadline, probably
copy-pasting an embed from somewhere. A README saying "please don't add inline scripts"
does not survive that.

**Outcome:** the build audits its own output and refuses to produce a release
containing an inline handler, a style attribute, a form, an iframe or an undeclared
origin — and prints the file, the line and the fix. Adding a legitimate third-party
embed is still possible; it just requires declaring it deliberately in one named list
rather than arriving unnoticed with a paste.

</details>

<details open>
<summary><b>A photograph-heavy site that still loads on campus Wi-Fi</b></summary>
<br/>

The unit's best argument is its photographs, and the honest ones are multi-megabyte
camera JPEGs.

**Outcome:** a build-time ladder emitting AVIF, WebP and JPEG across seven widths with
intrinsic dimensions in the markup, skipping any derivative already newer than its
master — and degrading to a plain copy when `sharp` can't build, so a teammate's
`npm run dev` still works. The pages ship ~12 KB of JavaScript and ~57 KB of CSS
against it.

</details>

<details open>
<summary><b>Motion that reads as craft, not decoration</b></summary>
<br/>

The first build leaned on GSAP and Lenis for scroll choreography. Both were removed:
they were runtime dependencies, they fought the CSP, and smooth-scroll hijacking is a
reading tax on a page people visit to find a date.

**Outcome:** CSS-only reveals gated behind a class that a single module sets — and
only when `IntersectionObserver` exists — with one authority reading
`prefers-reduced-motion` live. Nothing is ever hidden by a style written in JavaScript,
so a reader with scripts off gets the entire page.

</details>

---

## 🎯 Key Takeaways

- **Structure is a truthfulness tool.** Deduplicating facts into one file wasn't a DRY exercise — it was the only way to guarantee the site can't contradict itself in public.
- **Enforce what you'd otherwise document.** Rules that fail a build outlive rules that live in a README, especially on a codebase handed between students every year.
- **A framework is a decision, not a default.** Six static documents with no runtime dependencies load faster, deploy anywhere the institute puts them, and will still build in four years.
- **Verification is engineering work.** Reconciling reports against EXIF to date twenty events took longer than writing the chronology renderer, and it is the part that makes the site worth reading.
- **Build for the person who inherits it.** Deploy notes that name the one file to edit per change are as much a deliverable as the site itself.

---

## 🔭 Future Improvements

- **Wire the live sign-up flow** — the volunteer form URL is the one value left to set; until then every CTA falls back to the unit's email and says so, rather than pointing at a dead link
- **A volunteer-facing content workflow** so entries can be added without a pull request
- **Per-event galleries** linking the chronology to the photographs from that day
- **Automated accessibility and Lighthouse checks in CI**, alongside the existing link crawler
- **An annual-report view** generated from the same chronology the site already renders

---

<div align="center">
<sub><a href="../../README.md">← Back to portfolio</a></sub>
</div>
