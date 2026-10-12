# Decoder Catalogue (seed — growing on the research loop)

*Every decoder and code cracker, in library form. Grades: VERIFIED / CORROBORATED /
CLAIMED / SPECULATION.*

## Historical codebreakers
- **Napoleon 1809 homophonic cipher (AI-deciphered, Oct 2026):** a homophonic
  cipher letter to General de Marmont, unread for 217 years (~1,300 cipher
  units, 155 symbols), was closed by a multi-modal AI pipeline (image
  transcription → symbol segmentation → simulated annealing) from a single
  scanned image in about six hours — no recovered key. First real case study
  of machine-assisted cryptanalysis on an unsolved historical cipher.
  [CORROBORATED]
- **Enigma** (1918–1945): rotor cipher machine; broken at Bletchley Park with the
  Bombe — the lineage of breaking the "unbreakable." [VERIFIED]
- **Lorenz cipher / Tunny**: broken via Colossus, the first programmable digital
  computer. [VERIFIED]
- **Purple (Japan)**: broken by US Signals Intelligence before WWII. [VERIFIED]
- **JN-25 (Japanese naval operational code, WWII)**: ~45,000 five-digit code
  groups, superenciphered by ~18,000-entry additive tables; broken cumulatively
  by Stations HYPO/CAST/NEGAT — additive reuse and code-clerk mistakes were the
  entry. By April 1942 HYPO read ~10–15% of traffic within hours; that partial
  read plus the "AF = Midway" deception confirmed the Midway target, letting an
  outnumbered US fleet ambush and defeat the Japanese carriers (June 1942).
  Lesson: partial-but-timely reads are decisive, and breaks come from usage
  flaws, not the machine. [CORROBORATED]
- **Classical methods**: frequency analysis, Vigenère breaking (Kasiski/Babbage),
  one-time pads (unbreakable when used correctly). [VERIFIED]
- **Venona (1943–1980):** the only mathematically unbreakable cipher ever deployed
  — Soviet one-time pads — was broken by *reuse*: wartime pad production
  duplicated ~35,000 key pages, and Arlington Hall/NSA analysts found the "depth
  of two" (two messages under one pad page; subtract them and the key cancels).
  ~2,200 translations published (declassified 1995) exposed the atomic-spy rings
  (Klaus Fuchs, the Rosenbergs, Harry Gold) plus Hiss, White, Maclean, Hall.
  The canonical proof that breaks come from usage flaws, not machines — the
  Gauntlet hunts usage first. [VERIFIED]

## Crypto decoders
- RSA / discrete-log systems: threatened by **Shor's algorithm** on a large
  fault-tolerant quantum computer. [CORROBORATED]
- **Post-quantum migration**: NIST-standardized PQC algorithms (ML-KEM, ML-DSA)
  are rolling out now. [VERIFIED]
- AES-256: Grover's algorithm halves effective strength — still considered safe.
  [CORROBORATED]

## Media decoders — the VLC model
VLC/ffmpeg decode nearly every codec on earth: H.264, H.265/HEVC, AV1, VP9,
AAC, Opus, FLAC, MP4/MKV containers, subtitle formats. "Decode everything" is a
real, working model — the cost is maintenance against a moving target of new
formats. [VERIFIED]
- **AV2 (AOMedia Video 2, v1.0.0, finalized May 28 2026):** the open
  royalty-free successor to AV1 — new bitstream, not backward compatible with
  AV1 decoders; ~30% better compression at the same quality (prototype-stage
  claim); reference software AVM; VLC 4.0 demonstrated software playback at CES
  2026; no hardware decode in any shipping device yet (software only, ~5x
  heavier than AV1 — claimed; hardware expected 2027–2028 — speculation). Every
  new codec parser is new attack surface; "plays everything" is a moving
  target. [CORROBORATED]

## Protocol & language decoders
- **Wireshark dissectors**: the model for protocol decoding — hundreds of
  protocols, community-extended. [VERIFIED]
- **Machine translation / LLMs**: language decoding at scale; low-resource and
  ancient languages are active decipherment frontiers. [CORROBORATED]
- **Wireshark 4.6.9 dissector update (Oct 2026)**: updated dissection for QUIC,
  LoRaWAN, ZigBee ZCL, SGP.32, OpenFlow and more, plus 19 vulnerability fixes
  across dissectors — every dissector is a hostile-input parser.
  [CORROBORATED]
- **Opener / DECT NR+ open reference stack (Aug 2026)**: Apache 2.0 reference
  implementation (C, Zephyr RTOS) of the non-cellular 5G massive-IoT mesh
  standard — a new wireless decode target goes open. [CORROBORATED]
- **Apollo — foundation LLM for Ancient Greek (Sep 2026)**: first advanced LLM
  purpose-built for a dead language (~600M words of Ancient Greek); fills
  missing passages in fragmentary texts, gap-finding, dating, historical
  context, multiple candidates for scholar review. ~80% on masked-passage
  reconstruction; blind-study experts rated suggestions as-good-as-human 77%
  of the time, better 16-20%. Decoder template: dead-language foundation
  models scale decipherment the way cribs scaled Enigma — statistical
  reconstruction of the probable, never proof of the true. [CORROBORATED]
- **SPMTNet / XiXiaDB — structural-prior Tangut recognition (Oct 2026)**:
  deep learning that reads Tangut characters by their component structure
  (composition + spatial relations), not whole-glyph appearance — the general
  template for hieroglyphs/Mayan/cuneiform-class scripts, and the same order
  the Gauntlet uses on a foreign format: structure first, appearance second.
  [VERIFIED — paper at DOI 10.1038/s40494-026-03012-6]

## The quantum track (honestly scoped)
Quantum advantage is **problem-specific** (factoring, search, simulation,
optimization) — not a universal "decode all information" engine. Active research:
quantum error correction, quantum machine learning, quantum cryptanalysis.
- **IonQ real-time QEC decoder (Sep 2026).** Company claims the first end-to-end
  real-time quantum error correction decoder on one standard CPU; dual-decoder
  architecture, circuits simulating up to 408 logical qubits. [CLAIMED]
- **LR-QAOA QEC-operations benchmark (Oct 2026).** Jülich preprint; 10 QPUs from
  IBM, IQM, Quantinuum; Quantinuum Helios-1 led, 91-data-qubit tests; a readiness
  gauge before full error-correction experiments. [CORROBORATED]
- **Real-time measurement-and-reset at 100 qubits (Nature Physics, Oct 2026).**
  Rutgers/IBM: ~5,000 two-qubit ops + ~5,000 measurement-and-reset cycles,
  sharp chaos-to-control transition — the feedback capability QEC requires.
  [CORROBORATED]
- **PQC deadlines landing now.** Oct 2026: federal agency migration plans due;
  Dec 2026: FAR Council proposed contractor-compliance rule; Jan 2027: CNSA 2.0
  for new national-security-system buys (EO 14412 / OMB M-26-15).
  [CORROBORATED]
The universal quantum decoder stays [SPECULATION] until proven.

## Photonic comms & power

- **Chip-scale free-space beam steering (Opto-Electronic Advances, 2026).**
  MIT/SMART team: two-dimensional steering across a measured 161-degree field
  of view at near-diffraction-limited quality — a silicon photonic chip routing
  light through on-chip switches to a freeform micro-optical reflector,
  instead of a phased array of tuned shifters. A chip-scale steering front-end
  is what free-space optical comms needs to leave the lab bench.
  [CORROBORATED — peer-reviewed journal]
- **Self-stabilizing photonic lasers (Nature Photonics, Oct 2026).** Reichler
  et al: self-injection locking held across the full drive-current range cut
  frequency noise by more than 5,000x versus the free-running laser, with
  linewidth under 10 Hz and mode-hop-free 1.5 GHz chirps — all without active
  control. Ultralow-noise self-stabilizing lasers are the transmitter side of
  coherent optical comms, lidar, and quantum sensing.
  [CORROBORATED — peer-reviewed]
- **All-optical switching integrated on chip (Nature Nanotechnology, Sep
  2026).** Eindhoven/LioniX: first all-optical magnetization switching fully
  inside a silicon nitride photonic circuit — light delivered through an
  on-chip waveguide flips bits in cobalt-gadolinium ferrimagnets on
  picosecond timescales. Light writing memory with no electrical path is a
  storage side-channel shape the gauntlet keeps in its threat library.
  [CORROBORATED — peer-reviewed]
- **Photonic spectrum slicer past 200 GBaud (Communications Engineering, Oct
  2026).** Southampton-led team (DOI 10.1038/s44172-026-00801-6): a photonic
  integrated recurrent spectrum-slicing receiver pushes direct-detection
  formats (PAM-4 / on-off keying) to some of the highest symbol rates yet
  over dispersive fiber, with affordable detection hardware.
  [CORROBORATED — peer-reviewed]
- **Telecom-band quantum memory over 1 microsecond (Nano Letters, Oct 9,
  2026).** Goldschmidt's group: nanophotonic lithium-niobate platform holding
  multiple photons at once, aimed at manufacturable quantum memories for
  chip-based quantum computers and networks.
  [CORROBORATED — peer-reviewed]
- **Orbital laser power beaming tests (Oct 2026).** Star Catcher Protostar
  flew on SpaceX's Transporter-18 to attempt laser power transfer to a
  free-flying CubeSat — claimed first optical power beaming between two
  untethered spacecraft. Cowboy Space's Reason-1 aims for a first
  orbit-to-ground laser transfer test in late October 2026 (30-100 W into a
  10-20 m spot). Until the tests fly, these are beaming tests, not beaming
  systems. [CLAIMED — company announcements; independent reporting]

---
*This catalogue grows every 30 minutes via the research loop. New entries must
carry an evidence grade and a source.*
