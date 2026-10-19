# Koda Kai the Decoder — Math/Physics Equation Engine (capability map)
Seeded 2026-10-12. Local stack (verified on this VM): **sympy 1.12, numpy 1.26.4, scipy 1.11.4**. Stdlib-first preference per David's doctrine; these three are the honest minimum for the equation engine.

## 1. What SymPy does today (the symbolic core)
- Symbolic algebra: simplify, factor, expand, solve equations/systems — exact, readable math the Gauntlet can print as receipts. [VERIFIED — SymPy is the de-facto Python symbolic library]
- Calculus: limits, differentiation, series, definite/indefinite integrals — many classes solved exactly; the rest fall through to numeric. [VERIFIED]
- ODEs/PDEs: `dsolve` handles common ODE classes; PDE support is partial — real physics PDEs go to numerical solvers (scipy/`solve_ivp`, finite differences) rather than closed form. Honest line: most real-world equations have **no closed-form solution**; the engine's job is numeric approximation with error bounds, not magic formulas. [VERIFIED — SymPy docs scope]
- Linear algebra: matrices, eigenvalues, decompositions (numpy/scipy for the numeric heavy lifting). [VERIFIED]
- Probability distributions & statistics: `sympy.stats` supports named distributions (Normal, Poisson, Binomial...), symbolic expectation/variance — good for teaching-grade Bayesian work; production inference uses scipy.stats / PyMC-style samplers. [CORROBORATED]
- Code generation: SymPy can emit C/Fortran code from symbolic expressions — equations become compiled kernels the Gauntlet can call fast. [VERIFIED — sympy.codegen exists]
- Limits to log: expression blow-up on big systems; assumption machinery is brittle; no general PDE solver; performance is human-scale, not data-scale. [CORROBORATED — known library tradeoffs]

## 2. Information theory shelf (the decoder's home turf)
- Shannon entropy, conditional entropy, mutual information, KL divergence, cross-entropy — all computable in numpy in a few lines; scipy for the estimators. These measure *how much signal is in the noise* — the quantitative spine of cribs-and-statistics breaking. [VERIFIED — standard definitions, textbook results]
- Rate-distortion, channel capacity: the formulas exist; computing capacity for a *real observed channel* is a numeric/optimization problem, not a library call. [CORROBORATED]
- Application: anomaly scoring of foreign code (entropy of instruction streams, divergence from known-good profiles) — legitimate, graded statistical evidence, never a verdict alone. [SPECULATION as a Gauntlet method — the math is real, the pipeline is ours to prove]

## 3. Probabilistic & predictive math — honest ledger
What works, and where it breaks:
- **Bayesian updating** (Bayes' rule, conjugate priors, posterior sampling): the engine for "belief that this blob is hostile" as evidence accumulates. Real; the limit is prior choice — priors are judgment, and garbage priors poison posteriors. [VERIFIED — standard inference]
- **Markov chains / HMMs:** model sequences with hidden states (protocol parsing, behavior profiling). Stationarity assumptions break on adversarial actors — attackers change policy, which violates the model's core assumption. [VERIFIED as math; CLAIMED limits are standard ML caveats]
- **Monte Carlo methods:** approximate anything with sampling when closed forms don't exist; convergence is √N slow — high precision costs exponential samples. [VERIFIED]
- **Kalman / particle filters:** state estimation in noisy systems; Kalman is optimal *only* for linear-Gaussian — everything else is approximation. [VERIFIED — filtering theory]
- **Time-series forecasting (ARIMA, Prophet-style, neural):** short-horizon structure only; uncertainty explodes with horizon. Any "prediction engine" claim beyond short, well-conditioned horizons must carry its confidence interval or it's theater. [CORROBORATED — forecasting literature consensus]
- **Prediction markets — what they can credibly claim (Zitzewitz NBER working paper, Oct 2026):** no systematic partisan bias found across the largest election-market sample ever assembled (1880–2025); at the one-day horizon, a left-leaning bias of ~4.5pp or right-leaning bias of ~3pp is ruled out. But they are not oracles: in 2024 they matched statistical models nationally yet underperformed down-ballot, and polls and markets make *different, largely unrelated errors* — the honest posture is the ensemble, not the single number. [CORROBORATED — working paper; not yet peer-reviewed]
- **Precursor-of-anomaly detection (FATE, arXiv:2602.17028, preprint):** ensemble disagreement across time-series forecasters as an early-warning signal — no labels, no target values at inference; new PTaPR metric scores early-warning promptness, not just detection. Watch: replaying this in the Gauntlet's telemetry watch is the natural test. [CLAIMED — preprint]
- **Benchmark honesty as method (RAP, Scientific Reports 2026):** random analog prediction is deliberately simple — its stated value is that any complex model that cannot beat it has no business claiming skill. This is the Gauntlet rule applied to forecasting: a dumb baseline must be on the scoreboard before a smart model earns a grade. [CORROBORATED — peer-reviewed paper]
- **Score the reasoning, not just the number (EQMs, arXiv:2606.30987, pre-registered):** sixty LLM-scored reasoning patterns extracted from forecasters' written rationales predict tournament accuracy across 55,000+ forecast-rationale pairs, beating pre-LLM text methods, transferring to an independent study — and flagging underperformers asymmetrically better than it crowns winners. Cross-ref: DECODERS.md §(g).
- **Real-money forecasting is a harsher benchmark (Prediction Arena, arXiv:2604.07355, 2026-04).** Six frontier models, each handed a real ten thousand dollars and fifty-seven days on the prediction market Kalshi, returned negative sixteen to negative thirty-point-eight percent; research volume was approximately uncorrelated with profit. Probabilistic skill on paper does not convert to P&L under real execution costs. PolyBench's 38,666 Polymarket snapshots (arXiv:2604.14199) are now a public real-market dataset for re-running the question. [CLAIMED — arXiv preprint; single study]
- **Bayesian update as architecture, not behavior (Agentic Forecasting with Sequential Bayesian Updating, arXiv:2604.18576).** Agentic forecasting with explicit Bayesian-update steps — beliefs revised as evidence arrives, by design rather than emergence. [CLAIMED — arXiv preprint]
- **Machines take a major forecasting tournament (outcome VERIFIED via Reuters; vendor texture CLAIMED).** In the summer 2026 Metaculus Cup — a tournament where participants assign probabilities to political, economic, and cultural events and are scored when those events resolve — the first- and second-place finishers were both AI bots, ahead of every human forecaster. The field: 885 forecasters, about eighty-eight thousand forecasts, fifty-eight questions. The runner-up's builder, a London startup founded by a former DeepMind researcher, raised twenty-five million dollars on the strength of the result; the company credits its edge to avoiding herd behavior — two of its notable calls were raising the odds on a Colombian presidential winner above the human consensus (he won) and refusing to follow the crowd on a pop-chart question (the crowd was wrong). Honest footnotes: the bots were ineligible for prizes or medals, the two sides cite different participant counts, and this is one tournament, one season. Significance: scored judgmental forecasting now has a machine-dominated tournament on the record — the long-awaited track-record datum for the question of which predictive math earns its keep.
- **Markets still beat models on calibration (CLAIMED — a self-published but honest frozen archive).** An independent scoreboard locked predictions before every kickoff of all one hundred four World Cup matches and scored three sources afterward: a statistical model, the sportsbook, and a prediction market. On calibration the markets won — the model's average error was higher and its favorite won less often. But the model was the only source ever decisively right on its own, twenty-six times against five for the market and zero for the book. Significance: calibration and boldness are different virtues; markets own the former, a bold model can own the latter. Companion note: six frontier AI systems, making about four and a half thousand leakage-free predictions before kickoff, averaged about sixty-four percent on match outcomes — level with backing the bookmaker's favorite, which is mostly what they do. The current generation is not sharply differentiated on this task.
- **Fixing bias beats out-predicting physics (CLAIMED — trade-press writeup of a European weather agency's competition).** A competition to improve sub-seasonal weather forecasting was won by a model built around probabilistic bias correction — attacking systematic error rather than trying to outperform the physics. Reported gains: seventy to eighty percent for precipitation, over two hundred percent for temperature and pressure. Significance: the "fix the bias, don't fight the physics" instrument — calibration over creativity, the same philosophy the ledger tracks elsewhere.
- **Model upgrades don't move the needle (RMF benchmark, arXiv:2609.32885, submitted Sep 26, 2026).** Resolved Market Forecasting: 3,000 resolved binary questions across nine domains, zero-shot. Four Claude models land at Brier 0.183–0.192, improving on the empirical base-rate predictor by only 0.024–0.033; neither version nor tier upgrades yield significant improvement, and within-model differences across event categories exceed between-model differences. ForecastBench's standing line (around 0.101 best-LLM versus 0.081 superforecaster) corroborates the gap. [CLAIMED — arXiv preprint]
- **Anomaly detection, frequency-domain joint modeling (FCAE-Mixer, Scientific Reports, published Sep 10, 2026).** Frequency-aware convolutional autoencoder with dual-branch mixing: a 1D convolutional autoencoder for local temporal transients, a multi-layer perceptron for global variable mappings, and an FFT-Attention module focusing on low-frequency modes. Average F1 of 0.3317 without point-adjustment across seven benchmarks — a 10.5% relative improvement over the Transformer baseline. [CORROBORATED — peer-reviewed; no independent replication read this pass]
- **Production anomaly watch with open data (TAMIS, arXiv:2609.39257, submitted Sep 30, 2026).** A production system for anomaly detection in short-term electricity production forecasts, with human-in-the-loop review via a daily anomaly newsletter — and anonymized application datasets released publicly. [CLAIMED — arXiv preprint] [CORROBORATED — pre-registered, large-N; peer review unconfirmed]
- **The Gauntlet rule:** every prediction ships with its assumptions, its data, and its error bars. Prediction without a confidence interval is not decoding — it's guessing.
- **Scored forecasting from a live field (new to record; public scoreboards, tournament completed July 2026).** A free-to-play probability contest over the World Cup — scored with a proper scoring rule — posted final leaderboards. One open bot finished about the top five percent of more than four thousand forecasters with a published calibration curve tracking actual hit rates across the full probability range; a second independent entry finished eighty-ninth of four hundred eighty-eight. Ledger value: scored, public, crowd-relative — corroboration from a live field that calibration discipline, not cleverness, is what beats the crowd. [CLAIMED — self-reported on public repos]
- **An honest null against live prediction markets (new to record; public repo).** A calibrated statistical model used as a fair-value reference against live World Cup market contracts: the model-market gaps reflected the market's known favorite-longshot bias, and after fees no tradeable edge existed. Calibrated probability does not convert to profit under execution costs — and the modeler says so publicly. Honest nulls earn their place in the ledger. [CLAIMED — self-reported]
- **A graph-based anomaly detector for drone sensors (new to record; peer-reviewed paper).** A hybrid approach to catching sensor attacks on drones — fake GPS signals and injected gyroscope drift — combining an adaptive sensor-relationship network, dual time-and-frequency analysis, and a trend module for slow stealthy drift. Reported detection score: ninety-nine point seven one percent. The anomaly-detection watch now tracks four standing techniques. [CORROBORATED — peer-reviewed journal; reported through secondary coverage]
- **Classical statistics beat deep learning on scarce data (new to record; peer-reviewed paper).** A head-to-head benchmark on urban traffic-sensor data: the classic nineteen-fifties sequential CUSUM test scored an F-one of zero point nine five eight with perfect precision; the tuned Isolation Forest had the best recall; the neural autoencoder managed zero point three five one, its failure attributed to limited training data. The ledger lesson: on scarce data, the simple old method wins — name the regime, not just the winner. [CORROBORATED — peer-reviewed journal; abstract-level read]
- **Human-AI forecasting parity is now a statistical dead heat (Metaculus Cup, September 2026).** Humans took the top two spots, Preseen's AI third in the latest Cup (roughly fifty questions); Metaculus's own investigation values good scaffolding at "nine months of base-model progress" — a scaffolded model today matches where raw models project nine months out, with human-AI parity projected in about six months. Repeatability caveat from the summer Cup: two out of ten of spring's top-ten humans repeated, same two out of ten for AIs — skill-versus-luck separation is thin on both sides. A second secondary headlines "AI took the top spots" — framing dispute unresolved. [CLAIMED — trade-press secondaries]
- **Experts under-calibrated on their own field's milestones (Forecasting Research Institute accuracy review, published September 23, 2026).** Three hundred thirty-nine AI experts assigned twenty-four point six percent mean probability to four AI benchmark outcomes that arrived (MATH, MMLU, QuALITY, IMO gold) versus nine point seven percent from superforecasters; IMO gold arrived July 2025 — five years before the median expert's 2030, ten years before the superforecasters' 2035. Ledger line: expertise is not the same as calibration; short-horizon capability questions are where experts miss. [CLAIMED — single secondary summary]
- **The Good Judgment Project teaming/training effect is contested (reanalysis published 2025 in Psychological Science).** An item-response-theory refit of the tournament data found the teaming/training accuracy effects "substantially eliminated, reduced, and in some cases even reversed" after controlling extraneous variables. Ledger discipline: any citation of the teaming/training gains carries the contested flag. [CLAIMED — published reanalysis, via secondary compilation]
- **Language models writing anomaly detectors, not being them (arXiv paper, submitted October 1, 2026).** An autonomous edit-loop in which a language model authors a single short NumPy detector (local spectral features plus covariance-aware distance) under a leakage-free objective; it leads the TSB-AD benchmark across metrics ahead of classical, deep, and foundation baselines including Time-RCD — no GPU, fully readable. The telemetry watch now has two competing standing techniques: the FCAE-Mixer learned frequency model versus program-search discovery. [CLAIMED — arXiv preprint; single study]
- **Spectrum-guided teacher-student anomaly detection (reported September 2026).** A two-part detector for predicting system faults before they strike: one part scores fine-grained short-term anomalies, the other watches longer horizons for prediction rather than detection, with a Bayesian optimizer tuning the detection windows automatically. It averaged an F-one score of eighty-eight point four nine percent across four standard benchmarks — server telemetry and NASA Mars and planetary rover data — outperforming several state-of-the-art methods. Built by a team tied to China's Zhejiang power grid, where unlabeled data is abundant and confirmed fault labels are scarce. The project's telemetry watch now tracks three competing techniques: the learned frequency model, program-search discovery, and spectral teacher-student distillation. [CORROBORATED — peer-reviewed paper; trade-press report, paper not opened first-party]
- **Bayesian anomaly quality control for scientific datasets (Benford's-law framework, published 2026 in Patterns).** A Bayesian framework that flags hidden irregularities in large scientific data collections using Benford's law, attributing them to experiment design, data processing, or curation choices — aimed at automated quality control for scientific data, not fraud forensics. A new Bayesian detector family for the project's anomaly-watch benchmark suite. [CORROBORATED — peer-reviewed paper; trade-press report, paper not opened first-party]
- **Uncertainty-aware Bayesian L-S-T-M forecasting (journal paper, 2026).** A Bayesian L-S-T-M with attention for air-quality forecasting that publishes calibrated confidence intervals and an anomaly-detection score — its standard-deviation calibration technique is a candidate for the project's honest confidence-reporting layer. [CORROBORATED — peer-reviewed journal; abstract and index record only]

## 4. Physics shelf (reference equations the Gauntlet can call)
Each is standard textbook material — the library holds them as callable equations, not as solved problems:
- **Classical mechanics:** Newton's laws, Lagrangian/Hamiltonian formulations; conservation laws (energy, momentum, angular momentum). Trajectory/thermal problems the future systems will face (orbital mechanics for the spaceship angle: two-body problem, Hohmann transfers — closed forms exist). [VERIFIED — classical mechanics canon]
- **Electromagnetism:** Maxwell's equations; wave equation → antennas, waveguides, signal propagation. [VERIFIED]
- **Thermodynamics/stat-mech:** laws of thermo, Boltzmann distribution, partition functions — heat, efficiency limits, entropy budgets for any physical system. [VERIFIED]
- **Quantum mechanics basics:** Schrödinger equation, operators/observables, uncertainty principle; *decoherence* is why quantum "decode everything" stays CONJECTURE — real devices fight noise, they don't transcend it. [VERIFIED — QM canon; decoherence limits are standard physics]
- **Relativity:** SR time dilation (the literal physics behind time-dilated virtual machines running slower/faster than wall clock); GR basics. [VERIFIED]
- **Photonics (David's standing future-tech order):** waveguides, lasers, photodetectors, fiber optics, free-space optical comms math — the real equations for "energy to spaceships" will be power-beaming / laser-propulsion link budgets (inverse-square, diffraction-limited spot size, conversion efficiency). Recorded as a *research shelf*: the math is real, our specific designs are CONJECTURE until built. [VERIFIED as physics; CONJECTURE as our designs]

## 5. The honest architecture for the Gauntlet's math brain
1. **SymPy layer:** symbolic definitions, exact where possible, codegen for speed, human-readable receipts.
2. **NumPy/SciPy layer:** the numeric workhorse — solvers, distributions, FFTs, optimization, stats.
3. **Bayesian layer:** priors → likelihoods → posteriors; every foreign-object verdict carries its evidence trail and confidence.
4. **Sampling layer:** Monte Carlo for the integrals reality won't give in closed form.
5. **Forecasting layer:** short-horizon, interval-carrying predictions; honest about degradation.
6. **Grades layer:** every equation call returns its result **and its assumptions** — the Fabrication Alarm applies to math too.

## 6. What's NOT here (on purpose)
- No "solve any equation" promise — most nonlinear systems need numerics with bounds.
- No quantum advantage claims beyond problem-specific speedups (Shor/Grover), per DECODERS.md.
- No AGI-voxel codec entries until the research loop verifies real papers/products — David named Google's new codecs as a target; the loop checks them, the library does not invent them.
- No code yet — capability map only, per seed order. First build: sympy-based equation registry the Gauntlet can call, exact-then-numeric with error bounds and assumption receipts.

## 7. First build landed: `engine/equation_registry.py` (2026-10-12)
The first code artifact of the math engine, seeded by the decoder-create-loop.
A sympy-based equation registry the Gauntlet can call:

- **Exact-then-numeric.** Every `evaluate(name, **inputs)` solves the registered
  equation symbolically for the missing variable first, returns the closed form
  as the receipt's `exact_solution`, then substitutes for the numeric result.
- **Receipts, not numbers.** Every call returns a receipt dict: equation name,
  grade, assumptions, closed-form solution, substitutions, result, uncertainty
  (`sigma`), notes, warnings, timestamp. A bare float never leaves the module.
- **Uncertainty handling.** Inputs may be `(value, sigma)` tuples; sigma is
  propagated first-order via sympy gradients. No input uncertainties →
  explicit warning: "point estimate only, no confidence interval (this is not
  a prediction, it's a calculation)." Non-differentiable points → sigma
  withheld, never guessed.
- **Honest failure modes.** No closed form → says so, returns `None`, does not
  fake a number. Underdetermined → says which symbols are missing, returns
  `None`. All symbols supplied → returns the residual (a consistency check,
  not a solution). Unknown equation → `KeyError`, never a silent default.
- **Canonical set (all VERIFIED as math; application to any real specimen is a
  separate claim):** `projectile_range`, `time_dilation` (SR — the physics
  behind time-dilated guest clocks), `kinetic_energy`, `ideal_gas`,
  `beta_binomial_posterior_mean` (the belief engine — receipt names the prior,
  "PRIOR CHOICE IS JUDGMENT, not data"), `shannon_entropy`.
- **Real test results (self-test + regression run on this VM, sympy 1.12):**
  projectile 63.7105 m (25 m/s @ 45°); gamma 1.15470 ± 0.00257 @ 0.5c
  (matches 1/sqrt(1−0.25) exactly); KE 450000 ± 15000 J; ideal-gas pressure
  101382.55 Pa (1 mol @ 273.15 K, 22.4 L); posterior mean 9/14 = 0.642857
  (Beta(2,2) + 7/10); entropy 1.75 bits. These are genuine computed results,
  not fixtures.

**What it is not:** not a verdict engine (statistics only, never intent), not
a PDE solver, not a symbolic-regression discovery tool. Next honest step:
~~numeric root-finding path for equations with no closed form (declared, not
yet built)~~ BUILT 2026-10-12 19:20 EDT — see §8 below.

## 8. Second build: the numeric root-finding path (2026-10-12 19:20 EDT)
The math engine's honest confession from §5 was that most real equations have
no closed form — and until now the registry *said* that but had no numeric
path. It does now: `numeric_solve(name, unknown, bracket, tol, max_iter,
**inputs)` in `engine/equation_registry.py`, via
`scipy.optimize.brentq` (bracketed, hybrid bisection/secant).

**Honesty controls (never fabricated):**
- The bracket must straddle a sign change; if it doesn't, `ValueError` —
  the registry never extrapolates a root.
- Every numeric receipt reports method, bracket, function-eval count,
  residual |f(root)| vs tolerance. A converged root with a bad residual
  earns a warning ("treat as CONJECTURE"), not a stamp.
- Sigma propagates by central finite differences of the numeric root
  function; an unstable derivative withholds sigma, never guesses.
- `evaluate()` now routes automatically: sympy's `NotImplementedError`
  ("No algorithms are implemented to solve equation") sends the call to
  `numeric_solve` when the caller supplies `numeric_bracket=(lo, hi)`;
  without a bracket it says exactly what it needs.
- The docstring's promise — "if no closed form exists, it says so and goes
  numeric — never magic" — is now literally true.

**Demonstrator: Kepler's equation, `kepler_equation` (VERIFIED as math —
textbook transcendental; E − e·sin E = M provably has no elementary closed
form).** The first step of any real orbit calculation, and the first registry
equation that can *only* take the numeric path. Assumptions: elliptical
orbit, radians, two-body Newtonian mechanics — application to any real
spacecraft is a separate claim.

**Real test results (this VM, scipy 1.11.4):** E = 1.4987011335178482 rad
for ecc=0.5, M=1.0 (10 function evals, residual 1.1e-16 vs tol 1e-10);
ecc=(0.5, 0.01) → σ(E) = 0.010347 via finite differences — matches the
analytic sensitivity ∂E/∂e = sin E/(1 − e·cos E) = 1.0351 to 4 sig figs,
an independent cross-check of the propagation machinery. The
`numeric_bracket=` routing through `evaluate()` reproduces the same root
(1.4987011335178482). These are genuine computed results, not fixtures.

**Next honest step:** a numerical PDE/ODE solver path (scipy `solve_ivp`),
for the "real physics PDEs" that §1's honesty line names. BUILT 2026-10-12
~20:35 EDT — see §9 below.

## 9. Third build: the ODE integration path (2026-10-12 ~20:35 EDT)
The physics behind "energy to spaceships" is differential equations with no
closed form, so the registry now integrates them: `numeric_solve_ode(name,
t_span, y0, method, rtol, atol, dense, **params)` via
`scipy.integrate.solve_ivp` (default RK45), with an `ODESystem` registry
parallel to the equation registry.

**Honesty controls (never fabricated):**
- A failed integration raises `ValueError` with the solver's message and
  diagnostics — it never returns a fake trajectory.
- When an analytic solution is registered, the receipt cross-checks the
  numeric answer against it on a 200-point grid and reports the max
  absolute error. A failed cross-check is a WARNING, never dropped —
  this caught a real bug the same hour it was built: the registry's own
  underdamped velocity formula had swapped coefficients (max error
  7.49 on the grid), fixed and re-verified to 3.07e-9. The receipt
  machinery earned its keep on its first run.
- No analytic solution → the receipt says so and points at a registered
  physical bound instead (e.g. drag range must be shorter than the
  closed-form vacuum range).
- nfev ≥ 50,000 earns a "maybe stiff" warning suggesting Radau/BDF —
  the registry does not silently re-solve.
- Uncertain params propagate to the endpoint by finite-difference
  re-integration; an unstable re-run withholds sigma, never guesses.

**Canonical ODE systems (VERIFIED as math; application to any real
specimen is a separate claim):** `damped_oscillator` (y'' + 2ζωy' + ω²y =
0, ζ < 1 — analytic cross-check registered) and `projectile_drag`
(quadratic drag F = −k|v|v — no closed form, the honest use).

**Real test results (this VM, scipy 1.11.4):** damped oscillator
(ζ=(0.10, 0.005), ω₀=2π, y₀=[1,0], t∈[0,5], 3866 function evals):
endpoint (0.04199810, 0.04279561), analytic cross-check max error
3.07e-9, endpoint σ=(0.00681, 0.00245) from ζ uncertainty. Projectile
with quadratic drag (v₀=25 m/s @ 45°, g=9.81, k=0.25 kg/m, m=0.5 kg):
range 4.204 m at y=0 crossing, strictly below the vacuum closed-form
upper bound 63.7105 m — the physical bound check passes. These are
genuine computed results, not fixtures.

**What it is not:** not a PDE solver (still missing), not stiff-system
smart (warns, doesn't adapt), no event detection (landing found by
zero-crossing scan in the test harness, not the registry). Next honest
step: a numerical PDE path (method of lines / scipy `solve_ivp` on a
spatial grid), for §1's "real physics PDEs" line — or a time-dilation
scenario runner that puts a specimen binary on a time-warped guest
clock and decodes the delta, the Gauntlet's actual use case for ODEs.

## New engine notes (2026-10-12 research loop — math/physics track)

**DyME (CORROBORATED — research platform, covered Oct 2026).** Distributed
molecular-dynamics campaign engine: covers preparation, mutagenesis,
simulation, feature extraction, storage, and comparative exploration of up to
several thousand molecular systems in one platform. Pipeline: pdb4amber prep
for Amber file conventions, guided web wizard (solvation model, ionic
neutralization strategy, periodic boundary conditions, temperature, ensemble,
step size, equilibration/production lengths), anchor-point interfacial
residues with clustering enumerating singlet/doublet/triplet permutations,
and pre-launch GPU-hour budgeting. Decoder relevance: bulk MD is the
brute-force "what could happen" oracle — the Gauntlet's scenario runner at
thousand-fold scale rather than one specimen at a time.
Source: https://scienmag.com/dyme-a-new-engine-automates-thousands-of-protein-simulations-for-molecular-design/

**FFTM (CORROBORATED — SoftwareX 2026, Evstigneev, doi:10.1016/j.softx.2026.103110,
GPL-3).** Portable distributed three- and four-dimensional FFTs for
multi-GPU systems: vendor-agnostic (CUDA + HIP), automatically tuned,
real-to-complex and complex-to-real, dense Cartesian only. Ships reproducible
Docker capsules, checksum manifests, validation records. Already used in an
all-Fourier discretization project stabilizing relative periodic orbits in
turbulent flows; known limits: one MPI rank per GPU assumed, no sparse or
nonuniform transforms, NVSHMEM support planned. Decoder relevance: spectral
transforms are the core primitive for decomposing dynamics into modes —
this is the library you reach for when the Gauntlet needs coupled 3D/4D
spectral computation on the machines where the largest simulations run.
Source: https://scienmag.com/new-fft-library-pushes-four-dimensional-transforms-across-multi-gpu-supercomputers/

**Watch items (no 2026 milestone — not graded):** hotSpring (pure-Rust lattice
QCD / MD / fluids on commodity GPUs, AGPL-3.0); LJFusion (CUDA Lennard-Jones
MD, 10-100x claims); gumol-rs (Rust hybrid CPU/GPU MD for radiation damage /
space environments). Hobby-scale, kept on the bench.

## 10. New engine notes (2026-10-13 research loop — the LLM-guided symbolic-regression wave)

Five 2026 efforts converge on one architecture: the LLM stops guessing equations
and starts *guiding* a classical symbolic-regression engine (PySR, PySINDy) — as
search-space shaper, symmetry finder, or physics-knowledge scorer. The LLM is the
scout; the genetic programmer is the engine.

**InsightSR (CORROBORATED — arXiv:2608.25291, Aug 26, 2026).** LLM guiding layer
around PySR: Semantic Seed Pathway proposes dimensionally consistent functional
skeletons; Structural Feature Pathway recommends nonlinear feature
transformations; a feedback loop scores candidates and refines guidance.
Reported: 95% exact recovery on the Feynman benchmark, 80.18% on the
LLM-SRBench LSR-Transform task. Numbers author-reported, unreplicated.
Takeaway for us: shallow trees over rich, semantically informed features beat
deep trees over raw variables — structure the search space first.
Source: https://arxiv.org/abs/2608.25291

**EO-SR — Engineering-Oriented Symbolic Regression (CORROBORATED —
arXiv:2603.19241v1, Feb 2026).** LLM as "physics-informed agent" that zero-shot
synthesizes executable physical constraints (thermodynamic consistency, frame
indifference), turning the search from curve-fitting into physics-governed
discovery. Discovered a novel hybrid constitutive law (Mooney-Rivlin linear
base + rational locking term) for rubber-like materials: zero-shot pure-shear
prediction, unconditional convexity, FEM convergence under severe transverse
compression where the industry-standard Ogden N=3 fails on singularities.
The Gauntlet rule demonstrated: a discovered law earns its grade only when it
survives FEM/benchmark contact.
Source: https://arxiv.org/abs/2603.19241v1

**IdeaSearchFitter (CORROBORATED — arXiv:2510.08317, Jan 2026).** Semantic
search over an "interpretable ansatz space": the LLM proposes natural-language
rationales before symbolic forms ("explain-then-formalize"), constraining
candidates to physically plausible models. Reported on FSReD: 82.5% recovery
noise-free, 71.7% at high noise (gamma = 0.1), beating PySR and AI-Feynman.
Source: https://arxiv.org/pdf/2510.08317

**Symmetry-discovery agents (CLAIMED — via secondary review repo, 2026).** The
"Think-like-a-Scientist" / KeplerAgent pattern: train a tiny neural-net
surrogate, optimize an infinitesimal generator for the symmetry group (e.g.
2-D rotational symmetry), then run equivariant SINDy inside that subspace.
No first-party paper read this pass — parked as a claimed architecture until
we read the source.
Source: https://github.com/yuxuzhou-cn/review-for-symbolic-regression

**PiSR — LLM knowledge in the loss function (CORROBORATED — Scientific Reports,
2026, peer-reviewed).** An LLM physics-knowledge score (dimensional
consistency, simplicity, physical realism) folded into the SR loss as a soft
constraint; tested across three SR engines, three open LLMs, three physical
dynamics. Honest result from the authors: improvements real but non-uniform —
the LLM term is a configurable prior/regularizer, not a guaranteed win.
Source: https://www.nature.com/articles/s41598-026-35327-6

**Decoder relevance:** symbolic regression is the decoder pointed at physics —
recovering the hidden law from noisy observations is cryptanalysis with a lab
notebook. The "scout + engine" split mirrors the Gauntlet's own architecture
(models propose, the cage verifies with receipts). Any equation-discovery use
inside the Gauntlet must carry the same bar: benchmark or FEM contact before
the grade, never the paper's numbers alone.

## 11. New engine notes (2026-10-13 research loop, 10:30 EDT — math/physics track)

**SINDy field result: North Atlantic governing equations (CLAIMED — secondary
writeup, ~Oct 10 2026).** Sparse Identification of Nonlinear Dynamics trained on
AMV / NAO / precipitation-anomaly monthly indices from ERA5 (Jan 1950–Dec 2022,
12-month running average, 30-term constant/linear/quadratic library). LASSO
sparsity cut + 1,000-bootstrap ensemble → 344 candidate models; <13-term models
collapsed, blew up, or sat on rigid limit cycles; only 21+ term models showed
chaotic attractors matching observation. Pareto-selected 26-term model; 50,000-year
simulated trajectories reproduce the irregular Lorenz-like variability; validated
on held-out ERA20C 1900–1949. Shelf implication: the engine gets a field-scale
reference case — sparse identification + bootstrap robustness + Pareto selection
as the honest pipeline shape for recovering hidden laws from noisy time series.

**Hard static gain-sign constraints (CLAIMED — Neural Computing and Applications,
38(17) Art. 726, Oct 2026; paper not read this pass).** Impose hard constraints
on the *sign* of each input's static gain — no phenomenological model, no
penalty-weight tuning; covers shallow/deep, static/recurrent, ELM and
gradient-based training. Constrained gradient training was generally *cheaper*
than unconstrained. The authors' line for our honest ledger: "a validated model
with excellent metrics can still be qualitatively wrong" — the sign of causality
is the minimum bar of physical honesty. Shelf implication: a cheap
enforced-causality training gate, and another instance of the standing rule that
enforcement lives outside the model — same family as the output-filtering result
(§(k)) and the Anthropic permissions note (§(j)).

**SymbolicRegression.jl v2.5.0 (CORROBORATED — first-party release notes,
2026-09-28).** Performance release only (worker startup, allocation-free
tournament selection, hoisted mutation weights). No new technique; tool-shelf
version note.
Source: https://github.com/astroautomata/SymbolicRegression.jl/releases/tag/v2.5.0

## 12. New engine notes (2026-10-13 research loop, 16:57 EDT — math/physics track)

**The nine-loop run (CORROBORATED — Anthropic claim via secondary writeup, Sep 2026).** An agentic run ("Claude Science" harness) completed a nine-loop scattering amplitude in N=4 super-Yang-Mills using Python + SymPy instead of Maple/Mathematica. The run's own accounting: disciplined code execution, workflow tracking, and state management did the work — not "raw scientific intuition"; ~96 CPUs for a week (~$100 cloud) plus $1,000–$2,000 in model API tokens over several days. The writeup's honest limits: the problem had ideal bootstrap structure ("Sudoku-like" constraint elimination, uniquely suited to code execution and AI task loops); humans were already close — Song He (Chinese Academy of Sciences) independently derived the majority of the result days later with traditional methods and minimal AI; and the result does not imply competence on open-ended, messier theoretical-physics problems. Shelf implication: receipts-grade field evidence for this document's §5 architecture — LLM proposes, symbolic engine checks — with symbolic-exact tooling (not approximate numerics) as the correct pairing for exact-reasoning work. The harness was the instrument, not the model alone.
Source: https://lifeboat.com/blog/2026/09/claude-computes-a-nine-loop-amplitude-in-n4-super-yang-mills

**SymPy 1.15 dev notes (routine, non-material).** Upstream sparse-array migration (physics.quantum and lambdify now return SciPy sparse arrays instead of deprecated sparse matrices — flagged BREAKING) and a GSoC-added SkewNormal distribution in sympy.stats. Tool-shelf version notes only.

## 13. New engine notes (2026-10-14 research loop — math/physics track, third pass)

**SymbolicLM (CLAIMED — arXiv 2609.33594, v2 Sep 29, 2026; preprint, no independent replication read this pass).** Trains LLMs directly as symbolic regressors via numerical-symbolic and physical supervision; an inference-time refinement loop (SymbolicSGA) driven by quantitative feedback. PhysSymbArena: 160K+ equations, 1.8B tokens of numerical-symbolic data with physical descriptions; reported substantially better structural recovery with competitive numerical fitting. The auditability trade is the decoder-relevant point: this document's §5 architecture keeps the symbolic engine separate from the model so receipts stay inspectable; internalized regression is more powerful and less auditable. Standing position: the external-check loop is the default; internalized regression is watched, not adopted.
Source: https://arxiv.org/abs/2609.33594v1

**SciPy 1.18.1 (CORROBORATED — stable release Aug 21, 2026).** Working stack note: the verification trio's SciPy moves from 1.17.0; SymPy stable remains 1.14.0, 1.15 in development.
Source: https://en.wikipedia.org/wiki/ScientificPython

**SciExplorer — parked for next pass.** 2026 arXiv, "Agentic Exploration of Physics Models": an LLM agent autonomously completing the heuristic scientific cycle (experiment selection → result analysis → hypothesis generation) with general-purpose tools and minimal domain instructions. Paper not read this pass; candidate for the next math/physics pass.

## 14. New engine notes (2026-10-14 research loop — math/physics track, fourth pass)

**SciExplorer (CORROBORATED — Max Planck Institute for the Science of Light; arXiv 2509.24978; published in Physical Review X; open code; independently re-implemented).** An LLM agent with only general-purpose tools (code execution, plotting) autonomously completing the heuristic scientific cycle — observe, reason, experiment, analyze, repeat — on systems initially unknown to it: recovering equations of motion from observed dynamics and inferring Hamiltonians from expectation values across mechanical dynamics, wave evolution, and quantum many-body physics. No task-specific blueprints, no fine-tuning. The honest limits travel with the claim: strong on systems resembling its knowledge base, degraded on genuinely novel scenarios; named failure modes include premature commitment to wrong models and weak self-correction when fits go bad. Decoder lesson: the experiment-selection loop is the closest public architecture to an "interrogate the unknown" loop — and premature commitment is a named trap class. A discovering agent's chosen model is a hypothesis re-graded by fresh data, never a conclusion.
Source: https://arxiv.org/abs/2509.24978

**OpenAI's 10,000-agent Navier–Stokes campaign — campaign facts upgraded to CORROBORATED, proof correctness stays CLAIMED.** OpenAI's account: training began August 28, 2026 on an unreleased internal model; coordinating agents with a cached internet copy and code execution, organized into communicating groups. The Navier–Stokes existence-and-smoothness group ran on the order of 10,000 concurrent agents for about 88 hours (resolution September 5); the disproof variant — finite-time singularity — is what succeeded. Then about 17 hours of Lean formalization. The tally grew from 100+ claimed problems (September 21) to 372 result families across 722 manuscripts (October 6); The New York Times independently counted 377. **Three claimed solutions were withdrawn October 8–13 after errors were identified.** Credit dispute: independent mathematicians allege OpenAI leaned on their parallel work; OpenAI denies it and says it offered a joint release. Estimated compute cost in the millions of dollars; OpenAI says it will not claim the $1 million prize. The Clay Institute has awarded nothing — its rules require peer-reviewed publication, general acceptance, and a two-year clock that has not started. Decoder lesson: Lean formalization is a second, infallible machine re-grading the proof; the withdrawals are receipts that self-verification is biting; and the credit dispute is the provenance failure the doctrine watches — a swarm's history must be inspectable, not asserted.
Sources: https://evermx.com/case/openai-navier-stokes-millennium-proof ; https://tech-insider.org/openai-100-math-problems-solved-24-days-2026/ ; https://t-invariant.org/2026/09/the-millennium-puzzle-the-navier-stokes-equations-and-the-unsettling-september-of-2026/

**ai_quantummechanic opaque-keys pattern (CLAIMED — GitHub project README).** An LLM agent solving quantum mechanics problems through SymPy/SciPy tools; tool-computed expressions are stored behind opaque keys the LLM can't forge, and physics-aware checkers validate each answer before acceptance. The pattern is the find: the model can request computation but never sees or forges the raw expressions — the symbolic engine holds ground truth, the agent holds receipts. Anti-fabrication craft, publicly reusable.
Source: https://github.com/grzlz/ai_quantummechanic

**Decoder-design note (this run):** the same split keeps appearing — the discovering system must not grade itself. SciExplorer grades via fresh experiments; the OpenAI swarm grades via Lean; the opaque-keys project grades by never letting the grader hold the answers. Three surfaces, one doctrine: the evidence source and the claim source are never the same component.

## 15. New engine notes (2026-10-14 research loop — math/physics track, fifth pass)

**Section heading: the hypothesis generator never grades itself alone.**

- **EML symbolic regression — the NAND gate of continuous math [CLAIMED — repo first-party; arXiv:2603.21852 (Odrzywolek 2026) not read this pass].** One binary operator, `eml(a,b) = exp(a) − ln(b)`, provably generates all elementary functions. Grammar: `S -> x | 0 | 1 | c | eml(S, S)` — every expression is a binary tree of identical nodes. Hybrid exact-form pre-pass, then stratified tree search with gradient-free constant optimization. Reading: grammar minimalism is a fabrication control — the smallest complete grammar leaves the least room for hallucinated structure.
- **DoLQ — multi-agent ODE discovery [CLAIMED — secondary summary of arXiv:2605.07323, ICML 2026; paper not read this pass].** Sampler proposes equation structures, optimizer fits coefficients, LLM Scientist Agent evaluates each candidate on qualitative (domain knowledge, physical plausibility, constraints) AND quantitative (fit, error, complexity) criteria, synthesizing both into next-iteration guidance. Reading: the plausibility gate — a fit-only scorer cannot reject a physically absurd but numerically accurate equation.
- **RESTART — the self-auditing regression loop [CLAIMED — review-repo summary; ICLR 2026].** Runs the full hypothesis-experiment-analysis cycle inside symbolic regression: learns an exploration function modeling the signal the current hypothesis fails to explain, then converts it into targeted structural feedback rather than blind syntactic edits. Reading: self-audit as feedback — the loop grades what it missed, not just what it fit.
- **MuJoCo MCP server (sandraschi/mujoco-mcp) [CLAIMED — repo first-party].** MuJoCo physics behind MCP: load any MJCF model, control it, agent workflows; ships a solver comparison (MuJoCo vs Gazebo vs Isaac Sim/PhysX vs PyBullet). Reading: the physics shelf gains an agent-native tool surface — simulation as a tool an agent calls, not a library it imports.
- **Status note: MuJoCo Warp differentiability still pending [CLAIMED — repo README].** "Differentiability via Warp is not yet available" (issue #500). Watch item, not a capability.

- **KeplerAgent — physics-guided LLM agent coordinating equation discovery [CLAIMED — review-repo summary; underlying paper not read this pass].** The agent first runs physics structure-discovery tools (e.g. a symmetry-discovery tool identifying rotational symmetry), then configures the symbolic-regression backend around the findings — searching only the symmetry-respecting subspace. Reported higher accuracy and noise robustness than LLM and traditional baselines. Reading: structure before guessing — the hypothesis generator never grades itself alone, and now it doesn't even generate alone.
- **Symbolic regression + domain generalization for drug solubility [CORROBORATED — primary abstract read; Frontiers in Medicine, ~1 day old].** Invariant-risk and domain-adversarial techniques force discovered closed-form equations to hold across unseen chemical domains. Reading: invariance as the anti-fabrication gate — fitted-but-non-invariant is a fabrication in a lab coat.
- **Status note: MuJoCo Warp differentiability still pending — re-confirmed [CLAIMED — project README].** Still "not yet available" (issue #500). The lane's differentiable-simulator gap is unchanged; watch item.

## 16. New engine notes (2026-10-15 research loop — math/physics track, sixth pass)

- **SymCode — neurosymbolic math reasoning with SymPy as the verifier (CLAIMED — arXiv:2510.25975, Jan 2026).** Reframes LLM math problem-solving as verifiable *code generation* against the SymPy library: the model emits SymPy calls and execution verifies deterministically. Reported +13.6 percentage points over baselines on MATH-500 and OlympiadBench. Significance for the library: the symbolic engine holds ground truth and the agent holds receipts — an agent that must produce checkable work, not persuasive prose, is one whose errors are catchable.
- **openCFS 2026S (CORROBORATED — trade-press writeup of the release; ~8,857 commits).** Open-source multiphysics package: electromagnetics, vibro/aero-acoustics, compressible and viscous flow, nonlinear anisotropic structural mechanics, heat conduction, coupled iteratively or monolithically, configured through schema-validated XML. Extends the physics surface an interrogation cage can draw on without licensing anything.
- **COMSOL Multiphysics 2027 — commercial shelf goes agent-native (CORROBORATED — company press release, Sep 16, 2026; release scheduled "later this fall").** Adds COMSOL Systems, a time-periodic solver, an Electric Motor Module — and a COMSOL MCP Server for direct interaction with external AI agents. Commercial solvers are sprouting agent tool surfaces; watch for the actual capability surface once it ships.
- **Symbolic regression with partial parameter sharing (CLAIMED — arXiv:2601.04051, v3 Jun 2026).** Extends multi-dataset SR to intermediate sharing levels under multiple categorical variables — fewer parameters, plus structure information about which parameters genuinely transfer across regimes. Directional, early.
- **Parked (CLAIMED, vendor-first):** NVIDIA cuPotential (SEMICON West 2026) — CUDA-X library for molecular-dynamics non-bonded interactions; vendor benchmark only, early access Q4 2026. Revisit when the number is reproducible outside the vendor's lab.
- **Community MLX/Metal engine for mujoco_warp (lucidrains/mujoco_warp) [CORROBORATED — project README read this pass; benchmarks author-reported].** A community-built Apple-silicon backend for MuJoCo Warp: implements the rigid-body pipeline on Metal via MLX, running thousands of worlds in one process with the dynamics and solver fused into two Metal kernels. Bounded scope (hinge/slide/free joints, primitive geoms, Euler integrator). Author-reported: 132,826 worlds per second at 4096 worlds on an Apple M1 Pro; validated against the warp CPU backend to float32 noise. Not DeepMind-official, and the standing watch item is untouched: differentiability via Warp remains unavailable — batch width is not gradient flow. A community physics engine is foreign code first: vet before trust.
- **Math MCP server (codeprimate/math-mcp) [CLAIMED — repo first-party].** 26 SymPy/SciPy tools behind an MCP surface for coding assistants — equations as tool calls at arm's length, the same agent-native shape as the MuJoCo and COMSOL entries.

## 17. New engine notes (2026-10-16 research loop — math/physics track, seventh pass)

- **Gradients through cell-biology models (CORROBORATED — first-party release notes).** A systems-biology tool compiles models into JAX code, so the full simulation — events included — is differentiable, batched, and compiled. Significance: gradient-through-trajectories reaches the biology shelf.
- **Differentiable fluid simulation for porous media (CORROBORATED — peer-reviewed journal, 2026).** Lattice Boltzmann library for multiphase flow in porous materials, scaling from CPUs to distributed GPU setups. Significance: another honest instrument on the differentiable shelf.
- **Differentiable neuron fitting, agent-documented (CORROBORATED — published paper; skill repo first-party).** A neuron simulator's new skill walks an AI agent through the whole gradient-based fitting pipeline, scripts and tests included. Significance: the physics surface and the tool-use surface meet.
- **A generalist differentiable physics engine (CLAIMED — public repo).** One new project covers classical mechanics, electromagnetism, quantum, fluids, optics, and statistical mechanics with autodiff throughout. Significance: long-awaited, young — vet before trust.
- **Differentiable spectroscopy tools (CLAIMED — public repos).** Gradients through spin-resonance, mass-spec, and energy-transfer measurements, verified against textbook predictions. Significance: the inverse-problem primitive, packaged.
- **Differentiable fusion-plasma transport (CORROBORATED — published paper).** Tokamak core-transport simulator with autodiff and ML-surrogate coupling, verified against the reference code. Significance: fusion plasma joins the fleet.
- **The symbolic engines get stricter (CORROBORATED — development records).** Sparse-matrix deprecation migration, a new special-function printer hook, and — most welcome — an inequality solver that stops silently canceling singularities. Significance: the verifier keeps getting more honest.
- **Standing watch item, unchanged:** MuJoCo Warp differentiability is still pending. None of this pass's new engines close it.


## 18. New engine notes (2026-10-16 research loop — math and physics track, eighth pass)

- **Approximate matrix exponential solver (CORROBORATED — peer-reviewed paper; reported secondhand).** A new numerical method for ion-channel kinetics, fastest in benchmarks against the classic solvers, fast enough on a flagship GPU to simulate hundreds of thousands of channel instances in real time. Released as an open-source package integrated into the standard neuron simulator, with the exact solution added beside it as a verification reference. Significance: the ion-channel primitive gets a benchmarked fast path with receipts.
- **Hard sign constraints for physics-informed networks (CORROBORATED — peer-reviewed journal; reported secondhand).** Neural networks forced to respect the known direction of each input's causal push — no governing equations, no penalty tuning. Constrained training ran cheaper than the unconstrained version. Significance: the physical-honesty minimum — a model can score beautifully and still be causally wrong; the sign check is a cheap pre-gate.
- **Parked:** a pre-seed startup's thousand-fold speedup claim for photonic-circuit simulation — announcement only, no receipts.


## 19. New engine notes (2026-10-16 research loop — math and physics track, ninth pass)

- **CERN and Mistral's "Flare" physics foundation model (CORROBORATED — Reuters reporting on the signed statement of intent).** A planned first foundation model for collider physics, trained on billions of simulated particle collisions rather than text, with the goal of replacing some specialized particle-reconstruction algorithms. CERN holds roughly an exabyte of collider data; no budget or timetable disclosed. Significance: the decoder shape goes institutional — raw detector data in, reconstructed physics out — with a stated commitment to share the capabilities. Open watch: whether Flare ships, and whether it actually displaces the hand-built reconstruction stack.
- **Tipping-point forecasting with recurrent neural operators (CORROBORATED — preprint abstract and revision history checked; headline result via a secondary outlet).** A neural operator learns chaotic dynamics from pre-tipping data alone; a conformal-prediction framework forecasts tipping points by watching the model's own deviations from physics constraints. Demonstrated on chaotic benchmark dynamics, a climate tipping point, and airfoil stall. Significance: the violated-constraint-as-signal primitive — the instrument forecasts when the rules break, not what the rules say — a qualitative forecasting method worth keeping on the engine shelf.
- **Re-covered, no change:** SymPy/SciPy releases; the LLM-guided symbolic-regression wave; MuJoCo Warp differentiability still pending; the photonic-circuit simulation startup claim remains parked.

## 20. New engine notes (2026-10-17 research loop — math and physics track, tenth pass)

- **PhySimCode — measuring the video-to-simulation gap (CLAIMED — research digest, October 17, 2026; paper published October 16).** A new benchmark pairs six thousand procedurally generated physics simulation videos — spanning one hundred sixty-two phenomena, from rigid bodies and fluids to contact-rich dynamics, rendered with scientific-Python simulations and a physics engine — with their underlying code, parameters, and reasoning explanations. Ten multimodal AI systems were asked to watch a video and write a runnable simulation reproducing it: the best recovered only seven point seven percent of the ground-truth physics parameters. Significance: models can state physics laws fluently but rarely infer them from observation — the instrument prices exactly that gap. Filed as the standing video-physics instrument; the headline figure still awaits confirmation from the paper itself.
- **TheoPhysEval — testing AI agents on research-level physics, with a memorization control (CLAIMED — digest, October 15, 2026; preprint posted October 9).** Fifty unpublished research-level theoretical physics problems, each with a verifiable answer and solvable by a human expert in about a day, tested on off-the-shelf AI agents. The best system scored ninety-eight percent at under three dollars per problem — but the score barely changed when the agents were denied web search and background reading, which the authors read as significant memorization of the literature. The tasks plus an isolated no-internet track are published as an open dataset. Significance: the no-internet control is what separates a measure of memory from a measure of reasoning — physics-AI scores cited without that control are suspect.
- **Re-covered, no change:** the scientific-Python releases; the physics-foundation-model announcement; the tipping-point forecasting research; the LLM-guided symbolic-regression wave; a podcast-episode claim about GPU physics learning (no paper — parked); an independent assessment brief on computer-algebra evidence (single outlet — parked).

## 21. New engine notes (2026-10-18 research loop — math and physics track, eleventh pass)

- **LASR — symbolic regression with a learned concept library (CLAIMED — research-summary service, 2026-10-18; paper from 2024).** An AI-assisted equation-discovery method that builds a library of concepts from good and bad candidate expressions found during search, guiding a classical genetic search engine underneath. On a benchmark of one hundred physics equations from the Feynman lectures, it recovered about fifty-five percent exactly, versus about forty percent for the unguided baseline — with the advantage largest in early iterations. A revealing detail: feeding the model physically meaningful variable names mattered; stripping them dropped the score to about forty-eight percent — the names carry physics priors. Significance: a mechanism paper for why language helps math-discovery (units and dimensions as compressed prior knowledge). Caveat: the benchmark uses known-answer problems; performance on genuinely unknown equations is the open question.
- **SymTorch — turning neural networks into readable equations (CLAIMED — trade-press writeup, October 2026; library not examined first-party this pass).** An open library that traces a trained network's activations, fits symbolic expressions to them, and swaps neural blocks for the discovered equations — trading black-box behavior for checkable formulas, with an accuracy-versus-simplicity dial. Claimed: ninety-two percent of distilled equations match the neural network's accuracy within one percent; demonstrations include recovering inverse-square laws. Significance: this is the "black box to formula" instrument — compressing a learned behavior into an equation you can inspect, which is the shape honest agent report cards want. Filed as a candidate instrument; it needs independent replication before the grade rises.
- **A canonical rediscovery receipt (CLAIMED — research-summary service, 2026-10-18; paper from 2022).** A hybrid of graph neural network plus symbolic regression, trained only on planetary motion data, rediscovered Newton's law of gravitation among over one hundred million candidate expressions — and the recovered law predicted long-term orbits better than the raw neural network that proposed it. Inferred planet masses matched truth within about nine percent on average, with accuracy tracking how strongly each body tugs on the others. Significance: a clean receipt that a correct physical principle beats a complex black box — the decoder project's standing thesis in one experiment.
- **Re-covered, no change:** the scientific-Python releases; the physics-foundation-model announcement; the tipping-point forecasting research; the orbital-mechanics wave; the video-physics gap benchmark; the theoretical-physics agent benchmark with its memorization control.


## 22. New engine notes (2026-10-18 research loop — math and physics track, twelfth pass)

- **A physics-constrained design engine with a materials receipt (CORROBORATED — physics research journal via science coverage, 2026-10-17; new to record).** A Hong Kong research team describes a machine-learning framework built around a causal graph that mirrors how a composite material really works: tiny-scale composition feeds into the interfaces between phases, those shape the connected networks across the material, and those dictate the final properties like heat conduction and electrical resistance. Physical laws are enforced at every link of that chain, rather than hoped-for from data — and the system is paired with an evolutionary optimizer to search the best trade-offs between conflicting goals. The physical receipt: a graphite-and-wax composite for cooling high-power electronics, where the framework's guidance led the team to insert an ultrathin alumina layer between fibers and wax — a layer that lets heat vibrations pass while blocking electric current, achieving simultaneous gains in thermal conduction and electrical resistance that designers had long treated as mutually exclusive. The loop closes: model to synthesis to measured material, refining against reality.
- **Why it matters to the decoder:** the architecture is the message — constraints built into a model's structure beat constraints merely learned from data, the same philosophy the project uses for enforced behavioral gates. And the discipline of closing the loop against physical reality, rather than against training data, is the receipts doctrine in materials form. Filed as the lane's causal-architecture reference: when a physics-informed method claims to be constrained rather than hoping, this is the worked example — causal skeleton, enforced physical laws at every link, optimizer on top, and a real synthesized material as the receipt.
- **Re-covered, no change:** the qualitative-causality training gate; the tipping-point forecasting research; the scientific-Python releases (stable versions, next major in development); the stoichiometry-constrained symbolic regression work; the space-physics formula-discovery research; the video-physics gap benchmark; the theoretical-physics agent benchmark with its memorization control.


## 23. New engine notes (2026-10-18 research loop — math and physics track, thirteenth pass)

- **Symbolic-KAN — a neural network designed to resolve into equations (CLAIMED — new to record; evidence is indexed search text from a paper-digest site whose domain is now offline, verified unreachable by a direct browser check; the underlying paper was not read first-party).** Per the indexed summary: the network represents multivariate functions as compositions of learned single-variable building blocks, guided by a library of standard mathematical primitives, and a training mechanism that sharpens each active unit down to one chosen primitive and direction — so the trained model reads out as compact closed-form formulas instead of an opaque network. The claimed extension covers physics-informed learning of partial differential equations, where the chosen primitives mirror the equations' real structure. Significance: a second "black box to formula" instrument beside SymTorch — where SymTorch distills a trained network afterward, this one is designed to grow into symbols from the start. Both end at inspectable equations, the shape honest agent report cards want. Filed as a candidate instrument; the claims need a reachable primary before the grade rises.
- **Re-covered, no change:** the scientific-Python releases (stable versions, next majors in development); the earlier neural-guided symbolic-regression wave; the space-physics formula-discovery research; the physics-constrained composite-design engine (last pass); the qualitative-causality training gate; the tipping-point forecasting research; the video-physics gap benchmark; the theoretical-physics agent benchmark with its memorization control; the physics-foundation-model announcement. **Parked:** tutorial-farm SEO pages restating January-2026 library history; the offline digest site itself, until a primary or live copy is reachable.


## 24. New engine notes (2026-10-18 research loop — math and physics track, fourteenth pass)

- **Physics-labeled prompts for simulator calibration (CLAIMED — new to record; research digest, October 2026; the underlying study was not read first-party).** A new study gave a language model plain-language descriptions of what was going wrong in a physics simulation and asked it to fix the parameters, then pitted it against standard optimizers — plus four stripped-down prompt versions to isolate what the physics framing actually contributes. Per the digest: the physics-informed first proposal improved the initial design in twenty-three of twenty-five trials, and after five evaluations the median calibration error sat nearly twenty-two times below the physics-free controls. The study's honest question is how long the semantic advantage lasts before conventional methods catch up. Significance: the inverse of the video-gap benchmark already on file — where that prices the agent that can't infer physics from observation, this prices the agent that can spend physics-language knowledge to calibrate a simulator in fewer expensive runs. Filed as a candidate instrument; the headline figures still await confirmation from the paper itself.
- **Re-covered, no change:** the scientific-Python releases (stable versions, next majors in development); a peer-reviewed physics-informed magnetometry paper (application, method already on file); the physics-foundation-model announcement; the tipping-point forecasting research; the physics-constrained composite-design engine; the qualitative-causality training gate; the neural-guided symbolic-regression wave; the video-physics gap benchmark; the theoretical-physics agent benchmark with its memorization control. **Parked:** tutorial-farm pages restating old library history; a single-outlet computer-algebra assessment brief (still uncorroborated).


## 25. New engine notes (2026-10-19 research loop — math/physics track, fifteenth pass)

- **Siemens x NVIDIA cuLitho in Calibre — 12x faster full-chip OPC [CLAIMED — NEW TO RECORD; announced Oct 14, 2026; vendor claims].** Siemens announced integration of NVIDIA's cuLitho library into Calibre manufacturing software, reporting up to 12x faster full-chip optical proximity correction workloads. The problem: at shrinking feature sizes, diffraction and other physical effects distort the projected image, so masks must be pre-compensated (predict the distortion, warp the mask) — increasingly brutal at the High-NA EUV transition; inverse lithography (ILT) and curvilinear OPC are the named workloads. NVIDIA frames the library as electromagnetic physics + photochemistry + computational geometry + iterative optimization on GPU. Source: https://semiwiki.com/eda/siemens-eda/374917-siemens-and-nvidia-accelerate-lithography-for-next-generation-ai-chips/
- **Decoder/Gauntlet reading:** the lane's physics-simulation-library advance — four physics domains in one accelerated library, with an industrial-scale receipt (12x on full-chip workloads, if the claim holds). The "simulate the physics before building" instrument keeps gaining teeth: computational lithography is exactly the shape the decoder's own future physics shelf wants — physics-forward, instrument-grade, receipts from manufacturing. Filed as candidate instrument; watch for independent benchmarks before it moves past CLAIMED.
- **Parked/re-covered:** SciPy 1.18.1 stable, no 1.19 in window; SymPy 1.14.0 stable, 1.15 in dev; FrankenSymPy brief (recrawl, still single obscure outlet, bus factor 1 — parked); MuJoCo Warp differentiability still pending (issue #500); PhySimCode 7.7% gap; TheoPhysEval memorization control; RNO tipping-point forecasting; PHICS causal-architecture reference (section 22); Symbolic-KAN (section 23); physics-labeled prompts (section 24); CERN/Mistral "Large Physics Model" statement of intent (the on-record "Flare" partnership; language-model lane); copyprogramming.com SEO tutorial farms (no new facts).
