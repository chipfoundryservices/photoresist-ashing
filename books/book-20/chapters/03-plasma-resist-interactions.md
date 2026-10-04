# Chapter 3: Plasma-Resist Interactions

## Overview

Photoresist ashing occurs in **oxygen plasma**—a highly reactive environment containing electrons, ions, excited atoms, and radicals. Understanding which species attack resist, how energetically, and at what rates is essential for recipe development and selectivity tuning. This chapter quantifies plasma-resist interactions and develops predictive models.

**Learning Objectives:**
- Understand oxygen plasma generation mechanisms (CCP, ICP)
- Identify primary reactive species (O·, O⁺, metastable O₂)
- Quantify ion energy distributions and their effects
- Model chemical vs. ion-assisted ashing pathways
- Predict reaction rates and selectivity
- Connect plasma properties to process control

---

## 3.1 Oxygen Plasma Generation

### 3.1.1 Plasma Creation Mechanisms

Oxygen plasma is created by coupling RF energy (either capacitive or inductive):

```
CCP (Capacitive Coupling Plasma):
  RF voltage applied directly between electrodes (typically 13.56 MHz)
  Voltage creates oscillating electric field
  Free electrons accelerated across gap
  Electron-neutral collisions → ionization cascade
  
  Characteristics:
    - Higher ion energy (self-bias develops)
    - Lower electron temperature (Te ~2-3 eV)
    - Lower plasma density (10⁹-10¹⁰ cm⁻³)
    - Better control of ion energy via bias power

ICP (Inductive Coupling Plasma):
  RF coil creates oscillating magnetic field (typically 13.56 MHz)
  Magnetic field induces circular electron motion (cyclotron)
  Electron velocity increases without direct acceleration
  Result: Very high electron temperature
  
  Characteristics:
    - Lower ion energy (no DC self-bias)
    - Higher electron temperature (Te ~4-5 eV)
    - Higher plasma density (10¹¹-10¹² cm⁻³)
    - Better for radical generation (high Te)

Hybrid CCP+ICP:
  Coil for bulk plasma generation (ICP, high density)
  DC or RF bias on electrode (CCP, ion energy control)
  Result: High density + independent ion energy tuning
  Most production ashing chambers use hybrid approach
```

### 3.1.2 Oxygen Dissociation & Ionization

How does O₂ create reactive species?

```
Electron impact dissociation:

Primary pathway:
  e⁻ + O₂ → e⁻ + O(³P) + O(³P)
  
  Threshold: ~6 eV electron energy
  Cross-section: σ(6-10 eV) ≈ 2-3 × 10⁻¹⁶ cm²
  (Very small! But high electron flux compensates)

Competing pathways:

Excitation to metastable state:
  e⁻ + O₂ → e⁻ + O₂(¹Δ) [excited singlet delta oxygen]
  Lifetime: ~40 minutes (very stable, important for selectivity)
  
Ionization:
  e⁻ + O₂ → 2e⁻ + O₂⁺
  Threshold: ~12 eV
  Or further: O₂⁺ → O⁺ + O· (fast dissociative ionization)

Resulting species distribution (typical CCP O₂ plasma):

Species         Fraction of plasma    Notes
─────────────────────────────────────────
e⁻              1-5%                 Free electrons
O(³P)           ~10-20%              Atomic oxygen radical (reactive)
O₂              ~70-80%              Unreacted molecular
O⁺              ~1-2%                Molecular ion
O₂⁺             ~0.5-1%              Molecular ion
Metastable O₂   ~1-2%                Long-lived excited state
```

---

## 3.2 Reactive Species & Ashing Mechanisms

### 3.2.1 Atomic Oxygen (O·) – Primary Reactive Species

Atomic oxygen radicals are the **workhorses** of resist ashing:

```
Atomic oxygen radical O(³P):

Generation: e⁻ + O₂ → O· + O· (as described above)

Chemical reactivity with resist:

  C-H bond attack:
    R-CH₃ + O· → R-CH₂· + OH·
    R-CH₂· + O₂ → R-CH₂OO· (peroxyl radical)
    Propagation: R-CH₂OO· → R-CHO + ·OH
    
  Result: C-H scission, formation of aldehydes/ketones

Reaction cross-section:
  σ(O· + resist) ~10⁻¹⁵ cm² (large, favorable for reaction)
  
O· flux estimation:

In oxygen plasma:
  Electron temperature: Te ~3 eV
  Electron density: ne ~10⁹-10¹⁰ cm⁻³
  Dissociation cross-section: σ ~2-3 × 10⁻¹⁶ cm²
  Electron thermal velocity: v_e ~10⁷ cm/s
  
  Dissociation rate coefficient: k ~10⁻⁹ cm³/s
  O· production rate: n(O·) = k × n_e × n(O₂) ~10¹² cm⁻³
  
O· flux to surface (diffusive transport at 50 mTorr):
  Φ(O·) ~10¹⁵ radicals/(cm²·s)
  
Ashing rate contribution from O· alone:
  R = Φ × Y × M / ρ
  where Y ~1 carbon atom removed per O· collision
  M ~12 g/mol (carbon), ρ ~2 g/cm³
  
  R ~10¹⁵ × 1 × 12 / (6×10²³ × 2) ~10 nm/min (chemical only)
```

### 3.2.2 Oxygen Ions – Secondary & Controlling Force

While O· radicals provide the **base** ashing rate, **ions** determine selectivity and uniformity:

```
Ion species in oxygen plasma:

O⁺ (atomic oxygen ion):
  Formation: e⁻ + O · → 2e⁻ + O⁺
  Fraction: ~30-40% of total ions
  Ion energy: ~20-150 eV (set by plasma potential + bias)
  
O₂⁺ (molecular oxygen ion):
  Formation: e⁻ + O₂ → 2e⁻ + O₂⁺
  Fraction: ~60-70% of total ions
  Ion energy: same as O⁺ (same potential difference)
  
Ion bombardment effects:

Impact at 100 eV:
  - Physical sputtering: Y ~0.5-1.0 carbon atoms/ion
  - Ion energy dissipation in surface layer (~10 nm depth)
  - Creation of defects and reactive sites
  - Acceleration of chemical ashing (ion-enhanced)

Selectivity from ion energy dependence:

  Carbon (resist):      Sputtering yield Y_C ~0.8 at 100 eV
  SiO₂ (dielectric):    Sputtering yield Y_SiO2 ~0.3 at 100 eV
  Silicon:              Sputtering yield Y_Si ~0.2 at 100 eV
  
  Result: High-energy ions preferentially sputter resist
          Lower-energy ions have poor selectivity
          
Optimal ion energy for selectivity: 40-80 eV
  - Enough to help resist ashing (Y ~0.3-0.5)
  - Low enough that other materials unaffected (Y <0.1)
```

### 3.2.3 Metastable Oxygen O₂(¹Δ) – Selectivity Enhancer

Long-lived excited oxygen molecules improve selectivity:

```
Metastable O₂(¹Δ):

Formation: e⁻ + O₂ → e⁻ + O₂(¹Δ)
Excitation energy: ~0.98 eV above ground state
Lifetime: ~40 minutes (! extremely long for plasma species)

Reactivity:
  O₂(¹Δ) + resist → O₂ + oxidized products
  
  Key feature: Reacts differently with different materials
  - Resist (carbon chains): Rapid reaction (selective oxidation)
  - SiO₂: Very slow reaction (already oxidized)
  - Silicon: Moderate reaction (forms SiO₂ layer, then slows)

Selectivity consequence:

  Plasma with high O₂(¹Δ) content: Better selectivity
  ICP typically has higher O₂(¹Δ) (higher Te favors metastable formation)
  CCP typically has lower O₂(¹Δ)
  
  This is one reason hybrid CCP+ICP can achieve best selectivity
```

---

## 3.3 Ion Energy Distribution & Control

### 3.3.1 Measuring Ion Energy Distribution (IED)

An **RPA (Retarding Potential Analyzer)** measures the energy of ions reaching a surface:

```
RPA principle:

  Ions approach retarding electrode
  Applied voltage creates repulsive electric field
  Only ions with energy > applied voltage pass through
  Current vs. voltage → IED
  
  Measurement:
    Sweep voltage 0 to 500 V
    At each voltage, measure ion current
    dI/dV gives IED

Typical oxygen plasma IED (CCP mode, 100 V bias):

  Peak energy: ~70 eV (most probable)
  FWHM (width): ~30-40 eV
  Low-energy tail: ~10-20 eV (some ions lose energy in plasma)
  High-energy tail: ~150-200 eV (rare, multiply-charged ions?)
  
  Shape: Roughly Gaussian for CCP
         Can be broader for ICP (many collisions cool ions)

Quantitative relationship:

  E_ion(mean) ≈ 0.3 × V_bias
  
  Example:
    V_bias = 300 V → E_ion(mean) ≈ 90 eV
    This comes from ionization potential and sheath physics
```

### 3.3.2 Ion Energy Dependence of Ashing

Ashing rate changes dramatically with ion energy:

```
Ashing rate vs. ion energy (50 mTorr, 2000W coil, fixed T):

  E_ion      Rate        Selectivity (C/SiO₂)    Notes
  ─────────────────────────────────────────────────
  20 eV     ~40 nm/min   >20:1                  Chemical only
  50 eV     ~55 nm/min   ~15:1                  Moderate ions
  100 eV    ~70 nm/min   ~8-10:1                High ions
  150 eV    ~85 nm/min   ~5-6:1                 Very aggressive
  200 eV    ~95 nm/min   ~3-4:1                 Dangerous
  
Mechanism:

  Low E_ion (20-30 eV):
    - Ion sputtering minimal (Y < 0.2)
    - Ashing dominated by O· chemical attack
    - Selectivity excellent (Si/SiO₂ unaffected)
    
  Moderate E_ion (50-80 eV):
    - Ion sputtering significant (Y ~ 0.3-0.6)
    - Ion-enhanced chemistry important
    - Both resist and SiO₂ affected, but resist more
    - Good selectivity maintained
    
  High E_ion (>100 eV):
    - Strong sputtering of all materials
    - Ion contribution dominates (~40-50% of total rate)
    - SiO₂ sputtering noticeable
    - Selectivity degrades significantly

Production strategy:

  High selectivity requirement: Keep E_ion < 50 eV
  Balanced approach: E_ion ~60-80 eV (selectivity ~10-15:1)
  Fast ashing: E_ion ~100-150 eV (selectivity ~5-8:1, risky)
```

---

## 3.4 Temperature Effects on Plasma Chemistry

### 3.4.1 Temperature Dependence of Radical Reactions

Temperature doesn't change plasma generation, but it affects **surface chemistry**:

```
At higher wafer temperature (T = 50°C vs. T = 20°C):

Effect 1: Arrhenius acceleration (discussed in Chapter 2)
  Chemical reaction rate increases ~15%/°C

Effect 2: Radical desorption
  Low T: O· radicals stick to surface, accumulate
  High T: O· radicals desorb before reacting (less effective)
  Net effect: Slightly reduced O· reaction efficiency
  Magnitude: ~10% reduction per 20°C increase
  
Effect 3: Surface oxidation layer dynamics
  Low T: Oxide layer accumulates (protective)
  High T: Oxide layer decomposes (loses protection)
  Result: Selectivity changes (discussed in Chapter 2)

Combined thermal effect on selectivity:

  T = 20°C:  Selectivity ~20:1 (thick oxide layer, low Arrhenius boost)
  T = 40°C:  Selectivity ~15:1 (thinner oxide, higher Arrhenius for SiO₂)
  T = 60°C:  Selectivity ~10:1 (no oxide, SiO₂ exposed to full ashing)
  
Overall: 15% per degree Arrhenius + 5-10% thermal effects
         Total ~13-15% per degree observed (matches experimental)
```

---

## 3.5 Summary & Key Takeaways

1. **Oxygen Plasma Generation** — CCP (high ion energy, controlled) and ICP (high density, radical-rich) both used; hybrid approaches optimal.

2. **Atomic Oxygen O· is Primary Ashing Agent** — ~10-20 nm/min chemical ashing rate from O· radicals; provides base ashing with good selectivity.

3. **Ions Control Selectivity & Rate** — O⁺ and O₂⁺ ions (~50-100 eV) provide 30-40% additional ashing rate via sputtering and ion-enhanced chemistry; allow selectivity tuning.

4. **Ion Energy Dominates Selectivity** — Low E_ion (<50 eV) gives selectivity >15:1 but slow ashing; high E_ion (>100 eV) fast but risky selectivity <8:1.

5. **Metastable O₂ Improves Selectivity** — ICP-rich conditions increase O₂(¹Δ) which selectively reacts with resist over SiO₂.

6. **RPA Diagnostics Essential** — Measuring IED shows whether ions are in optimal range; drift in ion energy indicates equipment issues.

7. **Temperature Modulates Chemistry** — Arrhenius drives ~15%/°C rate change; also affects oxide layer and radical sticking (secondary effects).

---

**Next Chapter:** [Chapter 4 - Ashing Chemistries & Gas Selections](./04-ashing-chemistries.md)

---

**Chapter 3 Development Status:** Comprehensive plasma physics and chemistry framework  
**Version:** 1.0

