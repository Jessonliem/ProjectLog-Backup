# Envelope Area Reconciliation (Opaque Walls vs Window-Wall Ratio)

- Record-ID: AURA-581W39-20261009-1600-envelope-area-reconciliation
- Date: 2026-10-09 16:00
- Project-ID: AURA-581W39
- Type: Analysis
- Keywords: Building Envelope, Opaque Area, Exterior Wall, Window-Wall Ratio, Net Wall Area, Door Area, Above Ground Wall Area, Area Reconciliation
- People: Not provided
- Source: EnergyPlus tabular report and the generated pivot workbook (see body); user dictation
- Status: Completed
- Updated: 2026-10-09 16:23 — linked to the exterior wall performance record
- Updated: 2026-10-10 15:41 — closed both follow-up actions per user instruction

## Summary

Reconciled the opaque exterior wall area against the EnergyPlus tabular report. The extracted
`PROJECT WALL R11.9` area (1099.05 m²) is the E+ **Net Area** (wall gross minus **window and door**
openings), whereas the E+ Window-Wall Ratio table's "net wall" (1117.6 m²) subtracts **windows
only**. The 18.5 m² gap is the exterior **door** area. The Conditioned Window-Wall Ratio table is a
smaller scope (excludes walls bounding unconditioned spaces, e.g. the parkade) and cannot be
reproduced from the pivot, which has no conditioning dimension.

## Basis and evidence

- Source: `Proposed V4 TB11.9 infil1.2.htm` (E+ report) and `Proposed V4 TB11.9 infil1.2.envelope-pivots.xlsx`
  (workbook with a `Envelope Ratios` sheet and the `Opaque Exterior` table copied verbatim).
- `PROJECT WALL R11.9`: gross 1341.32 m², net 1099.05 m², 141 surfaces.
- E+ Window-Wall Ratio: Gross Wall Area 1698.30, Above Ground Wall Area 1341.35, Window Opening Area 223.75 m².
- Exterior windows (multiplied openings) 223.93 m²; exterior doors 18.53 m²
  (orientation N 4.04 / E 4.61 / S 2.53 / W 7.35).
- Reconciliation: gross 1341.32 = net 1099.05 + windows 223.93 + doors 18.53 (per-row rounding);
  window-only net = 1341.32 − 223.93 = 1117.39 ≈ E+ 1117.6.
- Conditioned Window-Wall Ratio net wall = 1070.9 m² (Above Ground Wall Area 1294.65).
- Related: `AURA-581W39-20261009-1619-exterior-wall-performance` (uses this reconciliation's door
  adjustment to derive the exterior wall performance area basis).

## Decision, assumption, or concern

- "Net wall area" is ambiguous: state explicitly whether it excludes windows only (E+ Window-Wall
  Ratio) or windows **and** doors (E+ Net Area used in the pivot). Both are now shown in the
  `Envelope Ratios` sheet: `Net Wall Area (Above Ground)` and `Net Wall Area (excl. windows & doors)`.
- The pivot cannot produce the Conditioned figure without a conditioning dimension per zone.

## Follow-up

- [x] Decide which net-wall definition is used for the envelope area deliverable. — Completed: 2026-10-10; Result: Closed per user instruction.
- [x] If the Conditioned ratio must be reproduced, add a zone conditioning flag to the extraction. — Completed: 2026-10-10; Result: Closed per user instruction.
