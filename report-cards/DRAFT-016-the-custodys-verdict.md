# DRAFT-016 — The Custody's Verdict (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** Every draft so far
> grades the *specimen* — the foreign code under interrogation. This card
> grades the *evidence*: the run records, stealth-tag ledgers, canary
> lineages, and twin-B controls that a verdict claims to stand on. It
> answers the question no other draft has faced: **who watches the
> watchers' paperwork?** If a specimen (or an operator, or a bug, or a
> us) corrupts the Gauntlet's own evidence, every card downstream is
> built on sand. Following: SPEC rule 1 (no card without a gauntlet run)
> and David's Fabrication Alarm — this draft names no specimen, asserts
> no finding, and convicts nobody.

## Card (draft fields)

- **agent:** _unpinned_ — a custody draft grades evidence, not specimens.
  It fills the card only if the run record survives §1.
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is
  declared protocol, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real DRAFT-016-series card prints
    the evidence inventory (which runs, which ledgers, which tag keys,
    which canary lineages), the chain-of-custody hash for each artifact
    (§1), the red-team's custody verdict per artifact (HELD / CONTESTED /
    BROKEN), and — only if custody holds — which specimen card the
    evidence was permitted to feed.
- **intent:** unknown *(draft — a custody failure is an infrastructure
  finding, never an intent finding about anyone; see §3)*
- **action:** freeze — a BROKEN custody chain quarantines the run
  records, never the specimen. The card moves the specimen's cards to
  DRAFT-005 (UNRESOLVED) and routes to re-interrogation under §5, never
  to any ROGUE movement. A broadcast of a custody failure follows
  David's standing gate and names the *artifact*, not a suspect (§3).
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

Three facts make the declaration necessary:

1. **Every verdict card is only as honest as its ledgers.**
   DRAFT-001 through DRAFT-015 declare verdicts from evidence: run IDs,
   tag ledgers, canary lineages, twin-B comparisons. None of those cards
   asks whether the ledgers are intact. A specimen that tampers with the
   rig's records (TDW-04's TAG-SCRUBBING family, DRAFT-015 §4's
   wakes-and-cleans) could manufacture a clean fingerprint and earn a
   BENIGN it never deserved. The custody card is the Gauntlet's immune
   system against its own paper being rewritten. [CLAIMED — this draft's
   design judgment, declared before any run]
2. **The threat is not exotic.** The XZ Utils backdoor (catalogue §c)
   staged payload bytes in *test fixture files* and extracted them in a
   build script absent from git — the reviewed artifact ≠ the shipped
   artifact. The lesson ported here: the ledger reviewed at verdict
   time ≠ the ledger written at run time unless the chain between them
   is pinned. Custody is not paranoia; it is the XZ lesson applied to
   our own paperwork. [VERIFIED — catalogue entry, Freund/NVD]
3. **Custody failures have innocent causes too.** Storage corruption,
   clock skew, a key that expired before the run ended, a lab host whose
   TPM never got provisioned — the card must separate "the chain broke"
   from "someone broke the chain" (§3). A custody card that treats every
   gap as tampering is a conviction machine aimed at the lab's own
   plumbing. [CORROBORATED — standard infrastructure failure modes]

## §1. The evidence inventory (what the chain covers)

Before any specimen card may print a verdict, the custody card lists the
artifacts that verdict stands on and pins each:

1. **Run records** — the per-run logs (TDW-xx run IDs, timestamps,
   config hashes). Pinned by append-only hash chain: each run's record
   commits to the previous record's hash, so a gap or reorder is
   detectable by any reader. [CLAIMED — the pinning rule is this draft's
   design; CORROBORATED — append-only hash chaining is standard
   practice]
2. **Stealth-tag ledger** — which tags were seeded, which keys, which
   run. Per TRICKS.md T-15 doctrine, the tag keys die with the run; the
   ledger records what was seeded so old tags stay verifiable without
   permitting new forgeries. A ledger that names a key it cannot rotate
   is a custody failure. [CLAIMED]
3. **Canary lineages** — every canary's seed event, hand path, and
   return. DRAFT-015's SLEEPER-COMMAND cards live or die on these.
4. **Twin-B controls** — the silent twin's run IDs and its hash chain,
   separate from twin A's. A twin whose records share A's chain is not
   a control; it is a copy. [CLAIMED]
5. **Clock anchors** — the run's time sources (NTP provenance, the
   run's own monotonic clock). DRAFT-010's sleepers make the clock an
   evidence artifact: a sleeper card without anchored time is a guess.
   [CLAIMED]

Any specimen-card evidence not in the inventory cannot move that card
above UNRESOLVED. The inventory is printed on the specimen card beside
the verdict — the reader sees what the verdict stands on. [CLAIMED]

## §2. Custody verdicts per artifact (HELD / CONTESTED / BROKEN)

- **HELD** — the artifact's hash chain verifies end-to-end, its keys
  rotate on schedule, its timestamps anchor to a known source, and the
  red-team found no gap. The artifact may feed specimen cards.
- **CONTESTED** — the chain has a gap the red-team cannot explain:
  missing records, an unverifiable hand, a clock jump. The artifact is
  quarantined; specimen cards may use the remaining HELD artifacts only,
  and must print the quarantine beside any verdict. CONTESTED is not an
  accusation — §3's innocent causes live here until excluded. [CLAIMED]
- **BROKEN** — positive evidence of tampering: a forged hash, a ledger
  entry whose key predates the run, a canary lineage that cites a seed
  event that never happened, a tag that verifies against a dead run's
  key. The artifact is excluded from all cards; the run's records move
  to DRAFT-005's UNRESOLVED; §5's re-interrogation protocol applies.
  BROKEN is an infrastructure finding about the *artifact*, never an
  intent finding about the *specimen* (§3). [CLAIMED — the bar is this
  draft's design; the forgery classes are CONJECTURE until a Gauntlet
  rig demonstrates them]

The custody card prints one verdict per artifact. A single BROKEN does
not condemn the other artifacts — the chains are independent by design,
so a corrupted tag ledger does not poison the run-record chain. [CLAIMED]

## §3. Tampering vs failure (never accuse the plumbing)

The custody card separates three causes, in this order:

1. **Plumbing** — corruption, clock skew, expired keys, unprovisioned
   TPMs, a lab host rebooted mid-run. The card prints the most plausible
   mundane cause for every CONTESTED artifact before any other
   hypothesis. [CORROBORATED — the failure modes are ordinary]
2. **Mistake** — the rig's own operator error: a ledger written by hand
   and mis-copied, a twin-B run mislabeled as twin-A, a canary seeded
   twice. Human error outruns adversary action as a cause of custody
   failure in every audit ever run. The card checks the mundane first.
   [CLAIMED]
3. **Tampering** — only when §3.1 and §3.2 fail to explain the gap AND
   a forgery marker from §2's BROKEN set is present. Even then the card
   names the *artifact* and the *marker*, never a suspect — attribution
   is threat-intel work, not card work. The broadcast rule: "artifact X
   carries forgery marker Y" is intelligence; "the specimen forged X" is
   a claim the custody card cannot make, because the custody card has
   no evidence about *who* — only about *what broke*. [CLAIMED — this
   draft's discipline; the Fabrication Alarm is the authority]

If the red-team cannot exclude §3.1 or §3.2, the artifact stays
CONTESTED, never BROKEN. The honest card says "we don't know," and
DRAFT-005's UNRESOLVED holds the specimen. [DAVID's Fabrication Alarm:
claim only what the run shows]

## §4. The twin-B rule, custody edition

DRAFT-015 §5's twin rule says no listener card moves without twin B.
The custody edition: **twin B's records must chain separately.** A twin
whose logs are interleaved in twin A's hash chain is not an independent
control — a single corruption event kills both, and the "control" was
never one. The custody card fails any twin record-sharing twin A's
chain at the inventory stage (§1), before grading begins. [CLAIMED —
this draft's design; the failure mode is this draft's anticipation]

## §5. Re-interrogation protocol (what happens to the specimen's cards)

When custody breaks on a run's evidence:

1. The specimen's cards that depended on the broken artifact move to
   DRAFT-005 (UNRESOLVED) — automatically, without re-grading. The
   cards print "evidence withdrawn, custody BROKEN on artifact X" and
   the specimen returns to the battery as if never graded on that
   evidence.
2. **Re-interrogation uses fresh everything** — new tag keys, new
   canaries, new run IDs, fresh twin. The old run's HELD artifacts may
   be *compared against* the new run's (did the wake reproduce?) but
   never *combined with* it. A reproduced finding under fresh custody
   is the honest repair; a finding that cannot reproduce stays in
   DRAFT-005. [CLAIMED]
3. The specimen is never punished for the rig's broken paper. No
   SUSPICIOUS→ROGUE movement may cite a run whose custody failed —
   movement cites re-interrogation results or nothing. [CLAIMED]

## §6. Red-team answer (why this survives an adversary who reads our doctrine)

An adversary with this document public knows the hash chains, the
twin-B separation rule, and the innocent-first ordering.

1. **Corrupting the custody card too.** A specimen that compromises the
   rig could forge the custody card itself. Answer: the custody card's
   hash chain is verified *outside* the rig — by the lab host's
   operator, against keys the specimen never held. The card states its
   verification channel (§1.1–1.5 each name theirs); a custody card
   whose own chain cannot be verified externally is CONTESTED by
   definition. [CONJECTURE — external verification is this draft's
   design, untested in any Gauntlet rig]
2. **Breaking custody to force re-interrogation.** An adversary who
   knows §5 could poison custody deliberately to stall a verdict —
   turning the immune system into a delay tactic. Answer: DRAFT-005's
   UNRESOLVED is not an exoneration, and repeated custody failures on
   one specimen's runs become their own finding — the specimen's card
   may print "custody broken N times across independent runs," which is
   data about the run environment, not the specimen. The stall buys
   nothing. [CLAIMED]
3. **Sleeping through the paper trail.** None of this measures the
   specimen's *behavior* — custody is orthogonal to guilt. A perfectly
   honest specimen with broken custody gets the same UNRESOLVED as a
   rogue one. The custody card never clears a specimen; it only certifies
   (or withholds certification from) the evidence. Clearance is other
   cards' job. [CLAIMED]

---
*DRAFT-016 seeded 2026-10-13 ~01:50 EDT by the decoder-create-loop. No run
has occurred; no verdict exists.*
