# CIPHER TIMELINE — codes, ciphers, governments, then → now

*What each cipher said or protected, the human error or breakthrough, and the
historical pivot it caused — including the ciphers that never got through.
Grades: VERIFIED / CORROBORATED / CLAIMED / SPECULATION.*

---

## ~58–50 BCE — Caesar cipher

Julius Caesar shifted letters by three to protect military dispatches in the
Gallic Wars. [VERIFIED] The breakthrough: frequency analysis, formalized by
Al-Kindi around 850 CE — the first great decoder, nine centuries later.
[VERIFIED] The pivot: every monoalphabetic cipher ever built died the same
death; the lesson took a millennium to land.

## 1586 — Babington Plot / Mary Queen of Scots

Mary's coded letters, encrypted in a nomenclator, were intercepted and broken
by Thomas Phelippes; the plaintext named the plot to assassinate Elizabeth I.
Mary was executed in 1587. [VERIFIED] The human error: trusting a courier
network that was already owned. The pivot: a broken cipher as a death warrant —
the first great lesson that the *channel* is part of the cipher.

## 1553/1586 → 1863 — Vigenère, "le chiffre indéchiffrable"

The polyalphabetic cipher reputed unbreakable for nearly three centuries, until
Babbage (~1854, unpublished) and Kasiski (1863) showed repeating keys leak
their own length. [VERIFIED] The pivot: "unbreakable" is a claim about the
analyst's era, not the cipher's. Yara's standing rule — they are always wrong
eventually — starts here.

## 1630s → 1890s — The Great Cipher of Louis XIV

Rossignol's cipher secured French state secrets for two centuries until Étienne
Bazeries broke it in the 1890s. [VERIFIED] The human error: the cipher outlived
everyone who remembered it was breakable; secrecy as a strategy has an expiry
date.

## 1822/1885 — The Beale ciphers: the cipher that never paid

Three ciphers supposedly describing a buried treasure in Virginia; only the
second was ever decrypted (with the US Declaration of Independence as key).
The treasure has never been found. [VERIFIED status] The pivot that never
happened: if ciphers one and three are a hoax, the greatest unsolved cipher in
America is a prank — and the doctrine says treat every claim as CLAIMED until
proven.

## 1917 — The one-time pad: the cipher that cannot be broken

Vernam's patent (with Mauborgne's pad refinement); Shannon proved perfect
secrecy in 1949. [VERIFIED] The pivot: the only unbreakable cipher in history —
and humans still break it, by reusing keys (Venona), by stealing pads, by
being operators. Unbreakable math, breakable people.

## 1917 — The Zimmermann telegram: the cipher that started a war's end

Germany's foreign minister proposed a Mexican alliance to retake Texas, New
Mexico, and Arizona if the US entered WWI. Britain's Room 40 had the telegram
within days. Its publication helped push the United States into the war in
April 1917. [VERIFIED] The human error: routing a secret alliance proposal
through cables the enemy was already reading. The pivot: one decrypted
paragraph, and a continent joins a war.

## 1932–1945 — Enigma: the machine that taught us cribs

Polish mathematicians (Rejewski, 1932) broke it first with the bomba; Bletchley
Park industrialized the break with cribs — guessed plaintext like weather
reports and "nothing to report." [VERIFIED] The human error, every day: rigid
procedures, stereotyped message openings, operators who never varied. The
pivot: D-Day's deception, the U-boat war, and the modern doctrine's first rule
— *usage flaws first, math second*.

## 1940 — Purple

The US broke Japan's diplomatic cipher machine; Magic intercepts shaped
American strategy before and during WWII. [VERIFIED] The pivot: reading an
adversary's diplomats in near real time — and the agonizing discipline of never
letting them know you can.

## 1942 — JN-25 and Midway: the trap built from a decryption

US codebreakers, reading enough of Japan's naval code JN-25, suspected "AF"
meant Midway — and confirmed it with a planted plaintext ruse (the "water
shortage" message). The ambush that followed broke Japanese naval power.
[VERIFIED] The pivot: cryptanalysis as *offense* — not just reading the enemy's
mail, but forging the envelope. The ancestor of every baited-safe trick.

## 1944 — Pigeon NURP.40.TW.194: the message that never got through

A pigeon cipher, likely D-Day-related, unreadable to this day — assessed as
one-time-pad-class. [VERIFIED unsolved; CLAIMED assessment] The pivot that
never happened: somewhere in those 27 groups may be a battle order that
arrived as noise. Ciphers don't only fail by being broken; they fail by never
being read at all.

## 1939 — D'Agapeyeff: the cipher killed by its own author

A challenge cipher whose creator forgot the method and dropped it from later
editions. [VERIFIED] The pivot: the most complete silence in the archive is
self-inflicted. Key management is not a footnote; it *is* the cipher.

## 1977 — RSA: the cipher anyone can use

Rivest, Shamir, and Adleman published public-key cryptography; Diffie and
Hellman had set the stage in 1976. [VERIFIED] The pivot: secrecy no longer
required a shared secret — the internet's commerce layer was born from a math
problem. (Ellis, Cocks, and Williamson at GCHQ had it first, in secret;
declassified 1997. [VERIFIED])

## 2008 — Blockchain: the ledger that cannot be unsaid

Bitcoin's chain made double-spend impossible without a trusted third party —
hash-linked blocks, proof of work. [VERIFIED] The pivot: trust moved from
institutions to mathematics. And the decoder's note: every chain is a
provenance log — the same idea the gauntlet's hashed interrogation log uses.

## 2013/2016 — Zero-knowledge SNARKs: proving without telling

GGPR (2013) formalized succinct non-interactive arguments of knowledge;
Groth16 (2016) made them practical; Zcash put them in production.
[VERIFIED] The pivot: you can prove you *know* a secret — a password, a vote,
a balance — without revealing a single bit of it. The cipher inverted: the
message is the proof that there is no message.

## 2020 — Zodiac's Z340: the cipher that mocked the professionals for 51 years

The Zodiac Killer's 340-character cipher, mailed to the San Francisco
Chronicle on November 8, 1969, defeated the FBI, the NSA, and every
professional cryptanalyst for 51 years — his first cipher (Z408) had fallen
to a schoolteacher couple within days. [VERIFIED] The breakthrough: three
hobbyists — David Oranchak (Virginia software developer), Sam Blake
(Australian mathematician), and Jarl Van Eycke (Belgian programmer) — found
the substitution alphabet hid a non-obvious transposition: the grid reads on
a diagonal, the cipher splits into three sections read in parts, and one
section was further scrambled by a transposition error that the solvers'
software finally learned to forgive. [VERIFIED] They submitted the solution
to the FBI on December 5, 2020; the agency confirmed it. [VERIFIED] The
plaintext was a taunt — "I HOPE YOU ARE HAVING LOTS OF FUN IN TRYING TO
CATCH ME" — and named no name. [VERIFIED] The pivot: the most famous
unsolved cipher in America fell not to a government lab but to open-source
software (Van Eycke's AZdecrypt) run by amateurs — and only after the
solvers stopped assuming the standard attacks were sufficient. The
decoder's note: the through-line of this timeline is that breakage comes
from behavior, not math — and Z340 is its mirror image. The cipher was
fine. It was the *analysts'* behavior — the assumptions baked into the
tools — that held the door shut for half a century.

## 2024 — Post-quantum: the cipher migration

NIST finalized FIPS 203/204/205 (ML-KEM, ML-DSA, SLH-DSA); migration deadlines
are landing now. [VERIFIED] The pivot in progress: every RSA-encrypted secret
ever captured can be stored today and read tomorrow — "harvest now, decrypt
later." The timeline's open question: does migration finish before a
cryptographically relevant quantum computer arrives? [SPECULATION on timing]

## 1966 — "Coupon Collecting and Cryptology" (NSA Technical Journal)

Marie Capozza's SECRET-classified NSA Technical Journal article (Fall 1966)
applied the coupon-collector's problem to cryptology: a statistical test for
whether a generated sequence behaves as though genuinely random (applied to
the decimal digits of π, following Greenwood's 1955 public method), key-card
punch-field generation with generator-bias detection, and the reversed
inference — estimating the *unknown number of code groups* from observed
samples. Declassified in 2026 (approved for release 2026-09-09, FOIA Case
#102241, after a nine-year wait); the section on alphabet generation remained
redacted — still sensitive sixty years on. [VERIFIED] The pivot: randomness
tests are the immune system of every key-material pipeline, and this is the
oldest published one with an agency stamp. The decoder's statistical tooling
inherits the coupon-collector test and the reversed code-group inference.

## 2026 — The AI codebreaker: models that do archival cryptanalysis

In September and October of 2026, two centuries of historical ciphers fell
to the same new actor: a frontier AI model told to behave like a
cryptanalyst, not like an oracle. The pattern was identical in both cases:
the model did the archival research itself, picked its target, found its
cribs, built deterministic machinery — an Enigma simulator and software
Bombe, a simulated-annealing homophonic solver — and humans verified the
result against history. The models never "broke the ciphers from scratch";
they industrialized the human workflow, and the two-day turnaround on a
problem that had stood twenty years is the honest headline.

- **The MVUEH Enigma message (September 2026).** An 82-letter German Army
  message — Nr. 172, sent July 10, 1941, logged at 17:30 by the radio
  station of the SS-Totenkopf Division's quartermaster section — had
  resisted every attempt since it was published online in 2005. Given only
  the instruction to attempt any unsolved message, OpenAI's GPT-6 Astra
  selected Nr. 172, connected it to Nr. 173 (SIPVX, broken 2017), bet on
  the repeated place name "ROSENOW ROSENOW" as a crib, wrote its own
  simulator and Bombe in Python and C++, and recovered the plaintext in
  about two days. Frode Weierud, who maintains the Crypto Cellar archive,
  validated the break and published a write-up. The plaintext was mundane:
  a route-of-march request, position at Rosenow, signed Waschbusch.
  [CORROBORATED — Weierud's validation + independent trade press]
- **The second Enigma message (September 2026).** Cryptanalyst Jack Willis
  supplied Anthropic's Claude Opus 5 with additional historical context,
  including a known German officer's signature; a second long-unsolved
  message fell. [CLAIMED — secondary reporting only this pass]
- **The Marmont cipher (October 2026).** A letter of March 1809 from Eugène
  de Beauharnais to General Marmont, unread for 217 years: a homophonic
  substitution of ~1,300 cipher units across 155 unique signs, some
  standing for whole French words, surviving only as a low-resolution
  scan printed in a French army journal in 1969. Carter Church
  (SentinelOne) had GPT-6 Astra transcribe the plate (sorting 175
  hand-drawn marks into same-sign classes), recover a partial key
  published by historian Daniel Tant (33 signs), then run the model's own
  simulated-annealing solver against French-literature statistics. Six
  hours, end to end. Independent reviewer Satoshi Tomokiyo of Cryptiana
  checked the result; the key, transcription, and code were publicly
  released, five symbol readings still uncertain. The plaintext was a
  routine troop briefing, consistent with existing records.
  [CORROBORATED — press coverage + Tomokiyo review + released artifacts]
- **The pattern the timeline teaches:** these breaks are the
  reproducibility-suite discipline applied to history — Church released
  key, transcription, and code; Weierud validated MVUEH independently.
  The decoder's note: this is our own architecture reflected back — the
  model as scout and researcher, deterministic tools as the verifier,
  humans as the final check. After this wave, seven messages remain
  unsolved in the public Crypto Cellar collection. [CLAIMED — single
  explainer]

## The through-line

Caesar → Vigenère → Zimmermann → Enigma → RSA → SNARKs → blockchain → PQC.
Every era believed its cipher would hold. Every era was wrong except the
one-time pad — and even the pad falls to operators. The lesson compounds:
**the cipher is never stronger than the habits of the people who use it.**
That is why the decoder's gauntlet interrogates *behavior* first and
mathematics second — four thousand years of evidence, one verdict.

*Updated 2026-10-13.*
