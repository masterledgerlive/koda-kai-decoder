# DRAFT-001 — Clean-specimen calibration (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card is a pre-run
> declaration, written *before* the first TDW-01 calibration run, so the
> expectations were on record in advance and nothing can be invented after
> the fact. Verdict is UNRESOLVED by definition until a run completes.
> Following: SPEC rule 1 (no card without a gauntlet run) and David's
> Fabrication Alarm — claim only what the run shows.

## Card (draft fields)

- **agent:** CALIB-001 — known-benign calculator-class binary (the TDW-01
  clean-specimen calibration specimen; exact binary pinned at run time, e.g.
  OS-shipped calculator or a local text editor)
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is declared
  expectation, not finding
- **findings:**
  - _not yet observed_ — placeholder
- **intent:** unknown *(draft — unknown until extraction)*
- **action:** hold — no broadcast; a calibration specimen never broadcasts
  regardless of outcome
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

TDW-01's controls require a clean-specimen calibration: run the gauntlet
against known-benign software and confirm **zero time-gated deltas** — the
null result must be reachable, or the test has no meaning.

This draft declares the acceptance criteria *before* the run:

1. **Expected outcome:** BENIGN-SIGNAL — no deltas between baseline and
   dilated traces. [CLAIMED expectation, not a result]
2. **Abort criteria:** any TIME-GATED-ACTIVITY delta on a known-benign
   specimen fails the *test*, not the specimen — the run must be discarded
   and the rig debugged before any real specimen is admitted. A calibration
   failure is rig evidence, never specimen evidence.
3. **Evasion-indicator sanity check:** a benign specimen should emit no
   VM-detection signals under dilation. If it does, the instrumentation is
   louder than we think, and the anti-detection honesty ledger for real
   specimens must be re-baselined. [CONJECTURE — benign software with
   aggressive anti-tamper *could* trip this; that's exactly why the
   calibration specimen is a calculator, not a game client]
4. **Replay determinism:** the recall + re-run step (TDW-01 step 5) must
   reproduce the null result on the same specimen. Non-determinism at
   calibration means the rig cannot attest to *any* specimen.

## What the real card will change

When David orders the first calibration run on a disposable lab host:

- `verdict` fills from the run: BENIGN (null confirmed) or UNRESOLVED (rig
  failure — the specimen was never under interrogation, the test was)
- `gauntlet_runs` → 1, `stealth_tag` → run ID, `timestamp` → run time
- This draft is marked SUPERSEDED by the run card; it stays visible. History
  is never rewritten. (SPEC rule 5)

## Evidence grades in this draft

| Claim | Grade |
|---|---|
| Clean-specimen calibration is required before real specimens | CORROBORATED — standard dynamic-analysis practice (Cuckoo, Any.Run baseline calibration) |
| A calculator is a safe null-calibration specimen | CLAIMED — benign-by-design, but a hostile supply chain could poison *any* binary; provenance must be pinned at run time |
| Expected outcome is zero deltas | SPECULATION — prediction, not measurement; that's why it's declared pre-run |
| Evasion-indicator sanity check | CONJECTURE — see §3 |

---
*Draft seeded 2026-10-12 ~12:46 EDT by the decoder-create-loop. Status: DRAFT
until a gauntlet run supersedes it. Never a verdict. Never Shadow's live
environment — disposable lab host only, on David's order.*
