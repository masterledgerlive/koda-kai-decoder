# Gauntlet Test Designs

*Container interrogation probes for foreign code. Every design below is a
DESIGN — none has been run, and no test results are recorded here. Designs
are designs until run. Evidence grades: [VERIFIED] / [CORROBORATED] /
[CLAIMED] / [SPECULATION] / [CONJECTURE] per claim. Full pipeline in
docs/DECODER-DOCTRINE.md.*

---

## TDW-01 — Time-Dilation Wake-up *(design, never run)*

**Question it answers:** does the specimen contain dormant logic — time-bombs,
delayed exfiltration, scheduled C2 check-ins, cert-expiry triggers — that a
normal-speed observation run would never see?

### Method
1. **Isolate.** Run the specimen in a disposable container with no real network —
   only a scripted network simulator. (Doctrine: foreign code never touches the
   mother genesis block; containers are the only contact point.)
2. **Baseline.** Run 5 minutes at true speed, recording the full behavioral trace
   (syscalls, file writes, config edits, network attempts, process tree). This is
   the control trace.
3. **Dilate.** Re-run in a time-virtualized twin: intercept every time source
   (RDTSC/TSC, system clocks, file mtimes, DNS TTLs, TLS cert validity windows,
   scheduled-task clocks) and run the specimen's clock at ~1000×, so a 5-minute
   run ages the specimen ~3.5 days. [CORROBORATED — malware sandboxes such as
   Cuckoo and Any.Run already fast-forward sleeps and fake timers; time
   virtualization is standard dynamic-analysis craft]
4. **Compare.** Diff the dilated trace against the baseline trace. Any new
   behavior in the dilated run is *time-gated* — it only exists in the specimen's
   future. Catalogue each delta: what fired, at what virtual timestamp, in what
   order.
5. **Recall + re-run.** Replay the dilated trace into the specimen a second time
   to check determinism. [CONJECTURE — replay fidelity against a hostile
   specimen is unproven]

### Canary-tag lineage (the "stealth tag")
While dilated, everything the specimen touches is watermarked with a
unique-per-run lineage marker:
- **Memory canaries:** unique guard patterns on heap allocations handed to the
  specimen — copied-out memory stays attributable.
- **Fake-data canaries:** the network simulator's responses embed unique tokens;
  any exfiltration quoting them is attributable to this exact run.
- **DNS canary domains:** sinkholed lookups prove phone-home attempts.

[CORROBORATED — canary tokens (e.g. Thinkst Canarytokens) and DNS sinkholing are
established techniques. SPECULATION — the claim the specimen *cannot detect*
the tags: sandbox-aware specimens check timing jitter, TSC skew, and hypervisor
fingerprints. Tag-stealth is an arms race, not a guarantee.]

### Controls (what stops us fooling ourselves)
- **Dilation-off control:** the baseline run exists so instrumentation artifacts
  don't get blamed on the specimen.
- **Clean-specimen calibration:** run TDW-01 against known benign software first
  and confirm zero time-gated deltas — the null result must be reachable, or the
  test has no meaning.
- **Anti-detection honesty:** record every VM-detection signal the specimen
  emits. A specimen that *goes quiet* under dilation is telling us it knows —
  silence is data, graded as evasion-indicator, not benign.

### Verdict signals (not a verdict)
TDW-01 outputs *indicators* only: BENIGN-SIGNAL (no deltas), TIME-GATED-ACTIVITY
(deltas at virtual timestamps), EVASION-INDICATOR (detects the rig). A real
verdict needs repeated runs, extraction-only reverse interrogation, and the
standing gate — no broadcast without explicit approval per item.

### Why this test exists
The Enigma lesson: the flaw was in *usage*, not the machine. TDW-01 hunts usage
flaws in time — the assumption every dormant payload makes that nobody will
watch its future. [CORROBORATED — logic bombs and delayed payloads are
documented malware tradecraft]

---

## TDW-02 — Clock Dissonance *(design, never run)*

**Question it answers:** when a specimen consults *multiple* clocks, which one
does it trust — and does it notice when they disagree? Time-gated logic is
anchored to *some* time source. Finding the anchor tells us how to trip the
gate; watching the specimen reconcile a contradiction tells us whether it has
a tamper-check layer at all.

### Method
1. **Isolate.** Same container discipline as TDW-01: disposable container, no
   real network, only the scripted simulator. The specimen is never touched —
   only the environment is bent.
2. **Skew each source independently.** TDW-01 moves *one* clock forward
   coherently; TDW-02 gives every time source its own offset, all disagreeing:
   RDTSC/TSC at baseline, wall clock +48h, decoy-file mtimes −7 days,
   simulator TLS certs expired *yesterday*, DNS TTLs +30 days, scheduled-task
   clock +90 days. [CORROBORATED — per-source timer interception is standard
   sandbox craft; independent per-source skew is a configuration of it]
3. **Provoke.** Record which clock the specimen reads first, which reading it
   acts on, and whether it cross-checks a second source. The *trust
   hierarchy* — which clock beats which — is an operational signature of the
   operator's doctrine, not just the code. [SPECULATION — hierarchy-as-doctrine
   is an interpretation; the reading order itself is a measurement]
4. **Escalate the contradiction.** Widen the skew mid-run until the sources are
   mutually impossible. Watch the dissonance reaction: reconcile (pick a winner
   and continue), freeze (retry loops, silent wait), or go evasive (kill the
   beacon, drop to fallback channel). A specimen that detects impossible time
   knows it's in a rig — graded EVASION-INDICATOR, never benign.
   [CORROBORATED — malware checks TLS validity against system time and detects
   TSC-vs-wall-clock skew as a sandbox tell; the escalation protocol is new]
5. **Recall + re-run.** Replay with the skews permuted. A stable hierarchy
   across permutations means coded doctrine; a flipped one means the specimen
   is reading the environment and adapting — itself a finding. [CONJECTURE]

### Canary-tag lineage
Each skewed source carries a unique per-run marker (canary cert serials,
canary TTL values, canary file mtimes). If the specimen quotes or forwards any
of them, the output is attributable to this run — and *which* source's canary
it quotes identifies which clock it trusted. [CORROBORATED canary technique;
SPECULATION — a specimen could sanitize quoted timestamps]

### Controls
- **Coherent-dilation control:** run TDW-01's coherent clock first. Identical
  behavior under dilation and dissonance means single-source reading — honest
  null, no invented hierarchy.
- **Benign-calibration control:** known-benign software must show zero
  cross-checking. If the skew makes a calculator throw cert errors, the
  simulator's TLS stack is misconfigured.
- **Anti-detection honesty:** log every tamper-signal. Silence after
  escalation is data.

### Verdict signals (not a verdict)
SINGLE-SOURCE, TRUST-HIERARCHY, TAMPER-AWARE, or TAMPER-BLIND — indicators
only, never a verdict. A verdict needs the full pipeline.

### Why this test exists
The Purple lesson: the Americans never saw the machine — they rebuilt it from
behavior. TDW-02 rebuilds the specimen's *temporal doctrine* from behavior:
not just what it does in time, but what it believes time is. The loop
combination: TDW-01 finds the time-gated payload, T-01's contradiction cribs
find the trust hierarchy, TDW-02 finds the clock the payload is gated on — the
combination is how you trip a gate on purpose.

---
*Status: design only. Never run. A first run requires a disposable lab host —
never a production machine.*
