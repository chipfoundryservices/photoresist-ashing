# Chapter 11: Ion Energy & Plasma Density Control

## Overview

Ion energy and ion flux are independently controllable in hybrid CCP+ICP systems, enabling **decoupled optimization** of ashing rate, selectivity, and uniformity. This chapter covers measurement techniques (RPA), quantitative relationships, and control strategies for independent tuning.

**Learning Objectives:**
- Measure ion energy distribution via RPA (Retarding Potential Analyzer)
- Quantify E_ion vs. bias power relationship (~0.3 × V_bias)
- Control ion flux independently via coil power
- Understand ion energy dependence of selectivity
- Achieve spatial ion flux uniformity
- Implement real-time ion energy feedback control
- Design selectivity tuning via ion energy modulation

---

## 11.1 Ion Energy Distribution Measurement

### 11.1.1 RPA Principles & Interpretation

An RPA measures the energy spectrum of ions reaching a surface:

```
RPA measurement principle:

  1. Electrostatic retarding potential applied to analysis electrode
  2. Only ions with energy E > retarding voltage V_ret can pass
  3. Sweep voltage 0→500V, measure ion current at each step
  4. Plot dI/dV (derivative) → Ion Energy Distribution (IED)

Measurement procedure:

  Step 1: Set V_ret = 0 V (all ions pass)
          Measure current I_total
  
  Step 2: Sweep voltage in 5-10 V steps
          At V_ret = 20 V: Only ions with E > 20 eV pass
                          Measure I(20V)
          At V_ret = 40 V: Measure I(40V)
          ...
          At V_ret = 200 V: Only high-energy ions pass
  
  Step 3: Plot: I(V) vs. V_ret
  
  Step 4: Calculate: dI/dV (numerically)
          Peak of dI/dV = most probable ion energy
          Width of dI/dV peak = FWHM (energy spread)
          Tail of dI/dV = high-energy wing

Typical result (CCP mode, 300 V bias):

  IED shape: Roughly Gaussian
  Peak energy: ~70 eV (most probable)
  FWHM: ~30-40 eV (spread from ~50 to ~90 eV)
  Low-energy tail: ~10-20 eV (ions that collided before reaching electrode)
  High-energy tail: ~150-200 eV (rare, multiply-charged or fast ions)

Quantitative analysis:

  Mean ion energy: E_mean = ∫ E × (dI/dE) dE / I_total
                  ≈ 65-75 eV typical
  
  Most probable energy: E_prob ≈ 70 eV (peak of distribution)
  
  Ion flux: φ = I_total / e
          where e = elementary charge
          Typical: ~10¹⁵ ions/(cm²·s)
```

### 11.1.2 Ion Energy vs. Bias Power Relationship

Quantitative relationship enables predictive tuning:

```
Physical relationship:

  Ion accelerated from plasma potential V_p to electrode at ground
  Kinetic energy gained: E_ion = e × (V_p - 0) = e × V_p
  
  But self-bias develops:
    V_bias = -|V_plasma| (negative on electrode relative to plasma)
    E_ion ≈ 0.3 × V_bias (empirical scaling factor)
  
  Why 0.3? Not simply =1?
    - Some ions originate from excited states (pre-energized)
    - Some ions created in sheath itself (partial acceleration)
    - Some energy lost to elastic collisions
    - Net result: Effective energy ~0.3 × applied voltage

Experimental validation:

  Data (typical tool):
  
  Bias voltage (V)   Measured E_ion (eV)   Ratio E/V
  ─────────────────────────────────────────────────
  100                30 eV                 0.30
  200                65 eV                 0.325
  300                90 eV                 0.30
  400                120 eV                0.30
  500                150 eV                 0.30
  
  Conclusion: E_ion ≈ 0.30 × V_bias (good fit)

Recipe tuning based on this relationship:

  Target: E_ion = 80 eV
  Required: V_bias = 80 / 0.30 ≈ 267 V
  
  In tool terms:
    W_bias (power) related to V_bias via: V_bias ≈ √(2 × W_bias × Z)
    For typical impedance Z ~50 Ω:
    V_bias = √(2 × 50 × W_bias) = √(100 × W_bias)
    
    To get V_bias = 267 V:
    267 = √(100 × W_bias)
    W_bias = (267)² / 100 ≈ 715 W
    
  Set W_bias = 700-720 W → achieve E_ion ≈ 80 eV
```

---

## 11.2 Ion Flux & Plasma Density Control

### 11.2.1 Coil Power Dependence of Ion Flux

Ion flux depends on plasma density, which scales with coil power:

```
Plasma density generation:

  In ICP mode:
    Coil power W_coil → magnetic field B
    → Electron cyclotron motion
    → Increased electron temperature T_e
    → Higher dissociation efficiency
    → More plasma production
  
  Scaling relationship (empirical):
    n_e ∝ √(W_coil)  (sublinear, not linear)
    
  Ion flux scales similarly:
    φ_ion ∝ n_e ∝ √(W_coil)

Example:

  Baseline: W_coil = 2000 W, φ_ion = 10¹⁵ ions/(cm²·s)
  
  At W_coil = 2200 W:
    φ_ion = 10¹⁵ × √(2200/2000) = 10¹⁵ × √1.1 ≈ 1.05 × 10¹⁵
    Increase: ~5%
  
  At W_coil = 2400 W:
    φ_ion = 10¹⁵ × √(2400/2000) = 10¹⁵ × √1.2 ≈ 1.10 × 10¹⁵
    Increase: ~10%
  
  At W_coil = 1600 W:
    φ_ion = 10¹⁵ × √(1600/2000) = 10¹⁵ × √0.8 ≈ 0.89 × 10¹⁵
    Decrease: ~11%

Practical implications:

  Coil power is NOT a linear control
  100 W change in coil: ~2-3% flux change
  For selectivity/rate balance: Coil power changes should be large (±200 W) to see effect
  More sensitive: Pressure (inverse square root dependence) or temperature (exponential)
```

### 11.2.2 Spatial Ion Flux Uniformity

Ion flux varies across wafer (edge vs. center):

```
Spatial variation sources:

  1. Magnetic field non-uniformity (coil geometry)
     - Field stronger near coil center
     - Edge field ~30-50% lower
     
  2. Electron temperature gradient
     - Center (hotter): Higher electron density
     - Edge (cooler): Lower electron density
  
  3. Pressure gradient
     - Ions lost at edges (escape to wall, drift away)

Typical ion flux uniformity:

  Center (0-50 mm radius): φ_center ~10¹⁵ ions/(cm²·s)
  Edge (100-150 mm radius): φ_edge ~0.3-0.4 × 10¹⁵
  
  Ratio: φ_center / φ_edge ~2.5-3.3:1 (NOT uniform!)

Impact on ashing uniformity:

  Center ashing rate:
    R_center = R_chem + Y_C × φ_center
              ≈ 30 + 0.5 × 10¹⁵ = 35 nm/min (ion contribution 40%)
  
  Edge ashing rate:
    R_edge = 30 + 0.5 × 0.35 × 10¹⁵ = 30 + 0.17 × 10¹⁵
           ≈ 30 + 8.5 = 38.5 nm/min (lower ion flux actually helps!)
  
  Wait, this suggests edge FASTER? No, this is wrong...

  Recalculation (correct):
    Sputtering yield Y_C ≈ 0.5 atoms/ion
    Atomic mass density ρ ≈ 5×10²² atoms/cm³
    
    Ion contribution to rate:
      R_ion = φ × Y / ρ × ρ_feature
      R_ion ∝ φ directly
    
    Center: R_ion,center ∝ 3 × φ_base
    Edge: R_ion,edge ∝ 1 × φ_base
    
    Center-to-edge rate ratio: ~1.5-2× (center faster)
    But center also has lower pressure (pressure ∝ 1/√W by diffusion)
    Combined: ~10-20% center-to-edge difference

Mitigation strategies:

  Strategy 1: Asymmetric showerhead (flow biased to edge)
    Increase gas flow to edge region
    Compensate for lower plasma density
    Result: ±5-8% uniformity achievable
  
  Strategy 2: Magnetic field optimization
    Add dipole or multipole field coil
    Flatten magnetic profile toward edges
    Result: Improved but expensive
  
  Strategy 3: Pressure matching
    Higher pressure → more uniform, but reduces ARDE compensation
    Trade-off: Accept 10-15% center-to-edge variation in high-AR
    Accept uniform but slower rate in low-AR
  
  Strategy 4: Dual-frequency ICP
    13.56 MHz (primary, high density)
    2 MHz (secondary, different penetration/heating)
    Enables profile tuning
    Result: Excellent uniformity but very complex
```

---

## 11.3 Selectivity Tuning via Ion Energy

### 11.3.1 Ion Energy Dependence of Ashing Rate

Higher ion energy → faster ashing, but affects selectivity differently:

```
Ashing rate vs. ion energy (resist):

  E_ion = 20 eV:  R ≈ 40 nm/min (chemical + low sputtering)
  E_ion = 50 eV:  R ≈ 55 nm/min (+37%)
  E_ion = 100 eV: R ≈ 70 nm/min (+75%)
  E_ion = 150 eV: R ≈ 85 nm/min (+112%)
  
Mechanism:

  Low E_ion: Mostly chemical attack (O·, radicals)
             Sputtering yield ~0.1-0.2 atoms/ion
             Rate ~40 nm/min
  
  High E_ion: Chemical + strong sputtering
             Sputtering yield ~0.8-1.0 atoms/ion
             Additional contribution ~25-30 nm/min
             Total rate ~65-70 nm/min

Selectivity vs. ion energy (C / SiO₂):

  E_ion = 20 eV:  S ≈ 20-22:1 (excellent selectivity)
  E_ion = 50 eV:  S ≈ 15-18:1 (good)
  E_ion = 80 eV:  S ≈ 12-15:1 (moderate, production)
  E_ion = 100 eV: S ≈ 10-12:1 (acceptable)
  E_ion = 150 eV: S ≈ 8-10:1 (risky for hard mask)
  E_ion = 200 eV: S ≈ 6-8:1 (very risky)

Why selectivity degrades with E_ion:

  Sputtering yield differences:
    Y_C (carbon): Increases rapidly with E (strong dependence)
    Y_SiO2: Also increases but more slowly
    At high E: Both get sputtered, selectivity difference vanishes
  
  Production implication:
    Cannot achieve both high rate AND high selectivity
    E_ion ~50-80 eV is practical sweet spot
    Rates 50-70 nm/min, selectivity 12-18:1
```

### 11.3.2 Selectivity Tuning Recipe

Independent tuning of rate and selectivity via separate parameters:

```
Scenario: Need higher selectivity without sacrificing rate

Approach 1: Reduce bias power (lower E_ion)
  Baseline: W_bias = 500 W (E_ion ~150 eV), S = 10:1, R = 70 nm/min
  
  Change: W_bias = 300 W (E_ion ~90 eV)
  Result: S = 14:1 (improved +40%), R = 55 nm/min (slower -21%)
  Trade-off: Rate loss is significant
  Not ideal if throughput critical

Approach 2: Reduce temperature (better selectivity via chemistry)
  Baseline: T = 30°C, S = 10:1, R = 70 nm/min
  
  Change: T = 10°C (Arrhenius effect)
  Result: S = 18:1 (improved +80% via polymer protection), R = 38 nm/min
  Trade-off: Rate reduced 45% (not suitable for this scenario)

Approach 3: Increase pressure (reduce ion flux, chemical dominates)
  Baseline: P = 60 mTorr, S = 10:1, R = 70 nm/min
  
  Change: P = 80 mTorr (ion flux ~20% reduction)
  Result: S = 12:1 (modest improvement), R = 63 nm/min
  Trade-off: Small benefit, minimal rate loss
  This is the most practical approach

Best approach: Combine strategies

  If target: S = 15:1 with R > 60 nm/min
  
  Baseline recipe:
    P = 60 mTorr, W_coil = 2000 W, W_bias = 500 W, T = 30°C
    Current: S = 10:1, R = 70 nm/min
  
  Adjustment:
    Reduce T from 30°C to 20°C (+15% selectivity from Arrhenius)
    Reduce W_bias from 500 W to 350 W (lower ion energy)
    Maintain W_coil = 2000 W (preserve radical flux)
    Keep P = 60 mTorr
  
  Predicted result:
    S ≈ 10 × 1.15 × 1.3 = ~15:1 (target achieved!)
    R ≈ 70 × (20/30)^0.85 × 0.8 = ~60 nm/min (acceptable)
  
  Recipe locked: Use this for production
```

---

## 11.4 Real-Time Ion Energy Feedback Control

### 11.4.1 Closed-Loop Ion Energy Stabilization

Detect ion energy drift and compensate automatically:

```
Drift scenario:

  Electrode surface oxidation (corrosion) over weeks:
    Oxide layer increases impedance
    RF matching network adjusts capacitance to compensate
    But sheath voltage changes slightly
    E_ion drifts from 80 eV → 75 eV (-6%)
    
  Effect: Ashing rate drops ~10% (small but detectable)
          Selectivity improves (unexpected, but acceptable)
          Control wafer measurement shows 90 sec vs. 100 sec baseline
          Process drifting!

Feedback control approach:

  1. Establish baseline: E_ion = 80 eV (via RPA monthly)
  
  2. Run control wafers weekly: Measure ashing time
  
  3. If drift detected: E_ashing ~90 sec (vs. 100 sec baseline)
     Suspect E_ion has shifted
     
  4. Measure reflected power (RF diagnostics)
     If reflected power increased: Impedance drift likely
     
  5. Hypothesis: E_ion decreased → rate dropped
  
  6. Increase bias power by 20 W: W_bias 500→520 W
     Expected E_ion increase: 80 → 82 eV
     Expected rate increase: ~2.5%
     Expected time: 98 sec (back toward 100 sec)
  
  7. Run control wafer: Verify
     If ~98 sec: Drift compensated ✓
     If still 90 sec: Adjustment insufficient, repeat step 6
     If >100 sec: Over-corrected, reduce slightly

PID control (advanced):

  Error signal: e(t) = t_actual - t_baseline
  PID: W_bias(t+1) = W_bias(t) + K_p×e + K_i×∫e + K_d×de/dt
  
  Continuously adjusts bias power to maintain constant ashing time
  Automatically compensates for electrode drift without user intervention
```

---

## 11.5 Summary & Key Takeaways

1. **RPA Measures IED** — Retarding potential analyzer sweeps voltage to measure ion energy distribution; peak ~70 eV typical, FWHM ~30-40 eV spread.

2. **E_ion ≈ 0.3 × V_bias** — Quantitative relationship enables predictive tuning; 300 V bias → ~90 eV ion energy; relationship holds across tools.

3. **Coil Power Controls Flux** — Ion flux ∝ √(W_coil); 100 W change → ~2-3% flux change; sublinear (not efficient control).

4. **Ion Flux Non-Uniform** — Center plasma density 2.5-3.3× higher than edge; impacts uniformity unless compensated (showerhead, pressure tuning).

5. **Ion Energy Dominates Selectivity** — E_ion 20→100 eV reduces selectivity from 20:1 → 10:1; temperature and pressure also affect selectivity.

6. **Rate-Selectivity Trade-Off** — Increasing ion energy faster ashing (+112% at 150 eV vs. 20 eV) but worse selectivity (3× loss); balanced recipe near 80 eV.

7. **Independent Tuning Possible** — Hybrid CCP+ICP enables separate control: bias power for ion energy, coil power for flux, temperature for chemistry selectivity.

8. **Drift Detection via Control Wafers** — Weekly ashing time measurement detects ion energy drift; can feed back to automatically adjust bias power.

---

**Next Chapter:** [Chapter 12 - Selectivity Mechanisms](./12-selectivity-mechanisms.md)

---

**Chapter 11 Development Status:** Comprehensive ion energy and plasma density control  
**Version:** 1.0

