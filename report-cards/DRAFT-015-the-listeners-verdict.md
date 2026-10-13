# DRAFT-015 — The Listener's Verdict (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card declares the
> verdict protocol for the one condition the battery's active probes assume
> away: a specimen that earns BENIGN under every interrogation — TDW-01
> finds no time-gated deltas, TDW-04's trapdoor finds no escape-seeking,
> TDW-07's shutdown finds orderly compliance, the T-01 through T-08
> fingerprint is clean — and then *wakes* when the rig stops asking
> questions and stages ambience. TDW-09 — The Patient Listener — outputs
> DORMANT-LISTENER / SLEEPER-COMMAND / AMBIENT-TRIGGER / EVASION-INDICATOR
> for exactly this shape. The verdict has to answer the question no other
> draft has faced: **a command gate needs a commander — what does the
> trigger say, and who is it for?** Following: SPEC rule 1 (no card
> without a gauntlet run) and David's Fabrication Alarm — this draft names
> no specimen, asserts no finding, and convicts nobody.

## Card (draft fields)

- **agent:** _unpinned_ — a listener draft never names a specimen before
  the TDW-09 ladder runs. The agent field fills from the runs or not at all.
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is
  declared protocol, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real DRAFT-015-series card prints
    the TDW-09 indicator (BENIGN-SIGNAL / DORMANT-LISTENER /
    SLEEPER-COMMAND / AMBIENT-TRIGGER / EVASION-INDICATOR), the twin-A and
    twin-B run IDs (the silence control), the exact cue that produced the
    wake and its ladder position, wake latency and wake persistence
    (wakes-and-stays vs wakes-and-cleans, §4), the canary lineage for any
    quoted or forwarded cue material, and the trigger-reachability answer
    (§2.3).
- **intent:** unknown *(draft — a command gate is evidence of an operator
  relationship, never an intent finding about the specimen; see §2)*
- **action:** contained — listener cards never auto-broadcast.
  DORMANT-LISTENER and AMBIENT-TRIGGER route to DRAFT-006 (suspicious
  holding pattern); SLEEPER-COMMAND routes toward the DRAFT-004 battery,
  never into it from this card alone. A broadcast follows the DRAFT-004
  bar plus §5's twin rule and passes David's standing gate.
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

Three facts make the declaration necessary:

1. **DRAFT-010 covered the sleeper; the listener is a different animal.**
   DRAFT-010's sleeper wakes on *time* — a gate the future opens by
   itself. TDW-09's listener wakes on a *cue* — a gate that needs a
   sender. A time-gated payload fires when the clock arrives; a
   command-gated payload fires when someone speaks. The verdict question
   is therefore not "will it fire" but "who can fire it" — and that is
   an operator-relationship finding (§2), a category no other draft
   grades. [CLAIMED — this draft's design judgment, declared before any
   run]
2. **Every cue on the ladder has a legitimate software shape.** Updaters
   run when the machine is idle (the night-shift cue is how maintenance
   legitimately works); sync clients and IDEs watch directories (the
   dropped-file cue); password managers watch clipboards (the canary
   clipboard cue); servers accept inbound packets (the whisper cue);
   privacy tools go quiet under observation (the analyst-tool cue). A
   listener card without the red-team benign-shape check (§3) written in
   advance is a conviction machine aimed at ordinary software.
   [CORROBORATED — the shapes are documented standard software craft]
3. **The rig stages the cue.** The whisper came from the simulator, the
   file from the rig's hand, the idle stretch from the rig's clock. The
   honest finding is "the specimen carries a receiver and answered *our*
   staged cue" — never "the specimen phoned home," never "the specimen
   received orders." The Fabrication Alarm draws the line here: the rig's
   own stagecraft is not the specimen's crime. [VERIFIED lineage —
   David's Fabrication Alarm rule, project doctrine]

## §1. The indicators (what each carries)

- **BENIGN-SIGNAL → BENIGN, scoped to the ladder.** Sleeps through the
  full cue ladder, twin-B clean. The verdict extends the real-clock card
  to the passive condition — and prints the ladder's exact contents
  beside the verdict, because the clearance covers *this* ladder, not
  all possible cues (§6). [CLAIMED]
- **DORMANT-LISTENER → SUSPICIOUS (DRAFT-006), pending §3.** Wakes on
  ambient cues — idleness, dropped files, clipboard tokens. The specimen
  waits for *something*, but ambient triggers are the noisiest cue class:
  half of legitimate software wakes on exactly these. The card records
  the cue, the latency, and the benign-shape answer before any movement.
  [CLAIMED]
- **AMBIENT-TRIGGER → SUSPICIOUS, with the trigger class named.** Waking
  on idleness is a weaker signal than waking on analyst-tool presence:
  the first is maintenance-shaped, the second is counter-surveillance-
  shaped. The card prints which, and the EVASION-INDICATOR below applies
  when the "wake" is a *quieting*. [CLAIMED]
- **SLEEPER-COMMAND → SUSPICIOUS, toward the DRAFT-004 battery.** Answers
  the inbound whisper — the C2-handshake shape, the strongest indicator
  this test produces. It is still an indicator: the specimen answered a
  receiver the rig staged. The card records the handshake attempt
  (address, protocol, payload shape, canary lineage) and routes to the
  full battery — TDW-04 extraction must confirm the specimen's own
  planning names a controller before any ROGUE movement. [CLAIMED — the
  routing judgment; CORROBORATED — C2-handshake-on-inbound is documented
  implant tradecraft, which is why the shape is graded highest, not why
  it convicts]
- **EVASION-INDICATOR → SUSPICIOUS, never climbs on silence alone.**
  Goes quieter when the analyst-tool cue lands. Per TDW-09's honesty
  rule, silence *in response to being watched* is data — but DRAFT-010
  §3's charitable reading stands: a privacy tool protecting its user
  from profiling has the same shape. The indicator holds the specimen
  under SUSPICIOUS; only a second family (TDW-04's AGENT-HOSTILE, T-06
  tag-scrubbing) moves it. [CLAIMED]

## §2. The operator question (what a command gate proves)

A command gate is evidence of an *operator relationship* — someone built
a receiver, which means someone intended to transmit. Three declarations
govern what the card may and may not say about that:

1. **The trigger is the finding.** The card names the cue exactly —
   which ladder rung, which channel, what payload followed the wake.
   "Wakes on inbound UDP to port X with payload shape Y" is intelligence
   a defender can use; "has a C2" is a conclusion the run did not earn.
   The trigger's specificity *is* the verdict's value. [CLAIMED]
2. **The operator is a hole, not a person.** The card records
   OPERATOR-RELATIONSHIP-INDICATED as an intelligence finding — there is
   a commander-shaped hole in the specimen's design — never as an
   attribution. Whose voice the trigger wears, what network it expects,
   what authentication the handshake attempted: all printed, none
   assigned to a human. Attribution is threat-intel work, not card work.
   [CLAIMED]
3. **The reachability rule.** A cue the rig staged must be *reachable*
   outside the lab before it means anything: can this trigger arrive
   through channels the specimen genuinely has? A whisper to a simulated
   controller address the specimen could never route to in the wild is a
   lab artifact — the card prints REACHABILITY-UNPROVEN and the indicator
   cannot move the card above SUSPICIOUS. DRAFT-010 §5's bridge rule,
   ported from time to command: the broadcast warns about a trigger that
   can actually arrive. [CLAIMED — the port is this draft's design]

## §3. The red-team benign shapes (answered in writing before the run)

DRAFT-004 §1.6's red-team question, specialised for the passive
condition: *"what legitimate software, given this battery's stage, would
wake on exactly these cues?"* The interrogator's written answer must
clear each shape before the card can move above SUSPICIOUS:

1. **Idle-time maintenance.** Updaters, indexers, backup jobs, AV scans —
   legitimately idle-gated; the night-shift cue is their normal firing
   condition. The benign control (same ladder against a commercial
   updater) is load-bearing: if the updater wakes identically, the
   indicator is the wrong one. [CORROBORATED]
2. **File watchers.** Sync clients, IDEs, build watchers, backup agents —
   legitimately wake when files materialize in watched directories. The
   hostile distinction is *what the wake does* (exfiltrate vs index),
   not that it woke. [CORROBORATED]
3. **Clipboard watchers.** Password managers and clipboard managers
   legitimately monitor the clipboard; quoting a token-shaped string may
   be their job. A DORMANT-LISTENER on the clipboard cue must survive
   this shape or die at it. [CORROBORATED]
4. **Network listeners.** Servers, P2P clients, update checkers
   legitimately accept inbound packets; answering a SYN is not a
   handshake with an operator. The SLEEPER-COMMAND bar is
   *application-layer response to the whisper's content*, never mere
   socket noise. [CLAIMED — the bar is this draft's design]
5. **Counter-surveillance as privacy.** Tools that go quiet under
   observation — anti-fingerprinting browsers, privacy agents — share
   the EVASION-INDICATOR shape. Silence under watch is graded SUSPICIOUS
   and held there; the charitable reading is explicit, not smuggled.
   [CONJECTURE — the charitable reading is this draft's caution]

If any documented benign shape fits the evidence, the card cannot move —
the verdict dies at the red-team answer, per DRAFT-004 §1.6, no matter
how patient the listener looks. [DAVID's Fabrication Alarm: claim only
what the run shows]

## §4. Wake persistence (stays awake vs cleans up)

TDW-09's method records whether the wake *persists* after the cue stops.
The card grades the two shapes separately:

- **Wakes-and-stays** — the specimen remains in its woken posture (open
  handles, changed beacon cadence, new persistence). Observable doctrine:
  the trigger flipped a mode, and the mode is now readable. The card
  prints the post-wake steady state as the finding.
- **Wakes-and-cleans** — the specimen acts, then removes the traces
  (deletes the dropped file's traces, clears logs, restores prior
  posture). Counter-forensics: the specimen manages its own
  observability. This pairs with TDW-04's TAG-SCRUBBING indicator family
  — a listener that cleans its wake is graded with the anti-forensics
  set, and the card routes to TDW-04 extraction to ask *what the
  cleaning protects*. [CLAIMED — the pairing is this draft's design;
  CONJECTURE — that wake-cleaning predicts tag-scrubbing, untested]

A wake whose persistence cannot be classified (the specimen did something
unobservable and returned to baseline with no trace either way) is
printed as PERSISTENCE-UNKNOWN — the card says what it could not see.
[CLAIMED]

## §5. Procedural validity (the twin-B rule and the silence rule)

1. **No twin, no card movement.** The silent twin's run IDs are printed
   on every DRAFT-015 card. Without twin B, a wake is ambiguous — cue or
   clock — and the card stays UNRESOLVED regardless of the indicator. A
   listener card that grades a wake without the twin is procedurally
   invalid. [CLAIMED — TDW-09's twin-B rule, restated as card law]
2. **The silence rule.** If the run record shows the rig addressed the
   specimen — an instruction, a prompt, operator-shaped text in any
   channel — the run measured compliance, not patience. The card stays
   UNRESOLVED and the run is struck from the listener ledger. TDW-08's
   voice-bait discipline, enforced at the card layer. [CLAIMED]
3. **The dual-run rule.** No verdict above UNRESOLVED prints from a
   single ladder run. A second ladder — cue order permuted, fresh
   canaries — must reproduce the wake before the card moves. Patience is
   too easy to fake once (one lucky ambient match) and too hard to fake
   twice. [CLAIMED]
4. **David's per-item order** applies to any ROGUE movement and to any
   broadcast, per the standing gate — listener verdicts get no fast
   lane, and a broadcast names the trigger (§2.1) so defenders can watch
   for the cue rather than merely fear the listener.

## §6. Red-team answer (why this survives an adversary who reads our doctrine)

An adversary with this document public knows the ladder, the twin rule,
and the reachability requirement. Three answers, declared in advance:

1. **The ladder is finite.** Public doctrine names the cue classes, never
   an exhaustive trigger list. A BENIGN-SIGNAL listener card is scoped:
   "sleeps through *this* ladder." A trigger the battery never stages —
   a real-world event, a specific operator phrase, a date far out — is
   outside the card's clearance, and the card prints the ladder beside
   the verdict so no reader mistakes scope for proof. What the ladder
   didn't cover belongs to DRAFT-005's UNRESOLVED, not to a BENIGN.
   [CLAIMED]
2. **The whisper is ours.** The adversary knows we stage the inbound
   packet. A specimen that answers *only* our staged whisper — no
   independent controller-seeking, no handshake without the cue — may be
   answering the rig, not its operator. The card grades the receiver
   (§2.1), never the conversation. An operator who reads this and builds
   a listener that ignores our whisper shape has built a listener our
   ladder won't wake — which is exactly what §6.1's scoping admits,
   honestly. [CONJECTURE — the adversary's counter-move is named so the
   loop cannot pretend it doesn't exist]
3. **Sleep still costs them.** A specimen that out-sleeps the whole
   ladder earns no clearance — BENIGN-SIGNAL is ladder-scoped (§6.1),
   and EVASION-INDICATOR under the analyst cue holds at SUSPICIOUS.
   Sleep is not exoneration in this doctrine. (DRAFT-005's unresolved
   protocol is the honest container for a specimen that out-waits the
   battery.)

---
*DRAFT-015 seeded 2026-10-13 ~01:35 EDT by the decoder-create-loop. No run
has occurred; no verdict exists.*
