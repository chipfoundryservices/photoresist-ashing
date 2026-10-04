# Chapter 14: Temperature Effects on Ashing

## Overview

**Temperature** is the most sensitive process parameter for photoresist ashing, affecting ashing rate (~15%/°C via Arrhenius), selectivity (polymer protection), and material integrity (oxidation, stress). Unlike RF power adjustments, temperature tuning enables recipe flexibility without changing plasma characteristics. This chapter quantifies temperature effects and demonstrates how to leverage them for selectivity optimization.

**Learning Objectives:**
- Understand Arrhenius temperature dependence of ashing rate (~15%/°C)
- Quantify selectivity changes with temperature
- Recognize polymer formation/decomposition temperature effects
- Understand oxidation kinetics at elevated temperature
- Model thermal stress from CTE mismatch
- Design temperature-based selectivity tuning recipes
- Identify safe operating temperature range for resist integrity

---

## 14.1 Temperature-Dependent Ashing Rate

### 14.1.1 Arrhenius Quantification

Ashing rate follows exponential temperature dependence:

```
Arrhenius equation:

R(T) = R₀ × exp(-E_a / kT)

where:
  R(T) = ashing rate at temperature T
  R₀ = pre-exponential factor
  E_a = activation energy (~12 kcal/mol for C/O₂)
  k = Boltzmann constant (1.987 × 10⁻³ kcal/mol·K)
  T = absolute temperature (Kelvin)

Practical calculation (temperature range for 3D NAND):

T = -10°C (263 K):   R ≈ 35 nm/min (baseline)
T =   0°C (273 K):   R ≈ 40 nm/min (+14% from -10°C)
T = +10°C (283 K):   R ≈ 46 nm/min (+31%)
T = +20°C (293 K):   R ≈ 52 nm/min (+49%)
T = +30°C (303 K):   R ≈ 60 nm/min (+71%)
T = +40°C (313 K):   R ≈ 69 nm/min (+97%, nearly 2×)
T = +50°C (323 K):   R ≈ 79 nm/min (+126%)

Temperature coefficient:

Measured as % change per 1°C:
  From -10 to 0°C:  (+14%) / 10°C ≈ 1.4%/°C
  From 0 to 10°C:   (+15%) / 10°C ≈ 1.5%/°C
  From 20 to 30°C:  (+15%) / 10°C ≈ 1.5%/°C
  Average:          ~1.3-1.5%/°C (~13-15% per 10°C)

Comparison: Temperature vs. other parameters

Temperature:  ±1°C → ±15% ashing rate change (VERY SENSITIVE)
Pressure:     ±5 mTorr → ±6% rate change
Power:        ±50 W → ±1% rate change

Conclusion: Temperature is PRIMARY control parameter
```

### 14.1.2 Activation Energy Analysis

Different materials have different E_a values:

```
Activation energies for oxidative processes in O₂:

Material        E_a (kcal/mol)    Reason
──────────────────────────────────────────
Photoresist     ~12              Weak C-H bonds, aromatic ring
Carbon HM       ~18-20           Stronger sp³ network
SiO₂            ~35-40           Very strong Si-O bonds
Si              ~40-50           Si-Si bonds, plus oxide formation

Temperature sensitivity comparison:

At high E_a, rate increases MORE with temperature

Rate increase from T₁ to T₂:

R(T₂)/R(T₁) = exp[E_a/R × (1/T₁ - 1/T₂)]

For T₁ = 20°C (293 K), T₂ = 40°C (313 K), ΔT = 20°C:

Resist (E_a = 12):  Ratio = exp[12/(1.987×10⁻³) × 0.000203] ≈ 2.1
                    R(40°C) / R(20°C) ≈ 2.1 (110% increase)

SiO₂ (E_a = 38):   Ratio = exp[38/(1.987×10⁻³) × 0.000203] ≈ 3.3
                    R(40°C) / R(20°C) ≈ 3.3 (230% increase!)

Implication:
  SiO₂ etch rate increases MORE than resist rate at high T
  Selectivity C/SiO₂ DEGRADES at high temperature
  At high T: Selectivity loss is inevitable (material science limit)
```

---

## 14.2 Selectivity Temperature Dependence

### 14.2.1 Multiple Competing Temperature Effects

Temperature affects selectivity through several mechanisms:

```
Mechanism 1: Activation energy differences
  Resist E_a ~12 kcal/mol, SiO₂ E_a ~38 kcal/mol
  At high T: Both accelerate, but SiO₂ accelerates more
  Result: Selectivity degrades at high T

Mechanism 2: Polymer protection layer
  Low T: Fluorocarbon or hydrocarbon polymer accumulates
         Acts as protective coating for SiO₂
         Selectivity enhanced: 20-25:1
  
  Moderate T: Polymer balance (some formation, some decomposition)
              Partial protection
              Selectivity moderate: 15-18:1
  
  High T: Polymer decomposes faster than it forms
          No protective layer
          Selectivity poor: 10-12:1

Mechanism 3: Carbon oxidation at high T
  Resist oxidizes to CO₂ more completely at high T
  But oxidation also affects SiO₂ surface layer
  Net effect: Small contribution to selectivity change

Combined temperature effect on selectivity:

T = -10°C:  Selectivity C/SiO₂ ≈ 25-27:1 (excellent)
            Rate: 35 nm/min (slow)
            
T =   0°C:  Selectivity ≈ 22-24:1 (excellent)
            Rate: 40 nm/min
            
T = +10°C:  Selectivity ≈ 20-22:1 (excellent)
            Rate: 46 nm/min
            
T = +20°C:  Selectivity ≈ 18-20:1 (good, production standard)
            Rate: 52 nm/min
            
T = +30°C:  Selectivity ≈ 15-18:1 (acceptable)
            Rate: 60 nm/min
            
T = +40°C:  Selectivity ≈ 12-15:1 (marginal)
            Rate: 69 nm/min
            
T = +50°C:  Selectivity ≈ 10-12:1 (risky!)
            Rate: 79 nm/min (fast)

Selectivity loss mechanism:

T increases 10°C → Selectivity decreases ~10-15%
T increases 20°C → Selectivity decreases ~20-30%
T increases 30°C → Selectivity decreases ~35-50%

Key insight: High T for throughput, low T for selectivity
           No way to have both without trade-off
```

### 14.2.2 Temperature as Selectivity Tuning Knob

Unique advantage: Adjust selectivity without RF power change:

```
Scenario: Need higher selectivity without rate sacrifice

Approach 1: Reduce bias power (lower ion energy)
  Baseline: W_bias = 500 W, S = 12:1, R = 65 nm/min
  Change to: W_bias = 300 W (lower E_ion)
  Result: S = 16:1 (+33% selectivity), R = 50 nm/min (-23% rate)
  Trade-off: Major rate loss (not acceptable for throughput)

Approach 2: Reduce temperature (Arrhenius + polymer effect)
  Baseline: T = 30°C, S = 12:1, R = 60 nm/min
  Change to: T = 10°C (lower by 20°C)
  Result: S = 20:1 (+67% selectivity), R = 45 nm/min (-25% rate)
  Trade-off: Significant rate reduction

Approach 3: Reduce coil power (fewer radicals, slower ashing)
  Baseline: W_coil = 2000 W, S = 12:1, R = 65 nm/min
  Change to: W_coil = 1600 W (lower by 400 W)
  Result: S = 14:1 (+17% selectivity), R = 52 nm/min (-20% rate)
  Trade-off: Modest improvement, reasonable rate loss

Best combination: Multi-parameter optimization

  Baseline recipe:
    P = 70 mTorr, W_coil = 2000 W, W_bias = 450 W, T = 25°C
    Current: S = 14:1, R = 58 nm/min
  
  Target: S = 18:1 with R > 50 nm/min
  
  Adjustment:
    Temperature: 25°C → 10°C (ΔT = -15°C)
      Effect: +20% selectivity (from Arrhenius + polymer)
            -20% rate (from Arrhenius)
    
    Coil power: 2000 W → 2100 W (maintain rate)
      Effect: ~+3% rate (compensate for T reduction)
    
    Bias power: 450 W → 350 W (further selectivity improvement)
      Effect: +15% selectivity (lower ion energy)
            -10% rate
  
  Combined prediction:
    S = 14 × 1.20 × 1.15 = 19.3:1 ≈ 19:1 ✓ (target achieved!)
    R = 58 × 0.80 × 1.03 × 0.90 = 42.9 ≈ 43 nm/min (slower than target)
  
  Refinement: Increase coil by additional 200 W
    Final: S ≈ 19:1, R ≈ 50 nm/min (target achieved!)
  
Benefit: Temperature-based tuning enables selectivity without major rate loss
```

---

## 14.3 Material Integrity & Temperature Limits

### 14.3.1 Carbon Oxidation at Elevated Temperature

At high temperature, carbon substrate oxidizes:

```
Carbon oxidation kinetics:

Reaction: C + O₂ → CO + CO₂ (oxidation)

Oxidation rate vs. temperature:

T = 20°C:  Oxidation ~0.5 nm/hour (very slow)
T = 40°C:  Oxidation ~1-2 nm/hour (slow)
T = 60°C:  Oxidation ~3-5 nm/hour (moderate, significant)
T = 80°C:  Oxidation ~8-15 nm/hour (fast, problematic)
T = 100°C: Oxidation ~20+ nm/hour (very fast)

During ashing (exposure time ~100 seconds = 1.7 minutes):

At T = 20°C:  Oxidation ~0.015 nm (negligible)
At T = 40°C:  Oxidation ~0.05 nm (negligible)
At T = 60°C:  Oxidation ~0.1-0.2 nm (still minimal)
At T = 80°C:  Oxidation ~0.2-0.4 nm (small but measurable)
At T = 100°C: Oxidation ~0.6+ nm (concerning!)

Oxide layer effects:

Thin oxide <1 nm: Acts as protective layer
                  Slows further oxidation (self-passivating)
                  Not a problem

Thick oxide >2-5 nm: Creates barrier to ashing
                     Changes etch dynamics
                     Affects selectivity
                     May leave residue (oxide + carbon)

Production implication:
  Temperature >80°C risks excessive carbon oxidation
  Oxide layer complicates residue removal
  Recommended maximum: T < 70-80°C
  Safe operating range: T < 60°C for minimal oxidation
```

### 14.3.2 Thermal Stress & Mechanical Damage

Temperature changes cause mechanical stress:

```
Thermal stress from CTE mismatch:

Carbon CTE: ~5 ppm/°C (carbon is expansive)
Substrate CTE: ~0.3-3 ppm/°C (Si, SiO₂ much less)
Mismatch: ΔCT = 2-5 ppm/°C

Thermal stress during ashing:

Temperature rise during ashing:
  Ambient start: T₀ = 20°C
  Plasma heat input: ΔT_plasma = 30-50°C
  Electrode temperature: T_electrode = 20°C (maintained by cooling)
  
  But heat penetrates substrate (transient heating)
  Surface temperature during ashing: ~40-60°C (transient)
  
  Net temperature swing: 40°C (from 20 to 60°C)

Stress calculation:

  Thermal stress: σ = E × ΔCT × ΔT
  
  where:
    E = Young's modulus (~100 GPa for carbon)
    ΔCT = CTE mismatch (~5 ppm/°C)
    ΔT = temperature change (~40°C)
  
  σ = 100 × 5×10⁻⁶ × 40 = 20 MPa (significant)

Stress effects:

  Compressive stress ~20 MPa:
    Carbon strength ~1-2 GPa (sufficient margin, 50-100× stronger)
    Risk: LOW for bulk carbon
  
  But at interfaces (adhesion):
    Carbon-substrate interface weaker
    Delamination risk if T cycling large
    Thermal cycling (each wafer): Adds stress
    After 1000 wafers: Cumulative stress ~20 MPa per cycle
    Risk of adhesion failure: MODERATE at high T
  
  Prevention:
    Keep T < 60°C continuous (minimize thermal stress)
    Avoid rapid temperature cycling (ramp slowly)
    Monitor substrate adhesion via periodic inspection

At very high T (>80°C):

  Thermal stress >30 MPa
  Risk of carbon film blistering/delamination
  Device yield loss from mechanical failure
  Production limit: T < 80°C (hard limit)
```

---

## 14.4 Practical Temperature-Based Recipe Optimization

### 14.4.1 Three-Temperature Strategy

Production recipes often use temperature modulation across three steps:

```
Example: Optimize selectivity and throughput via temperature

Base recipe (all steps same pressure/power):
  P = 70 mTorr, W_coil = 2000 W, W_bias = 400 W

STEP 1: High selectivity (conservative, protective)
  Temperature: T = 0°C
  Selectivity: 20:1 (excellent)
  Rate: 40 nm/min (slow)
  Time: 100 seconds
  Depth consumed: 67 nm (most of 80 nm resist)
  
  Goal: Remove bulk resist uniformly, no risk

STEP 2: Transition (balance rate and selectivity)
  Temperature: T = 15°C (gradual warm-up)
  Selectivity: 18:1 (still good)
  Rate: 48 nm/min (moderate)
  Time: 30 seconds
  Depth consumed: 24 nm
  
  Goal: Finish off most remaining resist, maintain selectivity

STEP 3: Fast finish (clean up end)
  Temperature: T = 25°C (warm for final push)
  Selectivity: 15:1 (acceptable for final nm)
  Rate: 55 nm/min (fast)
  Time: 15 seconds
  Depth consumed: 14 nm
  
  Goal: Complete removal, time-limited to avoid over-etch

Total recipe time: 145 seconds (~2.4 min per wafer)

Result:
  Total resist removed: 67 + 24 + 14 = 105 nm (complete)
  Effective selectivity: Weighted average ~18:1 (good!)
  Throughput: ~25 wafers/hour (reasonable)
  Margin: Safe margin throughout (no selectivity risks)

Alternative: Single-step optimized

  Single T = 15°C, same P/W
  Selectivity: 18:1, Rate: 48 nm/min
  Time: 167 seconds (170 sec for 80 nm)
  
  Comparison:
    Multi-step: 145 sec, 18:1 avg selectivity (better uniformity)
    Single-step: 167 sec, 18:1 constant (slower, same selectivity)
    
  Multi-step wins: 15% faster, same selectivity, better uniformity
```

---

## 14.5 Summary & Key Takeaways

1. **Arrhenius Temperature Dependence Strong** — ~15% ashing rate increase per 10°C; most sensitive process parameter; ±1°C variation → ±15% rate variation.

2. **Selectivity Peaks at Low Temperature** — T = 0°C: 22-25:1 selectivity via polymer protection and activation energy advantage; T = 40°C: 12-15:1 (degraded).

3. **Polymer Formation Temperature-Dependent** — Low T: thick polymer (20+ nm), excellent selectivity; high T: thin polymer (<10 nm), faster ashing but poor selectivity.

4. **Activation Energy Differences Drive High-T Selectivity Loss** — SiO₂ E_a ~38 kcal/mol vs. resist ~12 kcal/mol; at high T both accelerate, but SiO₂ faster → selectivity loss.

5. **Carbon Oxidation Accelerates at High T** — >80°C causes 15+ nm/hour oxidation; during ashing (100 sec), <1 nm at 60°C but 0.6 nm at 100°C; limits max T to ~70-80°C.

6. **Thermal Stress from CTE Mismatch** — 40°C temp swing → 20 MPa stress (manageable, but adds to cycling fatigue); >80°C risks delamination from adhesion failure.

7. **Temperature Best Selectivity Tuning Knob** — Lower T without RF power changes enables selectivity adjustment; unique advantage over fluorine etch approaches.

8. **Multi-Step Temperature Recipe Optimal** — Start cold (20:1 selectivity), warm through ashing (15:1 mid-recipe), finish warm (12:1 for final push); balances uniformity and throughput.

---

**End of Part III: Process Phenomena (Chapters 10-14) COMPLETE**

---

**Chapter 14 Development Status:** Comprehensive temperature physics and process control  
**Version:** 1.0

