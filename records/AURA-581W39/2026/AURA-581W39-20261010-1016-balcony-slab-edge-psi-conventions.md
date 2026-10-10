# Learning Notes — Balcony / Concrete Slab Edge Psi Conventions and Full-Height Energy Models

- Record-ID: AURA-581W39-20261010-1016-balcony-slab-edge-psi-conventions
- Date: 2026-10-10 10:16
- Project-ID: AURA-581W39
- Type: Learning
- Keywords: thermal bridging, Psi value, balcony, slab edge, clear field, spandrel panel, double counting, full-height model, floor-to-ceiling glazing, BC Housing, 9.1.3, 9.1.19, 9.1.21, 9.1.26
- People: Not provided
- Source: User-provided learning note `C:\Users\jesso\Downloads\Balcony_Slab_Edge_Psi_Learning_Notes.md`; BC Building Envelope Thermal Bridging Guide; BC Housing 2024 guide; ThermalEnvelope.ca data sheets
- Status: Recorded
- Updated: 2026-10-10 14:18 — added Chinese companion section (non-indexed) for readability

Units: all linear thermal transmittance Psi values are Btu/(h·ft·°F); all area U-values are Btu/(h·ft²·°F).

## Summary

A balcony thermal bridge cannot be judged by the Psi number alone. You must first identify the catalog node's **reference assembly**, the **clear-field heat flow that has been deducted**, and whether the **slab/curb projected area is already included in the Psi**. A lower vs. higher number is a clue to which convention is being used — it is not a fixed numeric threshold.

| Convention | What the Psi means | Catalog example | When used in a full-height facade model |
| --- | --- | --- | --- |
| **Additional heat transfer referenced to an opaque clear wall** | Node total heat transfer minus the reference-wall heat transfer over the same projected area. The wall area is still counted at the reference wall's U. | 9.1.19 uninsulated balcony slab root Psi = **0.458**; 9.1.21 with structural break Psi = **0.218** (both at about R-16.8 EIFS). | If the model actually uses the same reference-wall U in that region, add Psi × slab-root length on top of the wall heat transfer. If that region uses a different panel U, the baseline must be adjusted too. |
| **Linear value between floor-to-ceiling glazing, with the slab/curb area NOT deducted** | The heat transfer of the glass above and below is deducted from the detailed node, but the slab/curb projected strip has no corresponding opaque clear wall; most of that strip's heat transfer remains in the Psi. | 9.1.3 Psi = **0.974**; 9.1.26 Psi = **0.728**. Both sheets note they cannot be read against an opaque-wall clear field. | If the same projected strip is already built as a conducting spandrel/panel, adding the full catalog Psi double-counts the area heat transfer already in the model. |

Magnitude check: 9.1.3's **8 in slab + 6 in curb = 14 in**; its slab/curb region U = **0.832**, times **14/12 ft** ≈ **0.971**, close to the listed Psi **0.974**. 9.1.26's slab region U = **1.09**, times about **8/12 ft** ≈ **0.727**, close to the Psi **0.728**. This is a check for understanding the order of magnitude, not a general formula to back out every node's Psi.

## 1. Why does the catalog use the second convention?

The BC Building Envelope Thermal Bridging Guide, in *Dealing with Floor to Ceiling Glazing*, notes: when glazing runs from one floor slab to the next, both sides of the slab are glazing and **there is no obvious opaque clear wall to serve as the baseline** for that strip. The guide therefore deducts the glazing heat flow above and below the slab from the node's total heat transfer and reports the remaining slab/curb heat transfer per unit slab-edge length. It also lists two usable methods:

1. **U-value approach**: treat the slab/curb projected area as a separate opaque area, computed with its U-value; handle the other interfaces with the applicable nodes.
2. **Linear transmittance without area**: use the linear value without deducting slab area, but the clear-field area must be computed **excluding the slab projected strip**.

The guide's stated reason is to make the node data applicable to different adjacent wall combinations and to simplify the then-current practice of taking quantities by balcony length. **This explains why it is defined that way; it does not mean it is naturally suited to every energy-model geometry.** For models that build by floor-to-floor height and enter spandrels separately, the second method is indeed awkward.

In 2024, BC Housing's *Thermal Bridging at Balconies and Doors Guide* **provided another, more separable take-off example**: list the applicable clear-field curb/spandrel area, balcony, door sill, and other interfaces separately, to allow comparison of different insulation measures. It did not declare the old nodes obsolete, nor did it convert every old value on ThermalEnvelope.ca to a single convention. **The site currently retains entries of different versions and conventions**: e.g. 9.1.3 still lists about **0.974**, and the newer version of 9.1.26 still lists **0.728**. Users must still check the area basis node by node.

## 2. For a model that already has spandrel panels, how to avoid double counting?

First confirm whether the panel covers the slab/curb projected strip that the catalog Psi represents. If it does, and the catalog value explicitly uses the **without-area** convention, the conceptual additional linear value is:

**Psi to add = Psi_catalog − U_model,panel × A_overlap / L**

where `A_overlap / L` is the overlap height (ft), per ft of node length, that is **already counted as conducting area in the model**. Deduct only the slab/curb projected height, not mechanically the entire spandrel panel. The model's window/door areas, node take-off lines, and U conventions must also match the catalog reference. The remainder after deduction may include interface effects and differences between the actual construction and the model panel, and cannot simply be called pure structural thermal bridging.

The other route is to keep the full catalog Psi while excluding the corresponding slab/curb projected strip from the clear-field conducting area. Both routes should yield the same heat transfer; **you cannot both keep that strip's panel U×A and add the full without-area Psi**. If the software already explicitly models the full 2D/3D node, no additional Psi for the same node may be applied.

For a node **referenced to an opaque clear wall**, if the model uses exactly that reference wall in the same strip, add the catalog Psi directly; if the model uses a different panel, the general form is:

**Psi to add = Psi_catalog + (U_catalog,reference wall − U_model,panel) × A_overlap / L**

`Without area` is the special case of this general form where the reference U of the strip is zero. This formula is only a baseline-conversion bookkeeping of steady-state heat transfer; before use, verify the interfaces the catalog has already deducted (glazing, door, head/sill) to avoid double counting or omission.

## 3. The project estimate and values that must not be mixed

The project is a W3-series EIFS steel-stud wall, with a structural thermal break at the concrete balcony slab root, about one-third of the slab-root length corresponding to the door sill, and tentatively assuming the under-slab door head also takes one-third. Using the **paired** 9.1.19/9.1.21 as a conceptual estimate:

| Scheme | Slab root Psi | Door sill Psi | Door head Psi | Psi per ft of slab-root length |
| --- | ---: | ---: | ---: | ---: |
| With structural break (9.1.21) | 0.218 | 0.065 | 0.162 | `0.218 + (0.065 + 0.162)/3` ≈ **0.29** |
| No structural break (9.1.19) | 0.458 | 0.065 | 0.162 | `0.458 + (0.065 + 0.162)/3` ≈ **0.53** |

These catalog nodes use sliding doors; the project drawing is a low-threshold swing door, and the thermal-break product is not yet confirmed. **0.29/0.53 are estimates from similar nodes and must not be treated as product-certified values.** 9.1.3's **0.974** uses a different reference/area convention and cannot be used directly to replace or judge this W3 estimate.

## 4. Assessment of the guide's clarity

It is not accurate to say the guide "does not explain at all": the *Dealing with Floor to Ceiling Glazing* section clearly states that there is no opaque clear field, the two calculation methods, and that the slab area must be excluded when using the full linear value. **The currently accessible 9.1.3 PDF footnote states that its Psi is not referenced to an opaque-wall clear field and points to that section; the newer 9.1.26 PDF has a similar footnote.** However, a single PDF footnote does not directly give the operation "if the energy model is already built full-height with spandrel panels, how much already-counted U×A to deduct", nor does it prominently flag beside the catalog value whether the slab projected area is included. For an energy modeler who builds spandrels full-height, this still easily causes misreading or double counting. The assessment should be: **it states the convention and reading clues, but the warnings are not prominent enough and the model mapping must still be done by the user** — not "no explanation" nor "fully fixed after 2024".

**Minimum check before using a catalog value:** which clear field did this Psi subtract? which area's U×A has the model already counted? are the door sill/head already included? Only after the three are aligned, add Psi × L.

## 中文说明（不参与索引）

- **核心**：不能只看 Ψ 数值判断阳台热桥；先看目录节点的 **reference assembly、扣掉的 clear-field 传热、以及楼板/curb 投影面积是否已含在 Ψ 里**。数值高低是识别两种口径的线索，不是固定分界线。
- **两种口径**：①以 opaque clear wall 为基准的**附加**传热（如 9.1.19 Ψ = 0.458、9.1.21 Ψ = 0.218）；②落地玻璃之间、**未扣 slab/curb 面积**的线性值（如 9.1.3 Ψ = 0.974、9.1.26 Ψ = 0.728），后者不能按 opaque wall clear field 解读。
- **量级核对**：9.1.3 的 0.832 × 14/12 ≈ 0.971 ≈ 0.974；9.1.26 的 1.09 × 8/12 ≈ 0.727 ≈ 0.728。仅用于理解量级，不是通用反推公式。
- **为何这样定义**：BC 指南 *Dealing with Floor to Ceiling Glazing* 指出楼板两侧皆玻璃、无 opaque clear wall 可比，故扣掉上下玻璃、把剩余 slab/curb 传热按板边长度报告，并给出 U-value 与 without-area 两条路径。2024 BC Housing 指南给出更可拆分的取量示例，但未宣布旧节点失效，网站仍并存不同版本/口径。
- **已建 spandrel 面板如何避免 double counting**：`Ψ应添加 = Ψ目录 − U模型,panel × A重叠 / L`（without-area 情形）；以 clear wall 为基准时通式为 `Ψ目录 + (U目录参考墙 − U模型panel) × A重叠 / L`。不能既保留该带的 panel U×A 又完整叠加 without-area Ψ；软件已显式模拟 2D/3D 节点时不得再加。
- **本项目估算**：成对 9.1.19/9.1.21，取门槛、门头各占板根长度 1/3——有隔热 `0.218 + (0.065 + 0.162)/3 ≈ 0.29`、无隔热 `0.458 + (0.065 + 0.162)/3 ≈ 0.53`；目录门为推拉门、项目为低门槛平开门且隔热件未定，**并非产品认证值**。9.1.3 的 0.974 口径不同，不可直接替换或评判此 W3 估算。
- **评价**：指南有口径说明与阅读线索，但提示不够醒目、模型映射仍需使用者自行完成，既非“无解释”也非“2024 后已全面改好”。使用目录值前最短核对：这个 Ψ 减掉了哪块 clear field？模型已计入哪块 U×A？sill/head 是否已含？

## Supporting documents

- BC Hydro / BC Housing, Building Envelope Thermal Bridging Guide, Part 1 — "Dealing with Floor to Ceiling Glazing" — https://www.bchydro.com/content/dam/BCHydro/customer-portal/documents/power-smart/builders-developers/final-mh-BC-part-1-envelope-guide.pdf
- BC Housing, Thermal Bridging at Balconies and Doors Guide (2024) — https://www.bchousing.org/sites/default/files/media/documents/Thermal-Bridging-at-Balconies-and-Doors-Guide.pdf
- Thermal Envelope, detail 9.1.3 thermal data sheet — https://thermalenvelope.ca/pdf/thermal_data_sheet_9.1.3.pdf?version=v1.7.3
- Thermal Envelope, detail 9.1.26 thermal data sheet — https://thermalenvelope.ca/pdf/thermal_data_sheet_9.1.26.pdf?version=v1.9.0
- Thermal Envelope, detail 9.1.19 thermal data sheet — https://thermalenvelope.ca/pdf/thermal_data_sheet_9.1.19.pdf
- Thermal Envelope, detail 9.1.21 thermal data sheet — https://thermalenvelope.ca/pdf/thermal_data_sheet_9.1.21.pdf
- Original note: `C:\Users\jesso\Downloads\Balcony_Slab_Edge_Psi_Learning_Notes.md`

## Follow-up

- Consider migrating learning records to a dedicated learning-notes area (Obsidian vault) in the future.
- Related records: `AURA-581W39-20261010-0947-thermal-bridging-takeoff-basis`, `AURA-581W39-20261010-0959-psi-baseline-window-wall-curb`.
