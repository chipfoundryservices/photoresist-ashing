# Chapter 4: Ashing Chemistries & Gas Selections

## Overview

While **pure O₂ plasma ashing** dominates production (>90% of 3D NAND processes), alternative gas chemistries exist for specialized applications. This chapter surveys gas options, their selectivity/rate trade-offs, endpoint detection strategies, and integration considerations.

**Learning Objectives:**
- Understand pure O₂ ashing as production baseline
- Evaluate alternative chemistries (fluorine, hydrogen, nitrogen blends)
- Quantify gas mixture effects on rate and selectivity
- Design endpoint detection for different chemistries
- Assess cost and safety/environmental trade-offs
- Select optimal chemistry for specific integration scenarios

---

## 4.1 Pure Oxygen Plasma Ashing – Production Standard

### 4.1.1 Why O₂ Dominates

Pure oxygen ashing is by far the most common choice:

```
Advantages of O₂:

1. Safety & Handling
   - Non-toxic (air-like)
   - No special storage or handling (unlike F₂ or Cl₂)
   - OSHA-friendly
   - Chamber materials less critical (less corrosive than halogens)

2. Simplicity
   - Single gas source (no mixing, no blending)
   - RF system straightforward (standard 13.56 MHz)
   - Cost-effective (oxygen cheap, commodity supply)

3. Selectivity Mechanisms
   - Natural selectivity to SiO₂ (already oxidized)
   - Metal oxides form protective layers (slow further oxidation)
   - Resist is primary carbon target

4. Environmental
   - No toxic byproducts (CO₂, CO, H₂O are safe)
   - No ozone risk (unlike some fluorine processes)
   - Exhaust easily handled (standard abatement)

Disadvantages:

1. Speed vs. Selectivity Trade-Off
   - Cannot achieve both high rate AND high selectivity simultaneously
   - Must choose: fast (risky selectivity) or selective (slow)

2. Residue Formation
   - Incomplete oxidation creates CₓOᵧ residue (~10-20 nm typical)
   - Post-ashing cleanup required (thermal annealing or O₂ plasma)
   - Adds process time and complexity

3. Ion Energy Control Challenging
   - Ions (O⁺, O₂⁺) must be controlled precisely
   - Small changes in bias power → large selectivity changes
   - Recipe robustness difficult at high selectivity targets
```

### 4.1.2 Typical O₂ Process Parameters

Production recipes commonly use:

```
Standard O₂ ashing recipe (ArF resist, SiO₂ underlayer):

Pressure:        50-100 mTorr  (typical 70 mTorr)
Coil power:      1500-2500 W   (typical 2000 W)
Bias power:      200-600 W     (typical 400 W)
Temperature:     15-35°C       (typical 20°C)
Gas flow:        100-300 sccm  O₂ (typical 150 sccm)
Chamber type:    CCP or hybrid CCP+ICP

Resulting ashing rate: 50-70 nm/min
Resulting selectivity: 12-18:1 (C / SiO₂)
Etch time for 80 nm resist: ~90-150 seconds
Residue after ashing: ~15 nm CₓOᵧ

Post-ashing residue removal:
  Thermal annealing: 120°C × 45 min → 80% removal
  O₂ plasma: 5-10 min → 90% removal
  Total time: 50-60 min per batch (major cost driver)
```

---

## 4.2 Alternative Chemistries for Specialized Applications

### 4.2.1 Fluorine-Based Resist Stripping

For aggressive applications where selectivity to carbon (hard mask) is critical:

```
F₂ or CF₄/O₂ mixtures:

Chemistry:
  F· radical attacks resist C-H bonds (similar to O·)
  CF₄ + O₂ dissociation produces F· and O·
  
  Advantages:
    - Extremely fast ashing rates (100-200 nm/min!)
    - High selectivity to carbon hard mask (20-50:1)
    - Less residue formation (more complete decomposition)
  
  Disadvantages:
    - Electrode corrosion severe (F₂ attacks most metals)
    - Chamber wall damage (corrosive byproducts)
    - Toxic gas handling (F₂ hazardous)
    - Equipment cost doubled (corrosion-resistant materials)
    - Not compatible with standard resist ashing chambers

Application:
  Very specialized (research only in most fabs)
  Used occasionally for non-standard multilayer stacks
  NOT production-mainstream for 3D NAND
```

### 4.2.2 Hydrogen-Based Chemistries

Occasionally used for reducing conditions:

```
H₂/Ar or H₂/N₂ chemistries:

Mechanism:
  H· radicals attack C-H and C-C bonds (non-oxidative)
  Produces hydrocarbons (CH₄, C₂H₆, etc.) - gaseous, evacuated
  
  Advantages:
    - Non-oxidizing (metals are NOT oxidized)
    - Good for integrated metal removal (if metals present)
  
  Disadvantages:
    - Slower ashing rates (30-50 nm/min)
    - Poor selectivity (all carbon attacked equally)
    - Hydrogen safety (flammability concerns)
    - Chamber materials compatible but exotic

Application:
  Rare; mainly for specific multilayer structures
  Not suitable for 3D NAND (metal layers require protection)
```

### 4.2.3 Nitrogen-Containing Mixtures

O₂/N₂ or other combinations for selectivity tuning:

```
O₂/N₂ mixtures:

Chemistry:
  N₂ doesn't directly participate (inert diluent)
  Lowers radical concentration, slows ashing
  
  Effect of adding N₂:
    0% N₂:     Rate 60 nm/min, selectivity 15:1
    20% N₂:    Rate 45 nm/min, selectivity 18:1
    40% N₂:    Rate 30 nm/min, selectivity 22:1
    60% N₂:    Rate 15 nm/min, selectivity 25:1
  
  Advantage: Selectivity improves (via lower radical concentration)
  Disadvantage: Rate becomes impractically slow
  
  Production use: Almost never (can achieve same via temperature)

O₂/Ar mixtures:

  Argon used for ion bombardment assistance
  Ar⁺ provides sputtering complement to O· chemistry
  
  Mixture 90% O₂ / 10% Ar:
    Rate: 65 nm/min (slight increase from better ion contribution)
    Selectivity: 12:1 (slight degradation, more Ar⁺)
  
  Production use: Rare (coil power adjustment achieves same)
```

---

## 4.3 Selectivity Enhancement Strategies

### 4.3.1 Recipe Optimization for Selectivity

Multi-parameter tuning to achieve high selectivity in pure O₂:

```
Strategy 1: Temperature-Based
  Baseline recipe parameters, tune only temperature
  
  T = 0°C:   Rate 35 nm/min, selectivity 25:1
  T = 20°C:  Rate 50 nm/min, selectivity 18:1
  T = 40°C:  Rate 75 nm/min, selectivity 10:1
  
  Advantage: No other parameter change (robust)
  Trade-off: Slower ashing at high selectivity

Strategy 2: Pressure Modulation
  Lower pressure → higher ion energy → worse selectivity
  Higher pressure → lower ion energy → better selectivity
  
  At 2000W coil, 400W bias:
  
  P = 40 mTorr:   Rate 75 nm/min, selectivity 8:1 (fast)
  P = 80 mTorr:   Rate 55 nm/min, selectivity 15:1 (balanced)
  P = 120 mTorr:  Rate 35 nm/min, selectivity 22:1 (selective)
  
  Advantage: Allows rate/selectivity trade-off
  Trade-off: Impacts uniformity (pressure affects gas distribution)

Strategy 3: Ion Energy Control
  Lower bias power → lower E_ion → better selectivity
  
  Bias = 200W:  E_ion ~60 eV, selectivity 20:1, rate 40 nm/min
  Bias = 400W:  E_ion ~120 eV, selectivity 12:1, rate 60 nm/min
  Bias = 600W:  E_ion ~180 eV, selectivity 8:1, rate 75 nm/min
  
  Advantage: Direct selectivity control
  Trade-off: Impacts ashing uniformity (ion-driven ARDE compensation)

Multi-Step Recipe (Best Practice):

  Step 1: High selectivity etch
    P = 80 mTorr, Coil = 1800W, Bias = 300W, T = 15°C
    Selectivity: 20:1, Rate: 35-40 nm/min
    Time: 200-250 sec for 80 nm resist
    Residue: 25-30 nm (high)
    
  Step 2: Transition
    P = 60 mTorr, Coil = 2000W, Bias = 400W, T = 25°C
    Selectivity: 15:1, Rate: 50-60 nm/min
    Time: 30-50 sec
    Residue: 15-20 nm
    
  Step 3: Fast finish (if selective enough)
    P = 50 mTorr, Coil = 2200W, Bias = 500W, T = 30°C
    Selectivity: 10:1, Rate: 70-80 nm/min
    Time: 20-30 sec
    Residue: 10-15 nm
    
  Total time: 250-330 sec (~5-6 min per wafer)
  Selectivity maintained: Never below 10:1
  Final residue: ~10-15 nm (manageable post-ashing)
```

---

## 4.4 Endpoint Detection

### 4.4.1 Optical Endpoint Detection

Carbon depletion can be detected via optical emission:

```
Principle:

  Measure emitted light from plasma at specific wavelengths
  Different species emit at different wavelengths:
  
  Species          Wavelength    Emitted by?
  ──────────────────────────────────────
  C₂ (Swan bands)  ~500 nm       Carbon products (Swan bands)
  O(³P)            ~703.7 nm     Atomic oxygen (line)
  O₂               ~760 nm       Molecular oxygen (O₂ emission)

Carbon depletion detection:

  During ashing: C₂ emission from resist carbon products
    Signal ~200 mV (high)
  
  Approaching endpoint: Less carbon available
    C₂ signal drops ~50-70% (to ~50-100 mV)
  
  At endpoint: No more resist
    C₂ signal drops to ~10 mV (baseline noise)
  
Algorithm:

  1. Baseline measurement: Record C₂ level at start
  2. Monitor continuously: C₂ intensity vs. time
  3. Threshold trigger: When C₂ drops to 30% of initial
  4. Confirm: Multiple sensor reads (avoid noise spikes)
  5. Stop plasma at confirmed endpoint

Advantages:
  - Real-time detection (no delay)
  - Optical direct measurement (non-invasive)
  - Works with all gases (O₂, F₂, etc.)

Disadvantages:
  - Tool-to-tool variation (optical path different)
  - Resist thickness dependent (thick resist = longer time to endpoint)
  - False positives possible (plasma instability, line fluctuation)
```

### 4.4.2 Electrical Endpoint Detection

Plasma impedance changes as resist disappears:

```
Principle:

  Measure RF reflected power from plasma
  Reflected power correlates to impedance mismatch
  Resist depletion changes plasma conductivity
  
Mechanism:

  With resist present:
    - Ashing removes carbon (low conductivity)
    - Plasma conductivity partially limited by resist byproducts
    - Reflected power ~30-50 mV (moderate)
  
  As resist depletes:
    - Fewer carbon byproducts
    - Plasma conductivity increases (purer O plasma)
    - Reflected power increases to ~100-150 mV
  
  At endpoint:
    - Reflected power spike indicates clean plasma
    - Endpoint confirmed when spike threshold reached

Advantages:
  - Electrical measure (robust, no optical issues)
  - Complements optical (different physical basis)
  - Less tool-to-tool variation (RF standard)

Disadvantages:
  - Slower response than optical (~1-2 sec lag)
  - Affected by RF stability issues
  - Less intuitive (harder to interpret physically)
```

### 4.4.3 Multi-Sensor Approach

Production systems use **optical + electrical + time backup**:

```
Algorithm (robust production system):

  Sensor 1: Optical (primary, fast)
    - C₂ emission at 703.7 nm
    - Updated every 100 ms
    - Triggers endpoint alert when drops 70%
  
  Sensor 2: Electrical (secondary, confirmatory)
    - Reflected RF power
    - Updated every 200 ms
    - Confirms endpoint (power spike)
  
  Sensor 3: Time (safety backup)
    - Maximum etch time set to 1.3× average time
    - Prevents over-etch if both sensors fail
  
  Endpoint triggered when:
    (Optical drops 70%) AND (Electrical confirms) OR (Time limit)
    
  Safety margin: Multi-sensor AND logic prevents false endpoints

Weekly validation:

  Test wafer run: Measure actual etch time vs. predicted
  If deviation >±5%: Recalibrate optical/electrical thresholds
  If consistent drift: Equipment service needed

Tool-specific calibration:

  Each tool has unique optical path/electrical response
  Calibrate against known resist thickness on tool
  Document tool-specific thresholds in recipe
```

---

## 4.5 Safety & Environmental Considerations

### 4.5.1 Oxygen Safety (Non-Issue)

Pure O₂ ashing poses minimal safety concerns:

```
Oxygen hazards:

  Non-toxic (breathable at normal levels)
  Non-corrosive (inert with most materials at room T)
  Non-flammable (oxidizer, not fuel; supports combustion of other materials)
  
Plasma chamber safety:

  Oxygen plasma not hazardous in sealed chamber
  Standard chamber venting to atmospheric abatement OK
  No special containment required
  
Discharge/handling:

  Oxygen gas supply standard (medical grade available)
  No special piping or storage requirements
  Can use standard stainless steel or aluminum lines
```

### 4.5.2 Fluorine Chemistry Safety (Special Handling)

If fluorine-based ashing used (rare):

```
F₂ gas hazards:

  Highly toxic (LC₅₀ ~400 ppm for rats)
  Extremely corrosive (attacks all materials)
  Moisture-sensitive (reacts with water vapor)
  
Production implications:

  Special chamber materials required (Teflon coatings, etc.)
  Corrosion-resistant electrodes (expensive)
  Special abatement for F₂ (caustic scrubbing required)
  Training and safety protocols mandatory
  Cost multiplier: ~2-5× vs. O₂
  
Industry status: Almost never used in production (too expensive and complex)
```

---

## 4.6 Summary & Key Takeaways

1. **Pure O₂ Ashing is Production Standard** — >90% of 3D NAND processes use pure O₂; safe, simple, cost-effective.

2. **Rate vs. Selectivity Trade-Off Fundamental** — Cannot simultaneously achieve 80+ nm/min rate AND 20:1 selectivity in pure O₂; multi-step recipes address this.

3. **Temperature is Best Selectivity Tuning Knob** — ~15%/°C sensitivity allows selectivity adjustment without RF changes; enables robust recipes.

4. **Multi-Step Recipe Best Practice** — High selectivity step (slow, clean) followed by faster steps with lower selectivity (when resist nearly gone) balances yield and throughput.

5. **Alternative Chemistries Rare** — Fluorine faster but expensive; hydrogen/nitrogen offer no practical advantage; pure O₂ dominates.

6. **Multi-Sensor Endpoint Detection Critical** — Optical (primary) + electrical (confirmatory) + time (safety) prevents over-etch; tool-specific calibration required.

7. **Residue Inevitable with O₂** — Post-ashing cleanup (thermal + O₂ plasma) essential for ALD integration; adds 30-60 min per batch.

---

**End of Part I: Fundamentals (Chapters 1-4) COMPLETE**

---

**Chapter 4 Development Status:** Comprehensive gas chemistry and process selection  
**Version:** 1.0

---

## Part I Summary: Foundational Knowledge Established

**Chapters 1-4 provide complete fundamentals:**

- Chapter 1: Photoresist Materials (20.5 KB) — Composition, post-etch state, challenges
- Chapter 2: Decomposition Chemistry (22 KB) — Arrhenius kinetics, mechanisms, residue
- Chapter 3: Plasma-Resist Interactions (21 KB) — Species, ions, energy effects
- Chapter 4: Ashing Chemistries (18 KB) — Gas selection, endpoint detection, safety

**Total Part I:** ~81.5 KB of foundational physics and chemistry

**Next Phase:** Part II - Hardware Design (Chapters 5-9)

