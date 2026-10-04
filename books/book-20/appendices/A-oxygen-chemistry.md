# Appendix A: Oxygen Chemistry Reference Data

## A.1 O₂ Dissociation & Plasma Species

```
O₂ dissociation pathways in plasma:

Direct impact dissociation:
  e⁻ + O₂ → e⁻ + O₂* (excitation, elastic collision ~5 eV)
  e⁻ + O₂ → e⁻ + 2O (dissociation, requires ~5.1 eV)
  
Ionization:
  e⁻ + O₂ → 2e⁻ + O₂⁺ (ionization, requires ~12.1 eV)
  e⁻ + O₂ → 2e⁻ + O⁺ + O (dissociative ionization, requires ~18.4 eV)
  
Metastable formation:
  e⁻ + O₂ → e⁻ + O₂(¹Δ) (singlet delta, metastable, lifetime ~1 sec)
  e⁻ + O₂ → e⁻ + O₂(³Σ) (triplet, metastable, lifetime ~100 sec)

Major plasma species in O₂ discharge:

Species          Concentration      Role in ashing
─────────────────────────────────────────────
e⁻ (electrons)   ~10⁹ /cm³          Drive dissociation, ionization
O· (radicals)    ~10¹¹-10¹² /cm³    PRIMARY ashing mechanism
O₂⁺ ions         ~10⁹-10¹⁰ /cm³     Ion bombardment, sputtering
O⁺ ions          ~10⁸-10⁹ /cm³      Lower flux, less important
O₂(¹Δ)           ~10¹⁰ /cm³         Excited state chemistry
O₂(³Σ)           ~10¹¹ /cm³         Background excited state
O₃               ~10⁸ /cm³          Trace (minor)
```

## A.2 Radical Reaction Kinetics

```
O· radical oxidation of carbon:

Elementary reactions:

C + O· → CO (primary pathway)
Rate = k₁ × [C] × [O·]
k₁ (at 20°C) ≈ 5×10⁻¹¹ cm³/s (fast, radical-limited)

CO + O· → CO₂ (secondary)
Rate = k₂ × [CO] × [O·]
k₂ ≈ 1×10⁻¹⁰ cm³/s

C-H bond dissociation:

C-H + O· → C· + OH (free radical chain)
C· + O₂ → CO + O· (regenerate O·)

Net: Chain reaction, O· acts as catalyst
One O· can oxidize multiple C atoms before termination

Termination:

O· + O· → O₂ (radical recombination)
Rate = k_rec × [O·]²
k_rec ≈ 2×10⁻¹¹ cm³/s (second-order)

Radical lifetime in bulk gas: τ ≈ 1/[O·] × k_rec ≈ 1-10 ms
```

## A.3 Ion Species Characteristics

```
Ion energy distribution (IED) in capacitive discharge:

O₂⁺ ions:
  Thermal energy: ~0.1 eV (thermal motion)
  Sheath acceleration: ~0.3 × V_bias eV
  Total energy: E ≈ 0.3V_bias
  
  At V_bias = 200 V: E ≈ 60 eV
  At V_bias = 300 V: E ≈ 90 eV
  At V_bias = 500 V: E ≈ 150 eV
  
  FWHM of IED: ~20-30% of peak energy (narrow distribution)

O⁺ ions:
  Lower mass than O₂⁺
  Slightly higher mobility
  Less abundant (~10% of O₂⁺)
  Similar energy distribution

Ion flux calculation:

φ_ion = (j_bias / e) / (1 + M_ratio)

where:
  j_bias = bias current density (A/cm²)
  e = elementary charge (1.6×10⁻¹⁹ C)
  M_ratio = (coil current / bias current) mass ratio
  
Typical production:
  j_bias ≈ 10-20 mA/cm²
  φ_ion ≈ 10¹⁴-10¹⁵ ions/cm²·s
```

## A.4 Molecular Spectroscopy References

```
Optical emission lines useful for diagnostics:

Species    λ (nm)    Transition           Comment
─────────────────────────────────────────────────
O (I)      777       3P-3S (near-IR)      Very bright
O (I)      845       3P-3S variant        Secondary
O₂⁺        427       B²Σ-X²Π              Weak
O₂⁺        560       B²Σ-X²Π              Weak
O₃         254       UV absorption        Ozone signature
C₂         516       Swan band (d-a)      Resist signature
OH         309       A-X band (UV)        Trace

OES (optical emission spectroscopy) use:
  Monitor O atom density relative to baseline
  O· line ∝ dissociation efficiency
  C₂ signature indicates resist presence
  Sharp changes in C₂ → endpoint detection
```

## A.5 Temperature Effects on Dissociation

```
O₂ dissociation fraction vs. temperature (in bulk gas):

Temperature   Dissociation %    Notes
──────────────────────────────
300 K (27°C)     ~1%            Low thermal dissociation
400 K (127°C)    ~2%            Modest increase
600 K (327°C)    ~5%            Noticeable
800 K (527°C)    ~15%           Significant
1000 K (727°C)   ~35%           High
1200 K (927°C)   ~60%           Very high

In plasma (e-impact):
  Dissociation much higher (electron-driven)
  T_electron ≈ 1-2 eV (equivalent ~10,000-20,000 K)
  But T_gas much lower (300-400 K)
  
Gas heating in O₂ discharge:
  Power input ΔP = ~100 W (typical)
  Gas flow rate: ~100 sccm = 1.67×10⁻³ mol/s
  Heat capacity c_p = 3.5 R (diatomic O₂)
  Temperature rise: ΔT = ΔP / (ṅ × c_p)
                    ΔT ≈ 100 / (1.67×10⁻³ × 14.6) ≈ 400 K
  
  Bulk gas temperature rise ~400 K possible
  Combined with electrode cooling: net ~50-100°C elevation
```

---

**Appendix A Complete: Oxygen Chemistry Reference**

