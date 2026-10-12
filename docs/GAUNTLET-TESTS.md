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
*Status: design only. Never run. A first run requires a disposable lab host —
never a production machine.*
