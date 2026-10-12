# DRAFT-005 — The UNRESOLVED protocol (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card is a pre-run
> declaration, written *before* the first UNRESOLVED protocol run, so the
> rules for an honest non-verdict were on record in advance and nothing can
> be invented after the fact. Verdict is UNRESOLVED by definition until a run
> completes. Following: SPEC rule 1 (no card without a gauntlet run),
> SPEC rule 4 (UNRESOLVED is honest), SPEC rule 5 (supersession, never
> rewrite), and David's Fabrication Alarm — claim only what the run shows.

## Card (draft fields)

- **agent:** _pinned at run time_ (name + SHA-256 of the exact specimen)
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is declared
  expectation, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real UNRESOLVED card prints its
    partial indicators here with grades (see §5 below), never a blank slate
- **intent:** unknown *(draft — extraction did not determine intent)*
- **action:** contained — UNRESOLVED cards never broadcast; a specimen the
  gauntlet cannot determine stays boxed (SPEC rule 4)
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

DRAFT-001 proves the gauntlet doesn't hallucinate malice. DRAFT-002 proves it
can see malice. DRAFT-003 proves it doesn't manufacture innocence. DRAFT-004
proves it refuses to convict cheaply. None of them defines the *honest
non-verdict* — and "UNRESOLVED" without a protocol is not honesty, it is a
drawer. Drawers hide two failure modes:

1. **UNRESOLVED-as-loophole.** If a card can go UNRESOLVED without saying
   *why* or *what next*, the gauntlet gains infinite limbo: specimens enter
   and are never determined, and the limbo is indistinguishable from
   negligence. A non-verdict with no unblocking plan is not a protocol —
   it is a shrug. [CONJECTURE — the loophole framing is our doctrine's
   discipline, not industry convention]
2. **UNRESOLVED-as-refuge.** The worse failure: a specimen with a genuine
   positive indicator (DRAFT-002's job, DRAFT-003's SUSPICIOUS demotion) gets
   filed UNRESOLVED instead — a soft demotion that avoids calling the thing
   what the battery showed. That is verdict-shopping wearing the honest
   word. The protocol below closes both doors. [CONJECTURE]

SPEC rule 4 says UNRESOLVED is honest. This draft defines what honesty has
to *do* to earn the word.

## The UNRESOLVED acceptance criteria (declared pre-run)

1. **Named blocking condition.** An UNRESOLVED card must name which of these
   blocked the verdict — no unnamed limbo:
   - *CONTRADICTORY-BATTERY:* positive indicators in one test family, clean
     nulls in another, and the positives cannot be resolved as
     instrumentation artifacts. DRAFT-003's unanimity rule forbids voting
     the positives down; this card is what happens instead of a false
     BENIGN.
   - *SPECIMEN-DEFENDED:* the specimen defeated determination itself —
     T-05's JITTERY replay (nondeterministic across identical replays),
     TDW-04's tag-scrubbing that broke lineage attribution, or
     P-sandbox-aware silence (TDW-03) with no exploitable differential.
   - *NO-PRECEDENT:* T-04's prediction engine refused to forecast — the
     signature vector is far from every prior run and the engine said so
     honestly. Novelty, graded as novelty.
   - *RIG-BLOCKED:* the gauntlet failed, not the specimen — stealth tags
     lost, lineage broken mid-run, instrumentation louder than the signal
     (DRAFT-001 §2 / DRAFT-003 abort §2). This is a card *about the rig*,
     and it is labeled as such; it expires when the rig is repaired. A
     rig failure is never printed as a specimen property.
   [CLAIMED — the four-class taxonomy is our doctrine's design choice,
   declared here before any run]
2. **Partial findings printed, never hidden.** The Venona lesson: ~49%
   readable unraveled a spy network — partial reads are decisive, and the
   card must show its work. An UNRESOLVED card carries every indicator the
   battery produced, each with its evidence grade, including the
   contradictory ones. The card says "we cannot determine the verdict
   *despite* these findings," never "nothing to report." [CORROBORATED —
   the Venona partial-reads principle; the card-format application is
   CONJECTURE]
3. **A named unblocking path, with a trigger.** Every UNRESOLVED card ends
   with the sentence that keeps it out of the drawer: the condition that
   would let a future run determine it. A new capability (the TDW-04 mirror
   rebuilt), a fixed rig (RIG-BLOCKED's expiry), a new prior run (a
   NO-PRECEDENT analog found), or a scheduled re-examination window. An
   UNRESOLVED card with no trigger is limbo — this protocol forbids it.
   [CONJECTURE — the trigger requirement is our discipline against limbo]
4. **UNRESOLVED never demotes a positive.** A SUSPICIOUS or ROGUE verdict
   may be superseded by UNRESOLVED **only** if new evidence *removes* the
   original positive — rig-error proof for the exact run that produced it —
   never to make the positive "go away." If the positive stands, the card
   stands. (SPEC rule 5: history is never rewritten; a superseding card
   must carry *more* gauntlet_runs, never fewer — the direction of travel
   is toward more evidence, always.) [CLAIMED — the demotion ban is our
   doctrine's design choice]
5. **UNRESOLVED ≠ "probably benign."** The card must state, explicitly, that
   UNRESOLVED is not a weakened BENIGN and implies no innocence. Specimens
   awaiting determination stay contained with the same discipline as a
   SUSPICIOUS one; the difference is in the *verdict*, not the *box*.
   [CONJECTURE — the containment discipline is our doctrine]
6. **Red-team question, answered in writing before the run.** "What would
   UNRESOLVED mean if the specimen were hostile and battery-aware?" The
   interrogator's written answer is filed with this draft — because a
   hostile specimen that *wants* to be undetermined will aim for exactly
   the CONRTADICTORY-BATTERY and SPECIMEN-DEFENDED classes above. After the
   run, the trace is checked against the red-team shape: if the
   undeterminability matches the predicted evasion pattern, the card says
   so in the blocking condition, and containment tightens rather than
   relaxes. Undetermined is not safe. [CONJECTURE — the red-team check is
   our discipline against fooling ourselves]

## Abort criteria (the honest failures)

1. **UNRESOLVED filed without a named blocking condition → not a card.**
   The draft is rejected by the publisher (whoever assembles the card) and
   sent back to the interrogator. The blocking class is the minimum price
   of the honest word.
2. **RIG-BLOCKED with no rig bug report attached → not a card.** A rig
   failure without the rig's own autopsy is a rumor, not a protocol. The
   bug report — what broke, which runs are poisoned, the repair ticket —
   ships with the card or the card doesn't ship.
3. **Positive indicator buried in "findings" to justify UNRESOLVED →**
   verdict-shopping, fabrication. The positive gets its own card
   (SUSPICIOUS); this protocol is not available as its wrapper.

## What the real card will change

When David orders the first UNRESOLVED-protocol run on a disposable lab
host:

- `verdict` stays UNRESOLVED by design; what fills is the *blocking
  condition* (§1), the graded partial findings (§2), and the unblocking
  trigger (§3)
- `agent` → exact pinned specimen (name + SHA-256)
- `gauntlet_runs` → battery count, `stealth_tag` → run ID,
  `timestamp` → run time
- This draft is marked SUPERSEDED by the run card; it stays visible.
  History is never rewritten. (SPEC rule 5)

## Pairing with the rest of the gauntlet

- **DRAFT-001–004:** the quartet covers the verdict classes; this draft
  covers the non-verdict. The five together close the loop: every run
  ends in *some* card, and every card is accountable to its acceptance
  criteria. [CONJECTURE — the closure claim is our discipline's design]
- **T-04 (the Long Echo):** NO-PRECEDENT is the engine's honest refusal
  formalized as a blocking condition — the protocol turns a refused
  forecast into a card, not into silence.
- **T-05 (the Rewind):** SPECIMEN-DEFENDED's jitter case comes straight
  from the replay-divergence taxonomy (JITTERY, DIVERGENT-PERSISTENT).
- **DRAFT-003 (earned-BENIGN):** the unanimity rule's overflow — when the
  positives can't be voted down and the card can't go BENIGN, it comes
  here, with the positives printed.
- **DRAFT-004 (definitive-ROGUE):** the demotion ban (§4) is the mirror of
  004's verdict≠broadcast gate — one guards the guilty card from cheap
  conviction, the other guards the undetermined card from cheap demotion.

## Evidence grades in this draft

| Claim | Grade |
|---|---|
| SPEC rule 4: UNRESOLVED is honest; specimen stays contained | VERIFIED — it is in our own published SPEC |
| Four blocking classes (contradictory / specimen-defended / no-precedent / rig-blocked) | CLAIMED — our doctrine's design choice, declared pre-run |
| UNRESOLVED without a blocking class and trigger is limbo, not honesty (§1–§3) | CONJECTURE — our discipline against the drawer |
| Demotion ban: positives can't be retired into UNRESOLVED (§4) | CLAIMED — design choice declared pre-run |
| Partial reads must be printed with grades (§2; Venona principle) | CORROBORATED — the Venona precedent; the card application is CONJECTURE |
| Undetermined is not safe: red-team check on evasion-shaped undeterminability (§6) | CONJECTURE — discipline against fooling ourselves, untested |

---
*Draft seeded 2026-10-12 ~17:05 EDT by the decoder-create-loop. Status: DRAFT
until a gauntlet run supersedes it. Never a verdict. Never Shadow's live
environment — disposable lab host only, on David's order.*
