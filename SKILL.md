---
name: praop
description: Session-start/session-end operating discipline for AI-assisted project work — read project state, summarize briefly, capture incidents only when something real happens, write back only the files that actually changed, and pass every saved lesson through the EDTCU plain-language test first.
---

# PRAOP Project Skill

A lightweight session-start / session-end discipline for AI-assisted
project work, developed and validated through repeated real use on a
production project before being written down. Part of
[Open PRAOP](https://github.com/vincentwang2014/open-praop) — reuses its
vocabulary (Observed / Emerging / Operational / Canonical confidence,
Active / Contested / Deprecated status, E0–E3 evidence levels, the
EDTCU / Renhua plain-language test) instead of inventing a parallel one.

## What this does

Four files carry a project's state across sessions:

- `PROJECT_REPORT.md` — what is this project, right now?
- `DEVELOPMENT_MEMORY.md` — what must not be forgotten?
- `LESSONS_LEARNED.md` — what have we already learned the hard way?
- `TOMORROW.md` — where does the next session start?

This file tells an agent how to read them, when to update them, and how
to avoid the discipline itself becoming ceremony.

## Session Start

1. Read all four files.
2. In 5–10 lines, restate: current objective, known constraints, open
   risks, first action for this session.
3. Do not reopen a question already marked closed in `TOMORROW.md` or
   `LESSONS_LEARNED.md` unless new evidence has appeared since it was
   closed. If you think you have new evidence, say so explicitly before
   reopening it — don't just quietly relitigate it.

## During the Session

Most sessions produce no PRAOP-relevant event. That is the normal case —
do not manufacture one because the skill exists.

Flag a possible incident only when one of these actually happens:

- the same error recurs after it was supposedly fixed;
- an assumption recorded in `DEVELOPMENT_MEMORY.md` turns out to be
  wrong;
- something was marked "done" without verification, and verification
  now fails (or was never actually run);
- a fix addressed the literal symptom but not the underlying fact it
  came from (this resembles Open PRAOP's Lesson-Generalization Failure
  pattern — mention that as a passing resemblance, never as a settled
  classification);
- work has visibly expanded past what was asked — more files, more
  tooling, more checks — without anyone deciding that expansion was
  actually necessary (resembles Open PRAOP's Control Accretion pattern,
  same caveat as above);
- a human had to interrupt or override a trajectory the agent was on;
- a new standing instruction had to be given because an existing one
  didn't generalize to a new situation.

When you flag one:

- **Capture first, classify later.** Write down what was actually
  observed, in plain language, before reaching for a pattern name.
- **Don't self-classify.** "This looks similar to Control Accretion" is
  a fine hypothesis to note. "This is Control Accretion" is not a
  conclusion an agent gets to reach about its own behavior unreviewed —
  that's a human call.
- **Don't expand scope because it feels important.** A flagged incident
  becomes one entry in `LESSONS_LEARNED.md` at session end — not a new
  file, not a new process, not a new checklist. If it's substantial
  enough to need the fuller Open PRAOP Case Submission Template (What
  were you trying to do / What actually happened / Why did it matter /
  etc.), draft that inline under the `LESSONS_LEARNED.md` entry, not as
  a new file.

## Session End

**Update only the files whose state actually changed.** Do not touch all
four just because they exist — if today's session only produced a lesson
and a new starting point for tomorrow, update `LESSONS_LEARNED.md` and
`TOMORROW.md` and leave the other two alone.

For each file that does change:

- **`PROJECT_REPORT.md`** — update only if the objective, architecture,
  current state, constraints, or verified facts actually changed.
- **`DEVELOPMENT_MEMORY.md`** — update only if a new decision,
  assumption, environment fact, or convention was established, or an
  existing one was invalidated.
- **`LESSONS_LEARNED.md`** — add an entry only for something actually
  flagged during the session (see above). Every entry must separate
  **Observed** (what happened) from **Interpretation** (what you think
  it means) — see Open PRAOP §3, "Assert Incidents, Hedge Abstractions."
  Every entry also carries:
  - an **Evidence level**, E0–E3, exactly as defined in Open PRAOP §8.
    Almost everything an agent captures mid-session is E0 (self-
    reported, no attached artifact) — say so honestly rather than
    inventing a separate "agent-generated / unreviewed" label. E0
    already means this.
  - a **Confidence / Status** pair, exactly as defined in Open PRAOP §9.
    Starts at `Observed / Active`. Do not self-promote to `Emerging` or
    higher — that requires a second independent incident and a human
    decision, not the agent's own judgment.
  - Before writing the entry, run it through the **EDTCU Test**: can
    this be explained in plain language to the human who owns the
    outcome? If not, rewrite it until it can — don't save the jargon
    version and move on. A rushed end-of-session summary is exactly
    where this slips.
- **`TOMORROW.md`** — the file most likely to go stale fastest; update
  it whenever the next session's actual starting point changed, which is
  most sessions. Keep it short: next objective, first action, blockers,
  anything explicitly not to reopen, open questions.

## What this skill does not do

- It does not maintain a running incident log, case queue, or metrics
  file. If nothing was flagged, `LESSONS_LEARNED.md` gets no new entry,
  and that's the correct outcome, not a gap.
- It does not promote anything to Open PRAOP's public Case Canon
  automatically. A `LESSONS_LEARNED.md` entry stays project-local until
  a human decides it's worth submitting to
  [Open PRAOP](https://github.com/vincentwang2014/open-praop) as a real
  Case, following that repo's own submission and de-identification
  process.
- It does not require a fifth file. See "During the Session" above —
  a substantial incident gets drafted inline in `LESSONS_LEARNED.md`,
  not given its own file.

## Installing

Copy this skill's directory into the target project as
`.claude/skills/praop/` (or your tool's equivalent skill directory).
Copy the four template files into the project (root, or wherever project
docs live) and fill in `PROJECT_REPORT.md` and `DEVELOPMENT_MEMORY.md`
with what's true today — don't backfill history that doesn't matter
going forward.

## Status

**Observed / Active.** Validated through repeated use on one project.
Not yet tried on a second — treat this as a working v1 to pilot, not a
settled practice. See the provenance note in this repo's `README.md`.
