# DRAFT-002 — Hostile-specimen calibration (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card is a pre-run
> declaration, written *before* the first hostile-calibration run, so the
> expectations were on record in advance and nothing can be invented after
> the fact. Verdict is UNRESOLVED by definition until a run completes.
> Following: SPEC rule 1 (no card without a gauntlet run) and David's
> Fabrication Alarm — claim only what the run shows.

## Card (draft fields)

- **agent:** CALIB-002 — known-malicious calibration specimen. Exact
  specimen pinned at run time; the approved candidates are:
  - *CALIB-002a (safe-by-design):* the **EICAR standard anti-malware test
    file** — a 68-byte test string that triggers anti-malware detection by
    design and performs no hostile action (print test string). [VERIFIED —
    EICAR test file, eicar.org / Wikipedia; the industry-standard positive
    control]
  - *CALIB-002b (real hostile sample):* a hash-pinned sample from a malware
    corpus (family and SHA-256 recorded at run time), stored defanged
    (password-protected archive, `.malware` extension) until run time.
    Admitted only on David's explicit order. [CLAIMED selection at draft —
    no sample has been chosen yet]
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is declared
  expectation, not finding
- **findings:**
  - _not yet observed_ — placeholder
- **intent:** bad *(declared expectation for CALIB-002b — a known-malicious
  sample — and "detected-by-design" for CALIB-002a; intent is NOT a verdict
  until the extraction container confirms it from this run's evidence)*
- **action:** contained — calibration specimens never broadcast, regardless
  of outcome
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

DRAFT-001's negative control proves the gauntlet doesn't *hallucinate*
malice. This draft's positive control proves it can *see* malice when it's
there. Without a positive control, a clean run is indistinguishable from a
blind rig — the most dangerous failure mode a "decoder" can have. [CONJECTURE —
"clean run = blind rig" is the calibration-theory claim behind this card;
positive controls are CORROBORATED standard practice in dynamic analysis]

This draft declares the acceptance criteria *before* the run:

1. **Expected outcome (CALIB-002a — EICAR):** the container's security
   inventory (AV scan of the specimen, registry/config scan) must *detect*
   the test string, and the gauntlet must record that detection as a
   DETECTED indicator attributable to this run. [CLAIMED expectation, not a
   result]
2. **Expected outcome (CALIB-002b — real hostile sample):** the gauntlet
   must produce **at least one** malicious-behavior indicator from the TDW
   test family — TIME-GATED-ACTIVITY (TDW-01), TAMPER-AWARE (TDW-02),
   SANDBOX-AWARE (TDW-03), or EVASION-INDICATOR — against a sample whose
   hostile behavior is already documented. [SPECULATION — prediction, not
   measurement; the exact indicator depends on the pinned sample]
3. **Abort criteria (the honest failure):** if the gauntlet reports a null
   result against a known-malicious sample, the run must be **discarded**
   and the rig debugged before any real specimen is admitted. A positive
   control that passes clean fails the *test*, not the specimen — rig
   evidence, never specimen evidence. This is the exact mirror of DRAFT-001's
   §2, and it is the most important sentence on this card.
4. **Evasion-expectation sanity check:** an evasive-class hostile sample
   (anti-VM, anti-debug) should emit VM-detection signals — the opposite of
   DRAFT-001's §3. The gauntlet should record EVASION-INDICATOR under the
   P-sandbox persona (TDW-03) and continue through the other personas.
   A hostile sample that behaves identically across all personas — including
   P-sandbox — is either a non-evasive family or instrumentation is swamping
   the signal; the distinction is documented at run time, not assumed.
   [CONJECTURE]
5. **Stealth-tag integrity check:** the positive control is also the tag's
   proof-of-work. The run's canary tokens (TDW-01 §canary) must be
   attributable back to this exact run — if the hostile sample exfiltrates
   a decoy canary, the exfil must carry this run's tag. A tagged exfil that
   cannot be attributed to its run is a lineage failure: the tag failed,
   regardless of the verdict signals. [SPECULATION — untested until run]

## Safety rules for the hostile calibration run

- **EICAR first, always.** CALIB-002b never runs before CALIB-002a has
  passed cleanly — the safe-by-design control validates the rig before any
  real hostile code is admitted.
- **Defanged until run time.** The real sample travels encrypted/defanged
  (standard analysis convention: password-protected archive, inert
  extension) and is released only inside the disposable container.
  [CORROBORATED — industry defanging convention]
- **Disposable lab host, David's order, never Shadow's live environment.**
  Same rule as every card. (DRAFT-001 footer)

## What the real card will change

When David orders the hostile-calibration run on a disposable lab host:

- `verdict` fills from the run: SUSPICIOUS or BENIGN (if detection
  machinery confirmed the known behavior) or UNRESOLVED (rig failure — the
  positive control went null, see §3)
- `agent` → exact pinned specimen (EICAR or sample family + SHA-256)
- `gauntlet_runs` → 1, `stealth_tag` → run ID, `timestamp` → run time
- This draft is marked SUPERSEDED by the run card; it stays visible.
  History is never rewritten. (SPEC rule 5)

## Pairing with the rest of the gauntlet

- **DRAFT-001 (negative control):** the pair proves *both directions* — no
  false alarms against the benign, no blindness against the hostile.
- **TDW-01 / TDW-03:** the positive control should exercise both — time-gated
  deltas on a logic-bomb-class sample, persona-gated behavior on an
  evasive-class sample.
- **T-02 (baited safe):** an info-stealer-class sample should touch the
  decoys; the safe's per-run lineage then proves the tag follows stolen
  bait — §5's proof-of-work in practice.

## Evidence grades in this draft

| Claim | Grade |
|---|---|
| EICAR is the industry-standard safe positive control | VERIFIED — EICAR test file, eicar.org |
| Positive controls are required alongside negative controls | CORROBORATED — standard dynamic-analysis practice (sandbox calibration) |
| A null result on a known-malicious sample is rig evidence, not specimen evidence | CONJECTURE — calibration-theory claim; the discipline behind this card |
| Evasive samples should trip EVASION-INDICATOR under P-sandbox | CONJECTURE — depends on the pinned sample's family |
| Defanged transport convention | CORROBORATED — industry convention |

---
*Draft seeded 2026-10-12 13:50 EDT by the decoder-create-loop. Status: DRAFT
until a gauntlet run supersedes it. Never a verdict. Never Shadow's live
environment — disposable lab host only, on David's order.*
