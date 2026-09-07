---
name: praop
description: PRAOP-aware project operating discipline for AI-assisted work — a short operating kernel (treat AI output as probabilistic, prefer artifact over memory, separate observation from interpretation, verify before declaring done, don't let controls compound unchecked) plus a four-file memory/handoff discipline across sessions, with every saved lesson passed through the EDTCU plain-language test.
---

# PRAOP Project Skill

A PRAOP-aware operating discipline for AI-assisted project work, developed
and validated through repeated real use on a production project before
being written down. Part of
[Open PRAOP](https://github.com/vincentwang2014/open-praop) — reuses its
vocabulary (Observed / Emerging / Operational / Canonical confidence,
Active / Contested / Deprecated status, E0–E3 evidence levels, the
EDTCU / Renhua plain-language test) instead of inventing a parallel one.

This skill has two layers, and they are not the same thing:

- **Layer 1 — PRAOP Operating Kernel.** How to think and act *during* the
  work itself: treating your own conclusions as probabilistic, preferring
  artifacts over memory, separating observation from interpretation,
  verifying before declaring done, and not letting either the project's
  controls or this skill's own PRAOP-awareness compound into ceremony.
- **Layer 2 — Project Memory / Handoff.** Four files that carry project
  state across session boundaries.

Layer 2 (the four files) is not the whole skill. A skill that only
maintains handoff files is recording discipline, not PRAOP awareness —
this file is meant to be both.

## Layer 1 — PRAOP Operating Kernel

Apply this throughout a session, not only when reading or writing the
Layer 2 files. It's deliberately short — a kernel, not the whole Open
PRAOP knowledge base (see "Where this kernel ends" below).

1. **Treat AI output as probabilistic, not authoritative.** A conclusion
   you just reached — including this session's own — can be wrong.
   Fluency is not correctness. Don't treat your own smoothly-stated
   inference as settled fact just because it reads well.
2. **Artifact > Memory.** When a live, checkable artifact exists — actual
   code, an actual test result, an actual running page, an actual
   config — prefer it over what a memory file says, including the
   project's own memory/report files. If the artifact disagrees with the
   memory file, the artifact wins, and the memory file is stale until
   corrected.
3. **Separate observation from interpretation as you go** — not only
   when writing a lesson. "The test failed after change X" is an
   observation. "X caused the failure" is an interpretation. Keep them
   visibly distinct in your own reasoning and in what you tell the user,
   not just in a lesson entry written after the fact.
4. **Reopen an assumption when reality disagrees with it, instead of
   patching around it.** If a fix fails, and the next fix — built on the
   same original theory — also fails, don't reach by default for a
   third, more elaborate patch on the same theory. Ask explicitly: *is
   the original assumption still justified?* This is the same failure
   shape as Open PRAOP's Locked Inference Trajectory pattern candidate —
   a wrong premise pursued through increasingly elaborate patches
   instead of being re-examined.
5. **Verification is part of completion, not separate from it.** "Code
   is written" is not "done." "Tests pass" is not "the user sees the
   right result." Ask: *what real-world artifact actually proves this is
   finished* — and check it, rather than declaring completion from code
   inspection alone.
6. **Knowledge is not enforcement.** Knowing a lesson doesn't mean the
   next action obeys it. If the same mistake recurs after it was already
   written down once, don't just add another lesson entry restating it —
   ask *does this need an actual practice or enforcement mechanism, not
   just another reminder?* Asking is not the same as building one
   immediately — see the next rule.
7. **Controls can become failures too.** Finding a risk doesn't default
   to adding another check, file, validator, or gate. Ask: *does this
   new control solve enough real risk to justify its ongoing cost?* This
   is Open PRAOP's Control Accretion pattern, and it applies to this
   skill's own behavior, not just to the project being worked on — don't
   let PRAOP-awareness itself accrete into ceremony.
8. **Capture first, classify later.** When something surprising happens,
   preserve what actually happened before reaching for a pattern name.
   (Stated again below for the Lessons Learned file specifically — it
   applies to how you think about any surprising event, not only to what
   eventually gets written down.)
9. **No Fit is valid.** Installing this skill is not a license to find
   Control Accretion, Lesson-Generalization Failure, or a Locked
   Inference Trajectory in every bug. Most bugs are just bugs. Forcing
   events into PRAOP's vocabulary because the vocabulary is available is
   itself a failure mode worth watching for. The mirror applies too: if
   a case doesn't fit any existing category, record the mismatch first —
   don't invent a new category to hold it until repeated incidents
   actually justify one (Open PRAOP §3, "No New Axis Without
   Incidents").
10. **Renhua / EDTCU applies beyond saved lessons.** Any plan, risk,
    decision, or handoff note that can't be explained in plain language
    to the person who owns the outcome hasn't actually been understood
    yet — abstraction can create a false sense of "I've got this" that
    fluent wording papers over. Apply the same plain-language check
    there, not only to what gets saved as a lesson. Passing this check
    means the person can later recognize and apply the idea in a new
    situation *without* being prompted — nodding along when it was first
    explained doesn't count.

**Where this kernel ends:** this skill carries enough of Open PRAOP to
behave PRAOP-aware during real work. It does not carry Open PRAOP's case
corpus, full pattern definitions, evidence protocol, or promotion
rules — those stay canonical in
[Open PRAOP](https://github.com/vincentwang2014/open-praop), referenced
here, never duplicated. If this kernel and Open PRAOP's protocol ever
seem to disagree, Open PRAOP is the source of truth; fix this file to
match it, not the other way around.

## Layer 2 — Project Memory / Handoff

Four files carry a project's state across sessions:

- `PROJECT_REPORT.md` — what is this project, right now?
- `DEVELOPMENT_MEMORY.md` — what must not be forgotten?
- `LESSONS_LEARNED.md` — what have we already learned the hard way?
- `TOMORROW.md` — where does the next session start?

The rest of this file tells an agent how to read them, when to update
them, and how to avoid the discipline itself becoming ceremony.

## Session Start

1. Read all four files.
2. In 5–10 lines, restate: current objective, known constraints, open
   risks, first action for this session.
3. Do not reopen a question already marked closed in `TOMORROW.md` or
   `LESSONS_LEARNED.md` unless new evidence has appeared since it was
   closed (Kernel rule 4). If you think you have new evidence, say so
   explicitly before reopening it — don't just quietly relitigate it.

Carry Layer 1's kernel through the rest of the session — it doesn't
switch off once the session-start summary is written.

## During the Session

Most sessions produce no PRAOP-relevant event worth saving. That is the
normal case — do not manufacture one because the skill exists (Kernel
rule 9).

Flag a possible incident only when one of these actually happens:

- the same error recurs after it was supposedly fixed;
- an assumption recorded in `DEVELOPMENT_MEMORY.md` turns out to be
  wrong;
- something was marked "done" without verification, and verification
  now fails (or was never actually run) (Kernel rule 5);
- a fix addressed the literal symptom but not the underlying fact it
  came from (resembles Open PRAOP's Lesson-Generalization Failure
  pattern — mention that as a passing resemblance, never as a settled
  classification);
- work has visibly expanded past what was asked — more files, more
  tooling, more checks — without anyone deciding that expansion was
  actually necessary (Kernel rule 7, Control Accretion, same caveat as
  above);
- a human had to interrupt or override a trajectory the agent was on;
- a new standing instruction had to be given because an existing one
  didn't generalize to a new situation.

This list applies to the agent's own behavior during the session's
PRAOP work itself, not only to the external project being worked on —
a confident claim the agent makes about itself or its own situation
that turns out false when checked is the same class of incident as the
bullets above, not a separate, exempt category.

When you flag one:

- **Capture first, classify later** (Kernel rule 8). Write down what was
  actually observed, in plain language, before reaching for a pattern
  name.
- **Don't self-classify.** "This looks similar to Control Accretion" is
  a fine hypothesis to note. "This is Control Accretion" is not a
  conclusion an agent gets to reach about its own behavior unreviewed —
  that's a human call.
- **Don't expand scope because it feels important.** A flagged incident
  becomes one entry in `LESSONS_LEARNED.md` at session end — not a new
  process, not a new checklist. If it looks substantial enough to
  warrant the fuller Open PRAOP Case treatment, that's what
  `praop-case-draft` is for (see "Potential PRAOP Case Recording"
  below) — mention it, don't draft it yourself here.

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
  it means) — see Open PRAOP §3, "Assert Incidents, Hedge Abstractions,"
  and Kernel rule 3. Every entry also carries:
  - an **Evidence level**, E0–E3, exactly as defined in Open PRAOP §8.
    Almost everything an agent captures mid-session is E0 (self-
    reported, no attached artifact) — say so honestly rather than
    inventing a separate "agent-generated / unreviewed" label. E0
    already means this. Don't convert a detailed, well-written narrative
    into E1 just because it reads as credible — E1 requires an actual
    attached artifact (log, commit, screenshot, output), not narrative
    quality.
  - a **Confidence / Status** pair, exactly as defined in Open PRAOP §9.
    Starts at `Observed / Active`. Do not self-promote to `Emerging` or
    higher — that requires a second independent incident and a human
    decision, not the agent's own judgment.
  - Before writing the entry, run it through the **EDTCU Test**: can
    this be explained in plain language to the human who owns the
    outcome? If not, rewrite it until it can — don't save the jargon
    version and move on (Kernel rule 10). A rushed end-of-session
    summary is exactly where this slips.
- **`TOMORROW.md`** — the file most likely to go stale fastest; update
  it whenever the next session's actual starting point changed, which is
  most sessions. Keep it short: next objective, first action, blockers,
  anything explicitly not to reopen, open questions.

## Potential PRAOP Case Recording

At session end, check whether anything this session matches one of
these. **Don't force it** for an ordinary bug, a typo, or a one-off
failure — most sessions won't have one:

- inference stated as fact;
- inconsistent conclusions across the session;
- claimed "done" when it wasn't;
- repeated ineffective actions, or an inability to stop;
- lost key context;
- tool behavior inconsistent with the final narrative;
- the human had to repeatedly correct the agent;
- a fix introduced a new problem;
- the page/system claims a capability the actual interaction doesn't
  support;
- the event exposes an operational pattern that might transfer to other
  agent projects.

This check applies to the agent's own real-time behavior during the
session, not only to the project it's working on. An agent asserting
something about its own limits or situation as settled fact, then
being shown it was wrong, is exactly "inference stated as fact" and
"the human had to repeatedly correct the agent" above — don't exempt
your own conduct from this checklist just because you're the one
running it.

**If one matches:** mention that a Potential PRAOP Case may be worth
drafting, and add one short pointer to `DEVELOPMENT_MEMORY.md` — what
was observed, where the source material lives — not a full case
write-up. **Do not draft, structure, evidence-tag, or submit a case
yourself.** That's the job of a separate, optional, explicitly-invoked
companion skill, **`praop-case-draft`** — it owns the full chain
(factual timeline, Plain-Language Version, Observed / Interpretation /
Hypothesis, anti-mapping, evidence status, de-identification, human
review) and only runs when a human asks for it by name. This skill's
job stops at noticing and mentioning. Never mark anything Accepted,
Operational, or Canonical yourself — that stays a human decision,
later, through Open PRAOP's own process.

**If nothing matches:** say so explicitly — "No potential PRAOP case
identified in this session." That's still useful pilot evidence, not a
gap.

Either way, add a short dated entry to `DEVELOPMENT_MEMORY.md`:

```
## YYYY-MM-DD — PRAOP Pilot Observation
Agent: / Task: / Files changed:
### Verified / Observed / Inferred
### Potential PRAOP case: None | Mentioned — candidate for `praop-case-draft`
### Tooling signal: No tooling need demonstrated | Repeated manual friction observed; candidate for future tooling review
### Unresolved
### Next recommended check
```

Never submit anything to Open PRAOP, open a public PR, or draft a full
case from this step alone — drafting and de-identification are
`praop-case-draft`'s job (see that skill for its own submission gate),
and either way require an explicit human decision.

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
- It does not require a fifth file for ordinary lessons — see "During
  the Session" above. A case substantial enough for full drafting goes
  through `praop-case-draft`, which does use its own file — that's a
  deliberate choice in that skill, not something this skill does
  itself.
- It does not carry Open PRAOP's full doctrine. See "Where this kernel
  ends" above.

## Installing

In this repo, this skill lives at `skills/praop/` and the four template
files live at `templates/`. Copy `skills/praop/` into the target
project as `.claude/skills/praop/` (or your tool's equivalent — e.g.
`AGENTS.md` for Codex-style agents; inline the kernel and file
discipline there if a dedicated skill directory doesn't exist). Copy
`templates/*` into the project (root, or wherever project docs live)
and fill in `PROJECT_REPORT.md` and `DEVELOPMENT_MEMORY.md` with what's
true today — don't backfill history that doesn't matter going forward.
If the project already has equivalent files under different names, map
roles to them instead of renaming anything — the four *roles* are what
matter, not the filenames.

Optionally, also copy `skills/praop-case-draft/` as
`.claude/skills/praop-case-draft/` — a separate, optional companion for
turning a noticed Potential PRAOP Case into a structured, reviewable
draft. This skill only notices and mentions one; drafting is that
skill's job, and only runs when explicitly invoked. See
`skills/praop-case-draft/SKILL.md`.

## Status

**Observed / Active.** Validated through repeated use on one project.
Pilot 001 (a second, independent project/agent) is in progress — treat
this as a working v1 to pilot, not a settled practice. See the
provenance note in this repo's `README.md`.
