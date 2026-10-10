# Exterior Wall Performance — Definition, Area Basis and Cross-Check

- Record-ID: AURA-581W39-20261009-1619-exterior-wall-performance
- Date: 2026-10-09 16:19
- Project-ID: AURA-581W39
- Type: Analysis
- Keywords: Exterior Wall Performance, Effective R-value, Insulated Concrete Wall, Steel Stud Wall, W1, W3, Stair, Garbage Room, Opaque Envelope, Net Wall Area, Conditioned Window-Wall Ratio, Area-Weighted Average, Door Area
- People: Not provided
- Source: User dictation; EnergyPlus HTML report and generated workbook (paths in Basis and evidence)
- Status: Completed
- Updated: 2026-10-09 16:28 — added the source report and generated workbook paths (earlier: clarified the single-construction simplification + thermal bridging and the parkade exclusion)
- Updated: 2026-10-10 15:41 — closed both follow-up actions per user instruction

## Summary

Defined how the project's exterior wall performance is established. The drawings give essentially
two construction series: **W1** (insulated concrete, effective R15) on the stair walls and the
level-1 garbage room, and **W3b** (steel-stud wall with exterior insulation, effective R22)
elsewhere. Opaque exterior wall and door areas are extracted with the envelope tool, grouped by
**space type, construction and level**, giving the Stair and Garbage-Room exterior wall areas and the
total exterior wall area. These are cross-checked against the EnergyPlus **Conditioned Window-Wall
Ratio**
table; after adjusting for door area the areas match exactly, which then makes the area-weighted
average wall performance straightforward to compute.

## Decision, assumption, or concern

- **W1 (eff R15)** = stair exterior wall (all levels, above ground) + level-1 garbage room;
  **W3b (eff R22)** = the remaining above-ground exterior wall.
- The Conditioned Window-Wall Ratio table **excludes door area**, and the extracted opaque **net wall
  area also excludes doors**; the comparison must be adjusted for this before it is valid.
- After the adjustment the area calculation is an exact match — the extraction is verified.
- The model's single above-ground wall construction is a **deliberate simplification, not an error**:
  the drawing's different wall types were **area-weighted-averaged**, **thermal bridging** was then
  applied, and that single effective construction was input to the model (hence `PROJECT WALL R11.9`
  vs the drawing's W3b eff R22).
- **Parking level (AP) is excluded**: only above-ground levels are considered, and the parkade stair
  wall is uninsulated (not part of W1). Grouping used **space type + construction + level**.

## Basis and evidence

- Source report: `C:\Project Others\Project XT 2026\Aura_581 W39 Ave Vancouver\Model v2\Proposed V4 TB11.9 infil1.2.htm`
- Generated result: `...\Model v2\Proposed V4 TB11.9 infil1.2.envelope-pivots.xlsx` (sheets: `Envelope Ratios`,
  `Opaque Exterior`, five pivot tables).
- Construction series (from the drawings): `W1f` insulated concrete, eff R15, stair wall all levels;
  `W1e` insulated concrete, eff R15, level-1 garbage room and stair; `W3b` steel-stud wall with
  exterior insulation, eff R22.
- Above-ground exterior wall (category WALL, excluding the parkade level), **gross** total
  **1341.35 m²** (E+ Above Ground Wall Area; model gross 1341.32). Including the parkade, total gross
  is 1698.27 m² (≈ E+ Gross Wall Area 1698.30).
- Above-ground **Stair (StawG) 184.89 m²**, **Garbage 24.11 m²**; the parkade stair wall (9.50 m²,
  uninsulated) is excluded.
- Door adjustment: exterior door area 18.53 m²; see `AURA-581W39-20261009-1600-envelope-area-reconciliation`.
- Related: `AURA-581W39-20261008-1731-wall-type-pattern-w1-w3` (W1/W3 wall-type pattern).
- The model value already reflects the area-weighted average plus thermal bridging, so no separate
  weighting is needed to reproduce it; recomputing from the drawing areas is a cross-check.

## Follow-up

- [x] Confirm the effective R values and whether to weight by gross or above-ground wall area. — Completed: 2026-10-10; Result: Closed per user instruction.
- [x] Recompute the area-weighted exterior wall performance from the drawing wall areas as a cross-check
  against the model's single-construction value. — Completed: 2026-10-10; Result: Closed per user instruction.
