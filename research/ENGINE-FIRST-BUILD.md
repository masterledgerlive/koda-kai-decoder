# Koda Kai Decoder — Math Engine: First Build
Seeded 2026-10-12 by the decoder-create-loop. MIT. [CONJECTURE — "the registry
is production-grade for Gauntlet use" is untested; what follows is a working
seed with real, verified test output.]

## What was built
`engine/equation_registry.py` — a sympy-based equation registry the Gauntlet
can call, exact-then-numeric, with error bounds and assumption receipts.

Every `evaluate(name, **inputs)` returns a **receipt dict**, never a bare
number: equation name, grade (VERIFIED/CORROBORATED/CLAIMED/SPECULATION),
assumptions, closed-form solution, substitutions, result, uncertainty sigma,
notes, warnings, timestamp.

Rules it enforces on itself:
- Uncertainty propagates first-order from `(value, sigma)` inputs. No input
  uncertainties → explicit warning: point estimate only, no confidence
  interval — "this is not a prediction, it's a calculation."
- No closed form → says so, returns `None`, fakes nothing.
- Underdetermined → names the missing symbols, returns `None`.
- Unknown equation → raises, never silently defaults.

## Canonical equation set
All registered equations are textbook-canonical, graded VERIFIED **as math**.
Applying any of them to a real specimen is a separate claim the registry never
conflates: `projectile_range`, `time_dilation` (special relativity — the
physics behind time-dilated guest clocks), `kinetic_energy`, `ideal_gas`,
`beta_binomial_posterior_mean` (the belief engine; the receipt names the prior
because prior choice is judgment, not data), `shannon_entropy`.

## Real test results (sympy 1.12, genuine computed output)
| Equation | Inputs | Result |
|---|---|---|
| projectile_range | v=25 m/s, 45°, g=9.81 | 63.7105 m |
| time_dilation | v=0.5c, t=1 s | 1.15470 ± 0.00257 (matches 1/√(1−0.25) exactly) |
| kinetic_energy | m=1000 kg, v=30±0.5 m/s | 450000 ± 15000 J |
| ideal_gas | 1 mol, 273.15 K, 22.4 L | 101382.55 Pa |
| beta_binomial_posterior_mean | Beta(2,2) prior, 7/10 | 0.642857 |
| shannon_entropy | p=[0.5, 0.25, 0.125, 0.125] | 1.75 bits |

These are real evaluations, not fixtures. Regression checks also verified:
underdetermined inputs return `None` (not a fake number), and unknown
equations raise.

## What it is not
Not a verdict engine (statistical evidence only — never intent). Not a PDE
solver. Not a symbolic-regression discovery tool.

## Second build: the numeric root-finding path (2026-10-12)
`numeric_solve(name, unknown, bracket, tol, max_iter, **inputs)` via
`scipy.optimize.brentq` (bracketed, hybrid bisection/secant). The bracket
must straddle a sign change or it raises — the registry never extrapolates
a root. Every receipt reports method, bracket, function-eval count, and
residual |f(root)| vs tolerance; a converged root with a bad residual is
reported as CONJECTURE, not a receipt. Sigma propagates by central finite
differences; an unstable derivative withholds sigma, never guesses.

Demonstrator: **Kepler's equation** (E − e·sin E = M, provably no elementary
closed form — the first step of any real orbit calculation). Real output
(scipy 1.11.4): E = 1.4987011335178482 rad for ecc=0.5, M=1.0
(residual 1.1e-16 vs tol 1e-10); ecc=(0.5, 0.01) → σ(E) = 0.010347 —
matches the analytic sensitivity to 4 sig figs, an independent cross-check.

## Third build: the ODE integration path (2026-10-12)
`numeric_solve_ode(name, t_span, y0, ...)` via `scipy.integrate.solve_ivp`
(RK45 default), with an `ODESystem` registry parallel to the equation
registry. Failed integrations raise — never a fake trajectory. Registered
analytic solutions are cross-checked on a 200-point grid with the max
absolute error reported in the receipt; nfev ≥ 50,000 earns a "maybe stiff"
warning suggesting Radau/BDF. Uncertain params propagate to the endpoint
by finite-difference re-integration.

Honest proof it works: the cross-check caught a real bug on its first run —
the registry's own underdamped velocity formula had swapped coefficients
(grid max error 7.49). Fixed and re-verified to 3.07e-9 on the same grid.

Demonstrators: `damped_oscillator` (ζ=0.10±0.005, ω₀=2π, 5 s integration:
endpoint (0.04199810, 0.04279561), endpoint σ=(0.00681, 0.00245)) and
`projectile_drag` (quadratic drag, no closed form: 4.204 m range at 25 m/s
@ 45°, strictly below the 63.7105 m vacuum closed-form upper bound —
the physical bound check passes). All genuine computed results on the
build machine, not fixtures.
