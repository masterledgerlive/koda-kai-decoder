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
- **Score the reasoning, not just the number (EQMs, arXiv:2606.30987, pre-registered):** sixty LLM-scored reasoning patterns extracted from forecasters' written rationales predict tournament accuracy across 55,000+ forecast-rationale pairs, beating pre-LLM text methods, transferring to an independent study — and flagging underperformers asymmetrically better than it crowns winners. Cross-ref: DECODERS.md §(g). [CORROBORATED — pre-registered, large-N; peer review unconfirmed]
- **The Gauntlet rule:** every prediction ships with its assumptions, its data, and its error bars. Prediction without a confidence interval is not decoding — it's guessing.

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
