# Personal Cockpit

A shareable Claude **skill** that builds a *cockpit*: one glance-able weekly dashboard, delivered as a single HTML file
you open in a browser and tap to check things off. The week strip highlights today; checkboxes reset each Monday.

It is the render step of a small **file-coordinated agent system**. The agents never call each other. Each runs on its
own schedule and leaves dated files for the others to read. This skill reads what an email agent and a day-planner leave
behind, and writes the page you open.

```
email-agent        day-planner        morning-brief        chief-of-staff
drafts, never       books one          renders the          reports,
sends               focus block        page                 never fixes
    |                   |                  |                    |
    v                   v                  v                    v
briefings/          plans/             pages/               status/
```

Solid = writes. Each agent writes only its own folder. Dashed reads: the render step reads `briefings/` and `plans/`.
The chief-of-staff is oversight with no authority over the others.

## Quick start (by hand, no setup)

1. Install the skill (see below).
2. Tell Claude: **"Build my cockpit."**
3. Paste your week's calendar and any mail worth tracking, or let Claude read your connected calendar and email.

You get a finished HTML page. Refresh any time with **"refresh my cockpit"**: open items roll to the new week, finished
ones drop off, slipped dates resurface.

## Install the skill

Skills work on Free, Pro, Max, Team, and Enterprise plans. They require **Code execution and file creation** to be on.

1. **Enable code execution.**
   - Free / Pro / Max: Settings > Capabilities > turn on *Code execution and file creation*.
   - Team / Enterprise: an organization owner enables *Code execution and file creation* and *Skills* in Organization
     settings > Skills. (If the Skills menu looks greyed out, this is usually why.)
2. **Upload the skill.** Go to Customize > Skills, click to add a skill, and upload `personal-cockpit.zip` from this repo.
   Claude reads the `SKILL.md` inside and switches it on.
3. **Use it.** In any chat, say "build my cockpit" or "refresh my cockpit." Claude loads the skill automatically when
   it is relevant.

To remove it later: Customize > Skills > the "..." next to it > Delete.

> Only install skills from sources you trust. Skills can include instructions and code. Everything in this one is plain
> text and self-contained HTML; read `skill/SKILL.md` and the references before installing if you want to check.

## Automate it (optional)

To run every morning unattended you need an environment with scheduled tasks and shared file storage, such as Cowork or
Claude Code, not plain chat. Then:

1. Create four folders: `briefings/`, `plans/`, `pages/`, `status/`.
2. Set up the companion agents as staggered morning sessions. Specs are in `skill/references/companion-agents.md`.
3. Each writes only its own folder. The render step reads `plans/` and `briefings/` and writes `pages/`.

The hard limits hold for every agent: outside writes are limited to email drafts and one calendar focus block. Nothing
sends. Nothing edits a task tracker. Nothing runs if the app is closed.

## What's in this repo

```
personal-cockpit.zip        the installable skill (upload this into Claude; leave it zipped)
guide/
  personal-cockpit-guide.pdf  a printable one-file overview
skill/                      the same skill, unpacked for reading on GitHub
  SKILL.md                  the render agent
  README.md                 quickstart
  assets/cockpit_template.html
  references/architecture.md
  references/file-contract.md
  references/companion-agents.md
samples/                    a worked example
  plans-2026-06-08.md          sample day-planner output
  briefings-2026-06-08.md      sample email-agent output
  cockpit-2026-06-08.html      the page rendered from those two
  cockpit-refresh-2026-06-15.html  the next week after a refresh
```

`personal-cockpit.zip` and the `skill/` folder hold the same files. The zip is the one to download and upload into
Claude; the folder is there so people can read the source on GitHub without downloading anything.

## Make it yours

Rename, drop, or add sections freely; keep whatever your prior page used. Restyle the palette. The one thing to leave
intact is the `<script>` block in the template, which drives the live week strip and the weekly reset.

## License

MIT, see [LICENSE](LICENSE). Use it, fork it, adapt it, share it. If you build something nice on top, a link back is
appreciated but not required.
