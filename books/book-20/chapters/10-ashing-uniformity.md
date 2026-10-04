# Chapter 10: Ashing Rate Uniformity & ARDE Effects

## Overview

**ARDE** (Aspect Ratio Dependent Ashing) is the phenomenon where ashing rate varies dramatically with feature size and aspect ratio. In 3D NAND, ashing rates can vary **5-10× from dense features (narrow lines, close-packed) to isolated features (wide openings)**. This chapter quantifies ARDE, develops compensation strategies, and demonstrates multi-step recipes for achieving uniform ashing across complex patterns.

**Learning Objectives:**
- Understand ARDE mechanisms (ion depletion, neutral shadowing, polymer redeposition)
- Quantify ashing rate variation vs. aspect ratio
- Predict ARDE severity from feature geometry
- Develop compensation strategies (pressure modulation, pulsed plasma)
- Design multi-step recipes for deep trenches
- Implement in-situ feedback compensation
- Achieve ±5-10% uniformity across complex patterns

---

## 10.1 ARDE Mechanisms

### 10.1.1 Ion Depletion in High-Aspect-Ratio Features

When features are deep and narrow, ions cannot easily reach the bottom:

```
Geometry:

  Dense trench array:
    Width: 30 nm (narrow)
    Depth: 500 nm (deep)
    Aspect ratio: 500/30 = 16.7:1 (very high)

Ion transport into trench:

  At trench opening (top):
    Ion flux: Full ~10¹⁵ ions/(cm²·s)
    Ashing rate: 70 nm/min (maximum)
  
  At trench middle (250 nm depth):
    Ions must travel down narrow channel
    Ion velocity: ~5-10 km/s (typical, direction downward)
    Trench width: 30 nm (ions must not scatter)
    Mean free path: ~1 mm (at 80 mTorr, much larger than 30 nm)
    Result: Ballistic travel down trench OK (ions reach middle)
    Ion flux: ~80% of initial (~0.8 × 10¹⁵)
    Ashing rate: 60 nm/min (slight reduction)
  
  At trench bottom (500 nm depth):
    Ions have scattered somewhat (collisions with neutral O₂)
    Additional scattering angle: ~5-10° from vertical
    Lateral displacement: 500 nm × tan(7.5°) ≈ 65 nm
    Trench width: 30 nm (ion misses!)
    Ion flux: ~20% of initial (~0.2 × 10¹⁵)
    Ashing rate: 15-20 nm/min (70% reduction!)

Extreme deep (>800 nm):
    Ion depletion severe
    Ion flux: <5% of initial
    Ashing rate: <5-10 nm/min (near zero, starvation)
```

### 10.1.2 Neutral Radical Shadowing

Neutral radicals also have difficulty penetrating deep features:

```
Neutral radical transport:

  Radical velocity: ~500-1000 m/s (thermal velocity in gas)
  Trench geometry: Same 30 nm wide, 500 nm deep
  
  At trench opening:
    Radical flux: ~10¹⁵ radicals/(cm²·s)
  
  Into trench:
    Radicals can enter by diffusion + advection
    But once in trench: Collide with side walls frequently
    MFP in trench: ~30 nm (same size as trench width!)
    Result: Most radicals bounce off side walls
    Probability of reaching bottom: ~(30nm trench width / MFP)^N
    where N = depth / MFP = 500/30 = 16.7
    Probability ~ (1)^16.7 = <1% (extremely low!)
    
Radical flux at bottom:
    Only ~1-5% reaches depth via diffusive transport
    Ashing rate drops 20-50× from surface!
```

### 10.1.3 Polymer Redeposition in Deep Trenches

Ashing byproducts can re-deposit deeper in trench:

```
Byproduct transport:

  During ashing:
    Resist → CO + CO₂ + H₂O + CₓOᵧ fragments
    Fragments move upward (driven by gas flow)
    
  In deep trenches:
    Upward flow slower (constrained geometry)
    Fragments cool and condense (lower temperature deep in trench)
    Partial redeposition: CₓOᵧ polymer coats trench walls
    
  Polymer growth in trench:
    Top 100 nm: Minimal redeposition (hot, fast gas flow)
    Middle (100-300 nm): Moderate redeposition
    Deep (>300 nm): Heavy redeposition (cool, stagnant)
    
  Effect on ashing:
    Polymer layer acts as barrier
    Further ashing of resist beneath polymer slowed
    Ashing rate reduced by 2-3× in deep regions
    
  Cumulative ARDE from all mechanisms:
    Ion depletion: 3-5× reduction
    Radical shadowing: 5-10× reduction
    Polymer redeposition: 2-3× additional reduction
    Total: 5-10× reduction at trench bottom vs. top
```

---

## 10.2 ARDE Prediction & Compensation

### 10.2.1 Quantitative ARDE Models

Empirical and mechanistic models predict ashing rate vs. aspect ratio:

```
Empirical ARDE model:

  R(AR) = R_nominal / (1 + k × AR)
  
  where:
    R_nominal = ashing rate at isolated feature
    AR = aspect ratio (depth/width)
    k = ARDE coefficient (~0.05-0.1 for photoresist in O₂)

Example calculation:

  R_nominal = 60 nm/min (at AR = 0.5, shallow isolated feature)
  k = 0.08
  
  At AR = 5 (mild high-AR):
    R = 60 / (1 + 0.08 × 5) = 60 / 1.4 = 43 nm/min (28% reduction)
  
  At AR = 10 (typical 3D NAND):
    R = 60 / (1 + 0.08 × 10) = 60 / 1.8 = 33 nm/min (45% reduction)
  
  At AR = 20 (deep trench):
    R = 60 / (1 + 0.08 × 20) = 60 / 2.6 = 23 nm/min (62% reduction)

Mechanistic model (ion depletion dominated):

  R(depth) = R_surface × exp(-depth / λ_eff)
  
  where λ_eff = effective ion mean free path in trench
  
  For typical conditions: λ_eff ~100-150 nm
  
  At 500 nm depth:
    R = R_surface × exp(-500/125) = R_surface × exp(-4) ≈ 0.018 × R_surface
    Reduction: 55× (extremely severe!)
    
  This suggests ion depletion is primary ARDE cause
```

### 10.2.2 Pressure Modulation Strategy

Lower pressure improves ARDE by increasing ion range:

```
Effect of pressure on ARDE:

High pressure (100 mTorr):
  - Ion MFP ~0.5 mm (many collisions)
  - Ion depletion severe in high-AR
  - ARDE factor: 5-8×
  - But uniformity good (±8% across pattern)
  
Moderate pressure (70 mTorr):
  - Ion MFP ~0.7 mm (fewer collisions)
  - ARDE factor: 3-5× (improved)
  - Uniformity: ±10-12%
  
Low pressure (40 mTorr):
  - Ion MFP ~1.2 mm (ballistic, ions reach deep)
  - ARDE factor: 1.5-2× (excellent!)
  - Uniformity: ±20-30% (poor, center faster than edge)

Dilemma:

  High P: Uniform but severe ARDE
  Low P: Good ARDE but poor uniformity
  
Solution: Multi-step recipe

  Step 1: High P ashing (80-100 mTorr)
    Goal: Remove 60% of resist uniformly
    Ashing rate: 40 nm/min, ARDE ~4×
    Time: 90 seconds
    Result: 60 nm consumed uniformly
  
  Step 2: Transition pressure (60 mTorr)
    Goal: Remove next 30% with reduced ARDE
    Ashing rate: 50 nm/min, ARDE ~3×
    Time: 30 seconds
    Result: 30 nm consumed
  
  Step 3: Low pressure (40 mTorr, if safe)
    Goal: Remove final 10% and fill deep trenches
    Ashing rate: 70 nm/min, ARDE ~2×
    Time: 10-15 seconds
    Result: Final 10 nm consumed, deep trenches filled
  
  Total time: 130-135 seconds
  Final uniformity: ±8-10% (better than high-P alone)
  ARDE compensation: Effective
```

### 10.2.3 Pulsed Plasma Ashing

Reduce ARDE by cycling plasma on/off:

```
Pulsed plasma principle:

  Normal continuous ashing:
    Plasma on continuously → radicals/ions depleted constantly
    → Severe ARDE (factors 5-10×)
  
  Pulsed approach:
    Plasma on: 0.5 seconds (ashing active)
    Plasma off: 0.5 seconds (no ashing, allows diffusion/rebalancing)
    Repeat
    
  Effect during "off" phase:
    - No fresh ashing, so no additional depletion
    - Radicals/ions can redistribute via diffusion
    - Pressure equalizes between dense and open regions
    - Polymer redeposition reverses partially (thermal decomposition)
    - When plasma turns back on: More uniform radical distribution

ARDE reduction by pulsing:

  Continuous: ARDE factor 6× (dense 60 nm/min, isolated 10 nm/min)
  Duty cycle 50% (0.5s on/off): ARDE factor 3× (dense 40 nm/min, isolated 13 nm/min)
  Duty cycle 25% (0.25s on/0.75s off): ARDE factor 1.5× (dense 20 nm/min, isolated 13 nm/min)
  
  Trade-off:
    Lower duty cycle → Better ARDE
    BUT: Longer total time (process slower)
    Example: 80 nm resist @ 30 nm/min duty-cycle-50%
            → 160 seconds (2.67 min) vs. 80 sec continuous
            → 2× longer ashing time per wafer
            → Throughput cut in half

Production practice:
  Some tools offer pulsed mode for critical layers
  Most use multi-step pressure modulation (simpler, similar ARDE reduction)
```

---

## 10.3 In-Situ Feedback Compensation

### 10.3.1 Real-Time Ashing Rate Monitoring

Detect when ashing is complete or when ARDE is problematic:

```
Monitoring approach:

  Endpoint detection (discussed in Chapter 4):
    Optical: C₂ emission drops when carbon depleted
    Electrical: Reflected power changes as plasma conductivity shifts
    Combined: Multi-sensor endpoint
    
  Rate feedback (continuous monitoring):
    Measure etch time for known resist thickness
    Compare to expected time
    If actual > expected: Rate slower than target
    If actual < expected: Rate faster than target
    
  ARDE feedback:
    Run test structure with features of different AR
    After ashing: Measure remaining resist thickness (TEM or ellipsometry)
    Dense feature: Thin (over-etched)
    Isolated feature: Thick (under-etched)
    Difference: Quantifies ARDE severity

Control algorithm:

  If ARDE detected (dense much thinner than isolated):
    
    Option 1: Adjust pressure mid-ashing
      Reduce pressure (shift toward low-P: better ARDE)
      Causes rate to increase (faster ashing)
      Isolated features catch up
    
    Option 2: Adjust ion energy (bias power)
      Reduce bias (lower ion energy)
      Reduces ion assistance (lowers ashing rate)
      But affects selectivity (may worsen it)
      Less preferred than pressure modulation
    
    Option 3: Extend total ashing time
      Accept ARDE, continue until isolated features catch up
      Risk: Dense features over-etched (damage to hard mask)
      Only viable if selectivity margin sufficient

Feedback control loop:

  Measure endpoint optical/electrical signals
  Compare actual endpoint time to baseline
  If deviation >±5%:
    Adjust pressure or power for next wafer
    Run control wafer to verify
    Lock recipe if now on target
    
  Repeat weekly with fresh control wafers
  Predictive maintenance: If drift consistent, schedule electrode cleaning
```

---

## 10.4 Multi-Step Recipes for Deep Trenches

### 10.4.1 3-Step Recipe Example

Production recipe balancing uniformity, ARDE, and throughput:

```
Target:
  Ashing 80 nm ArF resist on carbon hard mask
  Feature mix: Dense (5 nm isolated to 30 nm wide features)
             + Isolated (50-200 nm wide openings)
  Trench depth: 500 nm (after hard mask etch)
  AR range: 1.7:1 (shallow openings) to 100:1 (narrow dense trenches)
  
Requirement:
  Uniformity: ±10% across wafer
  Selectivity: >8:1 (C / hard mask)
  No over-etch: <5 nm damage to hard mask

Recipe design (3-step):

STEP 1: High Selectivity, Moderate ARDE
  Pressure: 80 mTorr (high, for uniformity + selectivity)
  Coil power: 1800 W (moderate)
  Bias power: 300 W (low ions, excellent selectivity)
  Temperature: 20°C (baseline)
  Time: 100 seconds
  
  Predicted results:
    Ashing rate center: 40 nm/min
    Ashing rate edge: 38 nm/min (minimal pressure gradient)
    Depth consumed: ~67 nm (nearly all of 80 nm resist)
    Residue after Step 1: ~25-30 nm CₓOᵧ (high selectivity → more residue)
    
  ARDE status:
    Isolated features (wide openings):
      AR ~1.7:1, little ARDE
      Remaining resist: ~3 nm (almost gone)
    Dense trenches:
      AR ~100:1, severe ARDE during step
      But low pressure (~80 mTorr) helps
      Remaining resist: ~8-12 nm (still significant)

STEP 2: Transition (Balance Rate & Selectivity)
  Pressure: 60 mTorr (lower, to help deep features)
  Coil power: 2000 W (slight increase)
  Bias power: 400 W (moderate ions)
  Temperature: 20°C
  Time: 40 seconds
  
  Predicted results:
    Ashing rate: ~50-55 nm/min
    Depth consumed: ~35-40 nm (at average)
    
  ARDE compensation:
    Lower pressure helps deep trenches
    Dense trenches: Remaining ~5-8 nm
    Isolated: Nearly complete (some over-etch on top)

STEP 3: Fast Finish (Complete Deep Features)
  Pressure: 50 mTorr (low, ballistic regime)
  Coil power: 2000 W
  Bias power: 500 W (moderate ions, helps residue removal)
  Temperature: 25°C (slight temp increase to help decomposition)
  Time: 20 seconds
  
  Predicted results:
    Ashing rate: ~65-70 nm/min average
    Depth consumed: ~20-25 nm
    
  Final status:
    Dense trenches: <2 nm remaining (complete, within selectivity margin)
    Isolated features: Clean (may be slight over-etch, but width ~50 nm, so damage <2 nm)
    Selectivity maintained: No hard mask damage
    
Total recipe time: 160 seconds (~2.7 minutes per wafer)

Final uniformity:
  Center (isolated): 80 nm consumed cleanly
  Edge (isolated): 78 nm consumed (slight edge effect, ±2%)
  Dense trenches: 75-80 nm consumed (deep features filled, ±8%)
  Overall: ±8-10% (meets target)
```

---

## 10.5 Summary & Key Takeaways

1. **ARDE Severe in 3D NAND** — 5-10× ashing rate variation from dense to isolated features due to ion depletion, radical shadowing, and polymer redeposition.

2. **Ion Depletion Dominant** — Ions cannot penetrate deep trenches (ballistic in narrow channels); bottom of 500 nm trench gets <20% of ion flux from top.

3. **Neutral Shadowing Significant** — Radicals also blocked by side walls in high-AR features; diffusive transport insufficient.

4. **Polymer Redeposition Complicates Deep Trenches** — Byproducts redeposit in deep cool regions, adding 2-3× additional ashing rate reduction.

5. **Pressure Modulation Effective** — Lower pressure improves ARDE (ions reach deeper) but worsens uniformity (edge slower than center). Multi-step recipes balance both.

6. **Pulsed Plasma Reduces ARDE** — Cycling plasma on/off allows radical/ion redistribution. 50% duty cycle achieves ~3× ARDE reduction vs. 6× continuous, but doubles ashing time (throughput trade-off).

7. **Multi-Step Recipe Best Practice** — Three steps optimal: (1) High selectivity/pressure, (2) Transition, (3) Low pressure/fast finish. Balances uniformity, ARDE, and selectivity.

8. **In-Situ Feedback Prevents Over-Etch** — Optical + electrical endpoint detection combined with regular control wafer checks catches ARDE issues before hard mask damage occurs.

---

**Next Chapter:** [Chapter 11 - Ion Energy & Plasma Density Control](./11-ion-energy-control.md)

---

**Chapter 10 Development Status:** Comprehensive ARDE physics and compensation framework  
**Version:** 1.0

