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
for the "real physics PDEs" that §1's honesty line names.
