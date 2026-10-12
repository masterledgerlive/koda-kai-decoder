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
