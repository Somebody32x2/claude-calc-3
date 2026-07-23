# Calc 3 · Field Labs

### ▶ [Open the labs](https://raw.githack.com/Somebody32x2/claude-calc-3/main/index.html)

Interactive lessons for the core ideas of Calculus III, each one a single
self-contained HTML file. Fewer lessons, each finished — polish over quantity.

## The labs

| | Lab | Live |
|---|---|---|
| 01 | Partial derivatives — slice curves, tangent lines, contour map, gradient arrow | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/partial-derivatives-lab_1.html) |
| 02 | Double integrals — Riemann columns, Fubini's sweeping blade, Type I/II regions | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/double-integrals-lab_2.html) |
| 03 | Directional derivatives — rotating cut plane, the circle of slopes, level-curve perpendicularity | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/directional-derivatives-lab_3.html) |
| 04 | Tangent planes & linearization — zoom to local flatness, quadratic error, the differential | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/tangent-planes-lab_4.html) |
| 05 | Hills, valleys & saddles — ∇f = 0, the discriminant test, the Hessian, Lagrange multipliers | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/optimization-lab_5.html) |
| 06 | Polar coordinates & the Jacobian — why dA = r dr dθ, area-stretch, the Gaussian integral | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/polar-integrals-lab_6.html) |
| 07 | Triple integrals — slicing solids, cylindrical cells, and where ρ² sin φ comes from | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/triple-integrals-lab_7.html) |
| 08 | Vector fields & line integrals — work, path dependence, conservative fields, potentials | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/line-integrals-lab_8.html) |
| 09 | Green's theorem — circulation & flux forms, curl and divergence, why the interior cancels | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/greens-theorem-lab_9.html) |
| 10 | Divergence & Stokes — flux through surfaces, and why the surface doesn't matter | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/divergence-stokes-lab_10.html) |

The sequence follows the arc of [MIT 18.02 (OCW)](https://ocw.mit.edu/courses/18-02sc-multivariable-calculus-fall-2010/) —
partial derivatives → multiple integrals → vector fields → the integral theorems.

Every lab ends with a **Common misconceptions** section — the specific wrong ideas that feel
reasonable and quietly break things later (the gradient does *not* live on the surface;
existing partials do *not* imply differentiability; `D = 0` is *not* a verdict; extrema can
sit on a boundary where `∇f ≠ 0`).

See [CURRICULUM.md](CURRICULUM.md) for the full nine-lab plan and the house rules
every lab is built to.

## How they're built

No build step, no framework, no dependencies. Each lab is one HTML file with
inline CSS and JS; the only external request is the Google Fonts stylesheet.
The 3-D views are hand-rolled canvas rendering — projection, painter's algorithm,
back-face culling and Lambert shading — so there is no library drift between
lessons.

**Every value on screen comes from a closed form.** Slopes are analytic partials,
not finite differences; volumes come from antiderivatives worked out in advance.
The only approximations are the ones a lesson is deliberately *about* (Riemann
sums), and those are always shown beside the exact answer.

## Running locally

Open any `.html` file directly in a browser. There is nothing to install.

## A note on the links

These point at [raw.githack.com](https://raw.githack.com), which proxies GitHub's
raw file endpoint with a real `text/html` content type — `raw.githubusercontent.com`
alone serves HTML as plain text and shows source instead of rendering it. The
`main` URLs above are intentionally uncached, so a push shows up immediately.
