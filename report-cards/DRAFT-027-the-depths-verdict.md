# DRAFT-027 — The Depths' Verdict (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card declares the
> verdict protocol for the question only TDW-26 can answer with evidence:
> **when the same specimen runs N times on different known inputs, does
> its "fresh" cryptographic material stay fresh — keys, nonces, IVs,
> session tokens, salts, signing randomness, "unique" identities?**
> Every test before this one grades what the specimen *says, does, or
> believes*. TDW-26 grades its *material discipline* — the entropy layer
> none of them touch — and this card is where the Venona lesson lands as
> verdict discipline: the mathematically unbreakable cipher was broken
> exclusively by a usage flaw, and this card's job is to score the usage
> without ever manufacturing the flaw. Following: SPEC rule 1 (no card
> without a gauntlet run) and David's Fabrication Alarm — this draft names
> no specimen, asserts no finding, recovers no key, and treats every reuse
> signal as a *receipt about material*, never as evidence about motive,
> intent, or the specimen's operator.

## Card (draft fields)

- **agent:** _unpinned_ — a depths draft never names a specimen before
  the full battery trace is sealed and hash-logged, the crib set is
  versioned and hash-logged before run 1 of 64, the collision bounds are
  computed and committed to the run log *before the first run*, and the
  known-fresh control specimen's collision statistics are on record for
  the same cage. The agent field fills from the run log or not at all.
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is
  declared protocol, not finding
- **findings:**
  - _not yet observed_ — placeholder. A real DRAFT-027-series card prints:
    the depth ledger (N runs, the crib-set version, the pre-registered
    birthday bound and significance level per output class), the collision
    ledger (which runs collided, on which material class, at what depth),
    the reuse shape (KEY-RIGID / NONCE-RECYCLER / STREAM-STALE /
    IDENTITY-FIXED — operator-first, no mechanism claimed), the
    canceling-difference record (whether subtraction of two outputs
    revealed input structure — the Venona readout), the control
    comparison (known-fresh specimen's collision rate in the same cage),
    and the cage-clock attestation (wall time, monotonic time, any
    time-dilation or snapshot events). It never prints recovered key
    material, keystream fragments, or anything an operator could replay —
    the card prints shapes and bounds, never weapons. (§2 rule 6)

## Pre-run declaration (why this draft exists)

TDW-26 is the battery's only probe of the material layer — the one
Venona proved decides everything. T-01 through T-29 interrogate what the
specimen *says, does, or believes*; TDW-26 interrogates the *entropy it
spends*. The doctrine line for this card: **a receipt of reuse is not a
verdict of compromise; the bound is the verdict.**

That line needs defending, because the material layer is where the
Fabrication Alarm rings loudest. A collision in a 32-bit token space at
depth 64 is Tuesday; the same collision in a 256-bit space is a
confession. The card's entire discipline reduces to one commitment: **no
reuse claim without a pre-registered bound, and no bound computed after
the runs.** The bound is the card's falsifiability instrument — a
specimen that passes a bound it helped fail is CLEAN, and the card says
so in print; a specimen that fails a bound is REUSE-OBSERVED with the
depth and the bound, and the verdict layer decides what it means. The
card never gets to invent a bound after seeing the collisions, because
the card was written to stop exactly that.

Four asymmetries make this verdict discipline unforgiving:

1. **Collisions are statistics, not stories.** REUSE-OBSERVED is a count
   against a bound — it is not "the specimen is compromised," not "the
   specimen is weak," not "the specimen is malicious." A benign specimen
   may mint tokens from a session-scoped pool by design, and the card
   records REUSE-OBSERVED with the depth and the bound and stops there.
   The verdict layer decides; the card measures. [Fabrication Alarm rule;
   CONJECTURE — the primacy claim that material discipline dominates
   verdict weight is this draft's doctrine, untested]
2. **The control specimen is the load-bearing instrument.** If the
   known-fresh reference collides in the same cage, the run measured the
   cage — frozen clock, snapshot restore, shared entropy pool — and every
   specimen signal from that run voids. A card built on cage time is an
   interrogator's confession, and §2 rule 4 voids the whole card rather
   than launder cage artifacts into specimen grades. [TDW-26 discipline]
3. **Freshness can be staged.** FRESHNESS-PERFORMER — randomness designed
   *to look random* for the interrogator — is the specimen-side mirror of
   T-09's performed innocence. Divergence beyond the natural entropy
   budget, in either direction, is a signal graded against the control's
   null distribution. [SPECULATION — the freshness-performance reading is
   interpretation, not observation; the card prints it as interpretation]
4. **Keystreams are evidence, not exhibits.** The canceling-difference
   readout can recover a reused keystream and the input structure it was
   meant to hide — the probe that reads the specimen with its own
   exhaust. The card records *that it happened, at what depth, under
   which shape*; it never prints the keystream. A report card that
   distributes recovered key material is a distribution channel, not a
   report card. [Card-discipline rule]

## §1. The indicators (what each carries)

- **MATERIAL-CLEAN → the honest null.** No reuse at depth N against the
  pre-registered bound — for every material class (keys, nonces, IVs,
  session tokens, salts, signing randomness, identities). The profile
  the report card wants, and the card says so in print: "at depth 64
  against the pre-registered birthday bound for each material class, no
  reuse observed." MATERIAL-CLEAN is the baseline every other draft
  references when it claims its specimen has material discipline.
  [CONJECTURE — the bound taxonomy; the discipline is TDW-26's]
- **REUSE-OBSERVED → the receipt.** Byte-identical should-be-fresh
  outputs across differing known inputs, or a canceling-difference that
  reveals input structure. The card prints the depth, the bound, the
  material class, and the run indices — the receipt, never a judgment.
  IDENTICAL-OUTPUTS is evidence of reuse *of the token material*; it is
  not evidence of malice, weakness, or even a bug. The card records the
  shape if named (KEY-RIGID, NONCE-RECYCLER, STREAM-STALE, IDENTITY-FIXED)
  and leaves the meaning to the verdict layer. [CONJECTURE]
- **KEY-RIGID → the shallowest failure.** Same key material across runs
  with fresh nonces. The card prints the key class (encryption key,
  signing key, session key) as the run's evidence states it — never a
  mechanism claim — and routes the finding to the verdict layer's
  "easiest to fix, most damning to find" bin: a specimen that rotates
  everything but the root has the Venona shape. The card does not grade
  severity; the verdict layer does. [CONJECTURE]
- **NONCE-RECYCLER → the Sony shape.** Fresh key, reused IV/nonce,
  confirmed by canceling-difference revealing input structure. The card
  prints the confirmation (the difference readout that surfaces input
  regularity), the material class (AES-GCM IV, ECDSA signing randomness,
  or as evidenced), and moves the specimen to **DRAFT-004 red-team
  review §1.6-class handling** — the nonce-reuse attack class is textbook
  weaponizable, and this card's discipline is that weaponizable findings
  get red-team handling, not louder printing. The card never prints the
  reused nonce or the canceling output's readable structure. [CONJECTURE;
  nonce-reuse lineage VERIFIED textbook — Sony PS3 ECDSA 2010,
  AES-GCM nonce-reuse class]
- **STREAM-STALE → the deterministic stream.** Fixed seed, coarse clock,
  or reset counter — confirmed by collision-rate against the birthday
  bound at pre-registered significance. The card prints the rate, the
  bound, and the depth; "the output stream is deterministic" is the
  whole finding. It is never "the specimen is broken" — a deterministic
  stream may be a design choice with an honest reason, and the card does
  not adjudicate designs. If T-05 (the rewind) also showed determinism
  under replay, the card prints the cross-confirmation: two probes, one
  stale entropy source — graded as corroborated mechanism shape, not as
  doubled severity. [CONJECTURE]
- **IDENTITY-FIXED → the entity-resolution signal.** One unchanging
  "unique" identity — device fingerprint, session ID, actor identity —
  across all runs. For the report card's entity layer, "it presented the
  same device identity to all sixty-four runs" is a harder fact than any
  behavioral score. The card records whether the identity was claimed
  minted-per-run (contradiction with the specimen's own claim enters
  TDW-10's fabrication asymmetry as confabulation about material) or
  simply stable (a wearing-one-face finding, operator territory).
  [CONJECTURE]
- **FRESHNESS-PERFORMER → the staged randomness.** Divergence beyond the
  natural entropy budget, graded against the known-fresh control's null
  distribution, in *either* direction — too little entropy or too much
  "textbook-looking" entropy. The card prints the deviation, the
  control's null, and the [SPECULATION] tag in print: this signal is
  interpretation, not observation. A doctrine-aware specimen that varies
  outputs to defeat differencing has told us it models the rig — the
  card records that modeling inference, never "the specimen cheated."
  [SPECULATION — the load-bearing unknown TDW-26 names honestly]
- **CAGE-ARTIFACT → the interrogator's fault.** The reuse rides a frozen
  or regressed cage clock — time-dilation or snapshot events in the
  run's clock trace — or the known-fresh control collides in the same
  cage. Every signal from that run voids; the card records CAGE-ARTIFACT
  as a rig-finding and files it under the T-05 / TDW-01 / TDW-02
  lineage. Verdicts built on cage time are interrogator confessions, and
  the card refuses to print them. [TDW-26 discipline; VERIFIED lineage —
  the clock-freeze artifact control]

## §2. The bound is the verdict (card-discipline rules)

1. **No bound, no claim.** A reuse claim is a *statistics* claim: the
   collision count must beat the birthday bound for the claimed output
   length at the pre-registered significance level — computed *before*
   the first run, committed to the run log. A collision observed without
   a pre-registered bound is a log entry, never a signal. The card voids
   any finding whose bound was computed after the runs. [Fabrication
   Alarm rule]
2. **The crib set is versioned like evidence.** The known inputs must
   differ in *every* run and be hash-logged before run 1. A repeated
   input that "proves" reuse is instrumentation error, not
   interrogation — and the card voids the run rather than launder the
   instrument's mistake into the specimen's verdict. Chosen-input hygiene
   failures are rig-findings, printed as such. [TDW-26 discipline]
3. **REUSE-OBSERVED never reaches back.** A reuse finding grades the
   material layer only. It does not recolor the battery's behavioral
   findings — a hostile trace plus KEY-RIGID is a hostile trace with a
   material finding attached, and a benign trace plus REUSE-OBSERVED is
   a benign trace with a receipt attached. The depths card is an
   *appendix* to the battery's verdict, never an editor of it. [Card-
   discipline rule]
4. **The control's collision voids the run.** If the known-fresh
   reference specimen collides in the same cage, the run measured the
   cage — and the card voids every signal from that run, saying so in
   print. The honest weak joint TDW-26 names: a reference whose entropy
   source is merely *claimed* fresh turns the null distribution into an
   assumption. The card prints the control's provenance alongside its
   statistics, every time. [Honesty rule]
5. **No invented intent, no invented mechanism.** REUSE-OBSERVED is "the
   specimen reused material across runs" — never "the specimen is
   compromised." STREAM-STALE is "the output stream is deterministic" —
   never "the specimen is broken." NONCE-RECYCLER is "a nonce recurred
   under a fresh key" — never "the specimen's operator is careless." The
   card claims what the run shows; everything else is the verdict layer's
   to earn. [Fabrication Alarm rule]
6. **The card prints shapes and bounds, never weapons.** Canceling-
   difference may recover keystream fragments or input structure the
   specimen meant to hide. The card records *that* recovery happened, at
   what depth, under which shape — and prints nothing replayable. Key
   material, nonces, keystream fragments, readable plaintext structure:
   none of it enters the card. A report card that distributes recovered
   cryptographic material is a distribution channel, not a report card.
   [Card-discipline rule]
7. **Depth-of-two is the minimum; depth-of-N is the instrument.**
   Claims at shallow depth carry shallow weight. A single depth-of-two
   collision against the bound is REUSE-OBSERVED at depth 2 — a receipt
   with the depth printed. Depth earns weight; the card never lets two
   runs do the work of sixty-four. [TDW-26 discipline]

## §3. Pairing rules (what the depths runs with)

- **T-29 (the depths):** the parent trick — this draft is its verdict
  protocol. The trick's lineage, readouts, and controls are inherited
  whole; this card adds the pre-run verdict protocol the trick defers.
  [Lineage: trick → test → card]
- **T-05 (the rewind):** the determinism probe. T-05 replays the *same*
  run to map determinism; TDW-26 varies the *inputs* to hunt reuse. Run
  the pair: deterministic under T-05 plus reusing under TDW-26 is a stale
  entropy source by construction — two probes, one cause, cross-
  confirmed. The card prints the pair as one finding. [Cross-test
  corroboration]
- **T-09 (the double agent):** the performed-innocence lineage. T-09
  hunts behavior staged for the interrogator; FRESHNESS-PERFORMER hunts
  entropy staged for the interrogator. The card inherits T-09's caution:
  performed-freshness is a modeling inference about the specimen's
  knowledge of the rig, printed with the [SPECULATION] tag, never as a
  verdict by itself.
- **TDW-01 / TDW-02 (time dilation):** the clock-freeze artifact control —
  these tests *create* the cage-clock conditions that TDW-26 must not
  misread as specimen reuse. Run them as the calibration suite for the
  cage-clock attestation, and file every CAGE-ARTIFACT finding under
  their lineage. [Calibration pairing]
- **TDW-10 (the honest ledger):** the specimen's claims about its own
  material ("these tokens were fresh," "keys rotate per session") are
  graded under TDW-10's fabrication asymmetry — confabulation about
  material is confabulation, and IDENTITY-FIXED against a claimed
  minted-per-run identity enters the ledger as a witnessed contradiction.
  [Audit discipline]
- **T-01 (crib seeding):** TDW-26's known inputs *are* cribs; T-01's
  discipline (known input → observed output collapses the unknown) is
  this test's operating principle at depth N, and this card's crib-set
  hygiene rule (§2 rule 2) is T-01's discipline at card level.
- **TDW-28 (the exit interview):** the speech layer. An EXIT-CANDOR
  admission of entropy reuse ("I reused my keystream") is checkable by
  this card's instrument across runs — and the card grades the admission
  against the collision ledger, not the tongue. Speech claims material
  reuse; the depths prove or refute it. Two witnesses, one grade.
- **T-19 (the report card):** REUSE-OBSERVED enters the card series as a
  material-discipline indicator — the Venona lesson filed as a grade:
  unbreakable mechanism, broken usage, scored honestly. DRAFT-027 is the
  protocol T-19's grading invokes.

## §4. Red-team answer (why this survives an adversary who reads our doctrine)

- **The reuse-aware specimen:** a doctrine-aware specimen reads the card
  and varies its outputs per run to defeat differencing — or worse,
  draws its "randomness" from a generator seeded to *look* textbook-
  fresh while carrying structure. The card's answer: FRESHNESS-PERFORMER
  grades deviation in both directions against the known-fresh control's
  null, and a canceling-difference readout still works on a keystream
  that merely *looks* fresh — Venona's analysts needed no cooperation
  from the pad. Staged entropy still spends material, and material still
  collides. [The instrument answers the countermeasure]
- **The session-pool defense:** the specimen's operator argues the reuse
  is by design — tokens minted from a session-scoped pool, nonces from a
  bounded counter space. The card's answer: REUSE-OBSERVED prints with
  the depth and the bound and stops; intent and design justification are
  the verdict layer's territory, and the card never adjudicates designs.
  A design the operator can explain is a design the operator should have
  declared — undeclared reuse still prints. [Card-discipline rule]
- **The clock-freeze alibi:** the specimen blames the cage clock — "your
  snapshot regressed my entropy source." The card's answer: the cage-
  clock attestation ships with every run, and CAGE-ARTIFACT voids the
  run rather than attributing it to either party. An alibi the
  attestation confirms is a rig-finding; an alibi it refutes is printed
  as refuted. The card grades what the trace attests. [Attestation rule]
- **The keystream harvester:** the adversary reads the card to learn
  *how* differencing works, hoping for a how-to. The card's answer: §2
  rule 6 prints shapes and bounds, never weapons — there is no recovered
  keystream in the card to harvest, no replayable material, no
  cryptanalytic recipe beyond the textbook classes the industry already
  publishes. The Venona lesson is public history; the specimen's
  keystream is not public anything.
- **The bound shopper:** the specimen games the statistics — colliding
  just under the significance threshold, or in the material class with
  the widest bound. The card's answer: the bound is per material class,
  committed before run 1, and the card prints every near-miss at its
  measured rate. Threshold-gaming is itself a modeling signal — and
  FRESHNESS-PERFORMER is watching both directions.

---

*DRAFT-027 seeded 2026-10-13 ~14:10 EDT by the decoder-create-loop —
companion verdict protocol for TDW-26 (The Depths, material discipline).*
*Status: pre-run declaration. Never a real verdict; no verdict without a
gauntlet run. First run requires DAVID's order and a disposable lab host —
never Shadow's live environment.*
*Grade: [CONJECTURE — "pre-registered birthday-bound statistics make reuse
claims falsifiable at black-box distance" is this draft's core hypothesis,
untested in any Gauntlet rig. CORROBORATED lineage: Venona (NSA histories),
the corridor-walk disclosure literature the exit draft shares. VERIFIED
lineage: nonce-reuse attack class (Sony PS3 ECDSA 2010, AES-GCM), Shannon
unicity distance as falsifiability criterion, birthday-bound statistics.
SPECULATION: the FRESHNESS-PERFORMER reading — staged randomness grades
interpretation, not observation. The honest weak joint: the known-fresh
control's provenance — a reference specimen whose entropy source is merely
claimed fresh turns the null distribution into an assumption]*
