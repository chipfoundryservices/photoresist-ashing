# Appendix B: Photoresist Property Database

## B.1 Common Photoresist Materials

```
Resist type and properties:

ArF Resist (193 nm, most common for 3D NAND):

  Chemical formula: Novolac + PAG (photo-acid generator)
  Novolac base: C₆H₄OH oligomers (phenolic resin)
  PAG example: Onium salt (Ph)₃S⁺ PF₆⁻
  
  Physical properties:
    Density: 1.05-1.15 g/cm³
    Refractive index: 1.58-1.65 (at 193 nm)
    Glass transition T_g: 130-160°C
    Decomposition T_decomp: 200-300°C
  
  Ashing properties:
    Ashing rate in O₂ plasma: 50-70 nm/min (typical)
    Activation energy E_a: ~12 kcal/mol
    Selectivity to SiO₂: ~15-20:1 (production)
    Selectivity to resist C/HM: ~2.7-3:1 (challenging)
    Residue formation: 10-15 nm (CₓOᵧ after ashing)

EUV Resist (13.5 nm):

  Chemical composition: Similar to ArF in architecture
  PAG: Newer formulations (improved sensitivity)
  Dissolution properties: Tuned for higher EUV sensitivity
  
  Ashing characteristics (similar to ArF):
    Ashing rate: 55-75 nm/min
    E_a: ~12-13 kcal/mol (slightly higher than ArF)
    Selectivity to SiO₂: ~15-20:1 (same range)
    Residue: 10-15 nm (similar to ArF)
    Main difference: Pattern fidelity (line roughness)
                    LWR ~3-5 nm (EUV worse than ArF)

```

## B.2 Resist Thickness Specification Database

```
Typical resist thicknesses by technology node:

Logic/MPU (FinFET):
  32/28 nm: 80-100 nm
  22/20 nm: 90-110 nm
  14/10 nm: 90-120 nm
  7 nm:     80-100 nm

3D NAND (64L-128L):
  64 layers: 80-100 nm per resist layer
  96 layers: 90-110 nm
  128 layers: 100-120 nm
  176 layers: 120-150 nm (thicker for uniformity)
  
  Rationale: Thicker resist needed for deep trenches
  More resist → better top-to-bottom ashing uniformity

DRAM (1y nm - 20z nm):
  ~100-120 nm (similar to high-end logic)

Specification example (representative):

Resist: ArF, 100 nm target
Tolerance: ±5 nm (typical spec)
Minimum acceptable: 95 nm
Maximum acceptable: 105 nm

Post-ashing acceptance:
  Remaining resist: <2 nm (complete removal)
  Residue: <1 nm (CₓOᵧ)
  No defects (pinholes, cracks, delamination)
```

## B.3 PAG Performance Spectrum

```
Photo-acid generator (PAG) characteristics:

PAG type              Quantum Yield    Decomp Temp   Comments
─────────────────────────────────────────────────
Onium salt (standard) 0.8-1.0          300-400°C     Proven, widely used
Diazonium             0.7-0.9          250-320°C     Older technology
Sulfonate             0.9-1.0          350-420°C     Enhanced stability
Triphenylmethane      0.8-0.95         280-360°C     Modern development

Thermal stability impact on ashing:
  PAG decomposes at 200-250°C (during ashing exposure)
  Generates acid, which can crosslink resist
  Crosslinked regions etch slower
  Effect: Minor (1-2% rate variation, usually ignored)
  
  In hot ashing (>80°C):
    PAG decomposition accelerates
    Crosslinking increases
    Rate may decrease by 5-10%
    Selectivity can improve (crosslinked resist more stable)
```

## B.4 Resist Degradation During Post-Etch

```
Resist surface degradation after ashing (CₓOᵧ layer):

Composition and formation:

  Primary residue: CₓOᵧ with y/x ≈ 0.3-0.8
  
  Formation mechanism:
    - Incomplete oxidation of resist fragments
    - Redeposition from gas phase
    - Accumulates especially in cool regions
  
  Thickness: 10-20 nm (depending on recipe)
  Hardness: Similar to carbon (mechanically durable)
  Chemical nature: Partially oxidized polymer
                   Some C=O and C-O bonds present
                   Organic, not truly glassy

Reactivity profile:

  Thermal decomposition:
    T = 80°C: Very slow (<1 nm/hour removed)
    T = 120°C: Moderate (~5 nm/hour)
    T = 150°C: Fast (~15 nm/hour)
    T = 200°C: Very fast (complete removal 30 min)
  
  O₂ plasma removal:
    Low power (500 W): ~1 nm/min
    Moderate (1000 W): ~2 nm/min
    High (1500 W): ~3-4 nm/min

Post-ashing oxidation (air exposure):

  Resist surface oxidizes after ashing:
    t = 1 min: ~10-20 Å native oxide
    t = 60 min: ~80-100 Å (plateau)
  
  This oxide affects next process (ALD nucleation)
  Thinner is better: keep <30 Å by minimizing air exposure

```

## B.5 Resist Defect Sensitivity

```
Common defects post-ashing and yield impact:

Defect type          Occurrence    Yield Impact    Severity
─────────────────────────────────────────────────
Pinholes (resist)    ~10-100 ppm   0.1-1% loss     CRITICAL
Roughness >10 nm     ~1% of wafers 0.5-2% loss     HIGH
Residue >2 nm        ~5% of wafers 0.2-1% loss     MEDIUM
Notching >20 nm      ~0.1% of wafers <0.1% loss    LOW
Delamination         ~0.01% rare   Entire wafer    CRITICAL

Pinhole formation mechanism:

  Formed when:
    1. Resist roughness >10 nm
    2. Residue creates pinholes
    3. Over-etch at selectivity margin
  
  Prevention:
    - Minimize roughness (ion energy, temperature)
    - Thorough residue removal (<1 nm)
    - Endpoint detection with 5 nm margin
    - Spectroscopic monitoring (C₂ signal reliability)
  
  Detection:
    - Electrical (leakage current measurement)
    - Optical (darkfield inspection)
    - X-ray (critical layers only)

Yield models:

  Defect-free yield: Y = (1 - D_pinhole) × (1 - D_other)
  
  Example calculation:
    Pinhole occurrence: 50 ppm (0.005%)
    Other defects: 100 ppm (0.010%)
    Total defect rate: 150 ppm
    Yield: Y = 0.99995 × 0.9999 = 0.9998 = 99.98%
    Loss per wafer: 2 ppm (very small)
    Loss per 1000-wafer lot: ~0.2 wafers
```

---

**Appendix B Complete: Photoresist Property Database**

