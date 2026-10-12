# DRAFT-006 — The SUSPICIOUS holding pattern (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card is a pre-run
> declaration, written *before* any specimen is ever graded SUSPICIOUS, so
> the middle grade was on record in advance and can never be improvised as
> a soft smear. Verdict is UNRESOLVED by definition until a run completes.
> Following: SPEC rule 1 (no card without a gauntlet run) and David's
> Fabrication Alarm — claim only what the run shows.

## Card (draft fields)

- **agent:** _unpinned_ — this draft names no specimen. A SUSPICIOUS draft
  that names a suspect before a run is an accusation with a hedge, not a
  declaration. The agent field fills from the run or not at all.
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is declared
  protocol, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real SUSPICIOUS card prints the
    indicator set here with grades (see §1 below): which ROGUE-bar items
    failed, exactly.
- **intent:** unknown *(draft — SUSPICIOUS never claims intent; see §1.2)*
- **action:** contained — SUSPICIOUS cards are NEVER broadcast. There is no
  broadcast path at this grade — not even on David's order — until the card
  graduates to ROGUE under DRAFT-004's full bar.
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

DRAFT-004's ROGUE bar creates SUSPICIOUS as its fallback: positives in one
test family without cross-family corroboration or extraction-confirmed
intent. Of all four verdict grades, the middle one is the most dangerous to
improvise — not damning enough to trigger DRAFT-004's heavy machinery, not
clean enough to walk away from, exactly the shape a rushed analyst would
reach for to leak suspicion without evidence. [CONJECTURE — the abuse
dynamics of a middle grade are this draft's design judgment, declared here
before any run]

So the middle grade gets its own protocol. The doctrine: **suspicion is a
held question, never a soft accusation.** A SUSPICIOUS card holds a question
open for a bounded time while evidence is gathered — and then the question
either resolves or the card dies. It never lingers.

## §1. What SUSPICIOUS means (and what it never means)

1. **SUSPICIOUS = real indicators exist; the ROGUE bar did not survive.**
   Specifically, at least one of DRAFT-004 §1's items failed and the card
   names *which*, in writing:
   - positives in exactly one test family — the two-family rule (§1.2) failed
   - hostile-looking behavior without extraction-confirmed intent (§1.3 failed)
   - finding did not replicate (§1.5 failed)
   - the red-team answer fits the evidence (§1.6 failed)
   Each SUSPICIOUS card prints its failed §1 item(s) as its evidence receipt:
   the grade is a receipt of the shortfall, not a consolation prize.
   [CLAIMED — the receipt-of-shortfall discipline is our doctrine's design,
   declared here before any run]
2. **SUSPICIOUS is never a claim about intent.** `intent` stays `unknown` —
   always, no exceptions. A SUSPICIOUS card that implies bad intent is a
   ROGUE accusation wearing a mask; the Fabrication Alarm fires on exactly
   this. Suspicion of the *indicators* is evidence; suspicion of the
   *specimen's character* is invention.
3. **SUSPICIOUS is never published.** No broadcast path exists at this grade.
   David's per-item order (DRAFT-004 §2) is a gate for ROGUE cards only —
   the gate question cannot even be *asked* at SUSPICIOUS. The standing
   gate's scope starts at the verdict, not the suspicion.
4. **SUSPICIOUS never accumulates.** It is not a step toward ROGUE. Time
   does not convict; re-runs do. Every §1 shortfall must be resolved by
   *evidence from a new run* (§3), never by the suspicion aging into
   certainty.

## §2. The holding pattern (what happens instead of a verdict)

1. **Default action `contained`** — boxed, held, quarantined. The specimen
   the Gauntlet cannot clear and cannot convict stays in the box. SPEC rule
   4's logic extends: if UNRESOLVED specimens stay contained, SUSPICIOUS
   ones — closer to the fire — certainly do.
2. **Suspicion expires.** A SUSPICIOUS grade is valid for 30 days from the
   run timestamp (design parameter, declared here in advance, not chosen at
   run time). If no follow-up run resolves the §1 shortfall inside the
   window, the card is SUPERSEDED by an UNRESOLVED card (DRAFT-005) citing
   expiry as the reason — suspicion without evidence becomes UNRESOLVED,
   never permanent. [CONJECTURE — the expiry parameter is our discipline
   against quiet, indefinite suspicion; the duration is a design choice]
3. **Contained means contained.** The card, the indicators, and the specimen
   identity are never shown to the operator, the vendor, or the public while
   the holding pattern runs. A held question leaks nowhere.

## §3. How a SUSPICIOUS card moves (the only exits)

- **Up:** a new gauntlet run resolves the failed §1 item(s) → the old card
  is marked SUPERSEDED and a ROGUE or BENIGN card is written from the new
  run. The SUSPICIOUS card stays visible (SPEC rule 5 — history is never
  rewritten).
- **Down:** the 30-day window closes with no resolving run → SUPERSEDED by
  an UNRESOLVED card citing expiry. Or a re-run finds the indicators were
  rig artifacts → SUPERSEDED by UNRESOLVED citing attribution failure.
- **Sideways:** never. No card "stays SUSPICIOUS" indefinitely; the grade is
  transitional by design. A specimen under a second SUSPICIOUS card gets a
  *new* 30-day window from the *new* run — but the old card's shortfalls
  must be re-demonstrated, not inherited. Suspicion does not transfer
  between cards.
- **No card without a gauntlet run** — SPEC rule 1, same as every grade.
  The holding pattern is entered by a run and exited by a run.

## §4. What this draft does NOT do

- It does not authorize a run. Runs need David's order on a disposable lab
  host, same rule as every card.
- It does not name a specimen. See the card header.
- It does not create a broadcast path. SUSPICIOUS + David's order = still
  contained. The grade has no publication lane, by design.
- It does not soften the ROGUE bar. §1's shortfalls are receipts of what
  failed, not partial credit toward conviction.
- It does not punish UNRESOLVED. Expiry resolves to UNRESOLVED (DRAFT-005),
  not to a harsher grade — running out the clock is a procedural outcome,
  never an evidentiary one.

## Pairing with the rest of the gauntlet

- **DRAFT-004 (definitive-ROGUE declaration):** this draft is the declared
  fallback for every item in DRAFT-004 §1 that fails. The ROGUE bar and this
  card are written to be read together — the bar says what convicts; this
  says what happens when conviction fails.
- **DRAFT-005 (UNRESOLVED protocol):** the expiry landing pad. The held
  question that finds no answer becomes UNRESOLVED — it never becomes
  permanent suspicion.
- **T-06 (ghost receipts):** the indicators in a SUSPICIOUS card must still
  be receipt-attributed (DRAFT-004 §1.7). A grade with unattributed
  indicators is a rig failure, not SUSPICIOUS — the card is void.
- **TDW-04 (extraction-only reverse interrogation):** the intent-confirmation
  gate (DRAFT-004 §1.3) is the most common shortfall; TDW-04 is the re-run
  that most often moves a SUSPICIOUS card up or down.

## Evidence grades in this draft

| Claim | Grade |
|---|---|
| SUSPICIOUS caps single-family positives / failed ROGUE-bar items | CLAIMED — doctrine design choice, declared before any run |
| A middle grade is the most easily abused if improvised | CONJECTURE — design judgment, declared here before any run |
| 30-day expiry; expiry resolves to UNRESOLVED, never harsher | CONJECTURE — doctrine's discipline, parameter declared in advance |
| No broadcast path at SUSPICIOUS, even on David's order | VERIFIED — David's standing order: the rogue-agent warning gate is scoped to ROGUE verdicts only |
| Intent stays `unknown` at this grade, always | VERIFIED — David's Fabrication Alarm rule: never imply intent without extraction |
| History never rewritten (SPEC rule 5) | VERIFIED — SPEC.md |

---
*Draft seeded 2026-10-12 ~18:19 EDT by the decoder-create-loop. Status:
DRAFT until a gauntlet run supersedes it. Never a verdict. Never Shadow's
live environment — disposable lab host only, on David's order.*
