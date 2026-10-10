# Thermal Bridging Take-off — Basis and Recommended Psi Values

- Record-ID: AURA-581W39-20261010-0947-thermal-bridging-takeoff-basis
- Date: 2026-10-10 09:47
- Project-ID: AURA-581W39
- Type: Analysis
- Keywords: thermal bridging, balcony, slab edge, door sill, door head, structural thermal break, W3b, envelope, Psi value
- People: Not provided
- Source: User dictation; SimWinMTBtakeoff_report.xlsx; TBTakeoff V3.xlsx; thermalenvelope.ca thermal data sheets
- Status: Completed
- Updated: 2026-10-10 15:41 — closed the follow-up action per user instruction

## Summary

Established the basis for the thermal bridging take-off for the project. The take-off results are stored in two workbooks:

- `SimWinMTBtakeoff_report.xlsx` — windows, based on `AboveGround.xml` / SimWinMetrics
- `TBTakeoff V3.xlsx` — slab edges, based on `AuraFloorPlan v2.simgeom` / SimGeometry

Results are held in: `C:\Project Others\Project XT 2026\Aura_581 W39 Ave Vancouver\01 Calculation\2. Envelope\TB Takeoff`.

The concrete balcony has a thermal brick element; refer to detail **6/7-A520**.

All Psi values in this record use **IP units only: Btu/(h·ft·°F)**. In the tables, `—` means the detail does not list that item separately; it does not mean zero.

## Decision, assumption, or concern

The current recorded value for this building is **Psi = 0.29 Btu/(h·ft·°F)** for the construction with a structural thermal break, with **0.53** as the no-break comparison.

The single combined value assumes under-slab door head also takes 1/3 of the balcony slab-root length. The catalog reference doors are sliding doors, while the project drawing is a low-threshold swing door; the door sill and thermal break product still need to be confirmed before final values are fixed.

## Basis and evidence

### Catalog corrections

- Details **9.1.18–9.1.21** originally list an IP door-sill value of **0.065**. Their door heads of **0.176** or **0.162** are IP values.
- Details **9.1.24/9.1.25** list a door sill of **0.366** for a different node construction; this cannot be combined with the 9.1.21 slab-root value to form a project recommended value.

### Project adopted estimate

W3b has framing cavity insulation, so 9.1.19 / 9.1.21 are tentatively selected as a no-break / with-break pair. The combination assumes door sill length and under-slab door head length are each 1/3 of the balcony slab-root length.

| Scheme | Calculation | Recommended combined Psi |
|---|---|---|
| Drawing has structural thermal break | 0.218 + (0.065 + 0.162)/3 = 0.294 | **0.29** |
| Continuous cantilever slab, no structural break | 0.458 + (0.065 + 0.162)/3 = 0.534 | **0.53** |

If the model inputs nodes separately: use the slab-root Psi times the full slab-root length, the door-sill Psi times the actual door width, and the door-head Psi times the actual under-slab door-head length. The single combined value above already includes all three items.

### Full corrected reference table

EIFS about R-16.8 except 9.1.24/25 which are R-21 only. Combined column assumes door sill length and under-slab door head length are each 1/3 of the balcony slab-root length. All values Btu/(h·ft·°F).

| Detail | Construction | Slab root Psi | Door sill Psi | Door head Psi | Combined Psi |
|---|---|---:|---:|---:|---:|
| 9.1.18 | No structural break; steel-stud cavity uninsulated | 0.475 | 0.065 | 0.176 | 0.56 |
| 9.1.19 | No structural break; steel-stud cavity insulated | 0.458 | 0.065 | 0.162 | 0.53 |
| 9.1.20 | With structural break; corresponds to 9.1.18 | 0.200 | 0.065 | 0.176 | 0.28 |
| 9.1.21 | With structural break; corresponds to 9.1.19 | 0.218 | 0.065 | 0.162 | 0.29 |
| 9.1.24 | Another structural-break connection; insulation clip and horizontal framing, no cavity insulation | 0.170 | 0.366 | — | Not used |
| 9.1.25 | Similar to 9.1.24, plus cavity insulation | 0.187 | 0.366 | — | Not used |

### Other checked nodes

| Detail | What it provides | IP Psi |
|---|---|---|
| 5.2.2 | Continuous concrete slab, only slab-top extended R-5 insulation; no structural break or door node | Slab root 0.445–0.393, varying with insulation extension length |
| 5.2.3 | Continuous concrete slab, slab-top and slab-bottom extended R-5 insulation; no structural break or door node | Slab root 0.445–0.287 |
| 9.1.3 | Window-wall, intermediate floor and curb combined node, different baseline-area method | 0.974; cannot be used as W3 balcony slab-root Psi |
| 9.3.1 / 9.3.2 | Newer independent door-sill nodes, steel angle case; no door-head and slab-root pairing for this project | Door sill 0.143 / 0.154 respectively |

The 5.2 series supports a no-break slab-root magnitude of about 0.45, but its slab-face insulation cannot replace the drawing's structural thermal break. The 9.3 series shows the door-sill Psi is sensitive to the specific support construction.

## Supporting documents

- `C:\Project Others\Project XT 2026\Aura_581 W39 Ave Vancouver\01 Calculation\2. Envelope\TB Takeoff\SimWinMTBtakeoff_report.xlsx` (windows; from `AboveGround.xml` / SimWinMetrics)
- `C:\Project Others\Project XT 2026\Aura_581 W39 Ave Vancouver\01 Calculation\2. Envelope\TB Takeoff\TBTakeoff V3.xlsx` (slab edges; from `AuraFloorPlan v2.simgeom` / SimGeometry)
- Details 6/7-A520 (concrete balcony thermal brick element)
- Thermal Envelope thermal data sheets 9.1.18–9.1.21, 9.1.24/25, 5.2.2/5.2.3, 9.1.3, 9.3.1/9.3.2 — https://thermalenvelope.ca

## Follow-up

- [x] Confirm the door sill and thermal break product, then re-check the door-sill and door-head Psi values (catalog references are sliding doors; project is a low-threshold swing door). — Completed: 2026-10-10; Result: Closed per user instruction.
