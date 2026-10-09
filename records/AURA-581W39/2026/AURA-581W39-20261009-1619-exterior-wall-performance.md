# Exterior Wall Performance — Definition, Area Basis and Cross-Check

- Record-ID: AURA-581W39-20261009-1619-exterior-wall-performance
- Date: 2026-10-09 16:19
- Project-ID: AURA-581W39
- Type: Analysis
- Keywords: Exterior Wall Performance, Effective R-value, Insulated Concrete Wall, Steel Stud Wall, W1, W3, Stair, Garbage Room, Opaque Envelope, Net Wall Area, Conditioned Window-Wall Ratio, Area-Weighted Average, Door Area
- People: Not provided
- Source: User dictation; EnergyPlus tabular report and extracted opaque/door areas (see body)
- Status: Recorded

## Summary

Defined how the project's exterior wall performance is established. The drawings give essentially
two construction series: **W1** (insulated concrete, effective R15) on the stair walls and the
level-1 garbage room, and **W3b** (steel-stud wall with exterior insulation, effective R22)
elsewhere. Opaque exterior wall and door areas are extracted with the envelope tool, grouped by
**space type and construction**, giving the Stair and Garbage-Room exterior wall areas and the total
exterior wall area. These are cross-checked against the EnergyPlus **Conditioned Window-Wall Ratio**
table; after adjusting for door area the areas match exactly, which then makes the area-weighted
average wall performance straightforward to compute.

## Decision, assumption, or concern

- **W1 (eff R15)** = stair exterior wall (all levels) + level-1 garbage room; **W3b (eff R22)** = the
  remaining exterior wall.
- The Conditioned Window-Wall Ratio table **excludes door area**, and the extracted opaque **net wall
  area also excludes doors**; the comparison must be adjusted for this before it is valid.
- After the adjustment the area calculation is an exact match — the extraction is verified.
- The model names its above-ground wall construction `PROJECT WALL R11.9` (single construction), so
  the W1/W3 split is applied by **space type**, not by construction name.

## Basis and evidence

- Construction series (from the drawings): `W1f` insulated concrete, eff R15, stair wall all levels;
  `W1e` insulated concrete, eff R15, level-1 garbage room and stair; `W3b` steel-stud wall with
  exterior insulation, eff R22.
- Extracted exterior wall (category WALL), **gross** areas: total **1698.27 m²**
  (≈ E+ Gross Wall Area 1698.30), **Stair (StawG) 194.39 m²**, **Garbage 24.11 m²**; net wall
  1456.00 m².
- Door adjustment: exterior door area 18.53 m²; see `AURA-581W39-20261009-1600-envelope-area-reconciliation`.
- Related: `AURA-581W39-20261008-1731-wall-type-pattern-w1-w3` (W1/W3 wall-type pattern).
- Provisional area-weighted R (gross areas, W1 = stair + garbage): (218.50×15 + 1479.77×22) / 1698.27
  ≈ **21.1** — confirm the W1/W3 boundary and weighting basis before using.

## Follow-up

- Confirm whether the parkade stair wall (9.50 m², uninsulated parkade construction) belongs to W1.
- Confirm the effective R values and whether to weight by gross or above-ground wall area.
- Reconcile the model's `PROJECT WALL R11.9` naming against the drawing's W3b eff R22.
- Compute and record the final area-weighted exterior wall performance.
