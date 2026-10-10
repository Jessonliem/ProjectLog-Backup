# Learning Note — Fan Power and SFP Input Methods in Energy Simulation (Pragmatic Effective-SFP Workaround)

- Record-ID: AURA-581W39-20261010-1413-fan-power-sfp-modeling
- Date: 2026-10-10 14:13
- Project-ID: AURA-581W39
- Type: Learning
- Keywords: fan power, SFP, specific fan power, PTAC, PTHP, DesignBuilder, EnergyPlus, HRV, ERV, variable-speed fan, fan laws, UnitarySystem, VRF, effective average fan power
- People: Not provided
- Source: User-provided memo `C:\Project Others\Project XT 2026\Aura_581 W39 Ave Vancouver\01 Calculation\4. Mechanical\Equipment_YYYYMMDD\Fan power simulation.md`
- Status: Recorded
- Updated: 2026-10-10 14:18 — added Chinese companion section (non-indexed) for readability

## Summary

A technical memo consolidating a **pragmatic engineering workaround ("effective combined SFP" derivation)** and the concrete operating logic for feeding fan power / SFP into DesignBuilder / EnergyPlus, including how to match the modeling condition to the real operating condition.

Key points:
- Baseline method: rated fan power ÷ design/max airflow gives the SFP.
- Variable-speed-capable software degrades fan energy automatically via the fan curve and Fan Laws.
- HRV/ERV dedicated outdoor-air units are usually modeled at the low (continuous) airflow point.
- DesignBuilder's native PTAC/PTHP forces constant-volume cycling and would overestimate annual fan energy if the max rated power is entered.
- Where rebuilding the HVAC network is impractical, a time- and power-weighted **effective average fan power** is entered instead.

## 1. Standard baseline approach

- **Input principle:** the fan's rated baseline input uses the **nameplate rated fan power divided by the design/max airflow rate** to give the specific fan power (SFP, or fan power per unit flow rate).
- **Software degradation mechanism:** in energy software with a dynamic fan model (Variable Speed / Multi-Speed Fan), such as EnergyPlus / DesignBuilder, the system takes that operating point as the reference at **f = 1.0**. At each actual timestep the software reduces fan energy at low airflow using the **flow fraction** (f = V / V_design) combined with the **fan performance polynomial curve (corrected per Fan Laws, exponent typically 2.0–2.5)**.

## 2. Special equipment: HRV / ERV dedicated outdoor-air systems

- **Operating characteristic:** the nameplate or certification report (e.g. HVI / CSA-C439) usually lists the measured input electric power at the low airflow (continuous ventilation) and high airflow (boost / exhaust-linked) conditions directly.
- **Input methods:**
  - **Time-weighted average:** if modeled as a constant-airflow system, convert to an equivalent average fan power and SFP by the runtime fractions at low and high speed, per code / the project's actual operating strategy.
  - **Direct base SFP (lock the continuous OA point):** in real modeling, the window / dedicated outdoor air (OA) normally runs year-round at the code minimum ventilation rate (low speed), and the high-airflow condition is rarely triggered. Therefore, for HRV/ERV, use the measured power and airflow at the low-speed condition to derive the base SFP; the energy deviation is tiny and it best matches the annual base-energy performance.

## 3. Terminal fans (heat pump / FCU SA fan) in DesignBuilder — constraints and modeling options

- **Underlying limitation of DesignBuilder's native PTAC / PTHP template:**
  - The native DB PTAC/PTHP module is directly bound to EnergyPlus's `ZoneHVAC:PackagedTerminalHeatPump` / `Fan:OnOff` objects and is **forced to constant volume (Constant Volume / Cycling) in the UI, with no variable-speed or multi-speed option**.
  - If the max rated power (e.g. 85.4 W) is entered directly, the unit will always be accounted at full-load fan power during the on-cycle, so the energy-saving benefit of BLDC motor low-speed operation cannot be modeled, and the annual fan energy is significantly inflated.
- **Higher-accuracy alternatives (require changing the topology):**
  - **Unitary System substitution:** build a single-zone heat pump in Detailed HVAC using `AirLoopHVAC:UnitarySystem`, select `Fan:VariableVolume`, lock the high-speed supply airflow (e.g. 353 CFM), set a minimum flow ratio (e.g. 0.70), and define a custom fan power polynomial curve.
  - **VRF indoor-unit template:** switch to the VRF Terminal Unit template, whose underlying model supports variable-speed supply and multi-speed control.

## 4. Pragmatic engineering workaround: "effective combined SFP" derivation under constant volume

If the project uses DB's native PTAC / PTHP template (or to control modeling complexity and avoid rebuilding the Detailed HVAC network):

- **Core idea:**
  - Give up dynamic in-software speed degradation and instead perform a **runtime- and power-weighted conversion on the input side**, entering an **effective average fan power** directly.
- **Conversion logic and formula:**
  - Count or estimate the share of each speed condition during the main operating season (heating/cooling). For a residential/apartment space with good temperature control, the indoor unit spends most of the time in the low-airflow maintenance stage (about 70%–80% at Low, with a small share at Med/High):

    P_eff = w_low·P_low + w_med·P_med + w_high·P_high

  - For example FC-1 (LG LDN127HV4): about 39 W at low, about 58 W at med, 85.4 W at high:

    P_eff ≈ 0.75×39 + 0.20×58 + 0.05×85.4 ≈ 45–50 W

  - Use this effective power to compute the SFP entered into the model:

    SFP_eff = P_eff / Q_design ≈ 48 W / 353 CFM ≈ **0.136 W/CFM** (**0.288 W/(L/s)**)
- **Applicability and compliance note:**
  - This method avoids the large workload of rebuilding the HVAC network.
  - Even if the system starts/stops in constant-volume (CAV / Cycling Fan) mode, the annual cumulative fan energy stays highly consistent with the actual multi-speed operation, making it the most practical approximation for engineering compliance and fast delivery.

## 中文说明（不参与索引）

- **通用基准**：SFP = 铭牌额定风机功率 ÷ 设计/最大风量。具备动态风机模型的软件（EnergyPlus / DesignBuilder）以该工况点为 f = 1.0 基准，按风量比 f 与风机多项式曲线（Fan Laws，指数约 2.0–2.5）自动降低低风量能耗。
- **HRV/ERV 独立新风**：铭牌/认证（HVI、CSA-C439）直接给低/高风量实测功率。可①按运行时间加权折算，或②**直接锁定连续新风（低风量）点**核算基准 SFP——实际常年按规范最小换气量运行，偏差极小。
- **终端风机在 DesignBuilder 的约束**：原生 PTAC/PTHP 底层绑定 `ZoneHVAC:PackagedTerminalHeatPump` / `Fan:OnOff`，UI 强制恒定风量，无法模拟 BLDC 低速节能；直接输最大功率（如 85.4 W）会显著放大全年风机电耗。高精度替代：`AirLoopHVAC:UnitarySystem` + `Fan:VariableVolume`（锁定高档风量如 353 CFM、设最小风量比如 0.70、自定义风机曲线），或改用 VRF 室内机模板。
- **工程极简妥协（等效综合 SFP）**：放弃软件内变频降级，改在前端做**运行时间—功率加权折算**，直接输入等效平均功率 `P_eff = w_low·P_low + w_med·P_med + w_high·P_high`。例 FC-1（LG LDN127HV4）：`0.75×39 + 0.20×58 + 0.05×85.4 ≈ 45–50 W`；`SFP_eff = 48 W / 353 CFM ≈ 0.136 W/CFM ≈ 0.288 W/(L/s)`。
- **适用**：免去重构 HVAC 网络；即便定风量启停，全年累计电耗也与实际多档运行高度一致，是合规快速交付的实用近似。

## Supporting documents

- Source memo: `C:\Project Others\Project XT 2026\Aura_581 W39 Ave Vancouver\01 Calculation\4. Mechanical\Equipment_YYYYMMDD\Fan power simulation.md`
- Equipment notes: `...\4. Mechanical\Equipment_YYYYMMDD\Equipment Notes.txt`
- Submittals: `SB_MultiF_LowStaticDucted_LDN127HV4.pdf`, `SB_SZ_Ducted_LD097HV4_11_18.pdf`, `Panasonic-FV-10VE1-Submittal-Sheet.pdf`
- Related: `...\4. Mechanical\Zone Mechanical Input Summary5.xlsx`, `...\4. Mechanical\VMG Corridor Credit.xlsx`

## Follow-up

- Confirm the actual low/med/high speed power and airflow values once equipment is finalized, and re-check the effective SFP.
