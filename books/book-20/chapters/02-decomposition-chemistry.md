# Chapter 2: Photoresist Decomposition Chemistry

## Overview

Photoresist decomposition during ashing is controlled by **thermochemistry and kinetics**. Unlike simple thermal decomposition in a furnace, resist decomposition in oxygen plasma involves multiple competing pathways: thermal breakdown, chemical attack by radicals, and ion-assisted sputtering. This chapter quantifies these mechanisms and develops models for predicting ashing rates.

**Learning Objectives:**
- Understand thermal decomposition kinetics (Arrhenius relation, activation energy)
- Recognize chemical scission mechanisms (C-H, C-C bonds under attack)
- Quantify ion-assisted decomposition pathways
- Model reaction rates and temperature dependence
- Predict ashing rate from first principles
- Connect kinetics to selectivity and uniformity challenges

---

## 2.1 Thermal Decomposition Kinetics

### 2.1.1 Arrhenius Framework

Photoresist decomposition follows the **Arrhenius relation**, fundamental to all thermally-driven reactions:

```
Ashing rate: R(T) = R₀ × exp(-E_a / kT)

where:
  R(T)  = ashing rate at temperature T (nm/min)
  R₀    = pre-exponential factor (related to collision frequency)
  E_a   = activation energy (energy barrier, kcal/mol or kJ/mol)
  k     = Boltzmann constant = 1.38 × 10⁻²³ J/K = 1.987 × 10⁻³ kcal/(mol·K)
  T     = absolute temperature (Kelvin)

For photoresist ashing:
  Typical E_a ≈ 10-15 kcal/mol (oxygen-based, oxidative pathways)
  
Temperature-dependent rate constant:
  ln(R) = ln(R₀) - (E_a/R) × (1/T)
  
  Plot ln(R) vs. 1/T → straight line with slope = -E_a/R
  This allows E_a extraction from experimental data
```

### 2.1.2 Temperature Coefficient and Practical Range

The **temperature coefficient** quantifies rate sensitivity to temperature:

```
For carbon oxidation in O₂ plasma:
  Typical E_a ≈ 12 kcal/mol

Rate change over 10°C interval:

From T₁ = 20°C (293 K) to T₂ = 30°C (303 K):

R(30°C) / R(20°C) = exp[E_a/R × (1/T₁ - 1/T₂)]
                  = exp[12000 / 1.987 × (1/293 - 1/303)]
                  = exp[12000 / 1.987 × (0.003413 - 0.003302)]
                  = exp[12000 / 1.987 × 0.000111]
                  = exp[0.670]
                  ≈ 1.955

Ratio: R(30°C) / R(20°C) ≈ 1.96 (approximately 2×!)

Practical calculation (rule of thumb):
  ~13-15% rate increase per 1°C
  ~130-150% rate increase per 10°C
  ~2× rate change over 10°C common
```

### 2.1.3 Activation Energy from Experimental Data

Extracting E_a from ashing rate measurements:

```
Experiment: Measure ashing rate at different temperatures

Data (hypothetical):
  T = 20°C:   R = 50 nm/min
  T = 30°C:   R = 75 nm/min
  T = 40°C:   R = 112 nm/min
  T = 50°C:   R = 168 nm/min

Analysis using Arrhenius:
  ln(R₂/R₁) = (E_a/R) × (1/T₁ - 1/T₂)
  
For T₁=20°C (293K), T₂=30°C (303K):
  ln(75/50) = (E_a/1.987) × (1/293 - 1/303)
  ln(1.5) = (E_a/1.987) × 0.000111
  0.405 = (E_a/1.987) × 0.000111
  E_a = 0.405 × 1.987 / 0.000111 ≈ 7250 kcal/mol... 
  
  (This seems wrong—let me recalculate in SI units)
  
Using SI: E_a in J/mol, R = 8.314 J/(mol·K)
  ln(75/50) = (E_a/8.314) × (1/293 - 1/303)
  0.405 = (E_a/8.314) × 0.0001113
  E_a = 0.405 × 8.314 / 0.0001113 ≈ 30,300 J/mol ≈ 7.2 kcal/mol

Meaning: Low activation energy (pure thermal decomposition dominant)

For each temperature pair, calculate E_a separately:
  T₁=30°C→40°C: E_a ≈ 8.5 kcal/mol
  T₁=40°C→50°C: E_a ≈ 9.2 kcal/mol
  Average: E_a ≈ 8.3 kcal/mol

Fit to full dataset: Linear regression of ln(R) vs. 1/T
  Slope = -E_a/R (in SI units)
  More robust than pairwise comparison
```

---

## 2.2 Chemical Scission Mechanisms

### 2.2.1 C-H Bond Cleavage

The primary pathway for photoresist decomposition is breaking **C-H bonds** in the novolac backbone:

```
Novolac structure (simplified):

  ...—C—C—C—...
     | | |
     H H H
   (aromatic ring)

Oxidative scission (in O₂ plasma):

Pathway 1: Radical attack
  C-H + O· → C· + OH·
  C· + O₂ → CO₂ + other products
  
Pathway 2: Ion-assisted
  C-H + O⁺ (energetic) → C⁺ + H· + neutrals
  Products: CO, CO₂, H₂O

Bond dissociation energies:
  C-H: ~99 kcal/mol (very strong!)
  C-C: ~83 kcal/mol
  C-O: ~86 kcal/mol (but weak when adjacent to -OH)
  
Activation barriers:
  For O· attack: E_a ≈ 5-10 kcal/mol (low, favorable)
  For direct thermal: E_a ≈ 50-80 kcal/mol (high, unfavorable)
  
Implication: Radical attack dominates over pure thermal decomposition
```

### 2.2.2 C-C Bond Cleavage

Backbone scission occurs via C-C bond breaking:

```
Two carbon atoms in polymer chain:

  —C—C—
   | |
  (aromatic)

Attack mechanisms:

Mechanism 1: Oxygen insertion
  —C—C— + O₂ → —C—O—O—C— (peroxide intermediate)
           → —C=O + ·C— (radical formation)
           
Mechanism 2: Radical-induced scission
  —C—C— + O· → —C· + ·C—O (radical propagation)
           → —C—O—H + C· (abstraction)

Temperature effects:
  Low T: C-C bonds stable, resist survives longer
  High T: Thermal energy helps overcome bond dissociation energy
  Activation energy: E_a ≈ 8-15 kcal/mol (moderate)
```

### 2.2.3 Competitive Pathways & Selectivity

Different substrates decompose at different rates because of **activation energy differences**:

```
Activation energies for oxidative decomposition:

Material        E_a (kcal/mol)    Comment
─────────────────────────────────────────
Photoresist     ~10-12            Weak C-H, easy target
Carbon overlay  ~15-20            Stronger C-C network
SiO₂            ~30-40            Si-O very strong, hard to break
Si              ~40-50            Si-Si bonds very strong

Rate comparison at different temperatures:

At T = 20°C:
  Resist:  R ∝ exp(-12/kT) ≈ 50 nm/min (reference)
  Carbon:  R ∝ exp(-18/kT) ≈ 15 nm/min (3.3:1 selectivity vs. resist)
  SiO₂:    R ∝ exp(-35/kT) ≈ 1 nm/min (50:1 selectivity vs. resist)

At T = 40°C:
  Resist:  R ∝ exp(-12/kT) ≈ 190 nm/min (3.8× faster)
  Carbon:  R ∝ exp(-18/kT) ≈ 60 nm/min (4× faster)
  SiO₂:    R ∝ exp(-35/kT) ≈ 5 nm/min (5× faster)
  
Selectivity at 40°C:
  Resist/Carbon: 190/60 ≈ 3.2:1 (slight degradation from 3.3:1)
  Resist/SiO₂:   190/5 = 38:1 (degradation from 50:1)

Key insight: Higher E_a materials (SiO₂, Si) degrade selectivity
  MORE at high T because their activation energy is steeper
```

---

## 2.3 Ion-Assisted Decomposition

### 2.3.1 Physical Sputtering Contribution

**Ion bombardment** adds a physical component to chemical decomposition:

```
Ion sputtering mechanism:

  Energetic ion (O⁺, O₂⁺, ~50-100 eV)
           ↓ impact
  [Surface]
           ↓
  Energy transfer to surface atoms
  → Knock-on collisions (cascade)
  → Material displaced (sputtered)

Sputtering yield for photoresist:

  Y = number of atoms removed per incident ion
  
  Typical values:
    At 50 eV:  Y ≈ 0.3 atoms/ion
    At 100 eV: Y ≈ 0.8 atoms/ion
    At 200 eV: Y ≈ 1.5 atoms/ion

Energy dependence:
  Y(E) ≈ 0 for E < 10-20 eV (threshold energy)
  Y(E) ∝ E^α for E > threshold (power law, α ≈ 0.5-1)
  
Ashing rate contribution:
  R_physical = Ion_flux × Sputtering_yield × atomic_mass_density
  
  Example:
    Ion flux: 10¹⁵ ions/(cm²·s)
    Yield: 0.8 atoms/ion
    Atom density in resist: 5 × 10²² atoms/cm³
    Atomic mass: ~12 amu
    
    R_physical ≈ 10¹⁵ × 0.8 / (5 × 10²²) × (12 g/mol / 6×10²³)
             ≈ 3-5 nm/min (significant contribution!)
```

### 2.3.2 Ion-Enhanced Chemical Reaction

Ions don't just sputter; they also **enhance chemical reactions**:

```
Ion-enhanced mechanisms:

Mechanism 1: Subsurface damage
  Ion penetration creates dangling bonds and radical sites
  These sites are chemically reactive (easier for O· attack)
  Result: Chemical etch rate increased locally

Mechanism 2: Displaced atoms
  Ion collision displaces atoms (vacancies created)
  Oxygen can enter these vacancy sites
  Oxidation reaction accelerated (more surface area)

Mechanism 3: Energy input
  Ion impact transfers ~50-100 eV to surface
  Some energy remains as lattice vibrations
  Effectively "local heating" (not macroscopic T rise)
  Activation barriers overcome more easily

Combined ion + chemical rate:

  R_total = R_chemical + R_physical + R_enhanced
  
  Typical split at 100 eV ion energy:
    R_chemical:   40-50 nm/min (dominant, thermal + radical)
    R_physical:   3-5 nm/min (sputtering)
    R_enhanced:   5-10 nm/min (ion-accelerated chemistry)
    ────────────────────────────
    R_total:      48-65 nm/min
    
  Physical + enhanced contribution: ~20-30% of total rate
```

---

## 2.4 Reaction Products & Residue Formation

### 2.4.1 Ashing Products

When photoresist decomposes in oxygen plasma, various gaseous and solid products form:

```
Primary volatile products:

  Resist (CₓHᵧ organic) + O₂ →

  CO₂       (carbon dioxide)    ~30-40% of carbon atoms
  CO        (carbon monoxide)   ~20-30% (partial oxidation)
  H₂O       (water)             ~20-30% (from C-H scission)
  C₂Hₓ      (hydrocarbons)      ~5-10% (incomplete decomposition)
  CHₓO      (carbonyls, aldehydes) ~5-10%

Secondary products (in plasma):

  UV photons dissociate products → radicals
  Further oxidation: CO → CO₂ (slow, kinetically limited)
  
Selectivity consequence:
  If decomposition incomplete (kinetically limited)
  Some CO remains (not re-oxidized to CO₂)
  These partial oxides deposit as residue (CₓOᵧ)
```

### 2.4.2 Residue Formation Kinetics

**Residue** is the contradiction: we want to remove resist, but residue remains.

```
Residue composition:

  CₓOᵧ with typical y/x ratio 0.5-1.0
  
  Examples:
    C₁₀O₆ (partially oxidized aromatic)
    C₈O₈ (fully oxidized, but still polymeric)
    C₂O₃ (carbon monoxide polymers)

Formation mechanism:

  During ashing:
    1. Resist scission → small polymer fragments (C₂-C₅ species)
    2. These fragments partially oxidize: CₓHᵧ → CₓHᵧOᵤ
    3. Some fragments are volatile (desorb to gas)
    4. Some are non-volatile → redeposit on surface
    5. Net result: Residue layer growth

Residue thickness vs. time:

  Time 0-10s:   <1 nm (nucleation)
  Time 10-30s:  5-10 nm/min growth rate
  Time 30-90s:  Growth rate slows (diffusion-limited)
  Time 90-180s: Plateau at 5-20 nm (steady-state)

Factors promoting residue:

  Low temperature:
    - Slow decomposition (fragments survive longer)
    - Low re-oxidation rate (CO doesn't fully convert to CO₂)
    - Results: Thick residue (~20-30 nm)
  
  High ion energy:
    - Physical sputtering reduces residue (blasts it off)
    - Result: Thin residue (~5-10 nm)
    
  High pressure:
    - Ions don't reach surface (mean free path too short)
    - More neutral radical pathway (chemical only)
    - Results: More residue (~15-25 nm)
```

### 2.4.3 Residue Thickness vs. Selectivity Trade-Off

One of the **key insights** in Book #20:

```
Central trade-off in photoresist ashing:

To achieve HIGH SELECTIVITY:
  → Lower ion energy (reduce physical sputtering of underlayer)
  → Lower temperature (favor chemical activation barriers)
  → Higher pressure (increase radical flux, decrease ion flux)
  → Consequence: MORE residue (~20-30 nm)

To achieve LOW RESIDUE:
  → Higher ion energy (sputter off fragments, prevent redeposition)
  → Higher temperature (fully decompose all fragments to CO₂)
  → Lower pressure (higher ion flux, better residue sputtering)
  → Consequence: WORSE selectivity (~3-5:1 vs. ~8-12:1)

Production optimization:
  Selectivity priority: Sacrifice residue cleanup time
    - Multi-step recipe: High selectivity etch + residue removal
    - Post-ashing thermal + O₂ plasma to remove residue
    
  Residue priority: Accept selectivity risk (rare, dangerous)
    - Fast single-step ashing
    - Higher risk of underlayer damage
    - Only viable for non-critical layers

Standard approach:
  Step 1: Selective ashing (high selectivity, high residue)
  Step 2: Residue cleanup (separate process, thermal annealing or O₂ plasma)
```

---

## 2.5 Temperature Effects on Decomposition

### 2.5.1 Arrhenius Predictions vs. Experiment

Theory predicts ~15% rate increase per 10°C, but real systems show variations:

```
Experimental observation (ArF resist in O₂ plasma):

T = -10°C (263K):  R ≈ 35 nm/min
T =   0°C (273K):  R ≈ 40 nm/min (+14%)
T = +10°C (283K):  R ≈ 46 nm/min (+31%)
T = +20°C (293K):  R ≈ 52 nm/min (+49%)
T = +30°C (303K):  R ≈ 60 nm/min (+71%)
T = +40°C (313K):  R ≈ 70 nm/min (+100%, 2×)

Fits to Arrhenius: E_a ≈ 11 kcal/mol
  Prediction:  R(40°C)/R(20°C) = exp[(E_a/R)(1/293-1/313)]
             = exp[11000×0.0001105/1.987] ≈ 1.59 (59% increase)
  
  Observed:    R(40°C)/R(20°C) = 70/52 ≈ 1.35 (35% increase)

Discrepancy reason: Ion-assisted pathway
  - At low T: Ion contribution is constant (doesn't depend on T)
  - Thermal component follows Arrhenius
  - At low T: Thermal ∝ 30% of total, ions ∝ 70%
  - Temperature coefficient of mixed rate is lower than pure thermal

Mixed-rate analysis:
  R_total = R_chemical(T) + R_physical (constant)
  
  At low T: R_total ≈ R_phys (dominated by ion sputtering, no T dependence)
  At high T: R_total ≈ R_chem (dominated by chemistry, strong T dependence)
  
  Result: Nonlinear temperature dependence (S-curve)
```

### 2.5.2 Selectivity Temperature Dependence

Selectivity changes with temperature in complex ways:

```
Selectivity vs. temperature (resist / SiO₂):

T (°C)    E_a_resist   E_a_SiO₂    Selectivity   Reason
──────────────────────────────────────────────────────
-10       12           35          50:1          Large E_a difference
+10       12           35          35:1          Still good
+20       12           35          25:1          Degrading
+40       12           35          15:1          Poor
+60       12           35          10:1          Very risky

Mechanism: SiO₂ has higher E_a
  - At low T: SiO₂ etch suppressed (high barrier)
  - At high T: SiO₂ etch accelerated (barrier overcome)
  - Selectivity loss inevitable at high T

Polymer effect (additional):
  - Low T: Oxide layer (protective polymer) on SiO₂ surface
  - High T: Polymer decomposes (no longer protective)
  - This additional selectivity loss at high T

Optimal strategy:
  Selectivity priority: Use low-moderate T (20-30°C)
    - Keep SiO₂ E_a advantage
    - Maintain polymer protection
    - Selectivity: 20-25:1 achievable

  High throughput priority: Use moderate-high T (40-60°C)
    - Faster ashing rate
    - Selectivity: 10-15:1 (acceptable for non-critical layers)
    - Risk of hard mask damage increases
```

---

## 2.6 Summary & Key Takeaways

1. **Arrhenius Governs Rate** — Ashing rate follows R(T) = R₀ × exp(-E_a/kT) with typical E_a ~10-15 kcal/mol, creating ~15% rate change per 1°C.

2. **Multiple Pathways Compete** — Thermal decomposition, radical chemical attack, and ion-assisted sputtering all contribute to final ashing rate. No single mechanism dominates.

3. **Activation Energy Differences Drive Selectivity** — Resist (E_a ~10-12) vs. SiO₂ (E_a ~35-40) creates selectivity margin, but margin decreases at high temperature.

4. **Residue vs. Selectivity Trade-Off** — Conditions for high selectivity (low T, low ions) promote residue formation. Opposite conditions (high T, high ions) reduce residue but hurt selectivity.

5. **Temperature is Powerful Tuning Knob** — Unlike fluorine-based etch, photoresist ashing rate and selectivity are strongly temperature-dependent, enabling recipe optimization via T adjustment without RF power change.

6. **Ion Energy Matters Greatly** — 50-100 eV ions contribute ~20-30% of ashing rate via physical sputtering, and they directly affect residue formation (high ions = less residue).

7. **Decomposition Products Determine Residue** — Incomplete oxidation (CO, partial CₓOᵧ) creates residue. Higher temperature and better radical transport reduce residue by driving complete oxidation to CO₂.

---

**Next Chapter:** [Chapter 3 - Plasma-Resist Interactions](./03-plasma-resist-interactions.md)

---

**Chapter 2 Development Status:** Comprehensive kinetic framework established  
**Version:** 1.0

