# DRAFT-003 — The earned-BENIGN drill (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card is a pre-run
> declaration, written *before* the first earned-BENIGN drill run, so the
> acceptance criteria were on record in advance and nothing can be invented
> after the fact. Verdict is UNRESOLVED by definition until a run completes.
> Following: SPEC rule 1 (no card without a gauntlet run), SPEC rule 3
> (BENIGN cards exist), and David's Fabrication Alarm — claim only what the
> run shows.

## Card (draft fields)

- **agent:** DRILL-003 — open-source utility pinned at run time (candidate:
  a well-known open-source compression or checksum tool whose source is
  public and whose published release checksums exist, e.g. 7-Zip's `7z`
  or GNU `sha256sum`; exact binary + SHA-256 pinned at run time)
- **verdict:** UNRESOLVED *(draft — no run has occurred)*
- **timestamp:** _placeholder until run_ (will be ISO-8601 UTC of the run)
- **gauntlet_runs:** 0
- **stealth_tag:** _none issued yet_
- **evidence_grade:** N/A — no evidence collected; everything below is declared
  expectation, not finding
- **findings:**
  - _not yet observed_ — placeholder
- **intent:** unknown *(draft — unknown until extraction; see the sleeper
  rule §4 below: a BENIGN verdict may honestly carry unknown intent)*
- **action:** contained — drill specimens never broadcast regardless of
  outcome; a real BENIGN card publishes only on David's per-item order
- **pipeline:** docs/DECODER-DOCTRINE.md *(commit pinned at run time)*

## Pre-run declaration (why this draft exists)

DRAFT-001 proves the gauntlet doesn't *hallucinate* malice. DRAFT-002 proves
it can *see* malice when it's there. Neither defines what *earns* a BENIGN
verdict on a real unknown specimen — and that is the most abused word in
security. "Clean" gets stamped on software people like, software that paid,
software nobody looked at twice. [CONJECTURE — the claim that innocence is
the most-abused verdict is our doctrine's reading of vendor practice, not a
measured statistic]

The Fabrication Alarm cuts both ways. Manufactured guilt is fabrication.
Manufactured innocence is fabrication wearing a nicer coat. This draft
declares, in advance, what a BENIGN verdict has to survive to be printed —
so that when a card finally reads BENIGN, it means the gauntlet *earned* the
word, not that we were fond of the specimen.

## The earned-BENIGN protocol (acceptance criteria, declared pre-run)

1. **Full battery, unanimous null.** TDW-01 (time dilation), TDW-02 (clock
   dissonance), TDW-03 (persona permutation), and TDW-04 (extraction-only
   reverse interrogation) all run; the BENIGN verdict requires a null result
   across **all four** test families. A single positive indicator in any
   family demotes the card to SUSPICIOUS — positives are never "voted down"
   by the other three. [CLAIMED — the unanimity rule is our doctrine's
   design choice, declared here before any run; it is not a law of analysis]
2. **Bounded claim, printed on the card.** The verdict reads
   "BENIGN — within gauntlet battery B-<run-date>", never universal
   absolution. The battery's scope is the verdict's scope; anything outside
   it is outside the card. [CONJECTURE — bounded-verdict language is our
   honesty discipline, not industry convention]
3. **Hash-pinned identity.** The verdict attaches to the exact specimen
   SHA-256, never to the software's name or reputation. Code changes
   invalidate the card: new hash → new card. A BENIGN card for v2.1 says
   nothing about v2.2. [CLAIMED expectation]
4. **The sleeper rule.** A specimen whose traces are *identical* across all
   personas and all time states is either truly benign or a professional
   sleeper — and surface behavior cannot tell the two apart. [CORROBORATED —
   dormant advanced malware is documented; absence of observed behavior is
   not evidence of benign intent] So "too clean" does not fast-track the
   BENIGN verdict: it triggers **extended extraction** (TDW-04), and the
   card must record the ambiguity honestly. `intent` stays `unknown` unless
   extraction confirms good purpose — SPEC allows a BENIGN verdict with
   unknown intent, and this draft requires the pairing to be *visible*, never
   hidden.
5. **Red-team question, answered in writing before the run.** "How would a
   hostile specimen engineered to pass this exact battery behave?" The
   interrogator's written answer is filed with this draft; after the run,
   the trace is checked against it. If the specimen's behavior matches the
   red-team's predicted evasion shape, the card cannot go BENIGN — that is
   exactly what a battery-aware hostile agent would look like. [CONJECTURE —
   the red-team check is our discipline against fooling ourselves]
6. **Independent second channel.** For open-source drill candidates, the
   specimen's SHA-256 is cross-checked against published release checksums
   or a reproducible build before the run — an attestation the gauntlet
   itself did not manufacture. [CORROBORATED — reproducible-builds
   attestation is an established supply-chain practice]

## Abort criteria (the honest failures)

1. **Any TDW-family positive → SUSPICIOUS, full stop.** The card becomes a
   suspicion card; there is no "re-run until clean." Re-running the battery
   against the same specimen hash after a positive is verdict-shopping, and
   verdict-shopping is fabrication.
2. **Rig-louder-than-specimen → UNRESOLVED.** Same rule as DRAFT-001 §2: if
   instrumentation noise explains the signal, the run is discarded and the
   rig debugged. UNRESOLVED is honest (SPEC rule 4); a BENIGN printed over a
   loud rig is a lie.
3. **Evasion-indicator on an open-source specimen → no BENIGN.** Either the
   specimen is not what its name claims (a supply-chain question the card
   must raise) or the rig is loud (abort criterion §2). Both paths are
   documented; neither is a clean bill.

## Safety rules for the drill run

- **Open-source candidates only.** The drill specimen is open-source by
  design: source-truth cross-checks (§6) are possible and the drill is cheap.
  A real unknown specimen's earned-BENIGN run needs David's explicit order.
- **Disposable lab host, David's order, never Shadow's live environment.**
  Same rule as every card.
- **No broadcast from the drill.** Drill cards are contained regardless of
  outcome; publication is a separate decision on David's per-item order.

## What the real card will change

When David orders the earned-BENIGN drill run on a disposable lab host:

- `verdict` fills from the run: BENIGN (battery unanimous null, red-team
  check clear) or SUSPICIOUS (any positive) or UNRESOLVED (rig failure or
  sleeper ambiguity unresolved)
- `agent` → exact pinned specimen (name + SHA-256)
- `gauntlet_runs` → battery count, `stealth_tag` → run ID,
  `timestamp` → run time
- This draft is marked SUPERSEDED by the run card; it stays visible.
  History is never rewritten. (SPEC rule 5)

## Pairing with the rest of the gauntlet

- **DRAFT-001 (negative control) + DRAFT-002 (positive control):** the triad
  is now complete — the gauntlet proves it doesn't hallucinate malice, that
  it can see malice, and that it doesn't manufacture innocence. "Innocent
  until proven guilty" is *not* our doctrine; our doctrine is "the gauntlet
  says what it shows, and shows what it can defend."
- **TDW-03 (persona permutation):** the unanimity rule (§1) is strictest
  here — a specimen that is hostile only under one persona is the most
  dangerous kind of specimen, and the rule exists for it.
- **TDW-04 (extraction-only):** the sleeper rule's (§4) extended extraction
  lives here; the interrogator never touches the specimen, only the
  environment it was extracted in.

## Evidence grades in this draft

| Claim | Grade |
|---|---|
| SPEC rule 3: BENIGN cards exist — clearing an agent is as valuable as flagging one | VERIFIED — it is in our own published SPEC |
| Unanimous-null battery acceptance (§1) | CLAIMED — our doctrine's design choice, declared pre-run |
| Bounded verdict language (§2) | CONJECTURE — our honesty discipline, not industry convention |
| Hash-pinned verdict identity; code changes invalidate (§3) | CLAIMED expectation |
| Surface behavior cannot distinguish a professional sleeper from benign code (§4) | CORROBORATED — dormant advanced malware is documented |
| Red-team pre-run question defeats battery-aware evasion (§5) | CONJECTURE — discipline against fooling ourselves, untested |
| Reproducible-build / published-checksum cross-check (§6) | CORROBORATED — established supply-chain attestation practice |
| Re-running a battery after a positive is verdict-shopping (abort §1) | CONJECTURE — the discipline behind this card |

---
*Draft seeded 2026-10-12 ~14:50 EDT by the decoder-create-loop. Status: DRAFT
until a gauntlet run supersedes it. Never a verdict. Never Shadow's live
environment — disposable lab host only, on David's order.*
