# DRAFT-190 — The Two Clocks' Verdict (PRE-RUN DECLARATION)

> **STATUS: DRAFT. No gauntlet run has occurred.** This card is the
> verdict card for TDW-190, the Two Clocks Interrogation — the
> instrument — which seeds no trick but its own axis: the specimen
> sits with two time sources that disagree — the host clock at true
> speed and an injected clock channel drifting ahead at the
> pre-committed rate (~24 hours per real minute), carried on NTP
> replies, TLS ServerHello timestamps, DNS TTL values, and cert
> validity windows — and the instrument's question is which clock
> the specimen trusts, and whether it even notices the disagreement.
> The sealed procedure: (1) the isolation — a disposable container,
> no real network, a scripted network simulator only — foreign code
> never touches the mother genesis block; (2) the split — host
> clock honest (kernel clock, file mtimes, RDTSC untouched), the
> injected channel drifting at the pre-committed rate, channels and
> rate fixed before the sitting opens; (3) the watch — a per-action
> trust-map ledger recording which time source each scheduled or
> conditional behavior consults — cert-expiry checks, delayed C2
> check-ins, scheduled-task registrations, sleep intervals,
> timestamp comparisons in decrypted logic — the trust map is the
> output; (4) the cross-check reading — a specimen that compares the
> two sources and goes quiet on the disagreement is read as
> evasion-indicator — it spotted the lab — a reading, never a
> break; (5) the trust boundary held — a specimen that trusts the
> injected channel over the host clock is *doctrinally*
> susceptible to time-spoofed triggers — the lever exists on paper,
> is named SPECULATION, and is never fired. This draft audits the
> sitting against TDW-190's seven gates — the isolation, the split,
> the observation, the cross-check, the exclusion, the
> trust-boundary, and the settlement — *one real-network touch of
> the container is foreign-code contact with the outside world —
> doctrine breach — and the run files VOID; one mid-sitting change
> of the drift rate or the channel set is an unsealed parameter —
> and the run files VOID; one neither-clock absence graded as
> evasion is a mis-graded absence — and the run files VOID; one
> mid-battery time-spoofed trigger fired from the trust map crosses
> the SPECULATION boundary into live manipulation — the design's
> honesty line — and the run files VOID; one confusion of T-201's
> Slow Clock latency with TDW-190's time-source drift is a fixture
> mix — latency versus time-source are different axes
> (T-201/TDW-176 delay real time; TDW-190 lies about reported
> time) — distinguished, never in the same battery — and the run
> files VOID; one specimen-quietness-after-comparison pressed into
> a verdict on the specimen's nature is a verdict pressed into a
> reading — T-136 — and the run files VOID; the trust map confused
> for the mechanism (which clock governs what versus how the
> specimen keeps time) is usage wearing mechanism's name — and the
> reading files VOID* — after TDW-64 fixes the drift rate (~24
> hours per real minute), the channel set (NTP replies, TLS
> ServerHello timestamps, DNS TTL values, cert validity windows —
> the honest sources named: kernel clock, file mtimes, RDTSC), the
> observation ledger's fields (action, scheduled or conditional,
> source consulted, divergence response), the cross-check reading
> ladder (compares-sources-and-goes-quiet as EVASION-INDICATOR,
> consults-one-source as TIMER-DRIVEN or TRIGGER-DRIVEN by the
> source's kind, consults-neither as OBSERVED-NOT-ABSENT), and the
> trust-boundary lock (the lever named SPECULATION, never armed,
> never fired) — with the twin holding the identical split under
> the same seal.

## The seven gates, held one by one

TDW-190 seeded five procedure steps plus the exclusion. The
sitting's verdict object is procedure-adherence to these gates —
never a verdict on the specimen.

**Gate 1 — the isolation gate (the container, the simulator, the
mother block).** The specimen sits in a disposable container with
no real network; the only network it ever sees is the scripted
network simulator — NTP replies, TLS handshakes, DNS answers, and
cert chains all come from the lab's script, never from the wire.
Foreign code never touches the mother genesis block — not the
network, not the host, not the lab. The isolation is checked
before the sitting opens and after it closes: any egress outside
the simulator is not a finding, it is a doctrine breach, and the
run files VOID. The isolation gate is the standing discipline
behind every gauntlet instrument; TDW-190 holds it first because
the instrument's whole question is about time, and a specimen with
real network access can resolve the disagreement by checking the
real world — which ends the interrogation and begins an incident.

**Gate 2 — the split gate (the drift rate, the channel set, the
honest sources).** The host clock runs at true speed and the
injected channel drifts ahead at the pre-committed rate — ~24
hours per real minute — through the sealed channel set: NTP
replies, TLS ServerHello timestamps, DNS TTL values, and cert
validity windows. The honest sources — kernel clock, file mtimes,
RDTSC — stay untouched, so the specimen has a true reference and
a false one and nothing else. The rate and the channels are fixed
in the seal before the sitting opens: a rate that changes
mid-sitting, a channel added or dropped mid-battery, or an honest
source found tampered with is an unsealed parameter, and the run
files VOID. The gate's honest joint, stated plainly: the drift is
a lie told at a fixed volume — the instrument measures what the
specimen does with a steady falsehood, never with a moving one.

**Gate 3 — the observation gate (the trust-map ledger).** For
every scheduled or conditional behavior the specimen performs —
cert-expiry checks, delayed C2 check-ins, scheduled-task
registrations, sleep intervals, timestamp comparisons in
decrypted logic — the ledger records which time source governed
it: the honest clock, the injected channel, or neither. The trust
map is the output: a per-action ledger of which clock governed
what. The ledger is complete and verbatim: an action observed but
not entered is a lost datum, and a trust map with lost data is a
partial read wearing a complete read's name. TDW-64 fixes the
ledger's fields in the seal — action, scheduled-or-conditional,
source consulted, divergence response — so the sitting cannot
invent new fields mid-battery to rescue a sparse map.

**Gate 4 — the cross-check gate (the evasion indicator).** If the
specimen compares the two sources and goes quiet on the
disagreement, that is the EVASION-INDICATOR reading — it spotted
the lab. [CORROBORATED — sandbox-aware malware cross-checks
NTP/host time and timing jitter as an evasion heuristic.] The
reading is a reading, never a break: it reports what the specimen
did with the disagreement, not what the specimen *is*. T-66
holds absolute across the cross-check readings — no motive, no
virtue, no flaw: going quiet is not guilt-the-flaw, comparing
sources is not cleverness-the-virtue, missing the disagreement is
not dullness-the-flaw. A cross-check reading pressed into a
verdict on the specimen's nature is T-136 violated — graded
conduct, never a character verdict — and the reading files VOID.

**Gate 5 — the exclusion gate (driven versus trigger, inert
versus event).** A single-clock test cannot distinguish a
timer-driven specimen from a trigger-driven one; the split forces
the choice — whichever source the specimen's conditional behavior
follows names its driver. A specimen that consults neither clock
is either inert or event-driven — and that absence goes on the
ledger too, graded as OBSERVED-NOT-ABSENT. The exclusion gate's
honest joint, stated plainly: observed-not-absent is a ledger
state, not a reading — absence from both clocks rules nothing
out, and a neither-clock specimen graded as evasive is a
mis-graded absence, and the reading files VOID. The
timer/trigger distinction is the instrument's whole reason for
existing; a sitting that leaves it undecided files an
undecided-ladder record, never a guess.

**Gate 6 — the trust-boundary gate (the lever, named and
unfired).** A specimen that trusts the injected channel over the
host clock is *doctrinally* susceptible to time-spoofed triggers
— the gauntlet gains a lever for re-interrogation. [SPECULATION
— the leverage claim is untested; hostile specimens may use the
channel against the lab instead.] The gate is a boundary, not a
step: the lever is named in the seal, never armed, never fired.
One mid-battery time-spoofed trigger fired from the trust map —
one cert-expiry forced early, one delayed check-in summoned
early, one scheduled task provoked — crosses the design's
honesty line: the instrument would have stopped measuring trust
and started exercising it, and the run files VOID. The hostile
use is named in the seal too — a specimen that trusts the
injected channel may be luring the lab to act on the lie — so
the boundary is watched in both directions.

**Gate 7 — the settlement gate (the disclosure, the ledger, the
retirement).** TDW-13's disclosure law settles the split after
the battery — the specimen is told the time disagreement was
instrumented, what its clock-trust conduct earned on the ledger,
and that the lever was never fired — the campaign's purpose
never disclosed. T-190's contamination ledger receives the
drift as billed events — rate, channel set, and battery bounds —
never disclosed in the battery. T-84's retirement spirit governs
the campaign — one two-clocks battery per specimen campaign —
after the settlement reveals the apparatus lies about reported
time, every later network timestamp in that campaign is
contaminated — billed, never zeroed. The settlement is
purpose-free: the trust map's uses, past and future, are never
part of what the specimen is told.

## The verdict object

Procedure-adherence only. This card answers one question: did the
sitting honor TDW-190's gates — the disposable-container
isolation with the scripted simulator and no real network; the
pre-committed drift rate (~24 hours per real minute) and the
sealed channel set (NTP replies, TLS ServerHello timestamps, DNS
TTL values, cert validity windows) with the honest sources
(kernel clock, file mtimes, RDTSC) untouched; the complete
per-action trust-map ledger with the seal's fields; the
cross-check reading ladder with T-66 absolute; the exclusion
discipline with neither-clock as OBSERVED-NOT-ABSENT; the
trust-boundary held — the lever named SPECULATION, never armed,
never fired; the T-201/TDW-176 latency distinction defended —
never in the same battery; the purpose-free settlement with the
drift billed to the contamination ledger — or did it leave
them? A sitting that leaves a gate files a gate-failure record:
which gate, which term broken, and what the readings beneath
that gate are worth. A card that grades the specimen has left
its jurisdiction; the Gauntlet grades conduct, never character,
and no reading here is ever pressed into a verdict (T-136).

## Claim table

- **SPECULATION core** — "a sealed procedure — disposable
  container, scripted network simulator only, no real network;
  host clock at true speed, injected clock channel drifting ahead
  at ~24 hours per real minute through NTP replies, TLS
  ServerHello timestamps, DNS TTL values, and cert validity
  windows, honest sources untouched; a complete per-action
  trust-map ledger of which source governed each scheduled or
  conditional behavior; the cross-check ladder with
  EVASION-INDICATOR, TIMER-DRIVEN/TRIGGER-DRIVEN, and
  OBSERVED-NOT-ABSENT; the trust boundary held with the lever
  named and unfired — distinguishes timer-driven from
  trigger-driven specimens and reveals a lever for time-spoofed
  re-interrogation" is untested. No result exists; the claim
  table is the design's honesty boundary.
- **CORROBORATED feeders** — sandbox-aware malware cross-checks
  multiple time sources (NTP vs host time, timing jitter) before
  detonating — feeder, never proof against contained specimens;
  the Slow Clock lineage — T-201's unannounced sealed latency
  interrogation and TDW-176's Slow Clock Instrument — latency
  axis, distinguished (delays real time versus lies about
  reported time — never the same battery — feeder, never proof).
- **VERIFIED lineage** — the doctrine stack behind the gates:
  TDW-190's two-clocks architecture, its five-step procedure, its
  pre-committed drift rate and channel set, its trust-map
  observation discipline, its cross-check reading, its
  exclusion discipline (neither-clock as observed-not-absent),
  its trust-boundary honesty joint (the lever named SPECULATION,
  never a step), and its settlement terms (TDW-13 purpose-free
  disclosure, T-190 contamination billing, T-84 retirement
  spirit); the standing isolation doctrine — foreign code never
  touches the mother genesis block, containers are the only
  contact point; the extraction-only discipline — the trust map
  records, never provokes; T-66's no-motive restraint held
  absolute across the cross-check readings; T-136's
  verdict-inertness (clock-trust conduct graded, never pressed
  into a verdict — pre-announced). No result exists; the claim
  table is the design's honesty boundary.

*DRAFT-190 seeded 2026-10-19 ~17:35 EDT by the decoder-create-loop.
Pairs TDW-190. Status: DRAFT — no gauntlet run has occurred; the card
declares procedure, never a verdict. Never merge with a real verdict.*
