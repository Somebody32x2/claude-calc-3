# Calc 3 · Field Labs

### ▶ [Open the labs](https://raw.githack.com/Somebody32x2/claude-calc-3/main/index.html)

Interactive lessons for the core ideas of Calculus III, each one a single
self-contained HTML file. Fewer lessons, each finished — polish over quantity.

## The labs

| | Lab | Live |
|---|---|---|
| 01 | Partial derivatives — slice curves, tangent lines, contour map, gradient arrow | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/partial-derivatives-lab_1.html) |
| 02 | Double integrals — Riemann columns, Fubini's sweeping blade, Type I/II regions | [open](https://raw.githack.com/Somebody32x2/claude-calc-3/main/double-integrals-lab_2.html) |

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
