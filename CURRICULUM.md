# Calc 3 · Field Labs — Curriculum Plan

**Format.** One self-contained HTML file per lesson. No build step, no external JS.
Fonts from Google, everything else inline. Each lab renders with hand-rolled canvas
2D/3D so there is no library drift between lessons.

**Principle.** Fewer lessons, each finished. A lesson ships when its central idea has a
manipulable object that makes the idea *feel* obvious before any notation appears.

## House rules (established by Lab 01)

| Rule | Detail |
|---|---|
| Exact math | Every readout comes from a closed-form expression, never a finite difference. Numeric approximations are shown *only* when approximation is the lesson's subject (e.g. Riemann sums), and always beside the exact value. |
| Palette | `--x` coral = the x-direction. `--y` teal = the y-direction. `--grad` gold = the derived/answer quantity (gradient, volume, flux). Terrain ramp for heights. |
| Structure | Hero → three-card "the whole idea" → interactive lab → collapse-to-Calc-1 section → a second view of the same object → compute-by-hand worked examples → "where this goes next". |
| Interaction | Drag to orbit, scroll/pinch to zoom, sliders for position, toggles for layers. All state changes re-render synchronously; heavy work is `requestAnimationFrame`-throttled. |
| Failure | Whole script wrapped in try/catch feeding a visible `#errbar`. A broken lab must say so rather than render blank. |
| A11y | Real `<button>`/`<input>` elements, `aria-pressed`, visible focus rings, reduced-motion respected, 920px single-column breakpoint. |

## Sequence

### Track A — Differential (the local picture)

**01 · Partial derivatives** ✅ *shipped*
Freeze one variable, read the slope. Slice curves, tangent lines, cutting planes,
contour map with the gradient arrow.

**02 · Double integrals** ✅ *this lesson*
Deliberately placed second, not third. Partials answered "how does the surface
change *here*"; integration answers "how much surface is there *in total*" — the
opposite question, so it lands better as a contrast than as a continuation. It also
needs nothing from Track A beyond reading `f(x,y)`, which keeps the two tracks
independent for a reader who jumps around.
Riemann columns converging, Fubini's sweeping slab, Type I/II regions.

**03 · Directional derivatives & the gradient**
Any compass heading, not just the two axes. `D_u f = ∇f · u` as a dot product;
the cosine dial; why the gradient is the maximizer; level curves are exactly the
directions where the dot product vanishes. *Builds directly on 01 and reuses its
contour renderer.*

**04 · Tangent planes & linearization**
The plane through a point with the two partial slopes as its tilt. Zoom in until
surface and plane are indistinguishable — local linearity is the whole of
differentiability. Error surface `f − L` shown separately so the second-order
gap is visible.

**05 · Optimization: critical points & the second-derivative test**
Where both partials vanish, and why that isn't enough. The Hessian discriminant
as a classifier, demonstrated on the bowl / saddle / monkey-saddle already built
in Lab 01. Constrained optimization (Lagrange) as the closing act: the level
curve tangent to the constraint curve.

### Track B — Integral (the accumulated picture)

**06 · Polar double integrals & change of variables**
Why `dA = r dr dθ`. The Jacobian shown as the literal area-stretch factor of a
distorted grid — animate the map from `(u,v)` space to `(x,y)` space and watch
cell areas change.

**07 · Triple integrals, cylindrical & spherical**
Same slicing logic one dimension up. Solid region + sweeping cross-sectional
plane; coordinate system chosen by the symmetry of the solid.

**08 · Vector fields & line integrals**
Field visualization, a particle dragged along a path, `∫ F · dr` accumulating in
real time on a running-total gauge. Conservative vs. non-conservative shown by
walking two paths between the same endpoints.

**09 · Green's, Stokes' & the Divergence theorem**
The capstone. Circulation around a boundary = curl summed over the interior;
flux through a surface = divergence summed over the volume. Built as one
"shrink the loop / subdivide the region" visual reused at all three scales, so
the three theorems read as one theorem.

## Supporting work (not lessons)

- `index.html` — landing grid of lesson cards with progress state in `localStorage`.
- Shared `lab.css` / `lab.js` extraction — **deferred on purpose.** Duplicating the
  render core is cheap; a premature shared runtime would couple lessons that still
  need to diverge. Revisit after Lab 04, when three labs have proven what is
  genuinely common.
