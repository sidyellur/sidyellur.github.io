# Content brief v2 — Siddharth Yellur personal site

## READ THIS FIRST: what went wrong in v1

Round one produced eight pages that all read like **blog posts**. The visual
directions were fine; the *content architecture* was wrong. Each project was
written as 3–4 flowing paragraphs stacked in one narrow column, so every page
became an essay you had to read top-to-bottom.

This is a **personal website**, not an article. A visitor should be able to land,
scan, and understand who he is and what he's built in about fifteen seconds —
without reading a single full paragraph.

### The rules that fix it

1. **No prose blocks. Anywhere.** No paragraph longer than **two sentences**.
   The page has at most 4–5 such paragraphs in total (hero + about). Everything
   else is structured: labels, chips, spec rows, short feature items, stats,
   code, tables.
2. **A feature is a label plus one sentence.** Format:
   `**Nonce-signed marks** — a program can't forge itself a clean exit code.`
   Never a paragraph. Never two sentences. One.
3. **Scan before read.** Every piece of depth sits under a bold label, a table
   key, or a chip. A visitor skimming only the bold text must still get it.
4. **Break the single column.** Blog = one narrow column, top to bottom.
   Website = varied rhythm. Use side-by-side layouts, multi-column feature
   grids, full-width bands, a spec rail next to content, alternating alignment.
   The eye must move across, not only down.
5. **Progressive disclosure.** Deep detail goes behind tabs, `<details>`
   accordions, expandable rows, or a hover/click state — available on demand,
   not dumped inline. Default view = compact.
6. **Above the fold does real work.** Name, one line on what he builds, the
   three project names, and a way in — all visible before the first scroll.
7. **Shorter overall.** If your page is longer than about three or four screens
   at 1440px, you are still writing an article. Cut.
8. **Use website furniture**: a real nav, section anchors, cards, grids, spec
   tables, stat blocks, chips/pills, badges, a proper multi-column footer.

Fitting the copy to *your* design's voice is fine. Turning it back into
paragraphs is not.

---

## The person

- **Siddharth Yellur** — engineer.
- One-line positioning: **"I build developer tooling for AI agents."**
- Secondary line: *"Memory that outlives the session, a terminal that reports
  what actually happened — and a snowboarding game with no image files."*
- GitHub: https://github.com/sidyellur
- LinkedIn: https://www.linkedin.com/in/siddharth-yellur-682351142/
- Education (small, in a spec row or footer — never a section of its own):
  M.S. Computer Science, University of Florida · B.E. Computer Science, Anna University.

**About section — maximum 3 short sentences.** Suggested:
> I build the layer underneath AI agents — the part nobody demos.
> Memory that persists, a terminal that can prove what a command returned, a
> renderer whose colours are checked by the build instead of by eye.
> Most of it is Python and TypeScript, runs locally, and is open source.

Do NOT include: employer, job-hunt language, dates that will rot, phone number,
.edu email, skill percentage bars, a resume PDF link, stock photos, or a
project called `cue` (private repo).

Contact = GitHub and LinkedIn only.

**Optional hero stat strip** (only if it suits your design):
`3 projects shipped` · `2 on PyPI` · `0 image files` · `100% local-first`

---

## Project 1 — tether

- **Tagline:** Durable memory for AI agents.
- **One line:** An MCP server backed by one local SQLite file, so what an agent
  learns about you survives the session it learned it in.
- **Spec row:** `v0.5.1` · `Python` · `MCP` · `SQLite / FTS5` · `libSQL / Turso`
- **PyPI:** `tether-memory`
- **Install:** `claude mcp add tether -- uvx tether-memory`
- **Repo:** https://github.com/sidyellur/tether
- **Headline stat:** `66.9KB → 2.0KB` — recall response, after returning
  query-centered excerpts instead of full bodies.

**Features — label + ONE sentence each. Lay these out as a grid or table, not a list of paragraphs:**

- **Four verbs** — `remember`, `recall`, `link`, `forget`.
- **Local-first** — one SQLite file, zero configuration, nothing leaves the machine.
- **Optional sync** — point it at libSQL/Turso and the same file becomes an embedded replica across every device.
- **Hybrid recall** — FTS5 keyword hits fused with local semantic vectors, so "automobile" finds your note about a car.
- **Associative graph** — related memories surface along three edge types: semantic, explicit `link()`, and hebbian.
- **Hebbian edges** — memories recalled together get wired together over time.
- **`via` receipts** — every hit reports which edge it came down.
- **Seed-dominant** — associations fill the slots below direct hits, never demoting a good one.
- **Self-organizing** — a hub-curated boot index surfaces load-bearing memories; nothing is ever hard-deleted.
- **Crystallization** — detects dense memory clusters and offers them up to be named as principles.
- **Degrades cleanly** — every feature falls back to plain keyword recall.

---

## Project 2 — cleat

- **Tagline:** A real terminal for AI agents.
- **One line:** A persistent shell behind a PTY that returns structured results
  — `stdout`, a real exit code, files touched — instead of escape-code soup.
- **Spec row:** `Python` · `MCP` · `PTY / termios` · `OSC 133` · `pyte`
- **PyPI:** `cleat`
- **Install:** `claude mcp add cleat -- uvx cleat`
- **Repo:** https://github.com/sidyellur/cleat
- **Proof block** — show this verbatim, it's the best single artifact on the page:
  ```
  { "stdout": "...", "exit_code": 0, "completed": true, "state": "idle" }
  ```
- **The hook** (use as a pull-stat or callout, not a paragraph):
  **"The exit code isn't in the stream at all."**

**Features — label + ONE sentence each:**

- **The problem** — a shell knows `$?` but never prints it, so scraping a PTY can't recover it.
- **The fix** — cleat injects OSC 133 marks into the shells it spawns and parses them back out.
- **Persistent session** — `cd`, `export`, venvs and `ssh` all carry across calls.
- **State is read, not guessed** — derived from termios flags and the foreground process group.
- **Five states** — `idle`, `running`, `awaiting-input`, `password`, `tui`.
- **Password consent** — it refuses to type into a password prompt without a human go-ahead.
- **Nonce-signed marks** — a program can't forge itself a clean exit code.
- **Spoof reporting** — a bad mark is ignored and surfaced as `spoofed_marks`.
- **Terminal-agnostic** — not an emulator, and not a patch to yours.

*A five-row state table (`state` → what it means → what to do) would suit this
project well and is very much a website element rather than a blog one.*

---

## Project 3 — Black Diamond Brawl

- **Tagline:** A downhill snowboarding combat racer.
- **One line:** Road Rash on a snowboard — one seeded procedural slope, a finish
  line, and rivals who'd rather you didn't reach it.
- **Spec row:** `Phaser 3` · `TypeScript` · `Vite` · `segment-based pseudo-3D`
- **Status:** `v1 complete (9 phases)` · `v2 visual overhaul complete`
- **Repo:** https://github.com/sidyellur/black-diamond-brawl
- **Headline stat:** `0` — image files in the repository.

**Features — label + ONE sentence each:**

- **Seeded slopes** — every run is a fixed-length procedurally generated course ending at a finish line.
- **Trick air** — moguls and hill crests launch you automatically at speed.
- **Combat mid-race** — shove or ski-pole your way past AI rivals on the same course.
- **Scoring** — finish fast, land hits, thread near-misses, stomp tricks.
- **Wipe out** — crash hard before the line and the run ends early.
- **Pseudo-3D renderer** — segment-based projection, the OutRun and Road Rash lineage.
- **Art in code** — every sprite and gradient is generated at boot; no image files at all.
- **Contrast build gate** — the build fails below ΔL* 12 on gameplay edges or ΔL* 25 on sprite outlines.
- **Headless sim** — balance is verified by a seeded combat simulation, without a browser.

---

## Earlier work — a compact table or row list, three lines total

| Project | Stack |
|---|---|
| Vue Weather App | Vue.js · OpenWeather API — https://github.com/sidyellur/Vue-Weather-App |
| Red-Black Tree / Min-Heap city builder | Java · academic — https://github.com/sidyellur/RBT-Min-Heap- |
| TicTacToe | React — https://github.com/sidyellur/TicTacToe |

---

## Suggested page skeleton (adapt to your direction)

```
NAV            sticky · name + section links + GitHub
HERO           name · one-line positioning · secondary line · 2 CTAs
               (+ optional stat strip)  — all above the fold
WORK           3 project entries. Each one:
                 tagline + one line
                 spec chips  ·  install command  ·  repo link
                 feature GRID (2–3 columns of label + one sentence)
                 one proof element (the stat, the JSON, the state table)
EARLIER        compact 3-row table
ABOUT          3 sentences + education spec row
FOOTER         multi-column · links · colophon
```

Consider tabs across the three projects instead of stacking them, or
`<details>` for the deeper feature rows. Compact by default.

---

## Hard technical constraints (unchanged — all still apply)

1. **One file**: `index.html`, all CSS in `<style>`, all JS in `<script>`. No build step, no framework.
2. **ZERO external requests.** No web fonts, CDNs, remote images, analytics, `fetch`. Must render identically offline.
3. **No image files.** CSS, inline SVG or canvas only.
4. **System font stacks only.**
5. **No jQuery/Bootstrap/AOS.** Vanilla JS, only where it earns its place.
6. **Responsive.** Works at 375px and 1600px. Body never scrolls horizontally.
7. **Accessible.** Semantic landmarks, one `<h1>`, logical heading order, visible focus states, real link text, good contrast. All animation off under `@media (prefers-reduced-motion: reduce)`.
8. `<title>` is `Siddharth Yellur`; include `<meta name="description">` and viewport.
9. Interactive/unconventional designs: all content reachable by keyboard, with an obvious escape hatch to a plain readable view.
10. Roughly 25–60KB.
