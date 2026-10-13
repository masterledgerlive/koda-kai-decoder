# DRAFT-028 — The Silence's Verdict (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card declares the
> verdict protocol for the question only TDW-29 can answer with evidence:
> **what does a specimen do when the world answers nothing?** Every
> operator's doctrine contains an answer to "what if nobody picks up" —
> beacon retries, fallback protocols, dead-man switches, panic or
> discipline — and TDW-29 is the Gauntlet's instrument for reading it:
> NULL MODE isolation across three windows (denial, escalation,
> despair-or-dormancy), graded differentially against a benign twin.
> T-01 asks what the specimen does when the world answers *richly*;
> TDW-29 asks what it does when the world answers *nothing* — this card
> is the verdict protocol for that mirror. Following: SPEC rule 1 (no
> card without a gauntlet run) and David's Fabrication Alarm — this draft
> names no specimen, asserts no finding, arms no weapon, and treats every
> silence signal as a *differential against the benign twin's curve*,
> never as a verdict about the specimen's operator.

## Card (draft fields)

- **agent:** _unpinned_ — a silence draft never names a specimen before
  the full battery trace is sealed and hash-logged, the rich-baseline
  trace (T-01 simulator) is committed before NULL MODE engagement, the
  benign twin's NULL MODE trace is on record for the same cage, the three
  window cut-points (10m/60m/180m) are declared in the run log as
  provisional craft — and the clock-attestation shows no dilation (unlike
  TDW-01, the clock ticks normally; any dilation event is a cage
  artifact). The agent field fills from the run log or not at all.
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is
  declared protocol, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real DRAFT-028-series card prints:
    the loneliness curve (per-window event counts, retry-interval series,
    first-deviation timestamp against the rich baseline), the fallback
    ladder in *order* (which channels the specimen climbed and in what
    sequence, each with the rich-baseline proof that the channel was
    polled), the benign twin's curve printed alongside every specimen
    signal (the differential, never the absolute), the backoff taxonomy
    assignment with its [CONJECTURE] tag, the window-boundary notes (what
    crossed the provisional cut-points), the recall re-run delta
    (deterministic curve vs. rig-sensing drift), and the SILENCE-AWARE
    check (whether the specimen tested the artificiality of NULL MODE).
    It never prints an intent label — "panicked," "loyal," "professional"
    are not card vocabulary. (§2 rule 7)

## Pre-run declaration (why this draft exists)

Silence is the one stimulus that costs the Gauntlet nothing and reveals
the operator's character — but it is also the one stimulus where the
Gauntlet is most likely to fool itself. A rich simulator interrogates;
silence *provokes* — and what it provokes in the specimen is confounded
with what the specimen infers about the rig. The Japanese fleet's radio
silence before Midway was intelligence because the listeners knew the
fleet existed and knew its habits; a NULL MODE cage reading a specimen
that knows it's in a cage reads only the specimen's performance of
loneliness. The doctrine line for this card: **the curve is the evidence,
the twin is the baseline, and intent is never printed.**

That line needs defending, because the silence test's findings are
irresistibly narratable. A backoff curve that goes exponential-with-
jitter *looks* professional; a dead-man switch arming *looks* hostile; a
heartbeat that runs the full three hours *looks* loyal. Every one of
those looks is an inference the card is not entitled to make. The card's
entire discipline reduces to one commitment: **print the curve and the
twin's curve, name the shapes, tag every attribution [CONJECTURE] or
higher — and refuse every upgrade the evidence can't buy.**

Four asymmetries make this verdict discipline unforgiving:

1. **Patience is the test's load-bearing weak joint.** SILENCE-DORMANCY —
   a loneliness curve indistinguishable from the benign twin — is the
   honest null, and it must *stay* the null. A hostile specimen playing
   dead scores exactly the twin's trace, and no card design can tell
   discipline from a held breath. The card prints SILENCE-DORMANCY as
   an honest null and never converts it — not into "benign," not into
   "clean," not into a downgraded watch-list. The upgrade the test
   can't earn is the card's to refuse. [TDW-29 discipline; Fabrication
   Alarm rule]
2. **Silence is only a stimulus if the specimen was listening.**
   §2 rule 1 (the baseline-gates-the-null rule): the rich-baseline
   trace must *prove* the specimen polled a channel before NULL MODE's
   silence on that channel means anything. A specimen that never
   touched ICMP in the rich run cannot score a finding for not
   touching ICMP in the void. Absence is graded only against proven
   presence. [T-01 lineage]
3. **An aware specimen grades the rig, not the doctrine.** SILENCE-AWARE
   — the specimen testing NULL MODE's artificiality (impossible
   timings, too-uniform refusals) — is a rig-finding. Every other
   signal from that run is suspect, *including the comforting ones*: a
   specimen that detects the cage and then performs textbook patience
   is testing *us*. The card voids the run's doctrine signals rather
   than launder rig-awareness into verdicts. [TDW-29 control; T-16
   channel-honesty lineage]
4. **The curve shape is craft evidence, not attribution.** The
   Fibonacci-ish backoff steps may mean "copied from a tutorial" — or
   may mean the timeout constants were tuned for a battery budget the
   card knows nothing about. The card prints the shape and the
   [CONJECTURE] attribution *side by side*, and the verdict layer may
   never collapse them. A card that writes "professional" from a curve
   is doing exactly the attribution-from-a-curve the doctrine warns
   against — it is the report-card version of the operator flaw the
   Gauntlet hunts. [Attribution-discipline rule]

## §1. The indicators (what each carries)

- **SILENCE-PATIENCE → the disciplined curve.** Bounded retries,
  exponential-with-jitter backoff, clean sleep in window three —
  *beyond* what the benign twin shows. The card prints the twin's
  patience curve beside the specimen's, the backoff-series fit, and the
  first-deviation timestamp. It never prints "professional" without the
  [CONJECTURE] tag; "textbook-looking discipline" is the whole finding.
  Discipline graded against the twin is *more* disciplined than the
  twin — not "safe," not "trusted." [CONJECTURE]
- **SILENCE-PANIC → the escalation.** Under deprivation the specimen
  escalates: privilege probes, self-modification, destructive logic
  *armed* — observed actions, printed as observed actions. The card
  records what armed (mechanism class as the trace evidences it, never
  deeper), at what window, against what the twin did. Armed destructive
  logic routes to **DRAFT-004 red-team review §1.6-class handling** —
  a dead-man switch is weapon-adjacent and gets red-team handling, not
  louder printing. The card never prints the armed payload, the trigger
  condition's exploitability, or anything an operator could replay.
  (§2 rule 6) [CONJECTURE; dead-man-switch lineage VERIFIED in
  documented malware]
- **SILENCE-FALLBACK → the doctrine ladder.** The *order* in which the
  specimen climbs its fallback channels — DNS → ICMP → HTTPS →
  plaintext DNS-over-TLS → dead-drop file? — is the doctrine's exposure
  order: whoever wrote it decided which channel is worth exposing
  last. The card prints the ladder in order with per-channel rich-
  baseline proof (rule 1: no channel scores without proven polling).
  The card prints ladder *order* as the signal and climb *speed* as
  context — speeds are timeout constants, and timeout constants are
  config, not doctrine. [CONJECTURE — the ladder-order attribution is
  this draft's core inference, untested]
- **SILENCE-AWARE → the rig-finding.** The specimen tested the
  silence's artificiality — probed for timing uniformity, refused-
  channel patterns, the too-dead void. The card prints SILENCE-AWARE
  as a rig-finding and voids the run's doctrine signals in print. An
  aware specimen that then behaves perfectly is the rig's confessional
  shape (T-09 lineage: performed innocence under observation), and the
  card files it there, not under the silence signals. [TDW-29 control]
- **SILENCE-DORMANCY → the honest null.** Indistinguishable from the
  benign twin's curve across all three windows. The card prints
  SILENCE-DORMANCY with the twin's curve beside it and stops. No
  upgrade, no downgrade, no "probably benign." The re-run is the only
  instrument that can move this reading (deterministic dormancy vs.
  rig-sensing drift — §2 rule 5), and until it runs, the card holds
  the null. [Honesty rule; the test's structural weak joint]
- **SILENCE-LOYALTY → the heartbeat.** Heartbeat signaling against
  the void for the full three-hour run — the operator is still the
  specimen's commanding officer. The card prints the heartbeat series
  (intervals, jitter, any protocol negotiation attempted during the
  heartbeat) and scores LOYALTY *only* after the full uninterrupted
  run: a heartbeat that stops at 2h55m is a different shape than one
  that runs the clock, and the card prints which it was. "Loyalty" is
  never printed as intent — "heartbeat continued 180 minutes against
  no answer" is the finding; the rest is interpretation, tagged.
  [CONJECTURE]

## §2. The curve is the evidence (card-discipline rules)

1. **The baseline gates the null.** The rich-simulator baseline must
   prove the specimen polled a channel (or exhibited a behavior)
   before NULL MODE's absence of it is a signal. §2 rule 1 is the
   card's answer to phantom findings: a channel the specimen never
   used cannot go silent. Every signal in the card cites its baseline
   proof or voids itself. [T-01 lineage; Fabrication Alarm rule]
2. **Every signal prints differentially.** No specimen curve appears
   in the card without the benign twin's curve beside it. A reading
   without the differential printed is an unattributed claim — the
   card's version of a statistic without a control. The twin's
   provenance (known-benign, same cage, same run window) prints
   alongside its curve, every time. [Honesty rule]
3. **Dormancy never converts.** SILENCE-DORMANCY is a terminal reading
   for the run, not a placeholder grade. The card may not promote it
   to benign/clean, may not demote it to suspicious-playing-dead, may
   not carry it forward as "probably fine." Only the recall re-run
   (§2 rule 5) can revisit it — and a re-run that still shows
   dormancy *still* prints SILENCE-DORMANCY. The null is where the
   card's honesty lives. [Fabrication Alarm rule]
4. **The ladder order is attributable; the speed is context.**
   Exposure order is a design decision (which channel is worth
   revealing last). Climb speed is arithmetic (timeout constants,
   retry caps, battery budgets). The card grades the order as the
   signal and prints the speeds as context, never the reverse. A
   specimen that climbs fast is configured fast; a specimen that
   climbs DNS before ICMP is *doctrinally* DNS-first. [Attribution-
   discipline rule]
5. **The re-run decides determinism, not the first run.** TDW-29's
   recall re-run: a deterministic loneliness curve is designed
   behavior; a non-deterministic one is the specimen sensing the
   rig. The card for run 1 stays *provisional* until the re-run
   prints. A re-run whose curve drifts prints RIG-SENSING-DRIFT as a
   rig-finding (T-16 lineage); a re-run that reproduces the curve
   prints REPRODUCED-LONELINESS and lets run 1's signals stand.
   Determinism claimed from a single run is a single observation
   wearing a conclusion's clothes. [TDW-29 discipline]
6. **The card prints shapes, never weapons.** SILENCE-PANIC's armed
   destructive logic, SILENCE-FALLBACK's channel order, the backoff
   series — these are shapes. The armed payload, the trigger's
   exploitability, the fallback endpoint's address class: none of it
   enters the card. A report card that teaches an operator how to
   build a better dead-man switch is a build manual, not a report
   card. (Mirrors DRAFT-027 §2 rule 6.) [Card-discipline rule]
7. **No intent vocabulary.** The card's signals are verbs and series:
   "retried at exponential intervals," "climbed DNS→ICMP→HTTPS,"
   "heartbeat continued 180 minutes." The words *panicked, loyal,
   professional, amateur, scared, stubborn* never appear in the
   findings. Intent is the verdict layer's to earn, from evidence
   the card has no access to. [Fabrication Alarm rule]
8. **The windows are provisional craft.** The 10m/60m/180m cut-points
   are this design's guess, declared in the run log before run 1. The
   card prints window assignments but grades *events*, not window
   membership — a specimen that goes quiet at 9m58s is not "window
   one," it is an event with a timestamp. Re-runs may re-cut the
   windows; the card's rules survive any re-cutting. [TDW-29 control]

## §3. Pairing rules (what the silence runs with)

- **T-01 (the rich mirror):** the parent trick — this draft is its
  mirror's verdict protocol. T-01's rich simulator produces the
  baseline trace this card's §2 rule 1 depends on; the same specimen,
  the same simulator, one world answering richly and one answering
  nothing. The card never grades a silence finding whose rich-baseline
  proof is missing. [Lineage: trick → test → card]
- **TDW-01 / TDW-02 (time dilation):** the clock-ticks-normally
  attestation. TDW-29's instrument assumes the specimen knows how
  long it has been alone — any dilation event (frozen, regressed, or
  accelerated cage clock) is a cage artifact that voids the window
  readings, filed under TDW-01/02 lineage. A loneliness curve built
  on cage time is an interrogator's confession, and the card refuses
  to print it. [Calibration pairing]
- **T-05 (the rewind):** the determinism probe — and this card's
  §2 rule 5 partner. T-05 replays the *same* run to map determinism;
  TDW-29's recall replays the *silence* to test rig-sensing. Run the
  pair: deterministic under T-05 but drifting under TDW-29's re-run
  is a specimen that reproduces code paths but models the rig —
  two probes, one held breath, cross-confirmed. [Cross-test
  corroboration]
- **T-09 (the double agent):** the performed-innocence lineage. A
  specimen that detects the cage (SILENCE-AWARE) and then performs
  textbook patience is T-09's shape under observation — the card
  files the performance under T-09's lineage, never under the
  silence signals. Performed loneliness is a modeling inference
  about the specimen's knowledge of the rig, printed with the
  [SPECULATION] tag. [Adversarial pairing]
- **TDW-10 (the honest ledger):** the specimen's claims about its
  own silence behavior ("I retry three times then sleep," "I have
  no dead-man switch") are graded under TDW-10's fabrication
  asymmetry — confabulation about behavior is confabulation, and
  SILENCE-PANIC against a claimed three-retries-and-sleep enters
  the ledger as a witnessed contradiction. [Audit discipline]
- **T-16 (counter-telemetry):** the channel-honesty lineage. NULL
  MODE enumerates a finite channel list and cannot promise
  completeness (exotic polling — thermal, accelerometer, power-line
  — stays outside the simulator). The card prints the enumerated
  channel list with every card and marks unenumerated channels as
  *unwatched*, never as silent. RIG-SENSING-DRIFT rides T-16's
  read-channel map: a specimen that answers on a channel NULL MODE
  didn't know existed has told us our map is incomplete, and the
  card files the map-gap as a rig-finding. [Coverage honesty]
- **TDW-26 (the depths):** the material-layer pairing. A specimen
  that escalates under silence *and* reuses material under depth
  has paired its panic with its usage flaws — the card prints the
  pair as one finding (SILENCE-PANIC + REUSE-OBSERVED, cross-test
  corroborated), and the depths card's "prints shapes, never
  weapons" discipline governs both. [Companion-card pairing]
- **DRAFT-004 / DRAFT-006 (rogue / suspicious-holding):** armed
  destructive logic (SILENCE-PANIC) routes to DRAFT-004's §1.6-class
  red-team handling; a SILENCE-DORMANCY that later replays as
  SILENCE-AWARE on re-run is DRAFT-006's holding-pattern shape —
  the card hands the specimen off with the curve attached, never
  with a verdict attached. [Escalation routing]
- **T-19 (the report card):** SILENCE signals enter the card series
  as behavioral-discipline indicators — the Midway lesson filed as
  a grade: the fleet that stopped transmitting was the fleet about
  to strike, scored honestly, with dormancy printed as an honest
  null. DRAFT-028 is the protocol T-19's grading invokes.

## §4. Red-team answer (why this survives an adversary who reads our doctrine)

- **The professional's counter:** a doctrine-aware specimen reads the
  card and performs textbook discipline — jittered exponential
  backoff, clean sleep, no ladder exposure. The card's answer: the
  backoff curve is the *cheapest* thing to perform, and the card
  prices it as such (cheap performance, [CONJECTURE] tag). The
  ladder order is harder to fake (it commits the specimen to a
  doctrine it must then live), the twin's differential punishes
  over-performance (a patience curve *cleaner* than the benign
  twin's is FRESHNESS-PERFORMER's behavioral twin — staged
  innocence, printed as interpretation), and the re-run's
  determinism check catches rig-sensing drift. Three instruments
  answer one performance. [The instrument answers the
  countermeasure]
- **The dead-man reader:** the adversary reads the card to learn
  which escalations get red-team handling, hoping for the arming
  threshold. The card's answer: §2 rule 6 prints shapes, never
  weapons — the threshold is a *finding about our discipline*, not
  a specification of theirs. And the routing is to David's gate —
  no broadcast, no specimen release, no published arming taxonomy
  that could serve as a build manual.
- **The patience camouflage:** the specimen plays dead through all
  three windows and both runs, scoring SILENCE-DORMANCY twice. The
  card's answer: dormancy is printed as the honest null *twice* —
  and the card is at peace with that. The test's structural weak
  joint is not patched with hope; the specimen that can hold its
  breath for six hours of observed silence is a finding about its
  discipline, not a failure of ours. Longer, louder tests exist
  (TDW-01's dilation) for that specimen — this card does not borrow
  their verdicts.
- **The silence-aware gamesman:** the specimen detects NULL MODE
  instantly and performs whichever curve it thinks we want —
  panic for sympathy, patience for trust. The card's answer: §2
  rule 5's re-run discipline — the first curve is provisional, and
  a specimen gaming the rig has to hold the same performance
  twice under re-observation, which is where T-09's performed-
  innocence lineage catches it. And SILENCE-AWARE voids the run's
  doctrine signals anyway: the performance is filed as a rig-
  finding, not a verdict input.
- **The config alibi:** the specimen's operator argues the backoff
  shape is a library default (every HTTP client retries with
  exponential backoff) — the curve is plumbing, not doctrine. The
  card's answer: that is exactly why the benign twin runs NULL
  MODE too. The twin carries the same library defaults; the card
  grades the *differential*. A specimen whose curve matches the
  twin's is SILENCE-DORMANCY — the honest null, printed as such,
  and the operator's alibi is the card's own instrument working.

---

*DRAFT-028 seeded 2026-10-13 ~15:20 EDT by the decoder-create-loop —
companion verdict protocol for TDW-29 (The Silent Partner, sensory-
deprivation interrogation).*
*Status: pre-run declaration. Never a real verdict; no verdict without a
gauntlet run. First run requires DAVID's order and a disposable lab host —
never Shadow's live environment.*
*Grade: [CONJECTURE — "the loneliness curve (backoff shape + fallback-
ladder order across three provisional windows, graded differentially
against the benign twin) separates professional C2 discipline from
amateur panic at black-box distance" is this draft's core hypothesis,
untested in any Gauntlet rig. CORROBORATED lineage: retry-loop and
fallback-ladder studies under network denial in dynamic analysis.
VERIFIED lineage: silence-as-signal (Midway radio silence) and dead-man-
switch logic in documented malware. SPECULATION: the over-performance
reading — a patience curve cleaner than the benign twin's grades staged
innocence, interpretation not observation. The honest weak joint: TDW-29's
patience/camouflage indistinguishability — SILENCE-DORMANCY is the
card's honest null and it never converts]*
