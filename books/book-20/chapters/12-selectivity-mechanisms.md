# Chapter 12: Selectivity Mechanisms

## Overview

**Selectivity** — the ratio of ashing rates between photoresist and underlayers (hard mask, dielectric, metal) — is the central challenge in photoresist removal. Unlike fluorine-based hard-mask etch where selectivity is primarily chemical, photoresist ashing selectivity involves temperature-dependent chemistry, ion-assisted mechanisms, and selective oxidation. This chapter quantifies selectivity for key material pairs and develops multi-layer recipes.

**Learning Objectives:**
- Understand chemical selectivity mechanisms (activation energy differences)
- Quantify ion energy effects on selectivity for different materials
- Develop selectivity models for C/SiO₂, C/Si, C/Metal pairs
- Design multi-layer selectivity strategies
- Implement weekly validation protocols
- Optimize temperature and ion energy for specific integrations
- Manage selectivity risk in production

---

## 12.1 Fundamental Selectivity Mechanisms

### 12.1.1 Chemical Selectivity (Thermal/Radical-Driven)

Different materials have different activation energies:

```
Oxidative decomposition in O₂ plasma:

Material     Activation Energy    Why?
────────────────────────────────────────────
Photoresist  ~10-12 kcal/mol      Weak C-H bonds, aromatic ring
Carbon HM    ~15-20 kcal/mol      Strong C-C sp³ networks
SiO₂         ~35-40 kcal/mol      Very strong Si-O bonds
Si           ~40-50 kcal/mol      Strong Si-Si bonds

Temperature effect on selectivity:

At T = 10°C (low):
  Resist: Rate ∝ exp(-12/kT) = 30 nm/min
  SiO₂:   Rate ∝ exp(-38/kT) = 0.8 nm/min
  S(C/SiO₂) = 30/0.8 = 37:1 (excellent!)

At T = 30°C (moderate):
  Resist: 60 nm/min (+2× from Arrhenius)
  SiO₂:   2.5 nm/min (+3.1× from higher E_a)
  S(C/SiO₂) = 60/2.5 = 24:1 (still good)

At T = 50°C (warm):
  Resist: 120 nm/min
  SiO₂:   8 nm/min
  S(C/SiO₂) = 120/8 = 15:1 (degrading)

At T = 70°C (hot):
  Resist: 240 nm/min
  SiO₂:   25 nm/min
  S(C/SiO₂) = 240/25 = 9.6:1 (risky!)

Key insight: Higher E_a materials degrade selectivity MORE at high T
```

### 12.1.2 Ion-Assisted Selectivity

Sputtering yields vary with material:

```
Sputtering yields at 100 eV ion energy:

Material     Y (atoms/ion)    Reason
──────────────────────────────────────
Carbon       ~0.8             Weak bonding, low atomic mass
SiO₂         ~0.3             Strong Si-O bonds
Si           ~0.2             Strong Si-Si bonds
Cu metal     ~1.5             Low threshold energy
W metal      ~0.5             Refractory, strong bonds
Al           ~1.2             Moderate bonding

Ion-assisted ashing rate:

R_ion = Y × φ_ion × M / (ρ_feature × N_A)

where:
  Y = sputtering yield
  φ_ion = ion flux (~10¹⁵ ions/cm²·s)
  M = atomic mass (g/mol)
  ρ_feature = number density of atoms

For resist (carbon, M=12):
  R_ion ≈ 0.8 × 10¹⁵ × 12 / (5×10²² / 6×10²³) ≈ 20-25 nm/min

For SiO₂ (Si+O, M≈30 effective):
  R_ion ≈ 0.3 × 10¹⁵ × 30 / (2×10²² / 6×10²³) ≈ 3-5 nm/min

Selectivity from ion contribution alone:
  S = R_ion,C / R_ion,SiO2 ≈ 5-8:1 (good, but lower than chemical)
  
But ion contribution is only part of total rate:

Total rate = Chemical + Ion-assisted:

At high selectivity conditions (low E_ion):
  R_C_total ≈ 35 (chem) + 5 (ion) = 40 nm/min
  R_SiO2_total ≈ 2 (chem) + 0.5 (ion) = 2.5 nm/min
  S = 40/2.5 = 16:1 (selectivity good)

At high rate conditions (high E_ion):
  R_C_total ≈ 35 (chem) + 20 (ion) = 55 nm/min
  R_SiO2_total ≈ 2 (chem) + 3 (ion) = 5 nm/min
  S = 55/5 = 11:1 (selectivity degraded)
  
Implication: Ion energy control directly affects selectivity
```

---

## 12.2 Specific Material Pairs

### 12.2.1 Resist / SiO₂ Selectivity (Most Common)

The primary selectivity challenge in 3D NAND:

```
Standard production recipe (C/SiO₂):

Baseline conditions:
  P = 80 mTorr, W_coil = 2000 W, W_bias = 400 W, T = 20°C

Measured selectivity: S ≈ 15:1
  Resist ashing: 60 nm/min
  SiO₂ ashing: 4 nm/min
  
Selectivity map (varying temperature and ion energy):

T (°C)   E_ion (eV)   C rate    SiO₂ rate   Selectivity
───────────────────────────────────────────────────────
 0       60          40        2.0         20:1
 0       100         55        4.0         14:1
10       60          45        2.5         18:1
10       100         60        4.5         13:1
20       60          50        3.0         17:1
20       100         65        5.0         13:1
30       60          55        4.0         14:1
30       100         75        6.5         11:1
40       60          65        5.5         12:1
40       100         85        8.0         11:1

Selection strategy:

For maximum selectivity (>20:1):
  Use low T (~0°C) and low E_ion (~60 eV)
  Rate compromise: 40-45 nm/min (slower)
  Production time: 180-200 sec for 80 nm resist
  Risk: Very low (selectivity margin huge)

For production balance (15:1 selectivity, 60 nm/min rate):
  Use moderate T (~20°C) and moderate E_ion (~80 eV)
  Rate: 60-65 nm/min (good throughput)
  Production time: 100-120 sec for 80 nm resist
  Risk: Moderate (selectivity margin ~3-5 nm acceptable)

For high throughput (<8:1 selectivity, 80+ nm/min):
  Use warm T (~40°C) and high E_ion (~120 eV)
  Rate: 85+ nm/min (excellent throughput)
  Production time: <100 sec for 80 nm resist
  Risk: HIGH (only 1-2 nm selectivity margin, hard mask in danger)
```

### 12.2.2 Resist / Carbon Hard Mask Selectivity

Challenging because both are carbon-based:

```
Problem: Same elemental composition (C, H, O)
         Similar ashing mechanisms
         Lower inherent selectivity

Typical selectivity C/Carbon HM:

Hard mask carbon is denser, more cross-linked:

Photoresist: Loose aromatic polymer (E_a ~12 kcal/mol)
Carbon HM:   Dense sp³ network (E_a ~18 kcal/mol)

Selectivity at 20°C:

Resist ashing rate: 60 nm/min
Carbon HM rate: ~20-25 nm/min
Selectivity: S = 60/22 = 2.7:1 (LOW!)

Improvement strategies:

Strategy 1: Lower temperature (maximize E_a difference)
  At 0°C: Resist 40 nm/min, Carbon HM 15 nm/min → S = 2.7:1 (same ratio)
  (E_a difference doesn't change ratio, only absolute rates)

Strategy 2: Lower ion energy (reduce sputtering of hard mask)
  Resist (Y~0.8): Reduced sputtering effect modest
  Carbon HM (Y~0.6): Reduced sputtering helps slightly
  Result: S ≈ 3-4:1 (marginal improvement)

Strategy 3: Use oxide-protective layer
  Deposit thin SiO₂ or Al₂O₃ on carbon HM beforeetch
  Then etch through resist + oxide to carbon
  Oxide protects carbon HM
  Result: Effective selectivity very high (oxide etch stops etch)
  
  But this adds process complexity (extra deposition step)

Production approach:

For carbon hard mask ashing:
  Cannot rely on selectivity alone (too low, ~2-3:1)
  Must use time-based endpoint or dual-step approach
  
  Option A: Time-based ashing
    Calculate etch time for known resist + HM thickness
    Stop at time = resist removal (accept HM gets damaged 5-10 nm)
    Proceed to HM restoration etch (if needed)
  
  Option B: Dual-step approach
    Step 1: Conservative ashing (high selectivity, slow rate, stops early)
    Step 2: Verify via metrology (measure remaining resist, monitor HM)
    Step 3: Final trim if needed
    More time but safer
```

### 12.2.3 Resist / Metal Selectivity

Metals present additional challenges:

```
Metal oxidation in O₂ plasma:

Cu: Forms CuO (highly oxidizable)
W:  Forms WO₃ (moderately oxidizable)
Al: Forms Al₂O₃ (already oxidized)

Problem: All metals oxidize easily in O₂ plasma
         Oxidation rates can be comparable to resist ashing
         True selectivity may be low or negative (metals etch faster!)

Example: Resist / Cu selectivity

Resist ashing: 60 nm/min (normal)
Cu oxidation: ~15-30 nm/min (depending on plasma conditions)

S = 60/22 ≈ 2.7:1 (not great)

If S drops below 1:1, disaster!
  Cu oxidizes faster than resist ashing
  Cu gets consumed before resist completely removed
  Result: Photoresist remains on device, contaminates later steps

Prevention strategies:

Strategy 1: Metal protection layer
  Deposit TiN or Ta₂O₅ on Cu before ashing
  Protective layer slows Cu oxidation
  Can achieve S = 5-8:1 (Cu/Resist)
  
Strategy 2: Avoid direct O₂ contact
  Use pulsed O₂/N₂ or other chemistry (not standard)
  Complex, not production-standard

Strategy 3: Recipe design for metal safety
  Etch resist in completely separate chamber (different plasma)
  Or use aggressive endpoint detection
  Switch to mild O₂ ashing if metal appears (backward incompatible)

Production practice:

For metal underlayers:
  Add protective metal barrier during device design phase
  Use TiN barrier (standard anyway, dual-purpose)
  Confirm selectivity ~5-8:1 via test run
  Validate every wafer lot (metals are critical)
```

---

## 12.3 Multi-Layer Selectivity Requirements

### 12.3.1 Complex Stack Selectivity

Real 3D NAND often has multiple materials:

```
Typical stack (simplified):

  [Photoresist] ← Remove this
  [Carbon HM]   ← Protect this (S_C/HM ~2.7:1)
  [SiO₂]        ← Protect this (S_C/SiO₂ ~15:1)
  [Si]          ← Definitely protect (S_C/Si ~20:1)

Competing selectivity requirements:

Requirement 1: Protect carbon HM
  Need S_C/HM > 2:1 (minimum)
  Need S_C/HM > 3:1 (safe, for 10 nm margin)
  
Requirement 2: Protect SiO₂ underlayer
  Need S_C/SiO₂ > 3:1 (minimum)
  Need S_C/SiO₂ > 5:1 (safe, for 20 nm margin)

Requirement 3: Protect Si substrate
  Need S_C/Si >> 10:1 (natural selectivity huge)
  Not a real concern

Problem: Selectivity to HM much lower than to SiO₂
         Recipe tuned for HM selectivity sacrifices SiO₂ safety

Solution: Two-step approach

Step 1: Etch most of resist with optimized selectivity
  Conditions: High selectivity to HM
  Time: ~150 sec (conservative)
  Resist remaining: ~10-20 nm
  
Step 2: Inspect via TEM or CD-SEM
  If HM still intact and enough resist remains:
    Continue with same recipe (second wafer-worth of time)
  If HM looks attacked:
    STOP, adjust recipe, validate on test wafer
    
Result: Dual-layer selectivity achieved via timing + inspection
```

### 12.3.2 Multi-Material Recipe Validation

Weekly protocols ensure selectivity maintained:

```
Validation structure:

Control wafer stack:
  [ArF resist] 80 nm
  [Carbon HM] 30 nm
  [SiO₂] 200 nm (thick, won't reach bottom)
  [Si substrate]

Weekly procedure (every 7 days):

Day 1 (production):
  Run production wafers with locked recipe
  Time each wafer, record ashing times
  
Day 5 (mid-week check):
  Run one control wafer
  Measure remaining resist thickness (ellipsometry or XRR)
  Compare to baseline: Should be ~±5% same
  
  If drift >±5%:
    Ashing rate changed
    Possible electrode corrosion, gas depletion, thermal drift
    Adjust recipe or schedule service
    Do NOT proceed until controlled

Day 7 (end-of-week validation):
  Run full control wafer stack
  Etch and stop at standard recipe endpoint
  TEM cross-section to measure:
    Photoresist remaining: Should be <2 nm (fully removed)
    Carbon HM thickness: Should be >25 nm (no damage)
    SiO₂ surface: Should show no erosion
  
  Compare to baseline:
    Resist removal: 80±2 nm (✓ = fully removed, ✗ = incomplete)
    HM intact: Thickness within 1 nm of baseline
    SiO₂ safe: No measurable erosion

Pass/fail criteria:

  PASS: Resist fully removed, HM >25 nm remaining, SiO₂ untouched
        Continue recipe, no changes
  
  MARGINAL: Resist fully removed, HM >26 nm remaining, SiO₂ <1 nm erosion
            Acceptable (selectivity working), but marginal margin
            Monitor closely, schedule recipe refresh
  
  FAIL: Resist incomplete, OR HM <25 nm, OR SiO₂ eroded >2 nm
        STOP production, troubleshoot:
        - Check electrode condition (visual inspection)
        - Measure reflected power (impedance drift?)
        - Run fresh 2³ DOE to re-establish baseline
        - Do NOT resume production until validated

Quarterly refresh:

  Every 3 months:
    Repeat 2³ DOE with fresh process window
    Generate updated contour maps
    Validate baseline recipe still optimal
    Update control wafer expectations
    Check for any electrode changes/degradation
```

---

## 12.4 Summary & Key Takeaways

1. **Activation Energy Differences Drive Chemical Selectivity** — Resist E_a ~12 kcal/mol, SiO₂ ~38 kcal/mol; selectivity improves ~2× per 20°C decrease in temperature.

2. **Ion Energy Reduces Selectivity** — High E_ion increases sputtering contribution proportionally to material; low E_ion (~60 eV) better than high E_ion (~120 eV) for selectivity.

3. **C/SiO₂ Most Favorable** — 15-20:1 selectivity achievable in production; ~3-5 nm safety margin acceptable for 30 nm hard masks.

4. **C/Carbon HM Challenging** — Only 2.7-3:1 selectivity possible (same elemental composition); cannot rely on chemistry alone; must use timing or protective layers.

5. **Metals Oxidize Easily** — Oxygen plasma oxidizes Cu/W faster than resist sometimes; requires protective metal barriers (TiN) or separate process step.

6. **Multi-Material Stacks Require Compromise** — HM selectivity lowest; recipe tuned for HM protection is safest; verify selectivity to each layer via control wafers.

7. **Temperature Best Selectivity Tuning Knob** — Changing T without RF power changes selectivity exponentially; enables recipe flexibility within locked power envelope.

8. **Weekly Validation Critical** — Control wafer measurements catch selectivity drift early; TEM verification on endpoints ensures safety margins maintained.

---

**Next Chapter:** [Chapter 13 - Surface Morphology & Residue Formation](./13-morphology-residue.md)

---

**Chapter 12 Development Status:** Comprehensive selectivity framework  
**Version:** 1.0

