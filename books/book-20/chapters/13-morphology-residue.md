# Chapter 13: Surface Morphology & Residue Formation

## Overview

As photoresist ashes, the wafer surface undergoes dramatic changes: **roughness increases** (2 nm → 8-15 nm), **residue accumulates** (5-20 nm CₓOᵧ layer), and **notching** can occur at interfaces. These phenomena affect both process yield and downstream integration. This chapter quantifies morphology evolution, residue formation mechanisms, and device-level impacts.

**Learning Objectives:**
- Understand resist roughness evolution mechanisms
- Quantify residue formation vs. ashing parameters
- Predict notching at oxide-resist interfaces
- Quantify microloading effects on uniformity
- Model aspect-ratio effects on surface evolution
- Design recipes for minimal roughness and residue
- Understand device-level yield impact

---

## 13.1 Resist Roughness Evolution

### 13.1.1 Roughness Mechanisms During Ashing

Resist surface roughness increases significantly during ashing:

```
Initial condition (post-lithography):
  Surface roughness Ra: ~1-3 nm (relatively smooth)
  Reason: Novolac polymer smooth, developed pattern clean
  
During ashing (ion bombardment + chemical attack):

Mechanism 1: Ion-induced sputtering texture
  Energetic ions (50-100 eV) create surface damage
  Local sputtering creates small craters and peaks
  Random impact distribution creates roughness
  Sputtering yield Y ~0.5-1.0 atoms/ion
  Each ion removes ~5-10 atoms in cascade
  
  Roughness increase rate: ~0.05-0.1 nm per nm of material removed
  After removing 50 nm resist: Roughness increases ~2.5-5 nm

Mechanism 2: Polymer unevenness
  Fluorocarbon polymer (from ashing byproducts) redeposits unevenly
  Thick in some regions, thin in others
  Creates surface topography
  Effect: +2-4 nm roughness contribution

Mechanism 3: Aspect-ratio effects
  Wide open areas: Roughness increases uniformly
  Dense narrow trenches: High-AR features roughen more (ion/radical non-uniformity)
  Result: Roughness becomes aspect-ratio dependent
  
Final roughness (typical):

Time = 0:           Ra = 2 nm (initial)
After 20 nm ashed:  Ra = 4 nm (+2 nm)
After 50 nm ashed:  Ra = 8 nm (+6 nm, cumulative)
After 80 nm ashed:  Ra = 12-15 nm (final, heavy roughening)

Quantitative model:

  Ra(t) = Ra₀ + k₁ × d_ashed + k₂ × (d_ashed)²
  
  where:
    Ra₀ = initial roughness (~2 nm)
    d_ashed = depth of material removed (nm)
    k₁ = linear roughening coefficient (~0.05 nm/nm)
    k₂ = quadratic coefficient (~0.002 nm/nm²)
    
  Example: After removing 80 nm
    Ra = 2 + 0.05×80 + 0.002×80² = 2 + 4 + 12.8 = 18.8 nm
    (Heavy roughening!)
```

### 13.1.2 Device Impact of Resist Roughness

Post-ashing roughness affects downstream processes and device performance:

```
Roughness impact on ALD deposition (next process):

Initial roughness 2 nm:
  ALD nucleation excellent (smooth, predictable surface)
  First monolayer uniform
  Film properties: Excellent
  
Roughness 8-10 nm:
  ALD nucleation acceptable (moderate surface roughness)
  First monolayer thickness variable (~10% variation)
  Film quality slightly degraded
  
Roughness 15+ nm:
  ALD nucleation poor (very rough surface)
  First monolayer pinholes possible (thin in valleys)
  Film defects: Pinholes, thickness variation
  Yield impact: ~1-2% loss from defects

Device-level consequences:

Dielectric roughness >10 nm:
  - Pinhole defects in ALD/CVD layers
  - Leakage current increases
  - Device parametric failures
  - Yield loss: 2-5% typical
  
Oxide roughness >15 nm:
  - Capacitance variation (high-κ devices sensitive)
  - Electrical performance scatter
  - Threshold voltage variation
  - Yield loss: 5-10% possible

Production acceptance:
  Maximum acceptable resist roughness: ~8-10 nm
  Target: 5-8 nm (minimal roughening)
  Risk threshold: >12 nm (requires rework or scrap)
```

---

## 13.2 Residue Formation & Composition

### 13.2.1 Residue Chemistry & Growth Kinetics

**Residue** is the partially-oxidized carbon polymer remaining after ashing:

```
Residue composition:

  CₓOᵧ with y/x ratio 0.3-0.8 (F-free, unlike hard-mask etch residue)
  Examples:
    C₁₀O₃ (mostly carbon, some oxidation)
    C₈O₅ (balanced)
    C₅O₄ (heavily oxidized but still organic)

Formation mechanism:

  During ashing:
    1. Resist decomposition → CO + CO₂ + CₓOᵧ fragments
    2. Fragments move upward (driven by gas flow)
    3. Some fragments fully oxidize to CO₂ (gaseous, exits)
    4. Some remain partially oxidized (CₓOᵧ)
    5. In cool regions (deep trenches, bottom), fragments cool and redeposit
    
  Net result: Residue layer grows ~5-20 nm by end of ashing

Kinetic model:

  Residue thickness vs. ashing time:
  
  Time 0-10s:    <1 nm (nucleation)
  Time 10-30s:   ~5 nm/min growth rate (linear)
  Time 30-90s:   Growth rate slows (diffusion-limited deposition)
  Time 90-180s:  Plateau at ~15-20 nm (steady-state, redeposition ≈ removal)

Thickness vs. ashing conditions:

Temperature effect:
  Low T (0°C): Heavy residue (20-30 nm)
              Fragments don't fully decompose, redeposit easily
  
  Moderate T (20°C): Moderate residue (10-15 nm)
                     Some thermal decomposition helps
  
  High T (40°C): Light residue (5-10 nm)
                 Fragments more likely to oxidize completely

Ion energy effect:
  Low E_ion (20 eV): Heavy residue (20-25 nm)
                     No sputtering to blast off deposited polymer
  
  Moderate E_ion (80 eV): Moderate residue (10-15 nm)
                          Some ion sputtering helps remove polymer
  
  High E_ion (150 eV): Light residue (5-10 nm)
                       Aggressive sputtering reduces accumulation

Selectivity-residue trade-off:

  High selectivity recipe → Low T, low E_ion
                         → Heavy residue (25-30 nm)
                         → Must remove via post-ashing cleanup
  
  Fast rate recipe → High T, high E_ion
                  → Light residue (5-10 nm)
                  → Minimal post-ashing work
                  → BUT: Poor selectivity risk
  
  Production approach:
    Multi-step recipe balances: moderate residue + acceptable selectivity
    Residue removed in separate post-ashing step (thermal or O₂ plasma)
```

### 13.2.2 Residue Removal Post-Ashing

Residue must be removed before ALD or metallization:

```
Removal methods:

Method 1: Thermal Annealing (Standard)
  Procedure:
    Heat to 120-150°C for 30-45 minutes
    Residue decomposition: CₓOᵧ → CO₂ + CO (gaseous)
  
  Effectiveness:
    Initial residue: 15 nm
    After 120°C × 45min: ~2-3 nm remains (80-85% removal)
    
  Time: ~50 min per batch (significant throughput impact)
  Cost: ~$0.50/wafer (thermal chamber time)

Method 2: O₂ Plasma Ashing (Faster)
  Procedure:
    Run O₂ plasma at moderate conditions (500 W, no bias)
    Duration: 5-15 minutes
    Chemistry: CₓOᵧ + O₂ → CO₂ + CO (oxidation)
  
  Effectiveness:
    Initial residue: 15 nm
    After 10-min O₂ ashing: <2 nm remains (90-95% removal)
  
  Time: ~15 min (3× faster than thermal)
  Cost: ~$1.00/wafer (plasma time)
  
  Trade-off: Faster but more aggressive (risk some top-layer damage)

Method 3: Dual approach (Recommended)
  Thermal: 120°C × 30 min → 80% removal
  O₂ plasma: 5 min → additional 15% removal
  Total time: 40 min
  Total removal: ~95% (residue <1 nm)
  Cost: $1.50/wafer
  
  Benefit: Balanced speed and effectiveness
```

---

## 13.3 Notching & Microloading Effects

### 13.3.1 Notching at Oxide-Resist Interfaces

Interface damage can occur where resist meets oxide:

```
Notching mechanism:

  At oxide-resist interface:
    Oxide acts as etch barrier (lower etch rate)
    Resist below oxide ashes normally
    Undercut forms: Oxide overhangs, resist undercut
    
  Geometry:
    Notch depth: 10-20 nm typical
    Notch width: ~30-50 nm (extends laterally)
    Location: Directly under oxide layer

Severity levels:

  <5 nm notch:  Not visible, no device impact, acceptable
  5-10 nm notch: Visible in TEM, minor concern
  10-20 nm notch: Significant undercut, risk of resist instability
  >20 nm notch: Critical, risks resist lifting/peeling

Reduction strategies:

  Strategy 1: Lower ion energy
    High E_ion → aggressive sputtering → notching worse
    Low E_ion (~60 eV) → minimal sputtering → notching reduced
    Trade-off: Slower ashing rate
  
  Strategy 2: Higher pressure (better selectivity to oxide)
    High P → more diffusive transport
    Ions don't reach oxide edge as easily
    Result: Less undercut
    Trade-off: Poor ARDE compensation for deep trenches
  
  Strategy 3: Temperature tuning
    Thermal activation for resist dominates at high T
    But oxide also etches more at high T
    Net effect: Not major improvement
  
  Strategy 4: Two-step endpoint
    Step 1: Conservative ashing (stops with slight resist remaining)
    Step 2: Inspect via CD-SEM or TEM cross-section
    Step 3: Gentle final trim (if needed)
    Benefit: Avoids over-etch and excessive notching
```

### 13.3.2 Microloading Effects

Ashing rate varies with feature pitch (microloading):

```
Microloading definition:

  Rate difference between dense and isolated features
  Dense regions: Narrow lines, close pitch (20-30 nm spacing)
  Isolated regions: Wide openings (200+ nm pitch)
  Ashing rate ratio: R_dense / R_isolated = 0.8-1.2 (should be ~1.0 for uniformity)

Microloading mechanisms:

  Radical depletion:
    Dense features consume radicals locally
    Radicals depleted in high-density regions
    Result: Dense features etch slower
  
  Ion accumulation:
    Ions less affected by depletion (higher mobility)
    Ions may accumulate in dense regions
    Result: Can partially compensate for radical depletion

Typical microloading:

  At 50 mTorr (moderate pressure):
    Dense (30 nm line): Rate ~50 nm/min
    Isolated (300 nm opening): Rate ~50 nm/min
    Uniformity: ±5% (excellent)
  
  At 30 mTorr (low pressure, ballistic):
    Dense: Rate ~70 nm/min (faster, ions reach)
    Isolated: Rate ~50 nm/min (slower, ions miss edge)
    Uniformity: ±30% (poor!)
  
  At 100 mTorr (high pressure, diffusive):
    Dense: Rate ~30 nm/min (slower, radical depletion)
    Isolated: Rate ~35 nm/min (faster, radicals available)
    Uniformity: ±15% (acceptable)

Compensation:

  Microloading correction requires pressure optimization
  Moderate pressure (70-80 mTorr) provides good balance
  Multi-step approach: high-P for uniformity, low-P for deep features
  Typical achievable: ±10% microloading uniformity
```

---

## 13.4 Summary & Key Takeaways

1. **Roughness Increases Significantly** — 2 nm initial → 12-15 nm final (~6-8 nm increase); roughness >10 nm causes ALD nucleation defects and yield loss.

2. **Ion Sputtering Primary Roughening Cause** — Ion-induced surface damage creates craters/peaks; cumulative effect dominates over polymer contributions.

3. **Residue Inevitable with O₂ Ashing** — 10-20 nm CₓOᵧ residue typical; must be removed post-ashing (thermal or O₂ plasma) before ALD/metal deposition.

4. **Residue-Selectivity Trade-Off** — High selectivity (low T, low ions) → heavy residue; must use multi-step recipe to balance both requirements.

5. **Residue Removal Adds Process Time** — Thermal annealing 45 min or O₂ plasma 15 min; dual approach ~40 min total; significant throughput impact.

6. **Notching at Oxide Interfaces Possible** — 10-20 nm undercut typical; reduced by lower ion energy or two-step endpoint approach with inspection.

7. **Microloading From Radical Depletion** — Dense features etch slower (radicals consumed locally); achievable uniformity ±10-15% with proper pressure tuning.

8. **Device Yield Impact Real** — Roughness >10 nm, residue >2 nm, or notching >20 nm cause 1-5% yield loss via ALD defects, capacitance variation, or mechanical damage.

---

**Next Chapter:** [Chapter 14 - Temperature Effects on Ashing](./14-temperature-effects.md)

---

**Chapter 13 Development Status:** Comprehensive morphology and residue framework  
**Version:** 1.0

