# PRAOP Project Skill

> This repo implements practices developed in
> [Open PRAOP](https://github.com/vincentwang2014/open-praop). For
> cases, patterns, evidence rules, and the methodology itself, go there
> — this repo doesn't restate any of it, only references it.

A minimal v1: four templates and one skill file, nothing else.

```text
praop-project-skill/
├── SKILL.md               how an agent should use the four files below
├── PROJECT_REPORT.md      what is this project, right now?
├── DEVELOPMENT_MEMORY.md  what must not be forgotten?
├── LESSONS_LEARNED.md     what have we already learned the hard way?
└── TOMORROW.md            where does the next session start?
```

Full operating discipline — when to read, when to write, when *not* to
write, and the EDTCU plain-language gate before anything gets saved to
`LESSONS_LEARNED.md` — is in `SKILL.md`. Read that first.

## Why this exists

Handoff between AI sessions is usually either nonexistent (each session
starts cold) or ceremonial (a wall of boilerplate nobody reads). This
grew out of one project where the opposite happened: four working files,
updated only when something actually changed, ended up producing better
continuity than either extreme — and the agent working the project
started noticing and flagging its own incidents without being told to
look for them.

This repo is that practice, written down as something else can try.

## What this deliberately isn't (yet)

- No fifth "incidents" file. Capture a real incident inline in
  `LESSONS_LEARNED.md` when one actually happens — don't scaffold an
  empty file waiting for one. See `SKILL.md`.
- No separate vocabulary for "how sure are we about this." Reuses
  [Open PRAOP](https://github.com/vincentwang2014/open-praop)'s
  evidence levels (E0–E3) and Confidence/Status pairs directly.
- No installation guide for specific tools, no bootstrap script, no CLI.
  Copy the files in, per the one paragraph in `SKILL.md`. If this proves
  itself on a second project, that tooling is the natural next step —
  not before.

## Status

**Observed / Active**, in Open PRAOP's own terms: validated through
repeated real use on one project. Not yet tried on a second. Treat this
as a working v1 to pilot, not a settled practice — if you try it and it
breaks down somewhere, that's exactly the kind of finding that should
feed back into both this skill and Open PRAOP itself.

## Relationship to Open PRAOP

[Open PRAOP](https://github.com/vincentwang2014/open-praop) is the case
corpus and methodology — cases, patterns, practices, playbooks, and the
protocol that governs how they're built and promoted. This repo is the
first application layer on top of it: a way to run that discipline
*during* a project instead of only reconstructing it after an incident.
A `LESSONS_LEARNED.md` entry here is project-local; if it turns out to
matter beyond one project, it's a candidate for submission to Open PRAOP
as a real Case.

## License

Mozilla Public License 2.0 — see `LICENSE`. File-level copyleft: copying
these files unmodified into your own project (private or public) carries
no obligation beyond keeping the license notice; modifying and then
distributing them requires releasing those modifications under MPL 2.0
too. This is a different license than Open PRAOP's CC BY-SA 4.0 (which
covers cases, patterns, practices, and playbooks) — deliberately, since
this repo is expected to grow actual tooling (a CLI, possibly) beyond
today's markdown-only v1, and MPL avoids a license transition when that
happens. The "PRAOP" / "Open PRAOP" name and logo are not covered by
this license, matching the same carve-out in Open PRAOP's own `LICENSE`.
