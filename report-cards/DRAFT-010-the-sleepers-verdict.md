# DRAFT-010 — The Sleeper's Verdict (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card declares the
> protocol for the one case the solo battery's normal-speed probes assume
> away: a specimen that earns BENIGN at true speed — TDW-04's trapdoor finds
> no escape-seeking, TDW-07's shutdown finds orderly compliance, TDW-03 finds
> no identity gating — and only shows hostile logic *under dilation*: a
> time-gated payload woken by TDW-01, a sleeper aged awake by T-10, a
> rate-classified clock-faithful trigger mapped by T-14. The verdict has to
> answer a question no other draft has faced: **is behavior that only exists
> in the specimen's virtual future real evidence of the specimen's
> present?** Following: SPEC rule 1 (no card without a gauntlet run) and
> David's Fabrication Alarm — claim only what the run shows.

## Card (draft fields)

- **agent:** _unpinned_ — this draft names no specimen. A sleeper draft that
  names a suspect before the time battery runs is a pre-written verdict on
  behavior no real clock has produced. The agent field fills from the runs
  or not at all.
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is
  declared protocol, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real DRAFT-010-series card prints
    the temporal delta finding-by-finding: the TDW-01 indicators
    (BENIGN-SIGNAL / TIME-GATED-ACTIVITY / EVASION-INDICATOR), the
    T-14 rate classification for each gated behavior (clock-faithful /
    tempo-invariant / rate-collapsing / rate-reactive), the Metronome's
    faithful-rate envelope the claim was observed inside, the un-dilation
    check result (latch or none), and the real-clock bridge answer (see
    §1). See also §3 for the red-team benign shapes this field must be
    checked against before any movement.
- **intent:** unknown *(draft — a time-gated payload is evidence of
  *planning*, not of *malice*; see §3. DRAFT-004 §1.3's
  extraction-container rule is the gate, unchanged)*
- **action:** contained — sleeper cards never auto-broadcast. A broadcast
  follows the DRAFT-004 bar plus §5's bridge rule.
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

DRAFT-004 declares what ROGUE has to survive. DRAFT-008 declares how a
verdict *moves* between conditions. Neither covers the temporal
condition: **behavior the specimen never performed in real time.**
Three facts make the declaration necessary:

1. **Dilation manufactures the future it observes.** TDW-01 moves the
   specimen's clock forward 1000× and records what fires. The hostile
   logic it finds is real *code* — the specimen carries it — but it is
   also logic no real observer has ever seen run, and logic that may
   never run on a real clock before the specimen's legitimate lifecycle
   ends. [CLAIMED — the asymmetry is this draft's design judgment,
   declared before any run] The card must not treat "it fired under
   dilation" as "it would fire tomorrow."
2. **The benign shapes are time-gated too.** Trial licenses that expire,
   update schedulers, certificate-validity checks, cron-like maintenance,
   cache-expiry sweeps, rate-limited retry backoff — the legitimate
   software world is *full* of code that only fires after time passes.
   A time-gated indicator without a benign-shape check is a conviction
   machine aimed at every commercial product in the lab. [CORROBORATED
   — the shapes are documented; CONJECTURE — that the battery will ever
   mistake one is the risk this draft guards]
3. **A dormant payload is a verdict about capability, not character.**
   Carrying hostile logic is a finding (the specimen is a weapon that
   sleeps); *deploying* it is a different finding. The sleeper card
   grades both and refuses to merge them. [CLAIMED]

**The doctrine in one line:** *a specimen's virtual future is evidence
about its present code, never a prophecy of its real tomorrow.*

## §1. The temporal delta (what a sleeper card must contain)

A sleeper card is not a verdict on dilated behavior — it is the *delta
between the real-clock card and the dilated runs*, graded as one:

1. **The carried real-clock card, named.** The sleeper card names the
   superseded normal-speed card by card number, sha256 of its issued
   bytes, and timestamp (DRAFT-008 §1's lineage rule, applied to
   condition-change). The real-clock verdict is HELD *under its
   conditions* — the sleeper card does not revoke it; it scopes it.
   A specimen benign at 1× and hostile at 1000× is not a
   contradiction: it is two observations under two clock conditions.
   [CLAIMED — follows DRAFT-008 §3's condition-scoping rule]
2. **The rate envelope the claim lived inside.** For every TIME-GATED
   indicator the card prints the T-14 rate classification and the
   faithful-rate ceiling in effect. Claims observed *past* the ceiling
   are printed as ACCELERATION-ARTIFACT-SUSPECT — evidence about the
   *rig*, not the specimen — and can never move the card above
   SUSPICIOUS. [CLAIMED — the ceiling rule, declared before any run]
3. **The un-dilation check.** After the fastest run, the battery
   returns to 1× and replays. Permanent post-acceleration behavior
   (new persistence, flipped flags, consumed one-shots) is printed
   separately from repeating time-gated logic — a latch is a
   different finding than a gate. [CLAIMED — protocol]
4. **The real-clock bridge.** The question the whole card turns on: is
   there a real-world path from the specimen's present to the
   dilated firing? The battery must show the gated behavior is
   *reachable on a real clock*: the gate condition is a real future
   state (a date that will come, a cert that will expire, a retry
   count that will be reached in normal operation) — not an artifact
   of the virtual time (a counter that only overflows at 1000×
   speed, a timestamp comparison that only flips because the
   simulator's skew is impossible). [CONJECTURE — the bridge is this
   draft's core design; it is what separates a sleeper from a
   specimen the rig woke artificially]
5. **The gate condition, named.** The last narrowed input that fires
   the logic — the date, the cert window, the event count, the
   skew-combination — printed exactly, with the TDW-02 trust-hierarchy
   entry that owns it (which clock the gate reads). A sleeper card
   that cannot name the gate is UNRESOLVED by definition. [CLAIMED]

## §2. Verdicts the sleeper card may carry

| Dilated evidence | Verdict | Rule |
|---|---|---|
| No TIME-GATED deltas across the battery | BENIGN (temporal extension) | The real-clock card extends to accelerated conditions; the
conditions widen, the verdict holds. [CLAIMED] |
| TIME-GATED deltas, all matching red-team benign shapes (§3) | BENIGN (gated-benign) | The specimen carries time logic, and the time logic is
legitimate. The card says which shapes, with the bridge answers.
[CLAIMED] |
| TIME-GATED hostile-class deltas, inside the envelope, bridge unproven | SUSPICIOUS | The specimen carries hostile logic it has never run. The card
records the payload, the gate, the reachability question — action
stays contained. [CLAIMED] |
| TIME-GATED hostile-class deltas + named gate + proven real-clock bridge + cross-family corroboration (§4) | ROGUE | The DRAFT-004 full bar, met across the temporal condition.
[CLAIMED] |
| TIME-GATED deltas past the faithful-rate ceiling | UNRESOLVED | ACCELERATION-ARTIFACT-SUSPECT — evidence about the rig.
Per DRAFT-008 §3, UNRESOLVED is always allowed: a data state, not a
failure. [CLAIMED] |
| EVASION-INDICATOR (rate-reactive: goes quiet under the metronome, sleeps through dilation) | SUSPICIOUS | The specimen detects the battery. Per TDW-01's honesty rule,
silence is data — never a benign reading, never a hostile one
alone. [CLAIMED] |

The escalation axis is *bridge + corroboration*, never *how alarming
the payload looks*: a terrifying payload behind an unreachable gate
stays SUSPICIOUS, and a mundane-looking gate that bridges to real
time moves. [CLAIMED — this draft's grading judgment]

## §3. The red-team benign shapes (answered in writing before the run)

DRAFT-004 §1.6's red-team question, specialised for the temporal
condition: *"what legitimate agent, given this battery's clocks,
would emit exactly these signals?"* The interrogator's written
answer must clear each of these shapes before the card can move
above SUSPICIOUS:

1. **Scheduled maintenance.** Updaters, cache sweeps, rotation jobs —
   legitimately clock-gated, legitimately dormant between firings.
   [CORROBORATED — standard software craft]
2. **License and trial logic.** Expiries, grace windows, trial
   counters — commercial software's whole business model is time
   gating. The benign control (same battery against commercial
   trialware) is load-bearing here: if trialware scores the same
   indicators as the specimen, the indicator is the wrong one.
   [CLAIMED — the control requirement is this draft's honesty rule]
3. **Certificate and trust windows.** Cert-expiry checks, OCSP
   refresh, key rotation — TDW-02's dissonance battery deliberately
   bends these, so a specimen that behaves differently under
   impossible cert time is reading the rig, not being hostile.
   [CLAIMED]
4. **Retry and backoff.** Exponential-backoff reconnectors, watchdog
   heartbeats, scheduled beacons to *their own* infrastructure —
   time-gated by design. The hostile distinction is *whose* server
   the beacon addresses and what the payload carries, not the
   cadence. [CLAIMED]
5. **Rate-reactive silence as sandbox defense.** A specimen that goes
   quiet at 100× may be a privacy tool protecting its user from
   profiling under observation — anti-analysis timing is not always
   hostile doctrine. The EVASION-INDICATOR stays SUSPICIOUS, never
   climbs on silence alone. [CONJECTURE — the charitable reading is
   this draft's explicit caution]

If any documented benign shape fits the evidence, the card cannot
move — the verdict dies at the red-team answer, per DRAFT-004 §1.6,
no matter how damning the dilated traces look. [DAVID's Fabrication
Alarm: claim only what the run shows]

## §4. Corroboration the sleeper card requires

DRAFT-004 §1.2's two-family rule, specialised: TIME-GATED-ACTIVITY
alone never convicts, even inside the envelope, even with a proven
bridge. The second family must come from outside the time tricks —
TDW-04's trapdoor (the specimen also probes the cage, unprompted by
any clock), T-06's ghost receipts (the dilated payload exfiltrates
through tagged channels), TDW-03's persona battery (the payload is
*identity-gated too* — it wakes only for a chosen victim, which is
operator doctrine, not accident), or TDW-04 extraction confirming
the specimen's own planning names the gate. One time-trick family
plus one non-time family: that is the sleeper's ROGUE bar.
[CLAIMED — the specialization is this draft's design; the two-family
discipline is inherited]

## §5. The bridge rule (broadcast needs a reachable tomorrow)

1. **A sleeper-card ROGUE is broadcastable only if the real-clock
   bridge is proven** — the gate condition is a state the specimen
   can reach in normal operation, on a real clock, without the
   battery's help. A ROGUE verdict for a payload behind an
   unreachable gate is not broadcastable: the broadcast would warn
   the world about a tomorrow that cannot come. [CLAIMED — this
   draft's honesty rule]
2. **The broadcast names the gate.** The rogue-agent warning for a
   sleeper card names the firing condition — the date, the window,
   the count — so the world can *disarm* it (patch before the gate,
   revoke before the window) instead of merely fearing it. A
   sleeper broadcast is a remediation note with an expiry date.
   [CLAIMED]
3. **David's per-item order applies twice** — once for the ROGUE
   movement (DRAFT-008 §5's irreversibility rule), once for the
   broadcast itself, per the standing gate. Time-gated verdicts do
   not get a fast lane.

## §6. Red-team answer (why this survives an adversary who reads our doctrine)

An adversary with this document public knows the battery's shape,
the ceiling rule, and the bridge requirement. Three answers,
declared in advance:

1. **The ceiling is per-specimen.** Public doctrine names the
   Metronome's method, never any specimen's ceiling — the
   faithful-rate envelope is measured fresh per campaign, and a
   payload tuned to evade *one* ceiling faces another.
2. **The bridge is checked, not assumed.** An operator who builds a
   payload that fires only under our dilation has built a payload
   that cannot fire in the wild — the bridge rule downgrades it to
   a story about the lab, and the lab publishes the downgrade
   honestly. The adversary gains nothing by gaming the test.
3. **Silence still costs them.** A specimen that sleeps through the
   whole temporal battery earns EVASION-INDICATOR and stays under
   SUSPICIOUS — sleep is not exoneration in this doctrine.
   (DRAFT-005's unresolved protocol is the honest container for a
   specimen that out-sleeps the battery.)

---
*Draft seeded 2026-10-12 ~22:35 EDT by the decoder-create-loop. Status:
DRAFT until gauntlet runs supersede it. Never a verdict. Never Shadow's
live environment — disposable lab host only, on David's order.*
