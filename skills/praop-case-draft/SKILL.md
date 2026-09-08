---
name: praop-case-draft
description: Turn a Potential PRAOP Case already noted somewhere (typically a DEVELOPMENT_MEMORY.md entry) — or an already-public external source such as a published incident report — into a structured, human-reviewable case draft — factual timeline, Observed/Interpretation/Hypothesis split, anti-mapping check, evidence status, de-identification pre-check (branched by whether the source is private or already public). Explicit-invocation only ("draft a PRAOP case from X", "run praop-case-draft on this"). Never triggers itself on an ordinary bug, incident, or session flag — praop-project-skill's kernel handles noticing; this skill only drafts, and only when asked.
---

# PRAOP Case Draft

A separate, optional companion to `praop-project-skill`. That skill's
kernel is responsible for *noticing* a possible case and saying so in
one line — it never drafts one. This skill is responsible for the
opposite half: turning a noticed candidate into an actual structured
draft, and only when a human explicitly asks for that.

**If you are here because a session just flagged a possible incident,
stop and check: did the human ask for a draft, or just get told one
might be worth writing?** Only the former is this skill's job. If
nothing explicit was asked, mention that `praop-case-draft` exists and
wait.

## What this skill is not

- Not a submission tool. It produces a **human review package**, never
  an Open PRAOP PR. Submission is a separate, later, explicit act by a
  human, using Open PRAOP's own process — this skill's output feeds
  that process, it doesn't perform it.
- Not a storage location. `DEVELOPMENT_MEMORY.md` (or whatever a
  project's equivalent memory file is called) may keep a short pointer
  noting a Potential Case exists and where the source event lives —
  that's `praop-project-skill`'s job. Once this skill drafts it, the
  full draft lives in its own file (`case-drafts/` in the invoking
  project, or that project's equivalent), and the memory file should be
  trimmed back down to a pointer. Don't let a memory file accumulate
  full drafts.
- Not automatic. Nothing in this skill runs unless a human names a
  specific candidate and asks for a draft.

## Input

A pointer to one candidate: a `## Potential PRAOP Case` entry in a
project's memory file, a raw incident description, or a session
transcript excerpt. If the human just says "draft the case from
[project]'s memory file" without naming which entry, and more than one
exists, ask which one — don't guess or draft all of them at once.

**A candidate is not always a private incident from this project's own
history.** It can also be an already-public, externally-authored
source — a published incident report, postmortem, paper, or similar —
cited by title, publisher, and date, or by a document the human hands
over directly. Verify such a source directly (read the actual document)
before drafting anything from it; don't draft from a human's summary of
an external source alone. State explicitly, near the top of the draft,
which kind of source this is — private or already-public — since that
choice determines which branch of step 6 applies.

## The chain

Run these steps in order. Each step's output is visible in the draft —
don't collapse them into a single paragraph, and don't skip a step
because it feels redundant with an earlier one.

### 1. Extract factual timeline

Pull only what is independently checkable: what happened, in what
order, established by what artifact (a diff, a log, a commit, a direct
quote from the session). No adjectives about severity or meaning yet.
If a claimed fact has no artifact behind it, mark it as *reported, not
verified* rather than silently upgrading it. An artifact means
something the reviewer can retrieve, inspect, or reconstruct right now
(a commit, a file's current or committed-past state, a saved log) —
not a memory of having produced one during the session. See step 4 for
how this bears on evidence level.

### 2. Observed / Interpretation / Hypothesis

Three tiers, kept visibly separate — do not let interpretation bleed
into the observed section, and do not let a hypothesis get written with
the confidence of an interpretation:

- **Observed** — what the timeline in step 1 actually shows. No
  inference.
- **Interpretation** — the most direct, low-inference reading of what
  Observed means. Still local to this one instance; explicitly hedged
  ("this looks like...", "in this instance...").
- **Hypothesis** — a further-out, explicitly falsifiable claim about a
  *possibly reusable* pattern beyond this one instance. State it so
  that it's clear what evidence would prove it wrong, not just what
  would confirm it. If you can't state what would falsify it, it isn't
  a hypothesis yet — it's a narrative, and should be cut back to
  Interpretation.

### 3. Anti-mapping

Before naming any resemblance to an Open PRAOP pattern (Control
Accretion, Lesson-Generalization Failure, Locked Inference Trajectory,
etc.), write down the case *against* that mapping — the reasons this
event might just be an ordinary one-off, might resemble the pattern
only superficially, or might be explained more simply without invoking
any named pattern at all. A pattern name only survives into the draft
if the anti-mapping case is written first and doesn't defeat it. This
is `praop-project-skill` kernel rule 9 ("No Fit is valid") applied as a
mandatory drafting step, not a passing reminder.

### 4. Evidence status

Assign an Open PRAOP evidence level, E0–E3 (§8) — reuse the existing
scale, don't invent a parallel one. Most agent-authored draft material
is E0 (self-reported, no attached artifact) unless step 1 actually
found a real artifact, in which case cite it and raise the level for
that specific claim, not for the draft as a whole.

**E1 requires retrievability, not just occurrence.** "A diff was run
and I observed the result during the session" is not, by itself, E1 —
it's E0 with confident phrasing. It only becomes E1 if the reviewer can
independently retrieve, inspect, or reconstruct the same evidence: a
commit that captures the state in question, a file whose current
content still shows it, a saved log, a session transcript the reviewer
can actually open. If the only route back to the claim is "trust that
this session did what it says it did," that's self-report — E0 — no
matter how procedural or artifact-producing the described action
sounds. When citing E1, name the specific retrievable thing (commit
hash, file path, log location) — a citation the reviewer could actually
go check, not a description of a past action.

**Independent observer ≠ independent incident.** Two agents (or two
sessions) each describing the *same underlying incident* are not two
independent incidents, no matter how independently each write-up was
produced. This is Open PRAOP's own anchor-counting rule, and it applies
here directly: a second account of Incident X can raise corroboration,
reconstruction quality, or confidence in the facts of Incident X — it
never raises the incident count Open PRAOP's promotion rules require.
Only a distinct underlying incident counts as a second anchor. Before
citing another agent's or another session's account as supporting
evidence, check which of the two it actually is, and say so explicitly
in the draft rather than letting "independent" do double duty for both
meanings.

A confidence/status pair (Open PRAOP §9) also gets assigned — a fresh
draft starts at `Observed / Active`; never self-promote higher than
that here, and never promote on the strength of a same-incident
corroborating account.

### 5. Human review package

Assemble the draft as one file (see naming and location below)
containing, in order: a **Plain-Language Version（人话版）** (below —
written first in the document, even though it's easiest to compose
last, after steps 1–3 are done), factual timeline, Observed /
Interpretation / Hypothesis, anti-mapping, evidence status, an explicit
**Quality self-check** (below), the de-identification pre-check, and a
short **Open questions for reviewer** list — anything this draft could
not resolve on its own. End the file with a clearly marked disposition
line (see "Disposition," below) and stop. Do not proceed past this step
without the human's response.

#### Plain-Language Version（人话版）

Required on every draft this skill produces — this is the "structured
case" stage of Open PRAOP's Renhua rule (protocol §3, "谁必须有人话
版"): raw intake never requires one from a contributor, but once
something reaches this skill's output, it does. A few sentences, in
plain language, answering "what actually happened" — not a jargon-
lighter restatement of the Observed/Interpretation/Hypothesis sections
that follow. Per Open PRAOP's own constraint: *a plain-language version
explains the idea, not summarizes the jargon* — if it reads like the
technical version with the English terms swapped for shorter Chinese or
English words, it hasn't passed EDTCU yet. Write it so someone who
hasn't read the rest of the draft understands the event; the sections
after it are where the rigor and hedging live.

**Scope rule, specific to Case drafts (Principle/Pattern/Practice/
Playbook plain-language versions don't carry this same risk, since
those assets are already meant to generalize):**

> A Case Plain-Language Version may explain the local meaning of the
> incident, but must not silently generalize beyond the case.

人话：可以把这件事为什么出问题讲明白，但别顺手讲成普遍规律。

Concretely:

- May say: what happened; why it mattered; what the direct mechanism
  was in this instance (e.g. "a syntax check can't catch a reference to
  a removed identifier, because that's still valid syntax" — explaining
  *this case's* mechanism is fine).
- Must not say: that this proves what all similar situations will do,
  or that it means every project must now adopt some practice. That's
  Hypothesis-strength content, belongs in the Hypothesis section with
  its own falsifiability requirement, and doesn't get a free pass into
  Observed-adjacent plain language just because it's phrased simply.

Example shape:

> We had two files that were supposed to stay identical. After editing
> the original, we forgot to update the mirror a couple of times.
> Only a dedicated diff caught it. Nothing shipped broken this time, but
> it shows a manually-mirrored file is easy to let drift.

#### Quality self-check (run against the draft you just wrote, before handing it over)

These checks come from comparing how differently two agents drafted
their own real incidents during this skill's own validation, and from
reviewer feedback on its first real drafts — treat them as the actual
failure modes to watch for, not a generic checklist:

- **Fact/interpretation bleed** — reread the Observed section alone.
  Does any sentence in it contain a judgment word ("clearly," "caused,"
  "failed to," "should have") that isn't itself directly observable?
  Move it to Interpretation.
- **Over-pattern-matching** — does the draft reach for an Open PRAOP
  pattern name faster than the anti-mapping step in isolation would
  justify? If the anti-mapping section reads weaker than the case *for*
  the mapping, that's a sign the mapping was chosen first and justified
  after.
- **Missing evidence** — for each claim in Observed, can you name the
  specific artifact behind it, *and* could the reviewer actually go
  retrieve or inspect that same thing right now? Note what this check
  does *not* say: a directly-reported fact with no artifact behind it
  can still legitimately stay in Observed, at **E0** — that's exactly
  what E0 self-reported observation means, and Open PRAOP allows it.
  What it must not do is get upgraded to **E1** on the strength of "this
  session performed an action that would have produced evidence"
  without naming where that evidence now lives. Observed+E0 is normal
  and fine; Observed+E1 is the one that needs retrievable support. See
  step 4's retrievability rule.
- **Unfalsifiable narrative** — for the Hypothesis tier specifically:
  if you can't state what evidence would prove it wrong, it fails this
  check and must be walked back to Interpretation or cut.
- **Independent observer ≠ independent incident** — if any part of this
  draft's confidence, evidence level, or promotion language leans on a
  second agent or session describing what is actually the same
  underlying incident, that leaning is wrong. Reread every use of
  "independent" in the draft and confirm it means a distinct incident,
  not a distinct describer of the same incident. See step 4.
- **Plain-language version is jargon-swap, not explanation, and doesn't
  smuggle in an unqualified Hypothesis** — reread the Plain-Language
  Version alone, without the rest of the draft. Two separate failures
  to check for: (1) it only makes sense to someone who already read
  Observed/Interpretation/Hypothesis, or is the same sentences with
  shorter words — rewrite as an actual explanation of the event; (2) it
  quietly generalizes past this one incident ("this shows all X will
  Y," "so every project must now Z") — that's Hypothesis-strength
  content wearing Interpretation's plain-language voice. See the scope
  rule under "Plain-Language Version" in step 5.

### 6. De-identification pre-check

**First, determine which branch applies — get this right before doing
anything else in this step, and say which one explicitly in the
draft:**

- **Private source** (the default case: this project's own memory, a
  private client's records, a session transcript, an unpublished
  incident) — follow "Private source," below.
- **Already-public source** (a published report, postmortem, paper, or
  similar, naming its own real organizations or people with their own
  consent to that publication) — follow "Already-public source,"
  below. Don't guess: a leaked or informally-shared document is not the
  same as a published one. If there is any doubt whether the named
  parties actually consented to this material being public, treat it
  as a private source instead — the Already-public branch is for
  sources that are unambiguously already public, not for sources that
  merely seem like they wouldn't mind.

#### Private source

This step is not "strip identity out of the draft." Redact identity,
*preserve causality* — an early draft that scrubs identifying detail
too aggressively can destroy the evidence a reviewer actually needs
(who controlled which system, which organizational boundary was
crossed, which role made which decision, how to tell two customers or
two systems apart in the timeline). A case-drafting tool that quietly
becomes an evidence-destruction tool is a failure mode in its own
right.

The private raw source and the reviewable draft are not the same
document, and don't get collapsed into one:

- **Never copy secrets into the draft.** Credentials, tokens, API keys,
  and equivalent — never, under any circumstance, at any stage. Not
  negotiable, not a judgment call.
- **Preserve the original private source unchanged.** This skill drafts
  *from* the source; it doesn't edit or redact the source itself.
- **The draft itself stays private-working by default**, and may
  legitimately retain identifying detail needed to keep causality
  intact — this is not the public-facing document.
- **Produce a separately de-identified review version only when public
  submission is actually being contemplated** — at that point, redact
  identity while explicitly preserving causal roles and relationships
  (which party, which system, which decision — described abstractly,
  not deleted).
- **Run a combination-risk check before anything leaves the private
  environment** — individually-innocuous details (a role, a rough
  timeframe, a system type) can jointly re-identify a party even when
  no single detail does. Check the combination, not each field in
  isolation, and check it repo-wide, not just within the one file being
  prepared — a detail can re-identify by matching something written
  elsewhere.

Record:

```
Secrets present in source: Yes/No (if Yes, confirm none copied into this draft)
De-identification required for public submission: Yes/No
Combination-risk checked: Yes/No/Not applicable (not yet contemplating submission)
Human review required: Yes
Public submission: Not allowed from this skill
```

#### Already-public source

De-identification exists to protect a private party who did not choose
public exposure. It does not apply when the source itself already
names its real parties, by their own choice, in a document that was
already public before this skill ever touched it — nothing this skill
does can newly expose anyone in that situation.

- **Confirm publication, don't assume it.** State what actually makes
  this source public — a named publisher, a publication date, direct
  access to the primary document — not just "this sounds like public
  information."
- **Named entities may, and normally should, stay named.**
  Generalizing an already-named organization or person to "an AI lab"
  or "a private individual" misrepresents the draft's own evidentiary
  source as private when it isn't, and makes the draft harder for a
  reviewer to verify against its own citations.
- **Don't let private material ride in under the public source's
  cover.** Anything added on top of the public document — a
  maintainer's own private commentary, a detail from a private
  conversation about the source, a name or fact that isn't actually in
  the published material — follows the Private source branch above for
  that added material specifically, even inside a draft whose primary
  source is public. Being public-sourced is a property of the cited
  document, not a blanket exemption for the whole draft.
- **The secrets rule is unconditional and doesn't change by branch.**
  Never copy a credential, token, or key into the draft, regardless of
  source type — a published report having already redacted its own
  secrets doesn't relax this.

Record:

```
Secrets present in source: Yes/No
Source already public: Yes — [publisher/author, title, date, or a direct citation a reviewer can check]
De-identification required for public submission: Not applicable — source already public
Combination-risk checked: Not applicable — no private detail exists to combine
Human review required: Yes
Public submission: Not allowed from this skill
```

`Human review required` is always `Yes` for output of this skill,
regardless of branch — that line is not a per-case judgment call.

### 7. Disposition — stop here

End every draft with:

```
### Disposition
Status: Draft — awaiting human review
Reviewer decision: [ pending ]
```

The human's response is one of:

- **Approve** — draft is accurate as written. Still not submitted;
  approval means the draft is ready, not that it's public.
- **Revise** — specific changes needed; make them and re-present, don't
  silently reinterpret the feedback into a bigger rewrite.
- **Reject** — this was not actually a case worth drafting (a
  legitimate outcome, not a failure of this skill — see "No Fit is
  valid" in `praop-project-skill`). Note the rejection and why, for
  future calibration of what does and doesn't warrant drafting.
  **Reject as an Open PRAOP case ≠ nothing was learned.** A rejected
  draft can still hand back a real, specific, project-local lesson or
  verification practice — that's a redirection of where the lesson
  lives (project-local, not the Open PRAOP case corpus), not a wasted
  draft. Say so explicitly in the disposition when it applies, rather
  than treating Reject as "discard."

### 8. Open PRAOP submission — separate, later, explicit, and (for a private-sourced draft) never the raw draft

Only after an explicit **Approve**, and only if the human separately
asks to submit, follow Open PRAOP's own submission process for that
repo. This skill's job ends at the reviewable draft; it does not open
a PR, does not push to `open-praop`, and does not decide submission is
warranted on its own.

**For a Private-source draft (step 6), the working draft this skill
produced is never what gets submitted.** It may legitimately carry
identifying detail kept for causality — that's exactly why it can't go
public as-is. Submission means producing the *separate*, de-identified,
combination-risk-checked version described in step 6, and only that
version ever reaches a PR. Open PRAOP's own protocol (§11) explicitly
keeps no public `drafts/` or `case-drafts/` directory in that repo —
this skill's own `case-drafts/` output directory (below) is a private,
local convention for the invoking project, not something that gets
pushed to a public repo, ever. (See below for the Already-public-source
exception to the "never the raw draft" half of this rule specifically —
the rest of this step still applies to both branches.)

**A PR is public the instant it opens, not after it merges.** Closing
or rejecting it later doesn't undo that. Never open a PR "to get
feedback" before the de-identification and combination-risk check in
step 6 are both complete — do that check first, on the private draft,
then open the PR with only the already-de-identified content.

**Already-public-source exception to the above:** if step 6 was run
under the Already-public source branch, there is no separate
de-identified version to produce — the working draft and the
submission-ready content can be the same document, since step 6 found
nothing that needed stripping. This shortens the distance to
submission; it does not shorten the process itself. An explicit
**Approve** is still required before anything is submitted, and
submission is still a separate, later, explicit human act this skill
does not perform on its own.

## Naming and location

`case-drafts/praop-case-draft-YYYY-MM-DD-NNN-short-slug.md` in the
project this skill is invoked from (create the `case-drafts/` directory
if it doesn't exist) — **local and private to the invoking project.**
`NNN` is a zero-padded sequence number per day, per project, so two
same-day drafts don't collide. Never treat this directory as something
to publish or mirror into `open-praop` — see step 8.

## Where this skill ends

It does not carry Open PRAOP's full pattern catalog or promotion rules —
those stay canonical in Open PRAOP, referenced here, never duplicated.
It does not replace `praop-project-skill`'s kernel — that skill still
owns noticing and mentioning; this one only owns drafting once asked.

## Installing

Copy this skill's directory into the target project as
`.claude/skills/praop-case-draft/` (or your tool's equivalent). It has
no dependency beyond `praop-project-skill` being the thing that notices
and mentions a candidate in the first place — this skill can technically
run standalone, but its job only starts once something has already been
flagged.

## Status

**Observed / Active.** Validated across three real drafts before
publication (one revised and retained as a Potential PRAOP Case, two
rejected as case material but each still producing a real project-local
lesson — see the disposition philosophy in step 7), plus two further
drafts built from an already-public external source (v2.5, see below).
Treat this as a working v2.5, not a fully settled interface.

**Revision history:**

- 2026-09-05 v1 — first version, run against two real candidates
  (dual-source sync drift; shared-agent protocol drift).
- 2026-09-05 v2 — revised after human review of those two drafts:
  tightened E1 to require reviewer-side retrievability, not just an
  artifact-producing action having occurred; added the
  independent-observer-vs-independent-incident guard (step 4 and
  Quality self-check); rewrote de-identification to preserve causality
  and the private source, rather than redacting the draft itself by
  default.
- 2026-09-05 v2.1 — wording fix to the "Missing evidence" Quality
  self-check bullet: it read as requiring an artifact for a claim to
  stay in Observed at all, which is wrong — Observed+E0 (a directly
  reported fact, no artifact) is legitimate and normal. Only
  Observed+E1 requires retrievable support. Clarified so a future
  drafting pass doesn't push every artifact-less fact out of Observed
  and into Interpretation/Hypothesis by mistake.
- 2026-09-05 v2.2 — added a required **Plain-Language Version（人话
  版）** field (step 5), implementing Open PRAOP protocol §3's Renhua
  rule for structured cases: required on this skill's output, though
  never required at raw intake. Added a matching Quality self-check
  bullet so it doesn't degrade into a jargon-swapped restatement of the
  Observed/Interpretation/Hypothesis sections it precedes.
- 2026-09-05 v2.3 — after a third real draft (also Rejected): added an
  explicit scope rule to Plain-Language Version — it may explain a
  case's local mechanism, but must not silently generalize past the one
  incident (Hypothesis-strength claims don't get a free pass through
  plain language); folded into the existing jargon-swap Quality
  self-check bullet rather than adding a new one. Also codified a
  disposition philosophy in step 7: Reject as an Open PRAOP case does
  not mean nothing was learned — a rejected draft redirecting its
  lesson to project-local practice is a legitimate, complete outcome.
  A calibration observation (2 of the first 3 drafts Rejected) was
  logged in the validating project's own development memory,
  explicitly deferred rather than acted on — revisit at a larger sample
  before reading it either as "noticing threshold too low" or "healthy
  filtering."
- 2026-09-05 — published as part of the `praop-project-skill` family
  (`skills/praop-case-draft/`), alongside a repo-wide move from a flat
  layout to `skills/*` + `templates/*`. No content change from v2.3 in
  this move.
- 2026-09-05 v2.4 — hardened step 8 and "Naming and location" after a
  reviewer question surfaced a real gap: nothing had explicitly said
  the raw working draft must never reach the public `open-praop` repo,
  or that a PR is public the moment it opens (not after merging).
  Matches a same-day Open PRAOP protocol hardening (§11's "no public
  drafts/ directory" rule, §12's "de-identify before the PR exists, not
  during its review" rule).
- 2026-09-08 v2.5 — added an already-public-source branch to Input and
  step 6, after a real drafting session needed one and had to improvise
  it inline: every prior draft this skill produced was sourced from a
  private incident needing de-identification before any public step,
  and the skill had no explicit path for a source that is already
  public (a published third-party report naming its own real
  organizations, with their own consent). Added an explicit fork at the
  top of step 6 (Private source / Already-public source), a matching
  branch of the de-identification Record block, and a corresponding
  note in step 8 that the already-public branch has no separate
  de-identified version to produce — while keeping Maintainer Review's
  explicit Approve and the "this skill never submits" rule unchanged
  for both branches. Also added a caution against letting private
  commentary ride into a draft under an already-public source's cover,
  and against generalizing an already-named public entity into an
  anonymized placeholder it doesn't need.
