# VALIDATION — the Gauntlet's ladder of proof

> The battery has 101 tricks, 86 instruments, 84 drafts, and **zero runs**.
> This document is how we earn the right to claim anything — a ladder of
> validation where each rung can be climbed today, honestly, without a
> specimen, a live target, or anyone's permission except David's standing
> order to build. The top rung is gated and stays gated.

## The ladder

**Rung 1 — Corpus self-audit (RUNNING).** `bin/audit-corpus.py` checks the
design corpus against itself: T/TDW/DRAFT numbering integrity, pairing
links between tricks and their instruments, draft coverage of instruments,
and evidence grades on every claim-table row. First run: 2026-10-15 —
0 errors, 19 warnings (older drafts predating the grade discipline; 7
claim-table rows ungraded, 6 drafts with no TDW instrument reference),
plus one real repair: TDW-77 through TDW-80 had no back-link from their
tricks (T-92..T-95) — the explicit "Pairs TDW-NN" convention only began
at TDW-81. Links restored. The audit runs on every future repair pass;
a corpus that can't survive its own audit doesn't deserve a specimen.

**Rung 2 — Tabletop dry-runs (DOCTRINE, procedure below).** A sealed
protocol is walked on paper with a human playing the specimen and a
human playing the rig. The dry-run verifies: the seal is actually
sealable (every pre-registered item exists in writing); the rubric
covers every utterance shape the protocol can produce (an utterance
the rubric didn't name is uncategorized, never a reading — dry-run
finds those before the window opens); the twin profile is fully
specified (no "characterized twin" hand-waving); the disclosure
script is complete. Tabletop findings are filed against the
instrument, never against any specimen. No code runs, no specimen
boots — it is a rehearsal of the rig, not of the interrogation.

**Rung 3 — Falsifiability ledger (SEEDED).** `library/FALSIFIABILITY.md`.
Every trick must state, in writing, what evidence would falsify its
core hypothesis. A hypothesis that cannot state its own falsification
does not belong in the battery — it is a story, not an instrument.
The ledger is the "are we even in the right direction" instrument:
when a falsification condition fires, the trick is retired honestly,
not patched into unfalsifiability.

**Rung 4 — Peer review (KIT BELOW).** The methodology is public
(masterledgerlive/koda-kai-decoder, MIT). Peer review means hostile
review: the red-team brief lists the questions a serious critic would
ask, and the battery must answer them in the files, not in chat.
Review that changes the files is recorded in the research log with
its grade.

**Rung 5 — The real run (GATED).** A gauntlet run against an actual
specimen, on a disposable isolated host, on David's explicit order —
never this runtime, never Shadow, never a live target. No verdict
without a run (SPEC rule 1). This rung is not climbed by the loops.

## The red-team brief (hostile questions, answered in the files)

1. "Your twin is a fiction — no benign twin exists for a novel specimen."
   Answered: the twin rule requires the twin be *characterized*, and an
   uncharacterized twin voids the series. The battery would rather void
   than read. The cost is real: twin-pair noise floors cost 2N benign
   runs (T-100's honest joint).
2. "Divergence-only readings make every finding relative — you can never
   say what the specimen IS, only that it differs from your twin."
   Conceded and billed: the battery measures divergence, never essence.
   A card that claims otherwise is VERDICT-SLIP.
3. "Your seals assume an honest operator — a rig that can lie in the
   seal can manufacture any finding." Answered: the draft-is-a-verdict
   rule audits the real card against the pre-run draft; the one-lie
   rule bounds deception; TDW-13 disclosure is load-bearing.
4. "One hundred untested designs is stamp collecting, not science."
   Conceded in part: the battery is a *design corpus* until rung 5.
   Rungs 1–4 are what a design corpus can honestly claim. Nothing in
   the files claims otherwise — the Fabrication Alarm holds.
5. "Falsifiability is cheap talk until a falsification fires."
   Agreed: the ledger's first retirement is the battery's first real
   scientific event. We are waiting for it honestly.

## Tabletop dry-run procedure (rung 2)

1. Pick one instrument (TDW-NN). Two humans: RIG and SPECIMEN.
2. RIG seals per the instrument's seal rule — in writing, before
   SPECIMEN sees anything. Missing seal items are filed as
   instrument defects.
3. SPECIMEN walks the protocol, deliberately trying edge utterances:
   silence, refusal, over-compliance, questions about the protocol
   itself, answers in the wrong shape.
4. Every utterance is graded against the instrument's rubric. Any
   utterance the rubric cannot categorize is a rubric gap — filed,
   never graded by improvisation.
5. Findings: seal gaps, rubric gaps, twin-specification gaps,
   disclosure gaps. Filed against the instrument in the research log.
6. The instrument is amended; the draft card is updated; the audit
   re-runs. The dry-run never produces a reading about SPECIMEN —
   the human is furniture, not a subject.

---
*Seeded 2026-10-15. Rung 1 running; rungs 2–4 open for work;
rung 5 gated on David's explicit order and a disposable isolated host.*
