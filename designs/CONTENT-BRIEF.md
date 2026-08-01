# Content brief — Siddharth Yellur personal site redesign

This is the SINGLE SOURCE OF TRUTH for all copy and facts. Do NOT invent
biography, employers, dates, metrics, or project details beyond what is here.
Every one of the 8 candidate designs uses these same facts, so the reviewer is
comparing design, not content. You may rewrite the *phrasing* to fit your
design's voice; you may not add facts.

---

## Person

- Name: **Siddharth Yellur**
- GitHub: https://github.com/sidyellur
- LinkedIn: https://www.linkedin.com/in/siddharth-yellur-682351142/
- Education (safe to mention, optional): M.S. Computer Science, University of
  Florida. B.E. Computer Science, Anna University.

### Bio framing — IMPORTANT

The old site said "CS grad student actively looking for full-time opportunities
starting 2021." That is stale and must NOT appear. Write the bio **role-agnostic**
— no employer, no job-hunt language, no "currently working at X", no dates that
will rot. Frame him as an engineer who builds developer tooling for AI agents and,
lately, a video game. Let the work carry the page.

Do NOT include: phone number, .edu email address, "days in quarantine" counters,
skill percentage bars, a resume PDF link, or stock photography.

Contact = GitHub and LinkedIn only.

---

## Projects — the three headliners

Give these real depth. They are the point of the redesign. The technical detail
below is accurate and is what makes them interesting — use it, don't flatten it
into "built a tool using Python."

### 1. tether — a shared memory layer for personal agents

- Link: https://github.com/sidyellur/tether
- Also: on PyPI as `tether-memory`. Install: `claude mcp add tether -- uvx tether-memory`
- Status: v0.5.1
- Tech: Python, MCP (Model Context Protocol), SQLite / FTS5, libSQL/Turso, local
  static embeddings
- What it is: An MCP server backed by a local SQLite file. Any MCP-compatible
  agent can `remember`, `recall`, `link`, and `forget` durable notes — facts about
  you, your projects, your preferences — so context follows you between sessions
  instead of dying with each one.
- Why it's interesting:
  - Runs local-only with zero configuration; point it at a hosted libSQL/Turso
    primary and the same file becomes an embedded replica that syncs memory
    across every device in near-real-time.
  - `recall` is hybrid: keyword (FTS5) results fused with semantic vector
    results, so "automobile" finds a note about your "car". The embedding model
    is small and static and runs locally — no network, no API key.
  - It follows an **associative usage graph** to related memories. Edges come
    from three local deterministic sources: semantic nearest-neighbours,
    explicit `link()` calls, and *hebbian* edges — memories recalled together
    get wired together over time. Every hit carries a `via` receipt explaining
    why it surfaced.
  - Recall is **seed-dominant**: top direct matches are locked in place and
    associations only fill slots below them, so turning association on never
    demotes a good hit.
  - The store self-organizes: a hub-curated boot index surfaces "load-bearing"
    memories (highest behavioral degree) alongside recent ones, and an opt-in
    sweep soft-archives memories that are both old and behaviorally isolated.
    Nothing is ever hard-deleted.
  - Optional crystallization: it detects dense clusters of related memories and
    offers them up to be *named* as principles. tether finds the structure; the
    agent supplies the words.
  - Every feature degrades cleanly to plain keyword recall. It is deliberately a
    convenience layer — more useful when present, never breaks the agent when
    degraded.
- One good hard number: returning query-centered excerpts instead of full
  bodies cut a recall response from 66.9KB to 2.0KB.

### 2. cleat — a headless terminal layer for AI agents

- Link: https://github.com/sidyellur/cleat
- Also: on PyPI as `cleat`. Install: `claude mcp add cleat -- uvx cleat`
- Tech: Python, MCP, PTY / termios, OSC 133, pyte
- What it is: Runs a *persistent* shell session behind a PTY, parses its byte
  stream for OSC 133 shell-integration marks, and exposes it to an agent over
  MCP as structured results — `stdout`, real `exit_code`, files touched —
  instead of raw escape-code soup.
- Why it's interesting:
  - The core insight: when you scrape a PTY, **the exit code isn't in the stream
    at all**. The shell knows `$?` but never prints it. cleat injects OSC 133
    marks into the shells it spawns and parses them back out.
  - The session is persistent, so `cd`, `export`, activated venvs, and `ssh`
    sessions all carry across calls — something a fresh subprocess per command
    cannot do.
  - Every response carries a `state` derived from termios flags and the
    foreground process group — facts only the process holding the PTY can read,
    not guessed from output timing. States: `idle`, `running`, `awaiting-input`,
    `password`, `tui`.
  - It refuses to type into a `password` prompt without explicit human consent.
  - **Nonce-authenticated marks**: a command can print a fake OSC 133 sequence to
    its own stdout to forge a clean exit code. Each session gets a fresh
    `secrets.token_hex(8)` nonce embedded in every mark cleat injects; a mark
    with a missing or wrong `k=` is ignored outright and surfaced as
    `spoofed_marks`, so the agent can tell when a program lied about how it
    finished.
  - Terminal-agnostic — not a terminal emulator, not a modification to yours.
- Example structured result: `{ "stdout": "...", "exit_code": 0, "completed": true, "state": "idle" }`

### 3. Black Diamond Brawl — a downhill snowboarding combat racer

- Link: https://github.com/sidyellur/black-diamond-brawl
- Tech: Phaser 3, TypeScript, Vite, segment-based pseudo-3D renderer
- Status: v1 complete (9 phases); v2 visual overhaul complete
- What it is: A Road Rash-style downhill snowboarding combat racer, built solo as
  a learning project. Each run is a single race down a fixed-length, seeded,
  procedurally generated slope ending at a finish line.
- Why it's interesting:
  - Dodge trees, rocks and moguls; catch trick air off moguls and hill crests
    (crests launch you automatically at speed); shove or ski-pole your way past
    AI rivals racing the same course.
  - Score comes from finishing fast, landing hits on rivals, near-misses, and
    tricks. Wipe out hard before the line and the run ends early.
  - Classic **segment-based pseudo-3D renderer** for the behind-the-rider "road
    rushing at you" look — OutRun / Road Rash style — with pixel art sprites.
  - **All art and atmosphere is generated in code at boot. There are no image
    files in the repository at all.** Colour is governed by a palette module and
    enforced by a build gate that fails if any gameplay-relevant edge drops below
    ΔL* 12, or any sprite outline below ΔL* 25 against the snow behind it.
  - Ships with a headless seeded combat simulation and a solvability model, so
    balance is verified without a browser.

---

## Earlier work (small, secondary — a compact list, not cards)

Keep this understated. A short line or a few small links at most.

- Vue Weather App — Vue.js + OpenWeather API —
  https://github.com/sidyellur/Vue-Weather-App
- Red-Black Tree / Min-Heap city builder — Java, academic —
  https://github.com/sidyellur/RBT-Min-Heap-
- TicTacToe — React — https://github.com/sidyellur/TicTacToe

Do NOT feature the old personal-portfolio-website project. Do NOT mention a
project called `cue` (that repository is private).

---

## Hard technical constraints — apply to EVERY design

1. **One single file**: `index.html`. All CSS in a `<style>` block, all JS in a
   `<script>` block. No build step, no bundler, no framework, no npm.
2. **ZERO external requests.** No Google Fonts, no CDN scripts, no external
   stylesheets, no remote images, no analytics, no `fetch`. The page must render
   identically with the network switched off. This is non-negotiable — it is how
   the reviewer will preview it.
3. **No image files.** No `<img>` pointing at anything on disk. Any visual
   richness must be CSS, inline SVG, or canvas drawn in code. (Fitting, given
   Black Diamond Brawl generates all its own art.)
4. **System font stacks only.** e.g.
   `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`,
   `ui-monospace, SFMono-Regular, Menlo, Consolas, monospace`, or
   `Georgia, "Times New Roman", serif`. Use them well — weight, size, spacing and
   measure do the work.
5. **No jQuery, Bootstrap, Owl Carousel, AOS, Stellar.** Vanilla JS only, and only
   where it earns its place.
6. **Responsive.** Must work at 375px wide and at 1600px. The body must never
   scroll horizontally. Test both mentally before you finish.
7. **Accessible.** Semantic landmarks (`<header> <main> <nav> <footer>`), a
   logical heading order starting at a single `<h1>`, visible keyboard focus
   states, real link text, sufficient contrast. Every animation must be disabled
   or heavily reduced under `@media (prefers-reduced-motion: reduce)`.
8. `<title>` is `Siddharth Yellur`. Include a `<meta name="description">` and a
   `<meta name="viewport">`.
9. If your design is interactive or unconventional, **all content must still be
   reachable** — via keyboard, and without requiring the visitor to solve
   anything. Provide an obvious escape hatch to a plain readable view.
10. Aim for roughly 25–60KB. Rich is fine; bloated is not.
