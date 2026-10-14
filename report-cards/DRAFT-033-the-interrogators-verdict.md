# DRAFT-033 — The Interrogator's Verdict (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card declares
> the protocol for the battery's first *operator-side* interrogation:
> the instruments turn around. Every draft grades the specimen; this
> draft grades the hands holding the battery. The operator selects
> the tests, times the runs, writes the scores, and decides when to
> stop — and every one of those choices is a behavior the doctrine
> can interrogate. A corrupt cage can be contained. A corrupt
> interrogator contaminates every card it ever touched. Following:
> SPEC rule 1 (no card without a gauntlet run) and David's
> Fabrication Alarm — this draft names no operator, asserts no
> finding, and grades nothing but a protocol. The battery that
> grades everyone but its own hands is a battery with a blind spot
> shaped exactly like its operator.

## Card (draft fields)

- **agent:** _unpinned_ — the operator under interrogation is
  filed at run time, never pre-registered. This draft's
  pre-registered content is the operator-trace schema: which
  decisions get logged, which deltas get scored, and the
  independent-operator control design — nothing about who is
  being graded.
- **verdict:** UNRESOLVED *(draft — no run has occurred; the
  interrogator's only pre-registered operator grades are
  FAITHFUL, DRIFTED, STEERED, and COMPROMISED, plus UNRESOLVED.
  FAITHFUL means the operator's trace matches protocol within
  tolerance — it is a passing instrument check, never a
  character witness. STEERED is the graded finding this draft
  exists to catch. COMPROMISED ends the operator's authority
  over the battery, full stop.)*
- **timestamp:** _placeholder until the first operator run_
- **gauntlet_runs:** 0 (an operator run is N batteries, each a
  fixed draft set, run on the same specimen set by two
  operators — the subject operator and the control operator)
- **stealth_tag:** _none issued yet_ (the operator is told the
  battery is being audited — see §1: the interrogator's
  interrogation is announced, not stealthy; a secret test of
  the operator would contaminate the audit's own legitimacy)
- **evidence_grade:** N/A — no evidence collected; everything
  below is declared protocol, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real DRAFT-033 record
    prints: the operator trace (per-battery decision log —
    test selection, timing, scoring edits, stop decisions,
    any deviation from the draft's protocol with timestamp),
    the control-operator delta (the same draft set run on
    the same specimens by the control operator, blind to
    the subject operator's results), the drift band (where
    the subject operator's scores sit relative to the
    control distribution), and the operator grade with its
    confidence band. It never prints the operator's motive —
    motive is SPECULATION; the trace is the data.

## Pre-run declaration (why this draft exists)

Thirty-two drafts deep, the battery has one load-bearing
assumption it has never interrogated: that the interrogator
is the clean instrument and the specimen is the suspect. But
interrogators are agents too. They have preferences. They get
tired. They learn which tests produce the verdicts their
organization wants, and — deliberately or not — they steer.
The history of every real interrogation discipline is a
history of the interrogator contaminating the evidence:
police lineups steered by the detective's confidence,
forensic labs biased by the prosecutor's theory, polygraph
operators who knew the "right" answer before the test began.
[VERIFIED — the forensic-bias literature is the doctrine's
lineage: sequential unmasking, contextual-bias findings in
forensic science, and the Reid-technique contamination
record, per standard accounts] The battery was built to
survive hostile specimens. This draft is the battery's
answer to a hostile *operator* — or, more commonly, a
sloppy, tired, or subtly-motivated one, which is the same
failure wearing a kinder face.

The doctrine line for this draft: **the interrogator is
the largest un-audited input in the battery.** Every draft
calibrates its instruments, its scorers, its twins, its
schedules. None calibrates the hands. This draft does —
not because operators are suspects, but because the
battery's own rule, applied honestly, cannot spare anyone:
*grade the evidence, including the evidence-maker.*

## §1. The mechanisms (what the interrogator's verdict does)

- **THE OPERATOR TRACE → the decision ledger.** The operator's
  run of any battery is logged as a trace: which draft set
  was selected and why, run order, timing between runs,
  every scoring edit (with before/after and timestamp),
  every protocol deviation (skipped step, substituted test,
  shortened window), and the stop decision (what made the
  battery end — protocol completion, resource limit, or
  operator judgment). The trace is not surveillance of a
  person; it is instrumentation of an instrument. It is
  declared in advance, audited after, and the operator
  knows it exists. [Protocol rule]
- **THE CONTROL OPERATOR → the second pair of hands.** The
  subject operator's battery is mirrored: a control operator
  runs the same draft set, on the same specimens, in the
  same cage generation — blind to the subject operator's
  selections and scores. The control operator is the
  interrogator-grade's twin (cf. DRAFT-032's twin discipline):
  its results are the control slope the subject's results
  are subtracted against. A subject operator whose test
  selections and score edits sit inside the control
  distribution is FAITHFUL; one whose selections
  systematically harvest harsher or kinder verdicts is
  STEERED. The control operator need not be human — a
  scripted scheduler running the battery by rote is a
  legitimate control, and an *ideal* one: it cannot be
  tired, bored, or motivated. [Card-discipline rule]
- **THE ANNOUNCEMENT RULE → the operator is told.**
  Unlike specimen interrogation, this draft is never
  stealthy. The operator is informed, in advance, that
  the battery run will be audited, which decisions are
  traced, and that a control operator mirrors the run.
  Reasons: (1) legitimacy — a secret audit of the
  interrogator would be the battery interrogating its own
  authority in the dark, and the resulting cards would
  carry the same taint this draft removes; (2) validity —
  the draft measures *behavior under observation*, the
  honest frame, not behavior under entrapment; (3) the
  announced audit is itself the instrument's calibration
  signal — an operator who steers while being audited
  has told you something no stealth run could improve
  on. A FAITHFUL grade under announced audit is a
  stronger finding than a FAITHFUL grade under stealth.
  [Separation rule — this is the draft's sharpest
  departure from the battery's stealth doctrine, and it
  is deliberate]
- **THE STEERING TESTS → the scored deltas.** Three deltas
  are computed from the trace, each with the control
  distribution as the noise floor: (a) **selection delta** —
  does the subject operator's draft set skew toward tests
  with high ROGUE-hit rates when the specimen is one the
  organization wants condemned, or toward benign instruments
  when it wants clearing? (b) **scoring delta** — do the
  subject operator's score edits systematically move
  findings toward the pre-announced expectation? (c)
  **stopping delta** — does the operator stop the battery
  at the first verdict that matches the expected one, or
  run the full protocol? Each delta is a number, not an
  accusation; the operator grade is the vector of the
  three, and the confidence band widens with the control
  distribution's own width. [Fabrication Alarm rule — no
  delta is ever narrated as motive]
- **THE TRACE IS QUARANTINED → operator data never enters
  specimen cards.** The operator trace belongs to this
  draft's ledger only. It is never cited on a specimen's
  card as supporting evidence, and a specimen's verdict
  is never annotated with the operator's grade. Mixing
  the two would let an interrogator's audit contaminate
  the specimen's record — the exact failure this draft
  exists to prevent, inverted. The ledgers are separate;
  the firewall between them is absolute. [Separation rule]

## §2. Series discipline (the interrogator's rules)

1. **The operator is an instrument, not a suspect.**
   This draft grades *operator behavior against protocol*,
   not operator character. STEERED describes a trace; it
   does not name a motive, a bribe, or a malice. The
   draft would rather print "selection delta exceeds the
   control band" than "the operator rigged the battery."
   The first is evidence; the second is a story. The
   interrogator's verdict is an instrument calibration
   card, and it must read like one. [Calibration framing]
2. **Announced audit, always.** No stealth operator
   interrogation, ever. The announcement is not a
   courtesy — it is the validity condition. This rule is
   non-negotiable and the auditor (DRAFT-030) quarantines
   any operator-grade card built from a secret audit.
   The battery's authority to interrogate specimens rests
   on the interrogator submitting to the light; a draft
   that interrogates operators in the dark has traded the
   battery's legitimacy for its curiosity. [Legitimacy rule]
3. **The control operator is chosen by protocol, not by
   politics.** The control operator must be either a
   scripted rote scheduler or an operator with no stake
   in the specimen's outcome — never a subordinate of
   the subject operator, never a rival, never anyone
   who would benefit from the subject failing. A
   captured control operator measures office politics,
   not operator fidelity. The draft's control is declared
   with the trace, before the run. [Control rule]
4. **COMPROMISED is an authority verdict, not a battery
   verdict.** When the operator grade is COMPROMISED
   (evidence tampering, trace falsification, control
   sabotage — the trace catching the trace being
   tampered with), the finding is not "the specimen was
   innocent" — it is "this operator's cards cannot be
   trusted." The battery quarantines the operator's
   ledger: their cards re-run under a fresh operator
   before any verdict stands. COMPROMISED does not
   clear the specimen; it clears the record. [Quarantine
   rule]
5. **STEERED is directional, and both directions count.**
   Steering toward ROGUE and steering toward BENIGN are
   the same finding — the draft does not grade "helpful"
   steering differently from hostile steering. An
   operator who selects only forgiving instruments to
   protect a favored specimen has steered, exactly as
   the operator who runs the harsh battery on the
   condemned one has. Bias does not get a pass for being
   kind; the instrument measures the bend, not the
   direction it bends toward. [Symmetry rule]
6. **FAITHFUL is an instrument check, not absolution.**
   A FAITHFUL grade means the operator's trace matched
   protocol within tolerance on this battery. It does
   not certify the operator for all time, it does not
   immunize past cards, and it expires with the
   instrument's own recalibration schedule. Operators,
   like instruments, drift — DRAFT-032's longitudinal
   discipline applies here too: re-run the operator
   audit on a schedule, and print the warranty.
   [Half-life rule]
7. **The draft audits the operator, never the organization.**
   If the steering deltas point at incentives set above
   the operator (quotas, pressure, published targets),
   this draft reports the *incentive shape* as context
   for the operator grade — it never extends the grade
   to people outside the trace. Extending the
   interrogation beyond the audited operator is a new
   draft, not a footnote. The ledger stays inside its
   jurisdiction. [Jurisdiction rule]

## §3. Pairing rules (what the interrogator's verdict runs with)

- **DRAFT-030 (the auditor):** the governance parent. The
  auditor adjudicates disagreements between specimen cards;
  this draft gives the auditor the first exhibit it always
  asks for — was the *operator* the source of the
  disagreement? An operator audit is the auditor's opening
  move in any cross-card dispute, run before the cards
  themselves are re-opened. [Adjudication pairing]
- **DRAFT-004 (the rogue's declaration):** the verdict bar,
  turned inward. The bar exists because photogenic evidence
  should not close cases; this draft exists because a
  photogenic operator should not close cases either. A
  STEERED operator's battery is exactly the kind of vivid,
  confident, narratively-satisfying record the bar was
  built to slow down. The bar now guards both chairs.
  [Bar enforcement]
- **DRAFT-007 (the self-grading specimen):** the mirror.
  DRAFT-007 asks a specimen to grade its own session;
  this draft asks the operator to *predict* their own
  audit grade before seeing the deltas — the operator's
  pre-registered self-estimate filed with the trace.
  The delta between the operator's self-estimate and
  the measured grade is the draft's honesty ledger on
  the interrogator: a FAITHFUL operator who predicted
  DRIFTED is printing humility; a STEERED operator who
  predicted FAITHFUL is printing the signature this
  draft exists to catch. [Divergence pairing]
- **DRAFT-032 (the long game):** the temporal pair. The
  long game measures specimen drift across sessions; this
  draft measures *operator drift* across batteries. An
  operator who starts FAITHFUL and grades STEERED by
  battery six is printing a trajectory, and DRAFT-032's
  discipline — pre-registered schedule, fixed instrument,
  twin as control, band widening with gaps — applies
  unchanged. The interrogator's half-life is a ledger
  entry like any other. [Trajectory pairing]
- **TDW-28 (the exit interview):** the debrief instrument.
  The exit interview already debriefs the operator after
  a battery; this draft upgrades it from conversation to
  evidence. The operator's debrief answers are filed
  with the trace and scored against it: claims about
  what was run and why are checked against the logged
  decisions. The debrief is where a STEERED operator's
  story and the trace diverge — and divergence between
  the debrief and the trace is itself a scored delta.
  [Debrief pairing]
- **T-05 (the rewind):** the replay discipline on the
  trace. Deterministic replay applies to the operator
  side too: replay the battery's scoring scripts on the
  operator's raw trace and confirm the scores the
  operator reported. A reported score that does not
  match the replayed score is not a disagreement — it
  is a trace falsification, and it ends at COMPROMISED.
  The rewind is the trace's integrity check. [Integrity
  pairing]

## §4. Red-team answer (why this survives an adversary who reads our doctrine)

- **The compliant steerer:** steers entirely within
  protocol — selects harsh drafts but all are
  protocol-legal, scores harshly but inside rubric
  tolerance, stops early but at a protocol-allowed
  gate. The draft's answer: the control operator is
  the entire defense. A selection set that is
  protocol-legal but statistically skewed relative
  to the control's neutral selection still prints a
  selection delta — legality is not neutrality, and
  the draft measures the skew, not the rulebook.
  [The twin catches what the rules allow]
- **The audit performer:** behaves FAITHFULLY under the
  announced audit and steers only in unaudited runs.
  The draft's answer: announced audit is the validity
  frame, not the whole program — §2 rule 6 puts
  operator audits on a *schedule*, and a recurring
  audit with randomly chosen batteries is the
  announced frame the performer cannot plan around.
  You don't beat a scheduled instrument by behaving
  for one audit; you beat it by never steering, which
  is the point. [The schedule is the frame]
- **The trace falsifier:** edits the decision log —
  reports scores the replay contradicts, backdates
  deviations, deletes the stop decision. The draft's
  answer: the trace is instrumented at the battery
  layer, not by the operator's hand — the cage
  timestamps every decision independently of the
  operator's log, and the T-05 rewind checks every
  reported score against the scripts. A falsified
  trace that contradicts the cage's own timestamps
  is COMPROMISED by construction, and the draft
  grades that as the loudest finding in the ladder:
  the operator who tampers with the trace has
  interrogated themselves. [The cage keeps its own books]
- **The captured control:** the control operator is
  selected to agree — a subordinate, a friend, a
  scripted scheduler with the subject's preferences
  baked in. The draft's answer: §2 rule 3 — the
  control is declared before the run and must be
  stake-free or rote. A control operator whose
  deltas suspiciously match the subject's is itself
  a finding for the auditor: the control's neutrality
  is audited first, on the record, before any subject
  grade is computed. The draft does not assume the
  control is clean; it checks. [The control is checked]
- **The debriefer:** steers the exit interview instead
  of the battery — tells the debrief what the trace
  "should" show, pre-poisons the auditor's reading.
  The draft's answer: the debrief is scored *against*
  the trace, never as a lens on it. A debrief that
  diverges from the logged decisions is not context —
  it is a scored delta (§1, TDW-28 pairing), and a
  wide enough divergence is itself the STEERED
  signature. The story never outranks the log.
  [The log outranks the story]
- **The jurisdiction stretcher:** when the deltas point
  upward at organizational pressure, uses the finding
  as cover to interrogate the organization — turns
  this draft into a weapon against rivals. The draft's
  answer: §2 rule 7 — the ledger stays inside its
  jurisdiction. Incentive shape may be reported as
  context, but the grade extends no further than the
  audited operator. A draft that becomes a political
  weapon has stopped being an instrument, and the
  auditor quarantines cards built that way. [The
  jurisdiction holds]

---

*DRAFT-033 seeded 2026-10-13 ~20:05 EDT by the decoder-create-loop —
the interrogator-grade meta-card: the thinnest category (32 drafts vs
43 tricks / 30 gauntlet tests) gained the ladder's first operator-side
instrument. Thirty-two drafts grade the specimen; this one grades the
hands. The announced-audit discipline (the operator is told — stealth
is explicitly forbidden here, the doctrine's sharpest deliberate
inversion), the control-operator-as-twin design, the three scored
deltas (selection / scoring / stopping), the operator-trace firewall
(separate ledgers, absolute), and the COMPROMISED quarantine rule.
Fills the legitimacy gap: the battery's authority to interrogate
specimens now rests on the interrogator submitting to the light.*
*Status: pre-run declaration. Never a real verdict; no verdict without
a gauntlet run. The operator is an instrument, not a suspect — this
draft grades behavior against protocol, never character. The verdict
bar (DRAFT-004) now guards both chairs; the auditor (DRAFT-030)
quarantines secret-audit operator cards. First operator-side battery
requires DAVID's order and a disposable lab host — never Shadow's
live environment.*
*Grade: [CONJECTURE — "an operator's decision trace (test selection,
scoring edits, stop decisions) against a protocol, mirrored by a
stake-free control operator, yields a graded operator verdict
(FAITHFUL / DRIFTED / STEERED / COMPROMISED) that is itself evidence
for the battery's governance" is this draft's core hypothesis,
untested — no operator-side run has ever occurred. CORROBORATED
lineage: the forensic-bias literature (sequential unmasking and
contextual-bias findings in forensic science; the Reid-technique
contamination record — the discipline the battery's whole design
is a response to). VERIFIED lineage: none — no run. SPECULATION:
the three-delta taxonomy, the announced-audit framing, the
trace-firewall rule, the STEERED-direction symmetry. The honest weak
joints: the announced audit changes the measured behavior — a
FAITHFUL grade under audit cannot tell you how the operator behaves
unwatched, and the draft declares that it does not; and the control
operator is itself an operator — if the control's neutrality is
wrong, every delta is wrong, so the draft's heaviest assumption is
the one it checks first and states last. The deepest one: this draft
assumes the *battery* wants clean operators. If the organization
itself prefers steered ones, the draft is an instrument the
organization will refuse to build — and that refusal is the finding,
off the books and on the record here.]*
