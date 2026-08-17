# Personal Cockpit

A shareable skill that builds a **cockpit**: one glance-able weekly dashboard, as a single HTML file you open in a
browser and tap to check things off. The week strip highlights today; checkboxes reset each Monday.

It's the render step of a small **file-coordinated agent system**. Agents never call each other; they leave dated files
for each other to read. This skill reads what an email agent and a day-planner leave behind and writes the page you open.

## Fastest way to use it (by hand, no setup)

1. Install the skill (open the `.skill` file and Save it, if your org allows skills).
2. Say: **"Build my cockpit."**
3. Paste your week's calendar and any mail you want tracked, or let it read your connected calendar and email.

You get a finished HTML page. Refresh it any time by saying **"refresh my cockpit"** — open items roll to the new week,
finished ones drop off.

## To run it automatically every morning

You need an environment with scheduled tasks and shared file storage (e.g. Cowork or Claude Code, not plain chat). Then:

1. Create four folders: `briefings/`, `plans/`, `pages/`, `status/`.
2. Set up the companion agents as staggered morning sessions (see `references/companion-agents.md`).
3. Each writes only its own folder; this skill reads `plans/` and `briefings/` and writes `pages/`.

## What's in the box

- `SKILL.md` — the render agent (when it runs, what it reads, how it builds the page, safety limits).
- `assets/cockpit_template.html` — the generalized starting template.
- `references/architecture.md` — the four-agent system and its hard limits.
- `references/file-contract.md` — the shape of the shared dated files.
- `references/companion-agents.md` — specs for the email agent, day-planner, and chief-of-staff.

## Safety, in one line

It only ever writes the page. It never sends mail, books or moves events, edits a task tracker, or calls another agent.
Any companion agents are boxed too: drafts only, one calendar focus block, nothing sends.

## Make it yours

Rename, drop, or add sections freely; keep whatever your prior page used. Restyle the palette. The one thing to leave
intact is the `<script>` block in the template, which drives the live week strip and the weekly reset.
