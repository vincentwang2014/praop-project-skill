# PRAOP Project Skill

> This repo implements practices developed in
> [Open PRAOP](https://github.com/vincentwang2014/open-praop). For
> cases, patterns, evidence rules, and the methodology itself, go there
> — this repo doesn't restate any of it, only references it.

A small family of skills sharing one four-file operating discipline:
**`praop`**, the mandatory operating kernel, and **`praop-case-draft`**,
a separate, optional, explicitly-invoked companion for turning a
noticed Potential PRAOP Case into a structured, human-reviewable draft.

```text
praop-project-skill/
├── skills/
│   ├── praop/
│   │   └── SKILL.md              Layer 1 (PRAOP Operating Kernel) + Layer 2 (how to use the four template files)
│   └── praop-case-draft/
│       └── SKILL.md              optional companion: drafts a noticed case, only when explicitly invoked
└── templates/
    ├── PROJECT_REPORT.md         what is this project, right now?
    ├── DEVELOPMENT_MEMORY.md     what must not be forgotten?
    ├── LESSONS_LEARNED.md        what have we already learned the hard way?
    └── TOMORROW.md               where does the next session start?
```

## Migration note (2026-09-05)

This repo used to be flat — `SKILL.md` and the four template files sat
directly at repo root. It's now `skills/*` (one directory per skill)
and `templates/*`, so a second skill (`praop-case-draft`) has a clean
home instead of competing with the first for the root-level `SKILL.md`
filename. **`skills/praop/SKILL.md`** and **`skills/praop-case-draft/
SKILL.md`** are each the sole canonical source for their skill — no
root-level duplicate is kept. If you cloned or copied from the old flat
layout, re-copy from `skills/` and `templates/` now.

## Installing

- `skills/praop/` → your project's `.claude/skills/praop/` (mandatory
  kernel).
- `skills/praop-case-draft/` → your project's
  `.claude/skills/praop-case-draft/` (optional; only needed if you want
  the case-drafting workflow).
- `templates/*` → your project's root, or wherever project docs live.

See each skill's own `SKILL.md` for what to fill in and how the two
skills hand off to each other.

`skills/praop/SKILL.md` has two layers, and they're not the same thing:

- **Layer 1 — PRAOP Operating Kernel.** A short (10-rule) set of how to
  *think and act* during real work — treat your own conclusions as
  probabilistic, prefer artifacts over memory, separate observation from
  interpretation, verify before declaring done, reopen assumptions
  reality disagrees with, and don't let controls (including this skill's
  own PRAOP-awareness) compound into ceremony.
- **Layer 2 — Project Memory / Handoff.** The four template files, and
  when to read/write them.

A skill that only maintains four handoff files is recording discipline,
not PRAOP awareness. Read `skills/praop/SKILL.md` first — both layers
are there.

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

- No fifth "incidents" file for ordinary lessons. Capture a real
  incident inline in `LESSONS_LEARNED.md` when one actually happens —
  don't scaffold an empty file waiting for one. See
  `skills/praop/SKILL.md`. (A case substantial enough for full
  drafting goes through `praop-case-draft` instead, which does use its
  own file — a deliberate choice in that skill, not this one.)
- No separate vocabulary for "how sure are we about this." Reuses
  [Open PRAOP](https://github.com/vincentwang2014/open-praop)'s
  evidence levels (E0–E3) and Confidence/Status pairs directly.
- No bootstrap script, no CLI — just the copy-in steps under
  "Installing" above. If this proves itself further, that tooling is
  the natural next step — not before, and it'll live in this same repo
  (a `scripts/` directory, its own `LICENSE-CODE`) rather than a
  separate one.

## Status

**`praop`: Observed / Active**, in Open PRAOP's own terms: validated
through repeated real use on one project. Pilot 001 (a second,
independent project and agent) is in progress. Treat this as a working
v1 to pilot, not a settled practice — if you try it and it breaks down
somewhere, that's exactly the kind of finding that should feed back
into both this skill and Open PRAOP itself.

**`praop-case-draft`: Observed / Active**, validated across three real
drafts before publication (one revised and retained as a Potential
PRAOP Case, two rejected as case material but each still producing a
real project-local lesson). See its own `SKILL.md` for the full
revision history.

## Revisions

**2026-09-04 — added Layer 1, the PRAOP Operating Kernel.** The original
v1 was almost entirely Layer 2 (four-file handoff discipline), with
PRAOP vocabulary showing up mainly as classification hints for
`LESSONS_LEARNED.md` entries. That's recording discipline, not PRAOP
awareness — an agent could maintain the four files perfectly while never
actually behaving any differently during the work itself. Added a short,
10-rule kernel governing behavior throughout a session (assumption
handling, artifact-over-memory, verification-as-completion, control
accretion awareness, no-fit-is-valid), explicitly scoped to stay a
kernel — it does not carry Open PRAOP's case corpus, pattern
definitions, evidence protocol, or promotion rules, which remain
canonical in Open PRAOP only. No new files, no new vocabulary; every
kernel rule either names an existing Open PRAOP principle directly
(Artifact > Memory, Knowledge Is Not Enforcement, No Fit Is Valid) or is
stated as this skill's own operating behavior without inventing a new
named doctrine.

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

**Dual-licensed by file type, in one repo — not split across repos.**
Everything currently here (both skills under `skills/`, the templates,
this README) is content, licensed CC BY-SA 4.0 — see
`LICENSE-CONTENT`, matching Open
PRAOP's own content license exactly. Copying these files unmodified into
your own project (private or commercial) carries no obligation beyond
keeping the license notice; publicly distributing a *modified* version
of the files themselves requires keeping that modification under CC
BY-SA 4.0 too.

If this repo later grows actual executable code (a CLI, a session-end
updater, a format/de-identification checker), that code will live in its
own directory (e.g. `scripts/`) under a separate `LICENSE-CODE` — default
plan is Apache 2.0, decided when the code actually exists rather than
speculatively now. No need to fork this into a second repo for that; one
repo, two licenses, scoped by directory.

The "PRAOP" / "Open PRAOP" name and logo are not covered by either
license, matching the same carve-out in Open PRAOP's own `LICENSE`.
