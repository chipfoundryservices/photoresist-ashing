# Chapter 7: Pressure-Power-Temperature Phase Space

## Overview

Photoresist ashing has three primary controllable parameters: **pressure (P)**, **RF power (W)**, and **temperature (T)**. The 3D space of all possible (P, W, T) combinations defines the **process window**. This chapter maps that space, identifies operating regions, and develops recipes that balance ashing rate, selectivity, and uniformity.

**Learning Objectives:**
- Map 3D parameter space (pressure, power, temperature)
- Identify ashing rate and selectivity contours
- Locate robust vs. sensitive operating regions
- Develop DOE (Design of Experiments) strategies
- Perform sensitivity analysis for parameter tuning
- Design recipes for specific applications
- Implement feedback control for drift compensation

---

## 7.1 3D Parameter Space Fundamentals

### 7.1.1 Defining the Phase Space

```
Three primary parameters:

Pressure (P): 30-150 mTorr
  - Lower P: Higher ion energy, better ARDE compensation, worse uniformity
  - Higher P: Lower ion energy, better selectivity, more uniform
  - Typical range for 3D NAND: 50-100 mTorr

RF Coil Power (W_coil): 1000-3000 W
  - Lower W: Lower plasma density, slower ashing
  - Higher W: Higher plasma density, faster ashing
  - Typical range: 1800-2200 W (balanced)

Bias Power (W_bias): 100-800 W
  - Lower bias: Lower ion energy (~0.3 × V_bias)
  - Higher bias: Higher ion energy
  - Typical range: 300-600 W
  
  Note: Some tools use RF voltage directly instead of power
  Relationship: E_ion ≈ 0.3 × V_bias (quantitative)

Temperature (T): -10 to +60°C
  - Lower T: Better selectivity, slower ashing (Arrhenius ~15%/°C)
  - Higher T: Faster ashing, worse selectivity, oxidation risk >80°C
  - Typical range for 3D NAND: +10 to +30°C

Process window:
  Volume of (P, W_coil, T) space where process is feasible
  Ashing rate R_target ± 10%
  Selectivity S_target ± 2:1
  Uniformity ±10% across wafer
```

### 7.1.2 Quantitative Relationships

Ashing rate and selectivity depend on all three parameters:

```
Ashing rate model:

R(P, W, T) = R₀ × f_pressure(P) × f_power(W) × f_temperature(T)

where:

f_temperature(T) = exp(-E_a / kT)  [Arrhenius, E_a ~12 kcal/mol]
  ~15% increase per °C

f_power(W) ≈ √W  (sublinear dependence, plasma density scales as √P)
  100% power increase → ~40% rate increase

f_pressure(P) ≈ 1/√P  (lower pressure → higher ion energy, faster ashing)
  10 mTorr increase (70→80 mTorr) → ~7% rate decrease

Combined model (normalized to baseline):

R(P, W, T) / R_baseline = √(W/W_base) × √(P_base/P) × exp[-E_a/k × (1/T - 1/T_base)]

Example baseline:
  R_base = 50 nm/min at P_base = 80 mTorr, W_base = 2000 W, T_base = 20°C

At different operating point:
  P = 60 mTorr, W = 2200 W, T = 30°C
  R/R_base = √(2200/2000) × √(80/60) × exp[12/(1.987×10⁻³) × (1/303 - 1/293)]
  R/R_base ≈ 1.05 × 1.15 × 1.49 ≈ 1.8
  R ≈ 90 nm/min (78% faster)

Selectivity model:

S(P, W, T) = S₀ × f_selectivity(E_ion) × f_selectivity(T)

where:

E_ion ≈ 0.3 × V_bias = 0.3 × (W_bias / I_bias)  [quantitative relation]

f_selectivity(E_ion): Higher E_ion → worse selectivity
  20 eV: 20:1
  60 eV: 15:1
  100 eV: 8:1
  
f_selectivity(T): Lower T → better selectivity (oxide protection)
  +40°C: 10:1
  +20°C: 15:1
  0°C: 20:1
  -10°C: 22:1
```

---

## 7.2 Mapping the Process Window

### 7.2.1 2D Operating Contours (Temperature Fixed)

With temperature held constant, visualize (P, W) space:

```
Example operating map (T = 20°C, ArF resist on SiO₂):

Pressure (mTorr) on x-axis
Power (W) on y-axis

Operating contours plotted:

Ashing rate contours (lines of constant rate):

  40 nm/min line: High P, Low W
                 (80 mTorr, 1600 W)
  
  60 nm/min line: Moderate (70 mTorr, 2000 W)
  
  80 nm/min line: Low P, High W
                 (50 mTorr, 2400 W)

Selectivity contours (C/SiO₂):

  20:1 selectivity: High P, Low W
                   (100 mTorr, 1400 W)
  
  15:1 selectivity: Moderate
                   (80 mTorr, 1800 W)
  
  10:1 selectivity: Low P, High W
                   (60 mTorr, 2200 W)

Uniformity regions:

  ±8% uniform: P > 80 mTorr (high pressure, good uniformity)
  ±12% uniform: P = 60-80 mTorr (moderate)
  ±20% uniform: P < 60 mTorr (low pressure, poor uniformity)

Target operating point (example):

  Requirement: 60 nm/min, 15:1 selectivity, ±10% uniformity
  
  Solution region: Intersection of three regions
    - 60 nm/min contour
    - 15:1 selectivity contour
    - ±10% uniformity region
    
  Operating point: P ≈ 75 mTorr, W ≈ 1950 W (at T = 20°C)
  
Robustness analysis:

  If W drifts ±50 W: Rate changes ~5% (±2.5 nm/min)
  If P drifts ±5 mTorr: Selectivity changes ~2:1
  If T drifts ±5°C: Rate changes ~75% (±40 nm/min!) [Major effect]
  
  Temperature most sensitive → temperature control critical
```

---

## 7.3 DOE (Design of Experiments)

### 7.3.1 3-Factor DOE for Recipe Development

Efficiently map parameter space with minimal wafer usage:

```
Factorial DOE: 2³ design (8 experiments)

Three factors, two levels each:
  P: Low (60 mTorr) vs. High (100 mTorr)
  W: Low (1800 W) vs. High (2200 W)
  T: Low (10°C) vs. High (30°C)

Experiment matrix:

Run  P (mTorr)  W (W)   T (°C)   R_etch (nm/min)  S_C/SiO₂
───────────────────────────────────────────────────────
1    60         1800    10       35              22:1
2    60         1800    30       65              15:1
3    60         2200    10       42              20:1
4    60         2200    30       78              12:1
5    100        1800    10       25              25:1
6    100        1800    30       45              18:1
7    100        2200    10       30              23:1
8    100        2200    30       55              16:1

Analysis (main effects):

Main effect of P (average difference Low vs. High):
  R_etch: (35+42+65+78)/4 - (25+30+45+55)/4 = 55 - 39 = +16 nm/min
  (Lower pressure increases rate ~30%)
  
Main effect of W:
  R_etch: (42+78+30+55)/4 - (35+65+25+45)/4 = 51 - 42.5 = +8.5 nm/min
  (Higher power increases rate ~20%)
  
Main effect of T:
  R_etch: (65+78+45+55)/4 - (35+42+25+30)/4 = 60.75 - 33 = +27.75 nm/min
  (Higher temperature increases rate ~84%)
  Temperature DOMINANT EFFECT
  
Interaction analysis:

P×W interaction (does effect of P depend on W?):
  At low W: Low P (51 nm/min) vs. High P (28 nm/min) → +23
  At high W: Low P (60 nm/min) vs. High P (43 nm/min) → +17
  Interaction exists but small (effects independent)
  
P×T interaction:
  At low T: Low P (38.5) vs. High P (27.5) → +11
  At high T: Low P (71.5) vs. High P (50) → +21.5
  Larger interaction (effect of P stronger at high T)

Selectivity correlation:

  Lower P → Higher selectivity (as expected)
  Higher T → Lower selectivity (as expected)
  Combined effect powerful: High P + High T very poor selectivity (12:1)
  
Recipe design:

  Target: 50 nm/min, 18:1 selectivity
  
  From DOE data:
    Point 6: P=100, W=1800, T=30 → R=45, S=18:1 (close!)
    Point 5: P=100, W=1800, T=10 → R=25, S=25:1 (too slow, too selective)
    
  Best candidate: Run 6 (45 nm/min, 18:1 selectivity)
  Enhancement: Increase W to 1900 W to reach 50 nm/min target
  Predicted: R ≈ 50 nm/min, S ≈ 17:1 (acceptable)
```

### 7.3.2 Sensitivity Analysis

Quantify how sensitive the process is to parameter drift:

```
Parameter sensitivity ranking:

Define sensitivity: dR/dx where R = ashing rate, x = parameter

Temperature sensitivity (most important):
  dR/dT = R × (E_a / k × T²) ≈ 0.15 × R / °C
  At 50 nm/min: dR/dT ≈ 7.5 nm/min per °C
  ±3°C drift → ±22.5 nm/min drift (±45% of rate!)
  Conclusion: Temperature control CRITICAL

Pressure sensitivity:
  dR/dP ≈ -0.5 × R / P (mTorr)
  At 50 nm/min, 80 mTorr: dR/dP ≈ -0.31 nm/min per mTorr
  ±10 mTorr drift → ±3.1 nm/min drift (±6% of rate)
  Conclusion: Moderate; pressure control important

Power sensitivity:
  dR/dW ≈ 0.2 × R / W
  At 50 nm/min, 2000 W: dR/dW ≈ 0.005 nm/min per Watt
  ±100 W drift → ±0.5 nm/min drift (±1% of rate)
  Conclusion: Low; power control less critical

Ranking: Temperature >> Pressure > Power
  
Process control implications:

  Temperature: ±1-2°C control required (PID feedback essential)
  Pressure: ±5 mTorr control acceptable
  Power: ±50-100 W acceptable

Selectivity sensitivity:

  Temperature most important (Arrhenius drives selectivity)
  Ion energy (via bias power) secondary
  Pressure tertiary
  
  Strategy: Use temperature for selectivity tuning (no RF change needed)
            Use pressure/power for rate and uniformity
```

---

## 7.4 Recipe Development Workflow

### 7.4.1 Step-by-Step Process

```
Phase 1: Establish Requirements
  Target ashing rate: 60 ± 5 nm/min (wafer throughput requirement)
  Target selectivity: 15 ± 2 :1 (hard mask protection)
  Target uniformity: ±10% across 300mm wafer
  Maximum temperature: 35°C (oxidation/stress limit)
  Minimum selectivity: 12:1 (absolute minimum for safety)

Phase 2: Initial Exploration (8-run 2³ DOE)
  Run matrix as above (60-100 mTorr, 1800-2200 W, 10-30°C)
  Measure ashing time, uniformity, final hardness/damage
  Identify main effects and interactions

Phase 3: Central Composite Design (if needed)
  If DOE results show curvature, add center point + axial points
  Typically 13-point CCD design
  Enables quadratic model (nonlinear effects)

Phase 4: Response Surface Methodology (RSM)
  Fit polynomial model to experimental data:
  R(P, W, T) = a₀ + a₁P + a₂W + a₃T + a₁₁P² + ... (quadratic terms)
  
  Contour plot predicted optimal region
  Run validation experiments in predicted region

Phase 5: Robustness Validation
  Take predicted recipe
  Run 10 consecutive wafers
  Measure rate uniformity (should be ±5%)
  Confirm selectivity maintained (within 2:1)
  Document as baseline recipe

Phase 6: Production Deployment
  Lock recipe on chamber
  Run control wafers weekly
  Monitor ashing time, selectivity, yield
  Adjust only if drift >10% observed
```

---

## 7.5 Summary & Key Takeaways

1. **3D Phase Space Complex** — Ashing rate, selectivity, and uniformity don't scale linearly; interactions and nonlinearities present.

2. **Temperature Dominates** — ~15% rate change per °C; temperature control (±1-2°C) most critical for process consistency.

3. **Pressure-Power Trade-Off** — Lower P faster ashing but poor uniformity; higher P opposite. Optimal ~70-80 mTorr for 3D NAND.

4. **DOE Efficient for Mapping** — 2³ factorial (8 runs) identifies main effects and interactions; CCD adds refinement for nonlinearities.

5. **Sensitivity Ranking Clear** — Temperature >> Pressure > Power; focus control effort on temperature.

6. **Recipe Selectivity Tuning Unique** — Temperature-based tuning allows selectivity adjustment without RF power change; simplifies recipe flexibility.

7. **Robust Operating Regions Exist** — High P regions insensitive to parameter drift; low P regions sensitive but needed for ARDE compensation.

8. **Production Baseline & Monitoring Essential** — Establish baseline on control wafers; monitor weekly for drift; deploy robust recipe first (add tuning later if needed).

---

**Next Chapter:** [Chapter 8 - Chamber Coatings & Surface Protection](./08-chamber-coatings.md)

---

**Chapter 7 Development Status:** Comprehensive process parameter mapping framework  
**Version:** 1.0

