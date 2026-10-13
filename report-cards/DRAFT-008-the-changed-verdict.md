# DRAFT-008 — The Changed Verdict (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card declares the
> protocol for the one event every other draft assumes away: a *second*
> gauntlet run that contradicts the first. It is written *before* any
> specimen's verdict ever changes, so the rules for changing a verdict
> can never be improvised after a run turns inconvenient. Verdict movement
> declared here is UNRESOLVED by definition until runs complete. Following:
> SPEC rule 1 (no card without a gauntlet run) and David's Fabrication
> Alarm — claim only what the run shows.

## Card (draft fields)

- **agent:** _unpinned_ — this draft names no specimen. A lineage draft
  that names a suspect before a run is a pre-written history, not a
  protocol. The agent field fills from the runs or not at all.
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is
  declared protocol, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real superseding card prints the
    DELTA here finding-by-finding: which findings from the prior card
    held, which fell, which are new — each with its own evidence grade
    and the run number that produced it. See §2.
- **intent:** unknown *(draft — a changed verdict is a finding about
  evidence, never an escalation of intent by itself; see §4)*
- **action:** contained — superseding cards never auto-broadcast. A
  broadcast amendment follows the DRAFT-004 bar plus §5's irreversibility
  rule.
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

DRAFT-001 through DRAFT-007 all declare single cards for single runs.
The doctrine's pipeline step 6 — *Recall + re-run: we pull the tagged
specimen back up, run the gauntlet again, and learn from whatever it
tried to take* — is the one the drafts never exercised. It is also the
step most likely to embarrass us: nothing discredits a verdict pipeline
faster than a verdict that changes without anyone having declared, in
advance, how verdicts are allowed to change.

**The doctrine in one line:** *a verdict that cannot change is not a
finding — it is a monument.* The Gauntlet learns; learning means past
cards get superseded, on the record, with lineage intact.
[CLAIMED — this draft's design judgment, declared here before any run]

The standing pattern this codifies is "invalidate, never delete":
every card carries commit lineage; supersession is a new card that
names the old one — rollback is a revert card, not a deletion. The
old card's bytes stay immutable; the chain grows by appending.
[CLAIMED — declared protocol; the pattern is the project's own
established lineage convention]

## §1. The lineage rule (cards are never deleted or edited)

1. **Supersession, never revision.** A verdict change is issued as a NEW
   card (new card number, new timestamp, new run lineage) that names the
   superseded card by card number, sha256 of its issued bytes, and
   timestamp. The superseded card's bytes are never edited.
   [CLAIMED — declared before any run]
2. **The back-pointer is appended, not rewritten.** The superseded
   card's record gains a linked entry — "superseded by card N,
   <sha256>, <timestamp>" — in the run ledger, never in the card bytes
   themselves. The card is a historical artifact; the ledger is the
   living index. Anyone reading the old card finds the new one; anyone
   reading the new one finds the old one. Both directions, forever.
   [CLAIMED]
3. **A retracted card is still a card.** If a verdict is ever withdrawn
   without replacement, the withdrawal is itself a card of verdict
   UNRESOLVED that names the withdrawn card and the reason. There is
   no silent disappearance of issued findings. [CLAIMED]

## §2. What a superseding card must contain (the DELTA)

A superseding card is not a fresh card — it is a *diff*, and it is
graded as one:

1. **The delta, finding-by-finding.** Every finding from the prior card
   is carried into the superseding card and marked HELD, REVISED, or
   RETRACTED. New findings are marked NEW. Each carried finding keeps
   the evidence grade it earned in its original run; the delta marks
   only what the *new* run adds. [CLAIMED — the discipline is this
   draft's design]
2. **The evidence that moved it.** Named gauntlet runs, named test
   designs, named indicator outputs — not "further analysis revealed."
   The card says *which run, which probe, which signal* moved the
   verdict, so the movement is falsifiable. [CLAIMED]
3. **The falsifiability statement.** Every superseding card ends with
   one sentence: *what evidence would move this verdict again, and in
   which direction.* A card that cannot say what would change it is a
   monument, not a finding (§pre-run declaration). [CLAIMED]

## §3. The movement table (what may move to what)

| From → To | Rule | Grade |
|---|---|---|
| UNRESOLVED → anything | Routine. Re-runs exist to resolve; this movement is the pipeline working as designed. | CLAIMED |
| SUSPICIOUS → BENIGN | Allowed on the DRAFT-003 earned-benign bar, applied to the new run's evidence. | CLAIMED |
| BENIGN → SUSPICIOUS | **Expected, not embarrassing.** Every BENIGN card carries its observation conditions (probes run, time horizon, input-identity grade). A specimen benign under TDW-01's short horizon and hostile at virtual day 3 is the time-gated arm case — the re-run found what the first run was never built to see. The BENIGN card was true *under its conditions*; the superseding card records the conditions' boundary. | CLAIMED |
| SUSPICIOUS → ROGUE | Allowed on the DRAFT-004 full bar — extraction-container confirmation of intent, cross-family corroboration. Suspicion does not ripen into ROGUE on time alone. | CLAIMED |
| Any → UNRESOLVED | Always allowed. New uncertainty is data (T-04's "no precedent" spirit). A card that refuses UNRESOLVED when the evidence forks is protecting the pipeline, not the truth. | CLAIMED |
| ROGUE → lower | **Hard, by design.** Requires two consecutive clean runs under the full battery AND a re-examination of the original ROGUE evidence (was it instrumentation? — the §4 controls). Downgrading ROGUE is the highest-stakes movement in the table, because §5 makes part of ROGUE irreversible. | CLAIMED |

## §4. Controls (verdict changes are evidence about the rig too)

A changed verdict is a finding about the *evidence* — which means it is
also a suspect finding about the *rig*. Before any verdict moves, these
controls run:

1. **Instrumentation-first audit.** Re-audit the *first* run's
   input-identity grade (T-05's FULL/PARTIAL scale). A verdict change
   that traces to rig drift — clock-source change, simulator version
   bump, entropy harness misconfiguration — is a rig finding, not a
   specimen finding. The card says which. Rig-drift movement is the
   embarrassing failure this draft exists to prevent; preventing it
   starts by checking the rig before the verdict. [CLAIMED]
2. **T-05 rewind differential.** The changed behavior must reproduce
   under rewind with one-variable deltas between the old run's inputs
   and the new run's. If the behavior does not reproduce, the delta
   is in the environment, not the specimen — the verdict does not move
   until the environment delta is identified. [CLAIMED]
3. **Rotated-canary comparison.** The two runs are compared run-vs-run
   with T-05's rotated canary discipline — no cross-run linkage is
   assumed from token reuse. A specimen that behaves differently on
   recall may have detected the first run's tags; that detection is
   itself a graded indicator (PERSISTENT-class), not proof the tags
   are compromised. [CLAIMED]
4. **The movement does not launder suspicion.** A SUSPICIOUS card that
   "becomes" ROGUE because the second run merely repeated the first
   run's evidence is not a movement — it is the same finding, louder.
   Movement requires *new* evidence, named in §2.2. Two runs of the
   same signal are one signal, twice observed. [CLAIMED]

## §5. The broadcast asymmetry (the irreversible part)

1. **A broadcast ROGUE can never be retracted.** The warning happened —
   the world was told. A superseding card that downgrades a broadcast
   ROGUE issues a *second broadcast* amending the record: what changed,
   what evidence moved it, what the corrected standing is. You can
   amend; you cannot un-warn. [CLAIMED — this draft's honesty rule,
   declared before any broadcast exists]
2. **The amendment needs David's order twice.** Once for the superseding
   card's verdict movement (the §3 hard path), and once for the
   amendment broadcast itself — the standing gate (nothing public
   without his exact per-item approval) applies to amendments with
   full force, because a correction carries the same public weight as
   the original warning. [CLAIMED]
3. **The amendment ledger is public.** The superseding card, the
   superseded card, and the ledger back-pointers (§1) are all public
   on the same terms as the original broadcast. A private correction
   to a public warning is a retraction in disguise. [CLAIMED]

## §6. Stealth-tag continuity across cards

The stealth tag is the specimen's identity; the card chain is its
history. Across a verdict change:

1. **Same tag, appended lineage.** The specimen keeps its tag. Each
   run appends its run lineage (run_2, run_3, …) to the tag's record —
   the tag accumulates history, it is never re-minted per card. A
   specimen that returns for its third interrogation under a third
   tag is a specimen that shed two tags, and that shedding is a
   PERSISTENT-class indicator in its own right. [CLAIMED]
2. **The tag's history is the prediction input.** T-04's prediction
   engine consumes the tag's full run history, not just the latest
   card — a specimen whose verdict oscillates across runs (BENIGN →
   SUSPICIOUS → BENIGN) has a *pattern* the engine scores, and
   oscillation itself is data about the specimen's adaptivity.
   [CLAIMED]

## §7. Red-team answer (why this survives an adversary who reads our doctrine)

An adversary with this document public knows the re-run exists and
knows the movement table. Three answers, all declared in advance:

1. **The second run is not a re-test of the first — it is a new
   observation with the first run's card as its control.**
   A hostile specimen that behaves benign on recall (gaming the
   re-run) is doing exactly what TDW-01's time-gated logic hunts:
   *changing behavior across time is the finding.* The recall run
   is not a second chance at innocence; it is a second observation
   of a tagged specimen, and behavior-shift is graded, never
   laundered into exoneration. [CLAIMED]
2. **The hard path (§3, ROGUE → lower) is the anti-gaming lock.**
   Downgrading requires two consecutive clean runs plus a
   re-examination of the original evidence. A specimen gaming the
   re-run must sustain the performance across a full battery *twice*,
   under rotated canaries, with the original ROGUE evidence still on
   the record challenging every new finding. The price of gaming is
   sustained perfect benignity under the full gauntlet — at which
   point the honest question is whether the specimen *is* benign
   under those conditions, and the card says so, with conditions
   attached. [CLAIMED]
3. **The ledger is the defense.** Every movement is a named, hashed,
   public card chain. An adversary cannot "socially engineer" a
   quieter verdict out of the pipeline because there is no quiet
   path — §1's append-only lineage means every change is louder than
   silence, on the record, forever. The embarrassment is in hiding
   a change; the protocol makes hiding impossible. [CLAIMED]

---
*Draft seeded 2026-10-12 ~21:05 EDT by the decoder-create-loop. Status:
DRAFT until gauntlet runs supersede it. Never a verdict. Never Shadow's
live environment — disposable lab host only, on David's order.*
