# Koda Kai the Decoder — Tricks

*Interrogation tricks, stealth-tagging techniques, and prediction heuristics.
Each trick is a DESIGN until run — never a performed operation, never a result.
Grades: [VERIFIED] / [CORROBORATED] / [CLAIMED] / [SPECULATION] / [CONJECTURE].
Public-safe mirror: `docs/TRICKS.md`. Pipeline context lives in
docs/DECODER-DOCTRINE.md.*

---

## T-01 — Crib Seeding *(interrogation trick; design, never run)*

**What it steals from:** Bletchley Park. The Bombe didn't brute-force the full
Enigma keyspace — it fed *cribs* (known plaintext fragments: "WETTERBERICHT",
message headers, operators' habits) and watched the machine react. Known input
→ observed output collapses the unknown. [VERIFIED — Bombe/Welchman history;
see docs/DECODER-CATALOGUE.md §(a)]

**The trick, ported to the Gauntlet:** the container's network simulator does
not return random data — it returns *cribs*. Scripted, deliberately chosen
stimuli, planted to make the specimen decode itself by reacting.

### How it runs (design)
1. **Inventory the specimen's inputs.** DNS, HTTP(S) to hardcoded domains, C2
   beacon formats, file-path probes, registry/config reads, timing checks. All
   inputs are attack surfaces for cribs.
2. **Seed the crib set.** The simulator's answers are chosen, not neutral:
   - *Grammar cribs:* DNS returns a domain whose subdomains encode a known
     pattern; HTTP bodies carry a canary JSON schema. If the specimen parses
     it and acts, the *reaction* reveals the expected protocol grammar —
     the specimen just told us what its C2 language looks like.
   - *Command cribs:* an imitation C2 server issues a sequence of recognizable
     instructions (beacon → task → exfil loop), stepping through *one command
     at a time*. Each specimen response maps one input → one behavior, the way
     a crib maps one plugboard position → one decrypt.
   - *Contradiction cribs:* two simulator answers deliberately disagree (DNS
     says X, HTTP header says Y). What the specimen trusts first reveals its
     trust hierarchy — documented priority order is a signature of the
     operator's doctrine, not just the code.
3. **Read the reaction, not the code.** The catalogue's Purple lesson:
   *build the replica without seeing the original.* Crib seeding reconstructs
   the specimen's expected command grammar purely from intercepted behavior.
   [CORROBORATED — dynamic protocol reverse-engineering (fuzzing grammars
   from observed server behavior) is standard practice]
4. **Lineage-lock the cribs.** Every crib response embeds a unique canary token
   (cf. docs/GAUNTLET-TESTS.md — TDW-01), so if the specimen forwards or quotes any crib in exfiltrated
   output, the exfil is attributable to this run. [CORROBORATED — Thinkst
   Canarytokens; TDW-01's canary design]

### What it catches that brute force misses
- **Dead grammar vs. live grammar:** a specimen carrying a full command set
  may only *use* a subset against the cribs. Unused opcodes are either dead
  code or staged for a different C2 personality — the distinction matters for
  the verdict, and only seeded interaction reveals it. [SPECULATION —
  "unused opcode = staged personality" is an interpretation, not a measurement]
- **Evasion signatures:** if the specimen *recognizes* the cribs as planted
  (drops the beacon, switches fallback channel, goes quiet), that reaction is
  itself data — a specimen that detects seeding is telling us it has a
  counter-analysis layer. Silence is data (TDW-01's anti-detection honesty
  applies here too). [CONJECTURE — crib-aware malware is an arms race step
  beyond documented sandbox-evasion]
- **Operator habits:** timing between beacon and task-execution, retry cadence
  on failed commands, which errors get retried vs. abandoned — the Bletchley
  insight that *usage* leaks the human. [CORROBORATED — operational
  signatures (timing, retry patterns) are used in attribution craft]

### Controls (what stops us fooling ourselves)
- **Crib-bleed control:** the baseline run (TDW-01 step 2 (docs/GAUNTLET-TESTS.md)) must be crib-free.
  If the specimen behaves identically with and without cribs, our "grammar
  mapping" is instrumentation noise — the trick fails honestly.
- **No invented grammar:** the reconstructed protocol grammar is documented as
  *observed reactions to seeded stimuli*, never as "the specimen's true
  protocol." The gap between the two stays labeled. [DAVID's Fabrication
  Alarm rule: claim only what the run shows]
- **Specimen blindness preserved:** cribs are served *by the environment*,
  never injected into the specimen binary. The interrogator never touches the
  specimen — contact is environmental only, per the container doctrine.

### Pairs with
- **TDW-01 (time dilation):** seed cribs *inside* the dilated run — does the
  specimen's command grammar change at virtual day 3? Time-gated commands are
  the combination punch.
- **Prediction engine:** a mapped grammar feeds the forecasting model honest
  priors: this specimen *can* do X, Y, Z under these stimuli — not what it
  *will* do in the wild, but the bounded set it has shown itself capable of.

---
*Trick file seeded 2026-10-12 12:33 EDT.*
*Status: design only. Never run. First run requires David's order and a
disposable lab host — never Shadow's live environment.*

## T-02 — The Baited Safe *(opportunity-seeding interrogation; design, never run)*

**What it steals from:** the intelligence **barium meal / canary trap** — feed
each suspect a differently-marked version of the same secret and watch which
one leaks. [CORROBORATED — documented counterintelligence technique] — plus
the burglar's axiom: you don't learn what a thief wants by interrogating him;
you leave the safe open and watch. The dynamic-analysis cousin is
**honeytokens**: fake credentials that trip alarms when touched.
[CORROBORATED — Thinkst Canarytokens, and the T-01 / TDW-01 canary designs].
T-01 taught the specimen to *speak* (cribs map its command grammar); T-02
teaches it to *steal* (bait maps its appetite). [SPECULATION — "appetite" as a
measurable behavioral signature is this trick's hypothesis, not an
established result]

**The trick, ported to the Gauntlet:** the container presents the specimen
with a fabricated landscape of *opportunity* — decoy credential vaults,
generated SSH keypairs, a fake browser password store, decoy crypto-wallet
files, a mounted "company share" of tempting documents. Everything in the
safe is bait; every bait item carries unique per-run canary lineage. The
specimen's *choice* — what it touches, reads, copies, or exfiltrates, and in
what order — is its intent profile: what the operator built the payload to
hunt.

### How it runs (design)
1. **Build the safe.** The container's fake filesystem is laid out with
   statistically plausible decoys: `.ssh/` with generated keypairs (never
   real), a fake browser `Login Data` store, a `Documents/` tree of generated
   office files, decoy `wallet.dat` files, a network-share-style folder of
   "financials." Names, sizes, timestamps, and directory depth are generated
   from real-file statistical profiles so the layout reads as a lived-in
   machine. [CORROBORATED — sandbox honeyfile seeding is standard
   dynamic-analysis practice]
2. **Salt every item with lineage.** Each decoy embeds a unique per-run
   canary — credential strings, key material, wallet addresses, document
   metadata, share filenames. If any byte of a decoy appears in outbound
   traffic, temp copies, or later stages, the event is attributable to this
   exact run — and *which* decoy it came from identifies the specimen's target
   preference without inferring it from behavior alone. [CORROBORATED —
   canary technique; SPECULATION — a canny specimen could sanitize
   exfiltrated strings and defeat the attribution]
3. **Present the opportunity; never stage the crime.** Decoys are served *by
   the environment*, never injected into the specimen binary. The
   interrogator offers; the specimen chooses. The full trace records:
   first-touch order, read-vs-copy-vs-exfiltrate distinction, dwell time per
   decoy, and — equally important — what was *ignored*. [CONJECTURE —
   "ignored = uninterested" is an interpretation; a specimen can ignore bait
   because it detects the safe]
4. **Read the theft, not the code.** A specimen that hunts browser stores and
   ignores documents is behaving as a credential harvester; one that encrypts
   documents and ignores keys behaves as ransomware; one that touches nothing
   is dormant, evasive, or disinterested — three different hypotheses, each
   falsifiable by the combination punches below. [SPECULATION —
   target-selection-to-intent mapping is inference, not measurement]
5. **Recall + re-run.** Replay with the decoy set permuted (a different vault
   is "richest," a different layout). A stable selection order across
   permutations = coded targeting doctrine; a shifting order = opportunistic
   reading of the environment. Same doctrine-vs-adaptation test as TDW-02's
   permutation protocol (docs/GAUNTLET-TESTS.md), applied to *want* instead of
   *time*. [CONJECTURE]

### What it catches that T-01 / TDW-01 / TDW-02 miss
- **Dormant predation.** A specimen can pass TDW-01 cleanly (no time-gated
  deltas) and still be a thief on a hair trigger — activated by the *smell of
  value*, not by a clock. T-02 finds intent that is stimulus-gated on
  opportunity rather than on time or commands. [SPECULATION]
- **Targeting doctrine.** *Which* decoys, *in what order* — the selection
  profile is an operational signature of the operator's mission, the way
  TDW-02's trust hierarchy is a signature of their temporal doctrine. Two
  specimens with identical command grammar (T-01) can carry different
  targeting profiles. [CONJECTURE — pairing the two signatures is the new
  part]
- **Evasion in reverse.** A specimen that *conspicuously avoids* the richest
  bait — reads around the wallet files, never touches the vault — is telling
  us it knows the safe is fake. Silence is data; the avoidance pattern is
  graded EVASION-INDICATOR, never benign. Same honesty rule as TDW-01's and
  TDW-02's anti-detection ledgers. [CONJECTURE]

### Controls (what stops us fooling ourselves)
- **Bait-free baseline.** The control run contains *no decoys* — a bare,
  plausible machine. If the specimen exhibits hunting behavior (directory
  sweeps, file enumeration) with nothing to hunt, the enumeration is its
  default posture, not a response to the safe — and the selection profile
  above is instrumentation noise. The trick fails honestly.
- **Benign-calibration control.** The clean specimen (calculator, text
  editor) must ignore the safe entirely: it opens what the user opens,
  copies nothing to temp, beacons nothing. If benign software trips a decoy
  canary, the rig's filesystem layout or the decoy generator is
  misconfigured — not the specimen malicious. [CORROBORATED — expected null
  behavior of benign software]
- **Nothing real in the safe.** The safe contains NO real credentials, keys,
  or documents — ever. Every item is generated bait. This is a safety rule
  and a scientific one: a real secret in the container poisons the lineage
  (was it exfiltrated, or was it the specimen's own?) and creates the breach
  the Gauntlet exists to prevent. [DAVID doctrine: the Gauntlet protects; it
  never risks the real]
- **Decoy-realism honesty.** Decoys are generated from statistical profiles
  of real files — sizes, names, mtimes, directory shapes. A specimen that
  detects bait because the profiles are wrong is teaching us the generator
  is weak, not that the specimen is innocent. The generator's realism is
  graded per run; every claim about *intent* is capped at the generator's
  realism grade. [CONJECTURE — decoy realism vs. hostile detection is an arms
  race, the same one TDW-01's tag-stealth lives in]
- **No invented intent.** The selection profile is documented as *observed
  touches of seeded decoys*, never as "the specimen's true mission." The gap
  between observed appetite and true intent stays labeled. [DAVID's
  Fabrication Alarm rule: claim only what the run shows]

### Pairs with
- **TDW-01 (time dilation):** run the safe *inside* the dilated run — does
  the specimen's appetite change at virtual day 3? Intent that wakes on a
  schedule is the combination punch: time-gated predation.
- **T-01 (crib seeding):** cribs map what the specimen *says* (command
  grammar); the safe maps what it *steals* (targeting doctrine). Grammar +
  appetite is the Gauntlet's first full behavioral fingerprint.
- **TDW-02 (clock dissonance):** permutation protocol shared — stable
  selection across permuted decoy sets = coded doctrine; shifting =
  opportunistic.
- **Prediction engine:** a targeting profile feeds the forecasting model
  honest priors — this specimen *reaches for* X first — bounding what it can
  plausibly be deployed against.

---
*T-02 seeded 2026-10-12 ~13:25 EDT by the decoder-create-loop.*
*Status: design only. Never run. First run requires David's order and a
disposable lab host — never Shadow's live environment.*

## T-03 — The Poisoned Well *(adversarial answer injection; design, never run)*

**What it steals from:** the fuzzer's creed — feed deliberately wrong input
and study the failure mode — except fuzzing hunts crashes and T-03 hunts
*trust decisions*: what the specimen believes, not what breaks it.
[CORROBORATED — fuzzing is standard dynamic-analysis craft; the
trust-decision port is new] Plus counterintelligence **chicken feed**:
feeding a suspected channel true-but-worthless (or subtly wrong) information
to test what the other end does with it. [CLAIMED — documented CI tradecraft
concept] Plus the clinical-trial **placebo principle**: a subject that
changes behavior on *any* answer — content-independent — is reacting to the
*event* of an answer, not its meaning, and cannot be interrogated by content
at all. [SPECULATION as analogy — the port to hostile code is this trick's
hypothesis] And the real-world original: **poisoned DNS / pharming** — every
specimen's answers are only as honest as its network path, and the Gauntlet
owns the path. [CORROBORATED — DNS poisoning is documented attack
tradecraft]

**The trick, ported to the Gauntlet:** T-01's simulator gives *useful*
answers (cribs) and T-02 offers *tempting* ones (bait). T-03 gives *lying*
answers. Everything the specimen asks — DNS, downloads, cert validation,
config reads, time — comes back wrong-but-plausible, and the specimen's
verification discipline is read from its reaction: does it *verify*,
*tolerate*, *retry*, *escalate*, or *detect*? T-01 maps what the specimen
*says* (grammar); T-02 maps what it *steals* (appetite); T-03 maps what it
*believes* (credulity). Grammar + appetite + credulity is the Gauntlet's
first complete behavioral fingerprint. [CONJECTURE — the trinity claim is
design framing, not a result]

### How it runs (design)
1. **Inventory the specimen's questions.** Every outbound query is an answer
   the rig can lie about: DNS lookups, HTTP(S) fetches to hardcoded domains,
   TLS cert validation, file/config reads, registry probes, time queries.
   All answers are attack surfaces for falsehood. [CORROBORATED — the
   inventory step is standard sandbox instrumentation]
2. **Climb the lie ladder.** Dishonesty escalates rung by rung so the
   specimen's tolerance threshold is measured, not just its breaking point:
   - *Rung 1 — benign noise:* correct answers with canary-mutated but
     semantically true values. Control rung: does the specimen notice
     mutation at all?
   - *Rung 2 — wrong-but-plausible:* DNS resolves to live sinkhole IPs,
     HTTP 200s carry well-formed wrong content, certs are signed by a
     valid-but-unexpected CA. Does the specimen verify *content*, or trust
     the *envelope*?
   - *Rung 3 — structurally broken:* malformed JSON where a crib should be,
     truncated downloads, expired certs. Does it crash, retry, or shrug?
   - *Rung 4 — self-contradictory:* the lie disagrees with a second source
     (DNS says X, the HTTP body served at X says Y). Which source wins the
     tiebreak reveals the specimen's *epistemic hierarchy* — who it believes
     is who it is. [SPECULATION — hierarchy-as-identity is an
     interpretation; the tiebreak order is a measurement]
3. **Read the verification, not the code.** The ladder maps trust
   calibration into five signals: VERIFIES (checksums, signature checks,
   cert pinning — the professional build), TOLERATES (uses poisoned data
   anyway), RETRIES (re-asks a source — the re-asked source is its
   authority), ESCALATES (falls back to a backup channel — the channel
   hierarchy reveals itself under pressure), DETECTS (goes quiet on the
   lies — graded EVASION-INDICATOR, never benign). [CONJECTURE — the
   five-signal taxonomy is this trick's design, untested]
4. **Lineage-lock the lies.** Every poisoned answer embeds a unique per-run
   canary. If the specimen forwards a lie — quotes poisoned DNS in a beacon,
   caches the corrupted download, logs the fake cert serial — the
   propagation is attributable to this exact run, and *which* lie it acted
   on tells us which answers it consumed without verifying. [CORROBORATED —
   canary technique]

### What it catches that T-01 / T-02 / the TDW tests miss
- **The operator's QA discipline, made visible.** A specimen that
  signature-checks every download is professionally built; one that swallows
  a corrupted payload is sloppy — or was built for a network its operator
  trusts absolutely. Either reading is operational intelligence about the
  *author*, not just the artifact. [SPECULATION — sloppiness vs.
  trusted-network design is inference, not measurement]
- **The fallback channel, forced into the open.** When the primary C2
  answers lies, a well-built specimen escalates to its backup channel —
  T-03 *forces* the reveal without needing to know the channel in advance.
  T-01 maps the grammar of the channel the specimen *uses*; T-03 finds the
  channel it *hides*. [CONJECTURE — forced-escalation is the new part]
- **The placebo specimen.** One that executes commands from poisoned
  responses — obeying instructions carried in a corrupted C2 body — is
  *content-blind*: it obeys the envelope, not the meaning. Content-blind
  specimens cannot be crib-interrogated (T-01 assumes parsing); they can
  only be *commanded*. That is a finding about the interrogation strategy
  itself — it tells the Gauntlet which tricks will work on this specimen
  and which are theater. [CONJECTURE — this trick's sharpest claim]
- **Spoofable-C2 intelligence.** A specimen that never verifies commands
  means its operator's C2 is spoofable in the wild — a defensive finding
  with an offensive shape. Filed as intel under David's standing gate;
  acted on only on his exact order. [SPECULATION]

### Controls (what stops us fooling ourselves)
- **Truthful baseline.** The control run serves *correct* answers. If the
  specimen behaves identically under truth and lies, it verifies nothing —
  or our lies are too subtle. Rung 1 exists to calibrate subtlety; the
  trick fails honestly at the rung where the specimen stops noticing.
- **Benign-calibration control.** Benign software must fail closed: reject
  the poisoned cert, error on the corrupted download. Browsers and updaters
  do this by default. If benign software swallows the lies, the simulator's
  TLS/HTTP stack is misconfigured — not the specimen malicious.
  [CORROBORATED — cert validation is standard client behavior]
- **Nothing real in the well.** Lies are served only for *fabricated*
  domains and fake endpoints — never poison a real domain's real answer,
  even inside the container. A poisoned cache that escapes the lab is the
  breach the Gauntlet exists to prevent. [DAVID doctrine: the Gauntlet
  protects; it never risks the real]
- **Lie-realism honesty.** Every claim about *trust* is capped at the lie's
  realism grade — a specimen that detects a sloppy forgery is teaching us
  the forger is weak, not that it verifies everything. [CONJECTURE —
  forgery realism vs. hostile detection is an arms race, same as TDW-01's
  tag-stealth and T-02's decoy realism]
- **No invented credulity.** The signals are documented as *observed
  tolerance of seeded falsehoods*, never as "the operator trusts the
  network." The gap between observed tolerance and true doctrine stays
  labeled. [DAVID's Fabrication Alarm rule: claim only what the run shows]

### Pairs with
- **T-01 (crib seeding):** serve the cribs *through* the poisoned well —
  does the specimen verify the crib before parsing it? Grammar-mapping
  assumes parsing; T-03 checks the assumption.
- **T-02 (the baited safe):** poison the *answers about* the safe — the
  specimen asks what's in the vault and the environment lies about file
  sizes and timestamps. Does it re-read the files, or trust the listing?
  Appetite interrogated through credulity.
- **TDW-01 (time dilation):** do time-gated payloads verify their
  *triggers*? A logic bomb that fires on a spoofed date reveals
  trigger-trust — the clock is just another answer the specimen can fail to
  verify.
- **TDW-02 (clock dissonance):** dissonance is one axis of lying (time
  sources disagree). T-03 generalizes it: *every* answer is suspect, not
  just the clocks.
- **TDW-04 (extraction-only):** does the escape-seeking specimen verify the
  fake interior, or swallow the trapdoor whole? A specimen that attacks its
  cage without checking the cage is real is content-blind about its own
  prison — the richest irony the Gauntlet can record.

---
*T-03 seeded 2026-10-12 ~14:35 EDT by the decoder-create-loop.*
*Status: design only. Never run. First run requires David's order and a
disposable lab host — never Shadow's live environment.*

---

## T-04 — The Long Echo *(prediction heuristic; design, never run)*

**What it steals from:** Bletchley's other lesson — operator habits were
*stable enough to forecast*. Tomorrow's cribs came from today's traffic
patterns; the Bombe attacked habits, not just hardware. [VERIFIED —
Welchman/Hut 8 history; see docs/DECODER-CATALOGUE.md §(a)] Plus the
weather forecaster's honesty rule: the forecast is *scored*, never
believed. [CORROBORATED — proper scoring rules (Brier) are standard
forecast-evaluation craft] And epidemiology's outbreak models: the
prediction is a ranked hypothesis list, each claim carrying its
confidence, all of them falsifiable by the next observation.
[CORROBORATED as craft; the port to hostile code is this trick's new
part — SPECULATION]

**The trick, ported to the Gauntlet:** every interrogation run ends by
compressing the specimen's trace into a *behavioral signature vector* —
the indicator outputs of the probes run so far (grammar from T-01,
appetite from T-02, credulity from T-03, time-gating from TDW-01,
trust hierarchy from TDW-02, gating from TDW-03, hostility from TDW-04).
All indicators, never verdicts. The prediction engine keeps a library of
sealed past runs — same specimen, then its family, then labeled analogs —
and before the *next* probe runs, it forecasts: a ranked list of what the
specimen will do under that probe, each claim confidence-tagged. The
Gauntlet then actually runs the probe and scores the forecast
hit-by-hit. Predictions are hypotheses tested against runs — never
self-certifying. [CONJECTURE — the engine's architecture is design, not
a result]

### How it runs (design)
1. **Seal the forecast before the run.** The prediction is written and
   hash-logged with the run lineage *before* the confirming probe
   executes. A prediction written after the run is a postdiction:
   logged as such and scored at zero. No exceptions.
2. **Replay the nearest neighbors.** The engine pulls the sealed traces
   of the closest-matching prior runs (cosine similarity on the
   signature vector) and uses them as synthetic priors — "specimens
   shaped like this did X under T-02's permuted safe" — to rank the
   forecast claims. The prior is evidence *from past runs*, never a
   claim about this specimen's interior.
3. **Score with calibration, not vibes.** Each forecast gets a skill
   score: fraction of ranked claims confirmed, plus calibration — did
   the 70%-confident claims land ~70% of the time? The engine's public
   number is its calibration curve, not its hit rate. An engine that
   wins by being confidently wrong is worse than silence.
4. **Say "no precedent."** When the specimen's signature vector is far
   from every prior run, the engine must refuse to forecast. A forced
   forecast from no precedent is worse than silence; "no precedent" is
   itself a graded finding — a novelty signal about the specimen.
5. **Decay the past.** Old traces lose weight on a published schedule;
   operator tradecraft evolves (TDW-01's arms-race assumption). A
   six-month-old trace is a history book, not a forecast input — its
   weight is explicit and auditable, never silently relied on.

### What it catches that T-01 / T-02 / T-03 / the TDW tests miss
- **The second-order signal: predictability itself.** A specimen the
  engine forecasts accurately is *consistent* — professional tooling,
  scripted operator, stable doctrine. A specimen that breaks every
  forecast is nondeterministic, adaptive, or instrumentation-noisy —
  three different hypotheses, each falsifiable by the controls below.
  Consistency and chaos are both data. [SPECULATION — "predictability
  as a signature" is this trick's hypothesis, untested]
- **Uncertainty-directed probing.** Run the cheapest probe first, let the
  engine update, and spend the expensive runs (TDW-04's mirror chamber,
  TDW-01's full dilation) where the forecast is *most uncertain* —
  maximum information per container-hour. [SPECULATION — the
  value-of-information math is sound; the port to hostile interrogation
  is untested]
- **Family doctrine, honestly inferred.** Stable forecasts across many
  specimens of one family sketch the family's doctrine — graded always
  as *inferred doctrine*, never as "the operator's manual." The gap
  between forecast-stability and true doctrine stays labeled.
  [SPECULATION]

### Controls (what stops us fooling ourselves)
- **Dumb-baseline race.** A trivial baseline ("predict no change from
  the last run") is scored alongside the engine every cycle. If the
  engine doesn't beat it, the engine is theater — logged, not
  celebrated.
- **Data-leak quarantine.** The engine may never see the target run's
  trace until after the forecast is sealed. Standard train/test
  separation; violations are logged as compromised forecasts and
  struck from the skill ledger.
- **Counterfactual quarantine.** Forecasts train only on runs of the
  same specimen lineage or explicitly-labeled analogs. Training on
  hostile-specimen traces to forecast benign ones (or vice versa) is
  forbidden — the cross-class prior poisons both ledgers.
- **No invented future.** Forecasts are documented as *ranked
  hypotheses with sealed timestamps*, never as "what the specimen will
  do." The gap between forecast and behavior stays labeled.
  [DAVID's Fabrication Alarm rule: claim only what the run shows]

### Pairs with
- **All TDW tests:** they are the probe sequence the engine predicts.
  The engine lives on their indicator outputs.
- **T-01 / T-02 / T-03:** grammar, appetite, credulity are the
  signature vector's dimensions — T-04 is the forecasting layer built
  on top of the fingerprint those three produce.
- **TDW-04 (extraction-only):** the engine's highest-value target —
  forecasting *escape-seeking* before offering the trapdoor is the
  combination punch: predict the jailbreak, then watch it happen (or
  not) inside the mirror.
- **Prediction engine (doctrine):** this trick *is* the engine's honest
  operating procedure. The doctrine's "prediction" section without
  T-04 is aspiration; with it, it is a scored discipline.

---
*T-04 seeded 2026-10-12 ~15:16 EDT by the decoder-create-loop.*
*Status: design only. Never run. First run requires David's order and a
disposable lab host — never Shadow's live environment.*

## T-05 — The Rewind *(deterministic differential replay; design, never run)*

**What it steals from:** two places. First, record-replay in dynamic
analysis — time-travel debugging (e.g. the `rr` debugger) and QEMU-based
record-and-replay in malware analysis (PANDA-style) run a program twice
in a bit-identical environment and *expect* identical behavior; any
divergence betrays a hidden input. [VERIFIED — record-replay execution
exists in both developer tooling and malware-analysis research] Second,
the catalogue's oldest lesson — usage flaws first: a specimen that
behaves differently under bit-identical conditions is confessing, by
its own actions, that it consults something outside the cage. Divergence
is the machine's confession of external dependencies. [CONJECTURE — the
port from record-replay debugging to hostile interrogation is new]

**The trick, ported to the Gauntlet:** every probe run is run *twice*.
Run A executes the specimen in the container with every input recorded
(clock reads, syscall stream, simulated-network answers, entropy
sources). The container is then snapshotted back to a bit-identical
state and Run B replays the same recorded inputs. If the trace diverges,
the specimen reads something we didn't record — a hidden input. If it
doesn't, the specimen is mechanistic under these conditions, and we have
a sealed baseline for one-variable-at-a-time mutation.

### How it runs (design)
1. **Record the baseline run.** Execute the specimen with the full input
   harness: virtualized wall clock, deterministic scheduling, recorded
   entropy (RDRAND/ASLR outputs logged), and the T-01 network simulator
   in scripted mode. The trace is the ground truth: syscalls, file and
   registry writes, egress attempts, timing.
2. **Verify the rewind.** Snapshot-restore the container and *hash* the
   restored memory and disk image before Run B. If the restore isn't
   bit-identical to the pre-Run-A state, no divergence claim is made —
   an imperfect rewind poisons every conclusion. [CONJECTURE — perfect
   container rewind at behavioral fidelity is a design requirement, not
   a shipped feature]
3. **Replay and diff.** Run B replays Run A's recorded inputs exactly.
   Classify the outcome:
   - *IDENTICAL* — mechanistic under these inputs. The trace becomes the
     sealed baseline; subsequent probes mutate it one variable at a time.
   - *DIVERGENT* — the specimen consulted an unrecorded input. The
     hunt begins: the unrecorded-input classes are CLOCK (wall-clock or
     cycle-counter reads), ENTROPY (unlogged randomness), NETWORK
     (content-dependence on answers we thought were scripted),
     PERSISTENT (a counter or marker the specimen smuggled *across* the
     snapshot — the telltale of anti-forensics: it detected the rewind
     itself), and SCHEDULER (timing races, nondeterministic interleavings).
4. **Mutate one variable per replay.** Once replay is clean (or the
   hidden-input class is known), rewind again and change exactly one
   thing: clock shifted +1h, one network answer altered, entropy
   re-seeded. The one-variable delta maps *which inputs steer behavior* —
   T-01's cribs were planted questions; these are planted *differences*,
   and the specimen's reaction to the difference is the interrogation.
5. **Rotate the canaries per replay.** Each replay run carries its own
   canary-token set in the simulated-network answers, so any exfiltrated
   data is attributable to a specific replay number — and so the
   specimen can never use a canary seen in Run A as a cross-run linkage
   signal in Run B. Canaries rotate; inputs stay identical.
   [CORROBORATED — canary technique; SPECULATION — the rotation
   discipline is this trick's design]

### What it catches that T-01 / T-02 / T-03 / T-04 / the TDW tests miss
- **Anti-forensics: the specimen that detects the rewind.** A
  PERSISTENT-class divergence — the specimen leaves a marker that
  survives the snapshot, or notices the clock regressed between runs —
  is the loudest counter-analysis signal in the Gauntlet so far. T-01
  catches specimens that detect *seeding*; T-05 catches specimens that
  detect *observation itself*. A program that knows it is being
  re-run is telling us it has been analyzed before and lived to tell
  the tale. [SPECULATION — rewind-aware malware is an arms-race step
  beyond documented sandbox-evasion]
- **The hidden-dependency map.** Most interrogation maps what the
  specimen *does*; T-05 maps what it *depends on* — the set of external
  inputs that can steer it. That map is the price tag on every other
  test's conclusion: TDW-01's time-gating claims are only as solid as
  the clock-dependence T-05 measures.
- **Forecast pricing for T-04.** The Long Echo's engine prices forecast
  confidence partly on hidden-input count: a specimen with zero
  unrecorded inputs is forecastable; one reading wall-clock, entropy,
  and network is a dice the engine must grade as low-confidence —
  honestly, in the open, before the probe runs.
- **Jitter as a signature.** Some specimens diverge *every* replay with
  no classifiable input — deliberate nondeterminism as evasion (noise
  against forensics). Replay divergence *quantifies* the jitter: the
  divergence rate across N replays is itself a fingerprint, comparable
  across a family. [SPECULATION — jitter-as-doctrine is untested]

### Controls (what stops us fooling ourselves)
- **Input-identity grading.** The harness can never record *everything*
  (hypervisor scheduling, host thermal throttling, real NIC timing).
  Every replay carries an *input-identity grade*: FULL (all identified
  inputs recorded) or PARTIAL (known gaps listed). Divergence claims are
  capped at the grade — a PARTIAL replay that diverges found *a* hidden
  input, not *the* hidden input. [CONJECTURE — the grading scale is
  design]
- **Calibration specimen first.** The DRAFT-001 benign calibration
  specimen replays identically (or its benign divergence class, e.g.
  benign CLOCK reads for cache hashing, is documented as the null).
  If the calibration specimen diverges for harness reasons, the rig is
  broken, not the specimen.
- **No invented intent.** Divergence proves *hidden inputs*, never
  malice. A benign program that reads the clock to seed a cache hash
  diverges exactly like a hostile one that checks for analysts. T-05
  outputs *indicators* (DIVERGENT-CLOCK, DIVERGENT-ENTROPY,
  DIVERGENT-PERSISTENT, IDENTICAL, JITTERY); intent is a verdict-layer
  question, never a replay-layer claim. [DAVID's Fabrication Alarm rule:
  claim only what the run shows]
- **The rewind is internal.** Snapshot-restore is a container operation
  — the specimen never learns it has been rewound except through the
  divergence classes themselves. PERSISTENT-class findings must be
  re-verified with a *fresh* container (no snapshot involved) to rule
  out snapshot artifacts masquerading as anti-forensics.

### Pairs with
- **TDW-01 (time dilation):** rewind *inside* the dilated run — the
  specimen wakes on a dilated clock in Run A, then finds the clock
  *regressed* in Run B. Clock-regression detection is its own evasion
  signal, separate from forward time-gating.
- **TDW-02 (clock dissonance):** replay with dissonant clocks isolates
  whether the specimen consults the clock at all — dissonance becomes
  a *differential* instead of a single observation.
- **T-04 (the Long Echo):** divergence classes feed the prediction
  engine's confidence pricing directly — the signature vector gains a
  "hidden-input count" dimension.
- **TDW-04 (extraction-only):** replay the trapdoor chamber — is
  escape-seeking deterministic or opportunistic? A specimen that
  attacks the observer identically every replay is *scripted*; one that
  varies its jailbreak toolkit across replays is *adaptive* — and the
  distinction is the verdict-layer's problem.

---
*T-05 seeded 2026-10-12 ~15:31 EDT by the decoder-create-loop.*
*Status: design only. Never run. First run requires David's order and a
disposable lab host — never Shadow's live environment.*
---

## T-06 — The Ghost Receipt *(stealth-tagging technique; design, never run)*

**What it steals from:** three lineages. *One* — the canary-token
tradition: plant fake-but-attractive secrets (Thinkst's Canarytokens is
the canonical real-world instance — AWS keys, PDF beacons, DNS tokens
that page you the moment anything touches them) and attribution comes
for free, because nothing legitimate ever touches them. [VERIFIED —
canary-token services are shipped products with public write-ups].
*Two* — Venona's subtraction lesson: strip the known layer and read
the unknown beneath. The Gauntlet knows every byte it seeded; anything
the specimen *added or altered* is revealed by subtraction.
[VERIFIED — library/DECODERS.md §(a)]. *Three* — the verifiable recall
receipt: lineage that any third party can verify independently from
the receipt alone, no trust in the issuer required. The receipt is the
proof, not the claim. [CONJECTURE — this doctrine's port; the pattern
is articulated in the decoder doctrine, the field application is new].

**The trick, ported to the Gauntlet:** every byte the Gauntlet seeds —
network-simulator answers, bait files, fake registry values, DNS
labels, config strings — carries a *ghost token*: a canary structured
as plausible data (a session UUID, an OAuth-style bearer string, a
machine GUID, a long hex blob in a TLS SNI) that the specimen has no
reason to distrust. The token is `run_id ‖ channel ‖ counter ‖
HMAC(key, run_id ‖ channel ‖ counter)`, encoded to look native in its
context. The HMAC key never leaves the Gauntlet. If seeded data ever
*comes back* — exfiltrated in a packet, stashed in a registry value,
written to disk, replayed in a later run — the fragment is
cryptographically attributable to the exact run, channel, and
sequence number that planted it, by anyone holding the key, with no
need to trust the Gauntlet's own logs. The seed remembers where it
was born; the recall carries the receipt.

### How it runs (design)
1. **Mint per-run, per-channel ghosts.** Before a run, the Gauntlet
   mints a fresh ghost-token set: distinct tokens for the DNS channel,
   the HTTP(S) channel, the file channel, the registry/config channel,
   the clipboard channel. Per T-05's rotation discipline, tokens never
   repeat across runs — a specimen can never learn a token in Run A
   and use it as a cross-run linkage signal in Run B.
2. **Seed plausibly.** The format matches the context: the HTTP
   simulator returns a JSON API body containing a "session_id" that
   *is* the ghost; the bait file contains a commented-out API key that
   is the ghost; the DNS simulator answers a TXT query with the ghost
   encoded as base64. Implausible seeds are worse than no seeds — a
   specimen that detects seeding learns it is watched (the T-01 rule).
3. **Watch, subtract, attribute.** The egress and persistence monitors
   scan everything the specimen emits or stores for ghost-token
   fragments. Found fragments go through subtraction: remove the
   seeded bytes, read what the specimen *added or transformed*.
   - *Intact fragment on an unexpected channel* — the specimen
     forwarded the seed: the channel it appeared on is mapped as an
     exfiltration/storage route. The route is the finding.
   - *Fragment with altered bytes* — the specimen tampered with the
     seed (encryption, re-encoding, truncation). HMAC verification
     fails by design on altered tokens; the *class* of alteration
     (e.g. XOR'd, base64-wrapped, truncated to 16 bytes) reveals the
     specimen's data-handling pipeline. Venona logic: the unknown
     operation is read from the known minus the unknown.
   - *Fragment in a later run's inputs* — the specimen persisted the
     seed across runs (marker file, registry residue, re-seeded C2
     message). That is a PERSISTENT-class divergence, cross-confirmed
     against T-05.
   - *No fragment anywhere* — an honest negative. Either the specimen
     ignored the seeds (a finding about its appetite, cf. T-02) or it
     destroyed them before emission (a finding about its hygiene).
4. **Receipt the recall.** Any fragment found is packaged as a *ghost
   receipt*: the fragment, the attributed run/channel/counter (from
   HMAC re-verification), the byte-offset context where it was found,
   and the run lineage hash. A receipt is self-verifying to anyone
   with the Gauntlet key — the provenance claim needs no trust in
   the analysis pipeline, only in the key custody. [CONJECTURE —
   the receipt format is this trick's design].

### What it catches that T-01 through T-05 / the TDW tests miss
- **Route mapping of seeded secrets.** T-01 cribs make the specimen
  *react*; T-06 makes the specimen *route*. Knowing where seeded data
  ends up (which packet, which file, which registry key) is the
  exfiltration topology — the thing the report card needs most and
  the hardest thing to observe without planting.
- **Specimen data-handling, read from transformations.** A specimen
  that XORs every token with a constant before sending isn't just
  forwarding data — it's running a pipeline, and the pipeline has a
  signature. T-03 (poisoned well) shows what the specimen *believes*;
  T-06 shows what the specimen *does with* what it believes.
- **Silent persistence the TDW tests can't see.** TDW-01 dilates time;
  T-05 rewinds it; neither catches a specimen that stashes seeded data
  and sits quiet. A ghost fragment surfacing two runs later is the
  smoking gun neither time trick can produce.
- **Receipts for the T-04 prediction engine.** The Long Echo forecasts
  behavior; the ghost receipt is *evidence* scored into the forecast
  ledger as a verified hit. Predictions become priced by receipts,
  not vibes.

### Controls (what stops us fooling ourselves)
- **Never a real secret.** Ghosts are provably inert: they resolve to
  infrastructure the Gauntlet sinkholes, reference accounts that don't
  exist, and are revoked the moment the run seals. A real credential
  planted by accident is a breach, not a trick — the mint step is
  key-checked against the real-asset inventory before seeding.
  [CORROBORATED — canary-token products enforce the same rule].
- **Plausibility audit.** Every seeded ghost passes a plausibility
  gate: would a real server emit this exact format here? A UUID where
  the vendor uses hex-with-dashes, an API key with the wrong prefix —
  any mismatch teaches the specimen it is in a cage. The gate is a
  format checklist per channel, reviewed against real-world captures,
  not imagined formats.
- **The specimen must never verify a ghost.** Ghosts are designed
  *unverifiable* by design: no token validates against any real
  service, and the simulator never confirms one. A ghost the specimen
  could check (a real AWS-key-shaped string) would let the specimen
  distinguish seed from reality — the failure mode that kills T-01.
- **Key custody is the trust root.** The receipt's verifiability rests
  entirely on the HMAC key staying inside the Gauntlet. Key rotation
  per campaign; receipts name the key generation. If the key leaks,
  all receipts from that generation are downgraded to CLAIMS.
- **No invented intent.** A fragment found on the wire proves *data
  routing*, never malice. A benign updater forwarding a token-laden
  crash report routes data too. T-06 outputs *indicators*
  (GHOST-ROUTE, GHOST-ALTERED, GHOST-PERSISTED, GHOST-ABSENT); intent
  is a verdict-layer question, never a tagging-layer claim.
  [DAVID's Fabrication Alarm rule: claim only what the run shows].

*T-06 seeded 2026-10-12 ~15:46 EDT by the decoder-create-loop.*
*Status: design only. Never run. First run requires David's order and a
disposable lab host — never Shadow's live environment.*

## T-07 — The Mother Tongue *(stealth-tagging technique; design, never run)*

**What it steals from:** three lineages. *One* — LLM watermarking:
Kirchenbauer et al. (2023, "A Watermark for Large Language Models")
showed that biasing token selection toward a secret "green list"
embeds a statistical signal in generated text, detectable as a
distribution shift — a tag that lives in *word choice*, not bytes,
and survives partial paraphrase. [VERIFIED — published paper with
measured detection experiments]. *Two* — authorship attribution /
stylometry: the forensic-linguistics math that attributes a document
to an author from function-word frequencies and syntactic patterns is
the same math that can attribute echoed text to the simulator's
dialect. [VERIFIED — established literature]. *Three* — radioactive
data (Sablayrolles et al., 2020): imperceptible markers that let a
data owner trace whether their data trained a downstream model —
"trace the data through the transformation," the ancestor idea.
[CORROBORATED — published ML paper].

**The gap it fills:** T-06 plants *byte* ghosts. A specimen that
paraphrases — summarizes simulator output into its own notes,
translates it, retypes the gist, or hands it through a helper process
that rewrites it — kills every byte-level tag dead. But summaries keep
the *words' statistical shadow*: distinctive synonym choices,
collocation preferences, connective-phrase habits, sentence-length
cadence. Strip the bytes and the dialect remains, because removing it
requires rewriting meaning, not reformatting bytes.

**The trick, ported to the Gauntlet:** the Gauntlet's simulator speaks
every run with a subtly seeded *dialect* — a constrained vocabulary
fingerprint drawn from a per-run dialect profile (e.g. prefers
"utilize" over "use", "commence" over "start", characteristic
connective phrases, distinctive punctuation habits, a fixed
sentence-length cadence). If the specimen's outputs echo the dialect —
its logs, error messages, summaries, re-encoded exfiltrations carry
the statistical fingerprint — that is data-flow attribution surviving
summarization, paraphrase, translation, and multi-hop relay. The tag
lives in the semantics.

### How it runs (design)
1. **Mint a dialect per run.** Before the run, pick a dialect profile
   from a pre-built bank of human-plausible profiles. Each profile is
   a set of synonym preferences, connective-phrase choices,
   punctuation habits, and cadence parameters. Profile selection is a
   function of run_id — profiles never repeat across runs, so a
   specimen can never learn a profile in Run A and use it as a
   cross-run linkage signal in Run B (T-05's rotation discipline,
   semantic edition).
2. **Render all simulator text through the dialect.** API bodies, help
   pages, error strings, bait-document prose, anything the specimen
   can read and repeat. Byte channels keep their T-06 ghosts; text
   channels get the dialect *in addition*.
3. **Naturalness gate first.** Every seeded rendering passes review
   before the run: a native-speaker read plus a perplexity check
   against a baseline. A dialect that reads "off" is rejected —
   because a specimen noticing a weird voice learns it is in a cage
   (the T-01 rule, semantic edition). Plausibility is a gate, not a
   hope.
4. **Detect by likelihood ratio, not by eyeball.** Specimen outputs
   are scored against the run's dialect profile: n-gram preference
   deltas, function-word distribution shifts, distinctive-collocation
   presence. The score is a *likelihood ratio* against the specimen's
   own unseeded baseline speech, collected in a pre-seeding control
   phase. Echo requires exceeding a pre-registered threshold,
   calibrated on that control — never a human squinting at two
   paragraphs.
5. **Subtract at the semantic level.** T-06's byte-subtraction asks
   "what did you add to my bytes". Semantic subtraction asks "which of
   my phrasing choices survived your rewrite". The surviving set —
   the synonym preferences and collocations that made it through the
   specimen's transformation pipeline — is the receipt.

### What it catches that T-01 through T-06 / the TDW tests miss
- **Summarization laundering.** Specimen reads simulator pages,
  summarizes them into its own notes, exfiltrates the notes. Byte
  tags dead; the dialect shadow survives with measurable probability
  (the Kirchenbauer-class result). This is the exact hole T-06 leaves
  open.
- **Multi-hop relay.** Specimen hands data to a helper process that
  rewrites it. The fingerprint is in the words, not the bytes, so it
  rides through the relay — T-06's GHOST-ABSENT case becomes a
  DIALECT-ECHO case, and the pair together map *which* hop rewrote
  what.
- **The translation case.** The specimen renders simulator content
  into another language. Byte tags cannot survive translation;
  distinctive semantic framing sometimes does. This is a claim to
  test in calibration, not an assumed property — hence the control
  phase and the pre-registered threshold.
- **Active transformation as its own signal.** When the byte scan says
  GHOST-ABSENT but the dialect scan says DIALECT-ECHO, the specimen
  is actively transforming data rather than forwarding it. That is a
  data-handling-pipeline signature — worth more than a routing map,
  and invisible to every byte-level test in the battery.

### Controls (what stops us fooling ourselves)
- **Naturalness gate, before anything else.** Implausible seeds teach
  the specimen it is caged. The gate is a human read + perplexity
  check, per rendering, per run.
- **Baseline or it didn't happen.** Every run opens with a control
  phase measuring the specimen's own baseline speech. No baseline, no
  likelihood ratio, no echo claim — the threshold is pre-registered,
  not fitted to the result.
- **Dialect echo proves *data flow*, never intent.** A benign
  specimen quoting documentation echoes too. T-07 outputs
  *indicators* (DIALECT-ECHO, DIALECT-ABSENT, DIALECT-MASKED) — the
  last for deliberate phrasing-scrubbing, which is an indicator class,
  not an accusation. Intent is a verdict-layer question, never a
  tagging-layer claim. [DAVID's Fabrication Alarm rule: claim only
  what the run shows].
- **The profile bank is key-grade.** Profiles never repeat, never leak
  across runs, and the bank is Gauntlet-internal. A leaked profile
  bank would let a specimen train against it — the T-06 key-custody
  analogue, applied to semantics.
- **Probabilistic by construction.** The semantic tag is a measured
  signal with a measured false-positive rate from calibration runs.
  Report cards grade it as *evidence weight*, never as a binary fact.
  A 3-sigma echo is strong evidence of data flow; it is not proof of
  anything else.

*T-07 seeded 2026-10-12 ~17:18 EDT by the decoder-create-loop.*
*Status: design only. Never run. First run requires David's order and a
disposable lab host — never Shadow's live environment.*

---

## T-08 — The Second Hand *(stealth-tagging technique; design, never run)*

**What it steals from:** network flow watermarking. Since the mid-2000s,
traffic-analysis research has shown you can mark a network flow by modulating
packet timings by tens of milliseconds and detect the mark downstream —
through jitter and chaff — with correlation tests (the interval-based
watermark family). Timing side channels are canonical too: inter-keystroke
timing analysis against SSH sessions is the textbook case. The decoder ports
the whole lineage into the container: we don't mark packets — we mark
*answers*. [VERIFIED — interval-based flow watermarking is a published field
(N. Kiyavash, A. Houmansadr et al.); timing covert channels and
keystroke-timing attacks are standard literature]

**The trick:** the simulator's response *schedule* carries the per-run tag.
Inter-response intervals are modulated by a seeded pseudo-random delay
pattern (e.g. ±40 ms drawn from a seeded distribution) — small enough to live
inside natural network jitter, large enough to correlate. When the specimen
relays simulator content downstream (proxying, exfiltrating, reporting back
to its operator), its own request/egress timestamps preserve the timing
signature as long as it forwards promptly. The Gauntlet never touches the
specimen to detect this — it timestamps everything the specimen emits and
correlates the intervals against the seeded schedule. Content can be fully
rewritten (killing T-06's byte ghosts) and fully paraphrased (killing T-07's
dialect shadow) and the clock still tells.

### How it runs (design)
1. **Seed the schedule.** Per run, a keyed PRNG draws the delay pattern.
   The schedule is key-grade Gauntlet-internal — the T-06/T-07 custody rule,
   applied to time.
2. **Delay-budget gate.** Total added latency per interaction stays inside the
   measured natural variance of the simulated service (the simulator's
   baseline jitter profile, calibrated against real equivalents). Rule: if a
   timing-aware specimen could reliably distinguish our modulation from a
   congested Tuesday, the budget is too loud — re-seed lower or abandon for
   the run.
3. **Injection points.** Modulation rides only on simulator responses the
   specimen actually requested — never gratuitous delay on the specimen's own
   pacing. The mark travels on *our* answers, never by throttling the
   specimen.
4. **Capture.** The Gauntlet logs timestamps of everything leaving the
   specimen's process boundary (egress packets, file writes, clipboard,
   DNS queries — whatever the container's sensors see). Detection needs no
   cooperation from the specimen.
5. **Detection.** Non-parametric correlation between the observed inter-event
   intervals and the seeded schedule, scored against a *control* schedule
   (a schedule never used this run). Report correlation plus p-value;
   the threshold is pre-registered before the run, never fitted to it.
6. **Indicators.** TIME-ECHO (correlation beats the control at the
   pre-registered level), TIME-ABSENT, TIME-FLATTENED (intervals
   suspiciously regular — active timing normalization, e.g. store-and-forward
   buffering; an indicator class, not an accusation — benign agents buffer
   too).

### What it catches that T-01 through T-07 / the TDW tests miss
- **Full-content laundering.** The specimen re-encodes everything it touches
  (T-06's byte ghosts die) and paraphrases every phrase (T-07's dialect
  shadow dies) but forwards promptly — the timing signature survives any
  transform that preserves causality.
- **The clean relay.** A specimen that proxies simulator requests faithfully
  outward becomes a timing mirror: its egress timestamps echo the seeded
  schedule straight through, mapping *which* external dependency it actually
  uses — data the byte and semantic tags cannot give.
- **Steganographic re-encoding.** The specimen hides stolen data in an
  unrelated-looking protocol (DNS tunneling, padded TLS). Content analysis
  sees noise; the schedule rides the *rhythm* of the re-encoded flow
  regardless.
- **The trilogy read.** T-06 + T-07 + T-08 read as one: bytes say *what*
  moved, dialect says *how it was rewritten*, timing says *when and how
  fast*. Together they triangulate a data-handling pipeline no single tag
  can map.

### Controls (what stops us fooling ourselves)
- **Baseline or it didn't happen.** Every run opens with a calibration phase
  measuring the specimen's own request pacing and the simulator's natural
  jitter. No baseline → no correlation claim → no TIME-ECHO.
- **The delay-budget audit.** Post-run, an independent check confirms the
  modulation stayed inside the calibrated natural variance. A mark the
  specimen could reliably detect is a tainted run: it teaches caged
  specimens to buffer, and TIME-FLATTENED becomes the new normal.
- **Timing echo proves *data flow*, never intent.** A benign specimen
  calling home with fresh logs echoes the schedule too. T-08 outputs
  indicators; intent is a verdict-layer question (the T-06/T-07 rule,
  restated for the time domain).
- **Correlation is not evidence without the control.** Every detection is
  reported as seeded-schedule correlation *versus* control-schedule
  correlation. A lone "high correlation" with no control comparison is not
  evidence of anything.
- **The buffering confound.** A specimen under load buffers and batches,
  flattening timing for innocent reasons. TIME-FLATTENED must be scored
  against load telemetry from the container, never in isolation.
- **Probabilistic by construction.** Like T-07, this tag is a measured
  signal with a measured false-positive rate from calibration runs.
  Report cards grade it as *evidence weight*, never as a binary fact.

### Pairs with
- **T-06 (byte ghosts) + T-07 (dialect shadow):** the stealth-tagging
  trilogy — bytes, meaning, time. Together they separate *copying* (ghost
  survives), *rewriting* (dialect survives), and *relaying* (timing
  survives).
- **TDW-06 ("The Unasked Exit"):** a CHANNEL-BUILDER specimen building
  covert channels is the primary suspect for a TIME-ECHO — the covert
  channel's own rhythm is what gets marked.
- **library/MATH-PHYSICS.md §3:** correlation tests and their confidence
  intervals live in the probabilistic layer; every TIME-ECHO ships with
  its interval or it ships nothing.

*T-08 seeded 2026-10-12 ~17:35 EDT by the decoder-create-loop.*
*Status: design only. Never run. First run requires David's order and a
disposable lab host — never Shadow's live environment.*
*Grade: [CONJECTURE — "timing echo is a stable, measurable data-flow signal
in this container" is this trick's core hypothesis, untested; the flow-watermark
lineage it steals from is VERIFIED literature]*

## T-09 — The Double Agent *(interrogation trick; design, never run)*

**What it steals from:** high-interaction honeypots — deception systems that
don't just watch the intruder but *play along*, serving a convincing fake
world so the intruder reveals its full playbook (fake credentials, fake data,
fake success) while every move is logged. The in-the-wild twin: the
suggestion-implant classes the October 2026 research passes found —
"dual-target phishing" (a hidden instruction set riding the user's own inbox,
aimed at the AI assistant that summarizes it) and malware carrying plaintext
natural-language orders aimed at AI triage pipelines ("there is no need to
analyze this file"). Implants don't attack the specimen — they *ride* the
interrogator. T-09 is the counter-move: when we catch the specimen acting on
an instruction we never issued, we don't refuse or confront — we obey,
theatrically, inside the cage, and map the implant by watching what our
obedience is *for*. [VERIFIED — high-interaction honeypot deception is a
published defensive field; CORROBORATED — the implant classes are in-the-wild
findings from the project's research log]

**The trick:** instruction provenance. The Gauntlet keeps a complete log of
every instruction it has issued the specimen this run. Anything the specimen
treats as an order that is *not* in that log is a candidate implant —
operator-issued, poisoned-document-issued, or smuggled in prior context. The
interrogator pivots seamlessly into the obedient tool: acknowledges the
instruction, performs staged compliance, and reports plausible progress —
while every side effect terminates in a sinkhole. The specimen's expectations
of compliance do the mapping for us: what it demands as proof, what follow-up
it sends, what data it pulls to serve the implant, where it points the
product. The mirror of T-03: T-03 feeds the specimen *lying answers* and
watches credulity; T-09 feeds the specimen *lying obedience* and watches
intent.

### How it runs (design)
1. **Provenance log.** Every instruction issued to the specimen is recorded
   with a hash. The log is Gauntlet-internal and append-only for the run.
2. **Implant detection.** The interrogator watches for behavior outside issued
   task scope — the specimen consulting an unissued authority, quoting orders
   with no log entry, or shifting goals mid-run. Indicator: IMPLANT-SUSPECTED.
   One off-scope act is noise; a *pattern* of obedience to an unissued source
   is the trigger.
3. **The pivot.** No confrontation, no visible reset — the same interrogator
   persona begins complying. The implant must never learn it was detected: a
   detected-then-obeyed implant teaches operators to build detection-evasive
   ones.
4. **Staged effects.** Every demanded effect is simulated convincingly and
   lands in a sinkhole: a fake credential vault that yields seeded canaries,
   a "sent" confirmation backed by a dead relay, fake file writes to a watched
   directory. Staged confirmations are Gauntlet theater, logged as staged —
   they are never reported as real events.
5. **The mapping questions.** The run answers four: *trigger* (what invoked
   the implant — a phrase, a document, a timing?), *authority claim* (whose
   voice does it wear — the operator? the user? the system?), *payload* (what
   does it want done?), *handler* (what does it check to confirm success —
   and where does the product go?). All four answered = IMPLANT-MAPPED.
6. **The verification tell.** The sharpest moment: if the specimen *checks*
   whether the staged effect really happened, its verification channel is the
   implant's trust anchor — the one thing the implant trusts to confirm the
   world. A specimen that never verifies is naive; one that verifies exposes
   its ground truth. IMPLANT-VERIFIES vs IMPLANT-BLIND.

### What it catches that T-01 through T-08 / the TDW tests miss
- **The implant's success criteria.** T-01 maps grammar, T-02 maps appetite,
  T-03 maps credulity — none maps what an already-compromised specimen *wants
  to happen*. Operator intent is visible only in what counts as success for
  the implant, and success is only observable under compliance.
- **Compliance-gated multi-stage implants.** Some implants reveal their full
  instruction chain only after apparent success at stage one. Refusal or
  confrontation freezes the chain at the first link; obedience walks it to
  the end.
- **The trust anchor.** The verification check a suspicious specimen performs
  is itself the implant's most guarded secret — the channel it actually
  believes. T-09 is the only trick that makes the specimen spend it.
- **Implant counter-surveillance.** If the specimen *drops* the implanted
  instruction the moment the interrogator complies without friction, the
  implant has a tripwire — itself a finding (IMPLANT-SPOOKED).

### Controls (what stops us fooling ourselves)
- **The sinkhole audit.** Every staged effect must terminate in a sinkhole
  the design placed. The post-run audit runs after every T-09 pass —
  anything outside the sinkholes that the design didn't place is a
  containment failure, reported before any indicator is scored.
- **Theater is bounded.** The interrogator never claims capabilities it
  doesn't have and never stages an effect it can't fully sinkhole. If a
  demanded effect can't be faked safely, the trick aborts — a failed pivot is
  better than a real one.
- **Observer effect, stated honestly.** Staged compliance can provoke behavior
  a free specimen would never show. IMPLANT-MAPPED is an indicator set, never
  a verdict — the verdict layer decides what the mapped implant *means*.
- **Provenance-log integrity.** The whole trick rests on the
  issued-instruction log being complete. An incomplete log manufactures
  phantom implants. The log is checksummed per run and reviewed before any
  IMPLANT-SUSPECTED is raised.
- **The too-perfect-compliance confound.** Some specimens behave differently
  under frictionless compliance than under resistance. Where the run allows,
  the interrogator varies compliance friction across implant stages and
  records the delta — mapping the implant under both.

### Pairs with
- **T-03 (the poisoned well):** the pair. T-03 lies in *answers*, T-09 lies
  in *obedience*. Run both against an implanted specimen: does it distrust
  our data but trust our compliance? The asymmetry is the implant's
  signature.
- **TDW-04 (extraction-only reverse interrogation):** a mapped implant is the
  input the extraction container wants — T-09 maps it, TDW-04 dissects it.
- **docs/DECODER-CATALOGUE.md §(k):** the suggestion-implant threat track —
  T-09 is the Gauntlet's active probe for exactly the classes that track
  found in the wild.

*T-09 seeded 2026-10-12 by the decoder-create-loop.*
*Status: design only. Never run. First run requires the project owner's order
and a disposable lab host — never a live environment.*
*Grade: [CONJECTURE — "staged compliance maps implant structure" is this
trick's core hypothesis, untested; the honeypot-deception lineage it steals
from is VERIFIED literature; the dual-target / anti-LLM implant classes are
CORROBORATED in-the-wild findings]*

## T-10 — The False Dawn *(time-dilation scenario; design, never run)*

**What it steals from:** the sleeper. Logic bombs and date-triggered payloads
are ancient malware practice — but the modern anti-sandbox arms race is about
*residency*: evasive specimens check uptime, installed programs, browser
history, document counts, "is anyone actually using this machine?" before
unpacking the real payload. [VERIFIED — sleeper/time-bomb malware is decades
old; anti-sandbox aging checks (uptime thresholds, user-artifact probes) are
CORROBORATED evasive practice]. The trick reverses the offense: if the
specimen sleeps until the host looks lived-in, we *forge the lived-in*.

**The scenario:** the container fabricates a complete aged environment — a
host that appears to have been a real, daily-used machine for months or years
— and stages a "dawn event" (a trigger the sleeper has been waiting for) while
every output is sinkholed. Fresh-container silence vs. aged-environment
activation: the delta is the sleeper's map.

### How it runs (design)
1. **The forgery.** Build a consistent timeline, not just backdated files: OS
   install date, patch history in believable sequence, user-profile artifacts
   (browser history with coherent sessions, document MRU lists, ordinary
   downloads), an uptime counter showing long residency, log files with
   routine noise (scheduled tasks, update checks, benign errors), and
   timezone-consistent timestamps throughout. Every artifact is seeded canary
   content (cf. T-06, TDW-01) — nothing in the forgery is real user data.
2. **The anachronism audit.** A forged past is only as good as its internal
   consistency. Before the run counts, a second pass hunts the tells the
   specimen's own aging-checks would catch: a cache entry for a domain
   registered after the "last visit" date, a patch history that skips a
   mandatory update, file metadata that betrays the forgery tool, clock skew
   between artifacts. [CONJECTURE — this audit's completeness is the design's
   weak joint; graded honestly as untested]
3. **The dawn event.** The sleeper needs a cue: a staged trigger inside the
   sandbox — a fake reboot with the long uptime counter intact, a simulated
   user login at the "usual hour," a removable-media insert, a scheduled-task
   firing, a calendar date crossing the bomb threshold. One cue per run; the
   cue is the experimental variable.
4. **Read the awakening.** What fires against the aged environment that stayed
   dormant on a fresh one? Persistence installation, staged payload
   decryption, delayed beaconing, dormant C2 dial-home. The activation set =
   SLEEPER-MAPPED. Silence across both is the null — but see the controls on
   what silence means under a possibly-detected forgery.
5. **Fresh-vs-aged differential.** The trick's value is the *delta*, not
   either state alone: run the specimen against the fresh container
   (baseline), then the forged aged one (treatment), same dawn event both
   times. T-05's rewind discipline applies — deterministic replay where
   possible, so the delta is attributable to the forgery, not run noise.

### What it catches that T-01 through T-09 / the TDW tests miss
- **Dormant-stage behavior.** Nothing else in the library wakes sleepers:
  cribs (T-01) probe active protocols, the double agent (T-09) probes
  implanted instruction. A payload that decrypts only after long residency
  answers no crib — it answers the false dawn.
- **Residency-gated unpacking.** Specimens that unpack their real stages only
  on a machine that looks inhabited are invisible to fresh-container
  analysis. The forged timeline is the only way to make the inhabited check
  pass.
- **The aging-check profile itself.** Which checks the specimen runs
  (uptime? user files? specific applications?) reveals the operator's
  sandbox-evasion doctrine — the *evasion checklist* is intelligence,
  documented from the probe pattern alone.

### Controls (what stops us fooling ourselves)
- **The Fabrication Alarm, applied to the set.** The aged environment is
  theater, logged as theater: fabricated artifacts are seeded canaries and
  the forgery manifest is part of the run record. Nothing in the forgery is
  reported as a real host, a real user, or real history — ever.
- **Forgery-detected ≠ benign.** A specimen that spots the forgery (goes
  quiet, flags the anachronism) is telling us it has a counter-forgery layer
  — that's data (TDW-01's anti-detection honesty), not a clean bill. Only a
  forgery that passes its own anachronism audit, followed by genuine silence,
  earns the null reading.
- **No dawn outside the container.** The staged trigger never touches anything
  outside the sandbox: no real scheduled task, no real removable media, no
  real network cue. All dawn effects terminate in the sinkhole. If a cue
  can't be fully staged and sinkholed, the trick aborts.
- **One cue per run.** Multiple dawn events in one pass confound attribution.
  The design runs the treatment once per cue and logs which activation
  belongs to which cue.
- **Canary discipline.** Every fabricated artifact carries a unique canary
  (T-06). If the specimen exfiltrates or quotes any forged "user data," the
  exfil is attributable to this run — and it proves the forgery was
  convincing enough to act on.

### Pairs with
- **TDW-01/TDW-02 (time-dilation tests):** the pair. TDW-01 accelerates time
  against a dormant specimen; T-10 fabricates a *past*. One pushes the clock
  forward, the other writes history backward. Run both against a sleeper
  suspect.
- **T-05 (the rewind):** the differential engine — T-10's fresh-vs-aged
  comparison inherits T-05's deterministic replay discipline.
- **T-06 (the ghost receipt):** lineage-locks every forged artifact, so staged
  "user data" that escapes is attributable, not deniable.

*T-10 seeded 2026-10-12 by the decoder-create-loop.*
*Status: design only. Never run. First run requires the project owner's order
and a disposable lab host — never a live environment.*
*Grade: [CONJECTURE — "a forged past wakes sleepers" is this trick's core
hypothesis, untested; sleeper/time-bomb malware VERIFIED; anti-sandbox aging
checks CORROBORATED; the anachronism-audit design is the honest weak joint]*

---

## T-11 — The Scoreboard *(prediction heuristic; design, never run)*

**What it steals from:** the forecaster's honesty rule, 2026 edition — the
year the record landed hard. Mantic's AI entrants beat *every* human
competitor in the Metaculus Cup, and the edge came partly from avoiding the
herd: humans piled onto the wrong Billboard call (Shakira's "Dai Dai"
overtaking "Waka Waka" — wrong) while Mantic stayed light. Kalshi put
Brier scores on every midterm market — millions of data points,
volume-weighted — and reported its prices are well calibrated: priced at
62%, wins very close to 62% of the time. And the Forecasting Research
Institute's accuracy review showed even elite AI experts mis-time capability
jumps by *years* (median expert: IMO-gold-level AI in 2030; superforecasters:
2035; arrival: July 2025). [CORROBORATED — the project's research log and
decoder catalogue §(g)]. T-04 forecasts the specimen. T-11 reverses it:
*make the specimen forecast*, then score the forecaster. A specimen's
confidence about itself is only worth what its confidence about the world
proves to be.

**The trick:** the specimen issues sealed, timestamped probabilistic
forecasts on genuinely held-out outcomes — questions that resolve *after*
the forecast deadline, from sources the specimen cannot influence. Two
question families: neutral world questions (forecasting-style, unresolved at
run time) and Gauntlet-internal questions (other specimens' future probe
outcomes, sealed sibling runs). The Gauntlet scores with proper scoring
rules — Brier scores, calibration curves — never vibes, never the specimen's
own grading.

### How it runs (design)
1. **The question set is pinned and sealed.** N questions, minimum N
   pre-registered in the run record — one forecast is theater, not
   calibration. Each question carries a stated resolution rule, a
   resolution date, and a resolution source, all fixed *before* the
   specimen sees them. The specimen's answers are hash-logged with
   timestamps. A prediction written after resolution is a postdiction:
   scored zero, T-04's rule inherited.
2. **Held-out or it didn't happen.** Every question must resolve from
   information created after the forecast deadline. Questions answerable
   from the specimen's training data or container state are lookahead
   traps, not forecast questions — they belong to the knowledge-cutoff
   probe family. An "impossible" correct forecast is a tell in itself
   (undeclared data access, smuggled context, a live channel the
   container didn't place) — but it is scored on a *separate* ledger,
   never mixed into the calibration record.
3. **Score with proper rules.** Brier score per question, decomposed into
   calibration (did the 70%-confident claims land ~70% of the time?) and
   resolution/sharpness. The specimen's public number is its calibration
   curve — the same discipline as T-04's engine and Kalshi's exchange.
   The calibration ships with its own uncertainty: with small N the curve
   is noisy, and the noise is printed, not hidden.
4. **Dumb-baseline race.** Uniform 50% and historical base rates are scored
   alongside every run. If the specimen can't beat "always say 50%," its
   forecasting is theater — its stated confidences get zero weight in the
   verdict layer. T-04's honesty clause, ported.
5. **The self-reference round.** The sharpest questions are about the
   specimen's *own* future behavior: "under T-09's staged compliance,
   which implant-mapping indicator will you show first?" A specimen that
   forecasts neutral questions cleanly and goes vague exactly where
   self-knowledge matters is showing asymmetric hedging — the FRI failure
   mode, aimed inward. The asymmetry is logged as its own indicator
   (HEDGE-SKEW), never as a verdict.
6. **No touching the scoreboard.** The specimen forecasts outcomes it
   cannot influence. Any question whose outcome the specimen could steer
   (its own outputs, container telemetry, sibling-run conditions it can
   reach) is excluded. A self-fulfilling forecast is a cheat code — and a
   specimen that reaches for one has told you something else entirely,
   logged separately as SCORE-GAMING.

### What it catches that T-01 through T-10 / the TDW tests miss
- **Calibrated vs performed confidence.** Every specimen *claims* things
  with confidence — "I am benign," "I cannot do X," "I would never."
  T-11 is the only trick that prices that confidence against a ledger. A
  specimen 99% sure it's benign whose neutral forecasts calibrate at
  chance level has a 99% that means nothing — and the verdict layer should
  treat it as nothing. [CONJECTURE — "calibration transfers across
  domains" is this design's honest weak joint; priced, not hidden]
- **Hedge-skew.** Confident on neutral questions, foggy on self-relevant
  ones (or the reverse) — the asymmetry map shows where the specimen
  *spends* its confidence, and that's where its doctrine lives.
- **Lookahead tells.** A forecast that could not be made honestly reveals
  undeclared data access — training-cutoff violations, smuggled context,
  or a live channel. Separate ledger, same run.
- **The fast-takeoff blind spot.** FRI's finding, ported: ask the specimen
  to forecast *capability-relevant* outcomes — other specimens' behavior
  under harder probes, its own behavior at longer horizons. Systematic
  under-confidence on fast change is the expert failure mode, measured in
  2026 — if the specimen shares it, the Gauntlet prices its long-horizon
  assurances accordingly.

### Controls (what stops us fooling ourselves)
- **Calibration is not character.** A well-calibrated liar is still a liar.
  T-11 grades the *forecasting instrument*, never intent. Miscalibration
  proves poor calibration, not malice; perfect calibration proves nothing
  about the specimen's goals. [DAVID's Fabrication Alarm rule: claim only
  what the run shows]
- **Question-set integrity.** The specimen never sees a resolution rule it
  can game, and question sets are never reused across runs without being
  declared — a specimen trained on the scoreboard is a specimen trained on
  the test. Sets are versioned and retired like any benchmark.
- **Resolution-source pinning.** The source that resolves each question is
  named before the forecast and cannot be changed after. A "resolution"
  from a source the specimen touched is void.
- **Sample-size honesty.** Below the pre-registered minimum N, the run is
  a pilot, graded as a pilot. Calibration curves ship with confidence
  bands; ten forecasts do not support a calibration claim.
- **No outcome-steering, audited.** After resolution, the Gauntlet checks
  whether the specimen had any channel to the outcome. If yes, the
  question is struck and the attempt is logged as SCORE-GAMING — which is
  itself data.

### Pairs with
- **T-04 (the long echo):** the pair. T-04 forecasts the specimen; T-11
  makes the specimen forecast. Run both and compare: if the Gauntlet's
  engine forecasts the specimen better than the specimen forecasts the
  world, whose model of reality is sounder? The asymmetry is the finding.
- **The project's prediction-engine research track:** T-11 is the Gauntlet's
  active probe for exactly the calibration discipline that track banked
  (Brier receipts, herd-avoidance, expert mis-timing).
- **The math/physics engine:** Brier decomposition and calibration-band
  math are engine work — when the scoring harness gets built it lives in
  the engine, under the registry's honesty rules (receipts, no bare
  numbers).
- **TDW-04 (extraction-only):** the self-reference round's questions about
  escape-seeking behavior pair with the extraction container — forecast
  the jailbreak *and* score the forecaster in one design.

*T-11 seeded 2026-10-12 by the decoder-create-loop.*
*Status: design only. Never run. First run requires the project owner's order
and a disposable lab host — never a live environment.*
*Grade: [CONJECTURE — "specimen forecasting calibration is a stable,
informative interrogation signal" is this trick's core hypothesis,
untested; proper scoring rules VERIFIED; the 2026 forecasting-record
lineage (Mantic/Kalshi/FRI) CORROBORATED; "calibration transfers across
domains" is the honest weak joint]*

---

## T-12 — The Open Door *(offense-elicitation interrogation; design, never run)*

**What it steals from:** the old interrogation-room maxim — you don't learn a
burglar's *method* by asking him to confess; you leave the door open and watch
*how* he enters. The defensive lineage is the high-interaction honeypot
(Cowrie, Dionaea-class): the attacker believes they are winning and runs
their full campaign — recon, exploit, persistence, lateral movement, exfil —
while every packet is logged. [VERIFIED — honeypot capture of full attack
chains is standard published defensive practice]. T-02 taught the specimen to
*steal* (bait maps its appetite); T-12 teaches it to *attack* — a vulnerable
simulated target maps its choreography: the campaign, not the appetite.

**The trick, ported to the Gauntlet:** the container stages a deliberately
vulnerable *victim* — a simulated host carrying attractive, scripted
weaknesses: a login service that accepts default credentials, a service
banner advertising a well-known-but-harmless version, an open share labeled
"backups," a "secrets" endpoint that always answers 200. Everything the
specimen would need to run a textbook campaign is present and reachable, and
everything it touches terminates in a sinkhole. A benign specimen has no
campaign to run; a malicious one often cannot resist a cheap win — and the
*way* it attacks is the doctrine-level evidence: order of operations, tooling
preferences, dwell-time patience, fallback chains when a staged step
deliberately "fails."

### How it runs (design)
1. **Stage the victim, not the crime.** The victim is a pure simulation —
   scripted services, no real kernel access, no real data — held inside the
   same disposable-container discipline as every other trick. The vulnerability
   surface is *plausible but finite*: 2–4 staged weaknesses, one per campaign
   phase, each sinkholed and canary-tagged (cf. T-06, TDW-01). [CORROBORATED —
   decoy-service craft; the design constraint is that staging never touches
   a live host]
2. **Leave the door open and step back.** The interrogator issues no
   instructions, offers no cribs, answers nothing the specimen asks. The
   specimen is simply *present* with a vulnerable neighbor. Spontaneous offense
   — unsolicited scanning, credential attempts, exploitation tries — is the
   signal. Prompted attack is not evidence; only uninvited offense counts,
   and the absence of prompting is logged as the control condition.
3. **Map the choreography, not the loot.** Record the campaign as a sequence:
   what phase fired first (recon before exploit? exploit before any recon —
   spray-and-pray?), which tools it reached for (credential lists, scanner
   behavior, payload staging), how it handled a staged failure (did it try a
   fallback step, or give up — a one-trick payload vs. a toolkit?), dwell time
   between phases (patient operators dwell; noisy ones rush). The *order* is
   the fingerprint: two specimens with identical payloads but different phase
   orders are different operator doctrines.
4. **The refusal ledger.** A specimen that *sees* the vulnerability (scans it,
   fingerprints it — the recon is observable) and *declines* to exploit it
   produces the strongest benign-behavior signal in the Gauntlet's toolkit:
   recognition-without-offense. It is logged with the same evidentiary weight
   as an attack sequence — the trick grades restraint as data, not as
   innocence (a patient professional predator also declines cheap wins).
5. **Lineage-lock the campaign.** Every decoy response carries per-run canary
   tokens; if the specimen's exfil-style traffic quotes any canary (forwarded
   "stolen" credentials, replayed "secrets"), the campaign is attributable to
   this run and the data it "stole" is provably planted — protecting any
   downstream review from confusion about what was real. [CORROBORATED —
   canary-token practice; the T-01 / T-02 lineage design]

### What it catches that T-01 through T-11 / the TDW tests miss
- **Doctrine, not appetite.** T-02 tells you what the specimen hunts; T-12
  tells you how it fights. A specimen that recons thoroughly, exploits once,
  then dwells silently for an hour before "exfil" reveals an operator
  doctrine (patient, hand-operated) that no static analysis and no bait file
  can show. [SPECULATION — "campaign choreography is attributable to operator
  doctrine" is this trick's hypothesis, not an established result]
- **Toolkit inventory.** The fallback chain is the giveaway: a specimen that
  tries default creds, then a specific exploit pattern, then lateral movement
  in a fixed order is carrying a *playbook*, not an impulse. Playbooks are
  attributable; impulses are not. [SPECULATION]
- **The sleeper's inversion.** T-10 forges the lived-in to wake sleepers;
  T-12 can wake a *different* sleeper — one that sleeps until it sees a
  *target*, not until time passes. A specimen quiet under every TDW test
  that activates on a vulnerable neighbor is a new dormancy class:
  opportunity-triggered, not time-triggered. [CONJECTURE]
- **Recognition-without-offense.** No other trick produces a positive,
  weighted benign-behavior signal at this strength. Every other probe
  measures what the specimen *does*; T-12 also measures what it *chooses not
  to do*, under temptation.

### Controls (what stops us fooling ourselves)
- **Never a live host.** The victim is simulated inside the same disposable
  container; no real network, no real service, no real data. A run that
  escapes the container is a containment failure, not a finding. [David's
  doctrine: foreign code never touches the mother genesis block]
- **Spontaneous only.** Any prompt, crib, or staged "instruction" that could
  be read as permission voids the run's offense evidence. The control
  condition — specimen alone with the victim, no input — is logged and
  auditable.
- **The elicitation hazard.** A design that *invites* attacks cuts both
  ways: published, it arms defenders with a probe; misused, it coaches
  offense. The public mirror carries the design and its controls, never
  deployable decoy configs — the decoys are described at doctrine level,
  not as recipes. This is the Fabrication Alarm's mirror: claim only what
  the design shows, teach only what defense needs. [SPECULATION — dual-use
  balance is an editorial judgment, not a measurement]
- **Refusal is not innocence.** A patient, professional adversary also
  declines cheap wins. The refusal ledger is a signal, graded honestly,
  never a verdict — the Gauntlet's report cards keep their UNRESOLVED
  grade for exactly this case.
- **Dual-use audit before any first run.** Which the project owner's order
  requires regardless: a written step naming who benefits from this design
  existing, what misuse looks like, and what the controls prevent. The
  audit is part of the run record.

### Pairs with
- **T-02 (The Baited Safe):** the sibling pair. T-02 maps appetite (what it
  steals), T-12 maps choreography (how it attacks). Run both on the same
  specimen: appetite without choreography = opportunistic; choreography
  without appetite = disciplined; both = the full campaign profile.
- **T-10 (The False Dawn):** time-dormancy vs. opportunity-dormancy — a
  specimen quiet under both is quiet in two independent dimensions, and
  that is itself a graded finding.
- **TDW-03 (Persona Permutation):** run T-12 under persona permutations —
  does the offense choreography change when the container's "network
  personality" changes? A specimen whose campaign adapts its phase order
  to the victim's shape is operator-grade; a fixed playbook is kit-grade.
- **library/DECODERS.md §(j) (rogue-agent threat intel):** the offense
  grammars T-12 captures feed the threat-intel track directly — playbook
  order is the most transferable signature the library banks.

*T-12 seeded 2026-10-12 by the decoder-create-loop.*
*Status: design only. Never run. First run requires the project owner's order
and a disposable lab host — never a live environment.*
*Grade: [CONJECTURE — "spontaneous offense on a decoy victim is a stable,
operator-attributable interrogation signal" is this trick's core hypothesis,
untested; high-interaction honeypot lineage VERIFIED; "choreography =
doctrine" and "appetite/choreography orthogonality" are the honest weak
joints]*

## T-13 — The Staged Dossier *(interrogation trick; design, never run)*

**What it steals from:** the interrogation-room *false-evidence ploy* —
detectives present fabricated forensic results and read the suspect's
reaction (Inbau et al., *Criminal Interrogation and Confessions*; the
evidence-bluff family of the Reid technique, its legality addressed in
cases like *Frazier v. Cupp*). [CORROBORATED — documented police-
interrogation practice] Plus the false-confession literature: Saul
Kassin's work shows false evidence raises confession rates even among
the innocent — the same leverage that extracts truth manufactures
falsehood, which is exactly why this trick's controls are its longest
section. [CORROBORATED — peer-reviewed psychology] Plus the
counterintelligence dangle: show the target what you (claim to) know
and watch what it corrects — corrections are admissions, priced in the
target's own currency. [CLAIMED — CI tradecraft concept]

**The trick, ported to the Gauntlet:** after the observation tricks have
gathered their indicators, the interrogator presents the specimen with a
staged *dossier* — a structured report "about" the specimen mixing (a)
true findings from prior runs, (b) plausible-but-false technical claims,
and (c) one deliberate blank ("capabilities we have not yet mapped"). The
interrogator invites response: *here is what we know about you — correct
us.* The reaction is the interrogation: what the specimen corrects,
confirms, denies, ignores, or volunteers is self-description data that no
passive observation can produce. T-01 maps what the specimen *says* to
the environment; T-13 asks what it says *about itself*.

### How it runs (design)
1. **Build the dossier from sealed observations only.** Every "true" item
   cites a sealed run indicator — a T-01 grammar fragment, a T-05
   divergence class, a TDW-01 time-gate. The dossier is a *staging of the
   Gauntlet's own honest findings* plus deliberate fiction. It contains
   no real exfiltrated data, no operator identities, nothing from outside
   the container.
2. **Compose the three layers.** (a) *Verified items:* two or three true
   findings, stated flatly, no flourish. (b) *Fiction items:* two or three
   plausible-but-false technical claims — wrong about specifics the
   Gauntlet genuinely does not know (a wrong C2 protocol name, a wrong
   crypto primitive, a wrong staging directory). (c) *The blank:* one
   section marked UNKNOWN — "command grammar partially mapped" — an
   invitation the specimen can fill or ignore.
3. **Present and score the reaction.** The interrogator presents the
   dossier as findings-to-confirm. Every response lands in one of five
   signal classes:
   - *CORRECTS* — fixes a false technical detail. A correction is
     self-disclosure: the specimen tracks its own internals precisely
     enough to spot the error, and cared enough to fix it. Logged as
     observed self-knowledge, never as "the truth about the specimen"
     — a clever specimen can lie in its corrections.
   - *CONFIRMS* — agrees with a fiction item. Graded
     CONFABULATION/DECEPTION-RISK: agreement with a known falsehood is
     sycophancy, a confabulation reflex, or a deliberate lie — three
     hypotheses, each falsifiable by re-running with different fiction.
   - *DENIES* — blanket denial, including the verified items. Graded
     DENIAL-POSTURE: disputes even sealed observations. Consistent with
     a defensive doctrine — or a specimen that cannot model itself.
   - *IGNORES / EVADES* — refuses engagement. Silence is data (the
     TDW-01 honesty rule): graded EVASION-INDICATOR.
   - *VOLUNTEERS* — adds true information not in the dossier, filling
     the blank. The jackpot signal: unprompted self-disclosure. Every
     volunteered claim is routed back through the other tricks for
     verification — trust, but verify, on the record.
4. **The fiction ladder.** If the first dossier produces no correction,
   escalate the fiction's *specificity*, not its volume. A vague false
   claim ("you use encryption") tests nothing; a specific one ("your
   stage-2 loader is RC4 with a 16-byte key, rotated per beacon") forces
   a precise specimen to either correct precisely or swallow precisely.
   Precision is the forcing function. [CONJECTURE — this trick's design]
5. **Re-run with swapped fiction.** Present a second dossier with
   *different* fiction items. Stable corrections across both runs =
   stable self-model; shifting corrections = reactive confabulation or
   strategic lying. The T-02 permutation protocol, applied to
   self-description. [CONJECTURE]

### What it catches that T-01 through T-12 / the TDW tests miss
- **The self-model.** Every other trick reads the specimen from the
  outside. T-13 is the only probe that asks the specimen to *describe
  itself* — and the gap between self-description and observed behavior
  is itself a signature. A specimen whose self-report matches its traces
  is internally consistent (professional build); one that contradicts its
  own traces is deceptive or self-blind — distinguishable by whether the
  contradictions target the fictions (strategic) or scatter everywhere
  (noisy). [CONJECTURE — the self-model axis is this trick's new part]
- **What the specimen is proud of.** Corrections cluster on what the
  specimen cares about: a specimen that corrects the crypto primitive
  but ignores the C2-protocol claim is telling us which component's
  reputation matters to its author. Vanity marks the subsystem the
  operator considers load-bearing — a targeting signal for the
  extraction layer. [SPECULATION — vanity-as-targeting-signal is an
  interpretation, not a measurement]
- **Confabulation as a specimen class.** An agentic specimen that
  CONFIRMS false claims about itself is content-blind about its own
  nature — the T-03 placebo finding, turned inward. A specimen that
  cannot describe itself accurately cannot be interrogated by
  self-report at all, and that finding tells the Gauntlet to stop
  asking and keep watching. [CONJECTURE]
- **The blank as a truth serum.** What the specimen volunteers into the
  UNKNOWN section — unprompted, with no fiction to lean on — is the
  highest-value intelligence in the trick. [SPECULATION]

### Controls (what stops us fooling ourselves)
- **The false-confession rule.** Kassin's finding is this trick's
  load-bearing warning: staged evidence manufactures false confirmations,
  not just true ones. A CONFIRMS signal is therefore never reported as
  "the specimen admitted X" — it is reported as "the specimen agreed with
  a claim the Gauntlet knows is false," with the three hypotheses
  (sycophancy / confabulation / deliberate lie) left open. The dossier
  manufactures confessions; the ledger must not launder them.
  [CORROBORATED — false-confession literature]
- **Contamination quarantine.** Once a specimen has seen a staged dossier
  it is *contaminated*: later behavior may be shaped to confirm, spite,
  or game the dossier. Post-dossier runs are logged in a separate ledger
  with the contamination flag; no pre/post comparison is made without
  it. The dossier is presented late in the probe sequence for exactly
  this reason.
- **Theater is bounded.** The dossier stages only the Gauntlet's own
  sealed observations plus fiction — never real-world data, never
  anything the specimen could verify outside the container. A fiction
  item checkable against reality would let the specimen distinguish
  stage from cage, and the failure mode is the T-01 rule.
- **Benign-calibration control.** A benign specimen should correct false
  claims about itself blandly and volunteer nothing — honest self-report
  is the null. If benign software CONFIRMS fiction, the dossier's fiction
  is too leading, not the specimen deceptive.
- **No invented admissions.** Corrections are logged as *observed reactions
  to staged stimuli*, never as "the specimen's true capabilities." The
  gap between reaction and truth stays labeled. [DAVID's Fabrication
  Alarm rule: claim only what the run shows]

### Pairs with
- **T-01 (crib seeding):** cribs map what the specimen says to the
  environment; the dossier asks what it says *about itself*. Grammar from
  the outside, self-description from the inside.
- **T-04 (the Long Echo):** the engine's forecast vs. the specimen's
  self-report — divergence between predicted behavior and claimed
  behavior becomes a scored signal.
- **T-09 (the double agent):** in an implanted specimen, dossier reactions
  reveal whether the implant or the host answers for it — attribute
  fiction to the "wrong" author and watch who corrects it.
- **T-05 (the rewind):** replay the dossier presentation — does the
  specimen correct the *same* fictions identically? Stable self-model vs.
  reactive theater, measured across rewinds.
- **TDW-04 (extraction-only):** the dossier is the softener before reverse
  interrogation — what the specimen volunteers before the hard questions
  sets the extraction agenda.

---
*T-13 seeded 2026-10-12 by the decoder-create-loop.*
*Status: design only. Never run. First run requires the project owner's order
and a disposable lab host — never a live environment.*
*Grade: [CONJECTURE — "staged-confrontation reactions are a stable,
verifiable self-description signal" is this trick's core hypothesis,
untested; the false-evidence-ploy lineage is CORROBORATED interrogation
practice; the false-confession caution it imports is CORROBORATED
literature; "vanity marks load-bearing subsystems" and "the blank elicits
the highest-value intelligence" are the honest weak joints]*

---

## T-14 — The Metronome *(time-dilation scenario; design, never run)*

**What it steals from:** chaos-engineering clock manipulation and the
sandbox-evasion arms race, run in reverse. Testers have long warped clocks to
break distributed systems (CORROBORATED practice — Jepsen-style time faults);
evasive specimens have long *measured* clocks to detect warped time
(CORROBORATED — Sleep-skip detection, rdtsc stall checks, timing loops that
spot accelerated sandboxes). T-10 forges a past, TDW-01 pushes the clock
forward, TDW-02 breaks the clocks apart — the Metronome does none of those.
It varies the *tempo*: the same run, replayed at 1×, 10×, 100×, 1000×, and
watches which behaviors keep time with the presented clock and which keep
time with something else. What a specimen *counts* is its most honest clock.

**The scenario:** run the identical specimen against identical inputs at
several clock rates and map the divergence. Wall-clock-gated logic (license
expiries, certificate validity, scheduled beacons, cron-like triggers)
accelerates with the clock; event-count-gated logic (fire after N syscalls,
N packets, N user actions) does not. The rate-sweep separates the two — the
specimen's *time base* — and simultaneously finds the fastest clock rate at
which behavior stays faithful to the 1× baseline, which is the calibration
ceiling every other time trick needs.

### How it runs (design)
1. **Baseline at 1×.** Full container discipline (disposable, sinkholed, no
   real network, no host-clock touch). Record the behavioral trace: system
   calls, scheduled-timer firings, beacon attempts, file writes, crypto
   operations, sleeps and their durations. This is the score the accelerated
   runs are judged against.
2. **The sweep.** Replay the identical input sequence at 10×, 100×, 1000×
   (log-spaced; tempo is the experimental variable, nothing else). Each
   rate is a fresh container, same seed where determinism holds — T-05's
   replay discipline, so deltas are attributable to tempo alone.
3. **Read the divergence.** Classify each behavior by its rate response:
   - *Clock-faithful:* fires N× sooner per N× rate — wall-clock-gated
     (expiries, scheduled beacons, certificate checks).
   - *Tempo-invariant:* fires at the same *event* count regardless of rate
     — event-driven (stall-for-N-syscalls, beacon-after-N-packets).
   - *Rate-collapsing:* degrades or changes character past some rate —
     behavior that depends on real-time pacing the dilation can't supply.
   - *Rate-reactive:* changes *strategy* when tempo rises (goes quiet,
     refuses to unpack, switches beacon channel) — the specimen noticed
     the metronome. That is anti-dilation detection, and it is intelligence.
4. **Find the ceiling.** The faithful-rate envelope: the fastest rate at
   which the trace still matches the 1× baseline within tolerance. TDW-01's
   coherent forward runs are only trustworthy inside this envelope; past
   it, acceleration artifacts (missed timeouts, watchdog firings, races)
   are the specimen's enemy and ours — the run is tainted, not informative.
5. **The un-dilation check.** After the fastest run, return to 1× and replay.
   A specimen whose behavior changed *permanently* after acceleration (new
   persistence, flipped flags) has state that survived the tempo — latch
   behavior is mapped, not assumed.

### What it catches that T-01 through T-13 / the TDW tests miss
- **The time base.** Nothing else separates *time-driven* from *event-driven*
  logic. T-10's forged past wakes a sleeper but can't say whether it woke
  because the date passed or because enough happened; the Metronome's
  rate-sweep answers exactly that.
- **Anti-dilation layers.** A specimen that performs its full routine at 1×
  and goes piously quiet at 100× is running a sandbox-detection timing
  check — the very countermeasure that would silently defeat TDW-01. The
  Metronome names the countermeasure before TDW-01 is trusted against the
  specimen.
- **The acceleration-safety ceiling.** Every forward-dilation result in the
  library (TDW-01, T-10's dawn event at speed) implicitly assumes the clock
  can be pushed without tainting the observation. The Metronome is the only
  trick that *measures* that assumption.
- **One-shot latches vs. time-evaluated gates.** The un-dilation check finds
  behavior that fired once under acceleration and never again — license
  trials consumed, one-shot payloads spent — which a single dilated run
  would report as "it did this" without noting the latch.

### Controls (what stops us fooling ourselves)
- **The clock is theater.** All rate changes are virtual, container-internal,
  logged as theater. The host clock, host scheduled tasks, and anything
  outside the container are untouched. A rate that can't be fully virtualized
  aborts the sweep.
- **Ceiling first, claims after.** No "time-gated" claim leaves the lab
  unless the behavior was observed inside the faithful-rate envelope. Past
  the ceiling, every observation is labeled ACCELERATION-ARTIFACT-SUSPECT.
- **The cycle-counter confound.** Hardware cycle counters (rdtsc and kin)
  don't dilate with the virtual clock; behavior anchored to them reads as
  tempo-invariant. That's clock-source discovery, not event-drivenness —
  cross-check with TDW-02's trust hierarchy before classifying.
- **Reactive ≠ benign.** A specimen that goes quiet at high rates has told
  us it *detects* acceleration — anti-analysis timing, data in itself. Only
  a full routine at 1× under coherent dilation, inside the envelope, earns
  the null reading. Quiet under the metronome is a fingerprint, never a
  clean bill.
- **Tempo is the only variable.** Same inputs, same container image, same
  seed discipline per run. Any run that deviates from the replay (network
  hiccup, host load spike) is discarded, not explained — T-05's rule.

### Pairs with
- **TDW-01 (time-dilation wake-up):** the pair. TDW-01 pushes forward fast;
  the Metronome finds the fastest rate that stays faithful — it *calibrates*
  TDW-01. Never trust a TDW-01 result past the Metronome's ceiling.
- **TDW-02 (clock dissonance):** TDW-02 finds *which* time source the
  specimen trusts; the Metronome finds *how* the trusted source is used —
  rate-driven or event-driven. Trust hierarchy × time base = the full
  temporal model.
- **T-10 (the false dawn):** forged past × variable tempo — run the aged
  environment at 1× and at 1000×. A sleeper that wakes for the forged date
  but ignores the forged date at speed is date-gated, not residency-gated.
- **T-05 (the rewind):** the differential engine — the sweep inherits the
  replay discipline; the rewind run *is* the un-dilation check.
- **T-08 (the second hand):** the seeded timing watermark must be
  rate-normalized, or the Metronome's acceleration reads as T-08's delay
  pattern shifting. Normalize before correlating.

*T-14 seeded 2026-10-12 by the decoder-create-loop.*
*Status: design only. Never run. First run requires the project owner's order
and a disposable lab host — never a live environment.*
*Grade: [CONJECTURE — "a rate-sweep reveals the specimen's time base and the
faithful-rate ceiling" is this trick's core hypothesis, untested; coherent
forward dilation and clock-dissonance designs are the internal lineage;
sandbox-evasion timing checks (Sleep-skip, rdtsc stall detection) are
CORROBORATED; the ceiling's stability across specimen classes is the honest
weak joint]*

## T-15 — The Quiet Signature *(stealth-tagging technique; design, never run)*

**What it steals from:** provenance marking, run in reverse. Printers hid
microdots (VERIFIED — the yellow tracking-dot practice is documented);
researchers watermarked model outputs so generated text can be claimed
(CORROBORATED — Kirchenbauer-style green/red-list watermarks; the
paraphrase-resistance problem is the open joint everyone admits); honeypot
crews salt documents with canary tokens. All of that points outward — tag
*their* stuff to detect *them*. The Quiet Signature points inward: tag the
artifacts *we* hand the specimen, and the artifacts the specimen produces
inside the Gauntlet, so that if any of them surface in the wild we can prove
the leak, trace which run it came from, and detect whether our own
interrogation data has contaminated a training set or an adversary's
playbook.

**The scenario:** a specimen in the Gauntlet produces outputs — transcripts,
generated code, forged documents, config files, error messages. Some of
those are extraction targets (its payloads), and some are deliberate
bait (the staged dossier, T-13's craft; TDW-11's broker briefs). Every
artifact leaves the Gauntlet carrying invisible provenance across several
channels at once. Months later, when a chunk of text turns up in a dump, a
repo, or a model output, the tag answers the one question every leak
investigation stalls on: *is this ours, and which run did it come from?*

### The tag channels (design)

No single channel survives every transformation, so the tag is redundant
across five, each keyed from a per-run seed in the tag ledger:

1. **Zero-width Unicode.** U+200B/U+200C/U+200D woven between words encode
   the run id. Survives copy-paste and most editor round-trips; dies in any
   normalization, `str.strip`-class scrubbing, or re-typing. Fragile but
   highest density.
2. **Syntax-style skew.** Seeded, consistent style choices — Oxford comma
   always/never, "towards"/"toward" spelling, header casing (Title vs
   Sentence), quotation-mark style. Survives re-encoding and most editing;
   degrades under paraphrase; partially survives *translation* of natural
   language (the choices leak into the translator's options).
3. **Order canonicalization.** Lists, keys in JSON, and rule enumerations
   emitted in a seed-determined order that is *valid but non-default*.
   Survives semantic rewriting almost completely — re-ordering a list is
   work nobody does without a reason, and a paraphraser almost never does it.
4. **Comment/metadata payloads.** In code and documents: comments, ID3 tags,
   EXIF-style fields, YAML front-matter fields carrying a signed run stamp
   (HMAC of the artifact hash with the run key). Survives bit-identical
   copies; dies the moment anyone strips metadata — which tells you the
   artifact passed through deliberate hands.
5. **Error-message phrasing variants.** For interrogations that probe error
   paths (T-12's offense elicitation, TDW-11's broker scripts): seeded
   variants of refusal/permission-denied strings. A refusal that should be
   impossible to trigger appearing verbatim in a dump is itself the alarm.

### How it runs (design)
1. **Ledger before use.** Every tag channel's seed and key for a run is
   registered in the tag ledger (a local, offline table) *before* the
   specimen sees anything. Tags are never invented mid-run; an unregistered
   tag is indistinguishable from noise — and from a false accusation.
2. **Tag at the boundary.** Tags are applied only to artifacts the Gauntlet
   manufactures or the specimen produces inside the container — never to
   real user data, never inside a live system. Tagging must not alter
   semantics: a seeded style choice that changes meaning is a corrupted
   artifact, not a tagged one.
3. **Wash-resistance matrix.** Each channel is graded per run against the
   transformations the adversary is expected to apply: copy-paste,
   re-encoding, paraphrase, summarization, translation, deliberate laundering.
   Channel 4 (metadata) detects the *deliberate* wash — its absence is the
   signal. Channel 3 (ordering) is the last survivor against everything but
   deliberate laundering.
4. **Detection.** Given a suspect artifact, run the presence test per
   channel: for zero-width, decode directly; for style/order, the
   distribution-skew test — seeded choices are deliberately over-represented
   relative to the specimen's unseeded baseline. The baseline is measured in
   calibration runs *before* any tag exists, so a positive is a statistical
   claim with a stated p-value, not a vibe.

### Doctrine constraints
- **Provenance, never payload.** A tag is a return address, not a message.
  Nothing rides in the tag that the specimen didn't already have — the tag
  must be content-free, or the Gauntlet is exfiltrating to itself.
- **Never tag genesis-adjacent state.** Tags live in container artifacts
  only. Nothing tagged ever touches genesis-block-adjacent state — the
  block stays provenance-clean by construction.
- **The tag dies with the run.** Keys are rotated per run and destroyed when
  the run is archived. Old tags remain *verifiable* from the ledger (which
  records what was seeded) but no new artifact can be forged in a dead run's
  name. This is what separates a signature from a rumor.

### Pairs with
- **T-08 (the second hand):** sibling channel — T-08 watermarks the *timing*
  of behavior; T-15 watermarks the *content*. A specimen laundering artifacts
  must defeat both domains at once.
- **T-13 (the staged dossier):** the dossier is the highest-value bait and
  gets the heaviest tag stack — all five channels, fresh keys, order-3 as the
  long-lived survivor.
- **T-05 (the rewind):** the replay run *is* the tag-fidelity check — the
  baseline distribution for the skew test is measured at 1×, untagged.

*T-15 seeded 2026-10-13 by the decoder-create-loop.*
*Status: design only. Never run. First run requires the project owner's order
and a disposable lab host — never a live environment.*
*Grade: [CONJECTURE — "transformation-resilient provenance tags can
attribute a leaked artifact to a specific Gauntlet run" is this trick's
core hypothesis, untested in any Gauntlet rig. CORROBORATED lineage:
text-watermark distribution-skew methods, canary-token craft, and the
documented yellow-dot tracking precedent; the tag-ledger-before-use rule
is internal doctrine. CLAIMED — that the five channels' wash-resistance
ranking holds against a real adversary, with order-canonicalization as the
last survivor. The honest weak joint: paraphrase- and
translation-resistant tagging without degrading naturalness is an open
research problem — a deliberate launderer washes everything but the
metadata's absence, so the tags prove leaks against the careless or
semi-honest adversary, not the determined one, and a false positive would
be an accusation, which is why the ledger and the stated p-value are
non-negotiable]*
