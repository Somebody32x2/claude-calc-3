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
| Misconceptions | Every lab closes with a **Common misconceptions** section before the footer: a myth/reality grid naming the specific wrong ideas that feel reasonable. These are chosen for being *load-bearing* — each one, believed, produces confidently wrong work later. Written as "✕ the myth / ✓ actually", never as a list of rules. |
| Honest instruments | When a demo shows an exact quantity next to an approximation, the gap must be *explained on screen*, not left as an unremarked mismatch (see Lab 07's exact ÷ formula ratio). A visible unexplained discrepancy reads as a bug in the lab. Where two sides of a theorem are compared numerically, the tolerance is **relative**, and the residual is labelled as discretisation rather than disagreement. |
| Worked by hand | Every lab carries at least one `.byhand` block: a numbered, fully-substituted computation with the actual numbers — gradients evaluated at a point, dot products multiplied out, integrals with limits plugged in. No step elided with "similarly". Where a classic trap exists (forgetting to normalise, forgetting the `r`), the block *computes the wrong answer too* and shows how far off it lands. |
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

**03 · Directional derivatives & the gradient** ✅ *shipped*
Any compass heading, not just the two axes. `D_u f = ∇f · u` as a dot product;
the cosine law; why the gradient is the maximizer; level curves are exactly the
directions where the dot product vanishes. Reuses Lab 01's six surfaces verbatim —
same terrain, new question — so the generalisation from two axis slices to a freely
rotating cut plane is felt rather than asserted. The compass rose (every direction's
slope laid along its own heading, tips tracing a circle whose diameter is ∇f) is the
lesson's centrepiece. Adds marching squares for the single level curve through the
current point.

**04 · Tangent planes & linearization** ✅ *shipped*
The plane through a point with the two partial slopes as its tilt. A zoom window
with a fixed-tilt plane and a peeling surface makes "differentiable = locally
linear" literally watchable; the signed-error colouring and a diagonal error-slice
show the gap collapsing as the square of the window. Closes with the differential
`dz = fx dx + fy dy` as an estimation tool. Verified: partials exact, and the
max error falls ~16× per 4× zoom on every surface.

**05 · Optimization: critical points & the second-derivative test** ✅ *shipped*
Where both partials vanish, and why that isn't enough. A gradient vector field
where the arrows die at the critical points; the Hessian discriminant
`D = fxx fyy − fxy²` with the eigenvalues it stands for; a live local-shape panel
(ellipse vs hyperbola) with the Hessian's eigen-axes. Features `x³−3x+y³−3y`, which
carries a min, a max, and two saddles at once. Lagrange multipliers close it as an
interactive: a point walking a constraint circle, extremal exactly where ∇f ∥ ∇g.
Every one of the eleven critical points verified against a 48-direction numerical
probe. *(Fixed in build: a HiDPI `putImageData` bug that left the heatmap panels
painting only a corner.)*

### Track B — Integral (the accumulated picture)

**06 · Polar double integrals & change of variables** ✅ *shipped*
Why `dA = r dr dθ`. The polar grid with a movable tile that visibly grows with r;
the single sector whose exact area `½[(r+dr)²−r²]dθ` limits to `r dr dθ`; the
Jacobian shown as a measured area ratio between a uniform `(r,θ)` grid and its
warped `(x,y)` image (the ratio lands on the mid-radius = |J| = r); and a polar
Riemann sum over a disk with a "without the r" row that goes visibly wrong.
Verified: sector gap = ½dr/r exactly, area ratio = r to four places, and all disk
integrals converge to their closed forms. *(Design note: the disk radius and
integrand set were chosen to avoid the R = 2 coincidence where a constant
integrand's wrong-sum accidentally equals the right answer.)*

**07 · Triple integrals, cylindrical & spherical** ✅ *shipped*
Same slicing logic one dimension up, and deliberately framed that way — the
sweeping blade is the Lab 02 move re-run on a solid, so the section opens by
pointing back at it. Solids of revolution let the slice be a disk with an exact
`A(z)`, so the running volume is honest. The centrepiece is the `ρ² sin φ`
derivation: a spherical box has edges `dρ`, `ρ dφ`, and `ρ sin φ dθ`, and the
lab draws the line of latitude whose radius *is* that third factor — slide φ
toward a pole and watch it collapse. Verified: all four solids' slice integrals
match their closed forms, the cylindrical gap is exactly `dr/2r`, the latitude
radius equals `ρ sin φ` at every φ, and the spherical element integrates to
`4π/3`. The cell is drawn deliberately large for visibility, so a live
exact ÷ formula ratio (1.39 → 1.06 as it shrinks) makes the limit explicit
rather than leaving an unexplained mismatch on screen.

**08 · Vector fields & line integrals** ✅ *shipped* — MIT 18.02 L19–21
Field quiver, a walker on a parametrized path, and the integrand `F(r(t))·r′(t)`
plotted so the work is visibly the area under a curve. Four routes between the
same endpoints, with all sixteen field/path totals hand-derived in closed form
and verified against quadrature. Conservative fields get the curl test, a
potential, and the FTC-for-line-integrals shortcut shown against the brute-force
route. Misconceptions cover the simply-connected hypothesis (the vortex field
with zero curl and circulation 2π).

**09 · Green's theorem** ✅ *shipped* — MIT 18.02 L24–26
Both forms in one interactive with a circulation/flux toggle; boundary and
interior integrals computed by wholly independent methods (Simpson along the
parametrized curve vs. a masked grid over the region) so their agreement is the
theorem being *checked*, not restated — 24/24 pairs agree. Plus the cancellation
picture: subdivide, and every interior edge is walked twice in opposite
directions. That single argument is flagged as the seed of Labs 09 and 10 alike.

**10 · Divergence theorem & Stokes** ✅ *shipped* — MIT 18.02 L28–32
The capstone. Flux out of a sphere or cylinder vs. the divergence integrated over
the solid (8/8 agree, matching 4π, 2π·3, etc.). Then the Stokes showpiece: the
rim is a fixed circle, a slider morphs the cap from flat disk to tall dome, and
the curl flux **does not move** — pinned at 2π, because the boundary integral it
must equal never changed. Closes with the three theorems (plus the FTC) laid side
by side as one sentence: *∫ over a region of a derivative = ∫ over its boundary
of the original.*

### Alignment

The sequence deliberately follows the arc of **MIT 18.02** (OCW, Denis Auroux) —
partial derivatives → multiple integrals → vector fields → the integral theorems —
so a reader can pair a lab with a lecture. Lecture ranges are printed in each
lab's eyebrow. The one deliberate reordering is double integrals at Lab 02
instead of later; see the note under Lab 02 for why.

## Supporting work (not lessons)

- `index.html` — landing grid of lesson cards with progress state in `localStorage`.
- Shared `lab.css` / `lab.js` extraction — **still deferred, now with evidence.**
  Six labs in, the genuinely common core is small and stable: the CSS design tokens,
  the 3D projection (`fit`/`makeP`/`proj`), the `terrain` ramp, the orbit handler, and
  the `heatmap` DPR-safe fill helper (added in Lab 05, and the exact thing whose
  absence caused a corner-only-render bug). Everything else — surfaces, readouts,
  section logic — is per-lab and rightly so. A shared `lab-core.js` holding just those
  five primitives is now worth doing; it would also have prevented duplicating the
  heatmap bug fix across labs. Good candidate for the next housekeeping pass.
