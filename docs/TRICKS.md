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
