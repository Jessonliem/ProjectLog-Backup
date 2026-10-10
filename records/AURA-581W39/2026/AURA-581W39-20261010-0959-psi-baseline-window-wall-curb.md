# Learning Note — Why Detail 9.1.3 Psi Is So High (Psi Must Be Read Against a Baseline)

- Record-ID: AURA-581W39-20261010-0959-psi-baseline-window-wall-curb
- Date: 2026-10-10 09:59
- Project-ID: AURA-581W39
- Type: Learning
- Keywords: thermal bridging, Psi value, baseline, clear field, window-wall, curb, intermediate floor, BC Housing
- People: Not provided
- Source: User dictation; thermalenvelope.ca detail 9.1.3 data sheet; BC Housing Thermal Bridging at Balconies and Doors Guide
- Status: Recorded

## Summary

A learning note (not tied to this project's model) clarifying a detail question that came up while doing the calculation. The question: why is the Psi of detail **9.1.3** so high (0.974 Btu/(h·ft·°F)), given the intuition that a Psi value is a difference and so cannot be large when the base wall is poorly insulated.

The resolution: **Psi is a difference, but you must first ask "relative to what baseline."** Detail 9.1.3 is the junction of a **window-wall with an intermediate floor and a concrete curb**. Its Psi = 0.974 is *not* referenced to an undisturbed opaque wall. In the calculation, the glass heat transfer above and below the slab is deducted, but the strip of height occupied by the slab and curb has no corresponding opaque clear wall to deduct. Therefore the heuristic "poor base-wall insulation means a small Psi" cannot be applied here.

## Basis and evidence

- Mass check of the magnitude: detail 9.1.3 has an **8 in slab + 6 in curb**, a projected height of about **14 in**. The data sheet gives **U_s = 0.832 Btu/(h·ft²·°F)** for that portion. Multiplying: 0.832 × 14/12 ≈ **0.97 Btu/(h·ft·°F)**, essentially the listed **Psi = 0.974**. This indicates the Psi largely carries the heat transfer of that concrete region itself, not merely "extra leakage added to a poor wall."
- The node's R-10 insulation sits on the **inside of the curb**, and there is no slab-root structural thermal break as in the project drawing.
- Consequently, **0.974 cannot be compared directly against the project's insulated-balcony estimate (0.29)** to infer the benefit of a thermal break. The former concerns the slab and curb region under the window-wall and uses a different area-deduction method; the latter is a project estimate for the W3-series wall, balcony slab root, and about one-third door width.
- BC Housing's follow-up guidance also notes specifically that older balcony and door nodes may use combined heat transfer, and that nodes must be aligned on clear field, counted interfaces, and area method before any comparison.

## Supporting documents

- Thermal Envelope detail 9.1.3 data sheet — https://thermalenvelope.ca/pdf/thermal_data_sheet_9.1.3.pdf
- BC Housing, Thermal Bridging at Balconies and Doors Guide — https://www.bchousing.org/sites/default/files/media/documents/Thermal-Bridging-at-Balconies-and-Doors-Guide.pdf
- Related project record: `AURA-581W39-20261010-0947-thermal-bridging-takeoff-basis`

## Follow-up

- None. (This note may later be migrated to a dedicated learning-notes area.)
