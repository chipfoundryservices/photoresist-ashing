# Chapter 1: Photoresist Materials & Post-Etch Challenges

## Overview

Photoresist is the lithographic mask that transfers circuit patterns onto semiconductor layers during manufacturing. After patterning (via lithography) and pattern transfer (via etch), the photoresist must be completely removed before the next process step. This chapter establishes what photoresist is, why it must be removed, and what challenges arise during removal.

**Learning Objectives:**
- Understand photoresist composition and lithographic chemistry
- Recognize photoresist states after lithography and etch
- Identify challenges in selective photoresist removal
- Appreciate why photoresist ashing becomes critical at advanced nodes
- Connect resist removal to device yield and manufacturing cost

---

## 1.1 Photoresist Chemistry & Composition

### 1.1.1 Basic Novolac Resist Formulation

Modern photoresists for semiconductor patterning use **chemically-amplified resist (CAR)** technology with three main components:

```
Photoresist formulation (typical):

Component 1: Novolac Resin (base polymer)
  - Phenolic-formaldehyde condensation polymer
  - Aromatic backbone with hydroxyl (-OH) groups
  - Structure: Benzene rings linked by CH₂ bridges
  - Mass fraction: 70-80% of resist
  - Molecular weight: 1000-5000 g/mol (oligomeric to polymeric)

Component 2: Photoacid Generator (PAG)
  - Small organic molecule that generates acid upon UV exposure
  - Examples: Onium salts (triphenylsulfonium, diaryliodonium)
  - Mass fraction: 5-15% of resist
  - Mechanism: UV photon → acid cation + counter-anion

Component 3: Additives (5-10%)
  - Surfactants (surface tension control)
  - Solvent (PGMEA, propylene glycol monomethyl ether)
  - Anti-quenchers (protect acid from deactivation)

Total resist thickness: 50-100 nm (advanced DUV)
                        20-40 nm (EUV, more aggressive)
```

### 1.1.2 Lithographic Chemistry

The resist undergoes chemical changes during exposure and development:

```
Step 1: Unexposed resist (pristine state)
  - Novolac backbone stable
  - PAG dormant
  - Resist is insoluble in alkaline developer

Step 2: UV Exposure (lithography)
  - Photon (λ = 248 nm for KrF, 193 nm for ArF, 13.5 nm for EUV)
  - PAG absorbs photon → generates acid (H⁺)
  
  Example: Triphenylsulfonium salt (TPS)
  TPS⁺ + hν → TPS*⁺ → [H⁺ + neutral radical]
  
  Acid diffuses through resist (20-100 nm diffusion length)

Step 3: Post-Exposure Bake (PEB)
  - Temperature: 90-110°C, ~60 seconds
  - Acid catalyzes deprotection (if protection groups present)
  - OR acid catalyzes crosslinking (increases solubility loss)

Step 4: Development (alkaline rinse)
  - Exposed regions: Acid catalyzed material → more soluble
  - Unexposed regions: Original novolac → insoluble
  - Developer removes exposed resist, leaves patterns

Result: Pattern formed by differential solubility
        Lines/trenches: Cleared resist
        Spaces: Protected resist
```

### 1.1.3 Post-Lithography Resist State

After lithography and development, the resist remains on the wafer:

```
Resist layer characteristics after patterning:

Physical state:
  - Thickness remaining: ~30-80 nm (varies by node, design)
  - Surface roughness: ~1-3 nm (RMS)
  - Adhesion: Good (via adhesion promoters like HMDS)
  - Density: ~1.2-1.3 g/cm³ (porous polymeric structure)

Chemical state:
  - Exposed regions chemically modified (crosslinked or deprotected)
  - Unexposed regions pristine novolac
  - Acid residue (PAG byproducts) distributed throughout
  - Some unfinished deprotection reactions (kinetically limited at PEB)

Pattern fidelity:
  - Line width: Per design (45 nm to >100 nm depending on node)
  - Line edge roughness (LER): 8-15 nm (3σ, major yield driver)
  - Critical dimension (CD): ±5-10% uniformity required
```

---

## 1.2 Etch Process & Post-Etch Resist State

### 1.2.1 Resist as Pattern Mask During Etch

After lithography, the patterned resist serves as an **etch mask** to transfer patterns into underlying layers:

```
Pattern transfer sequence:

Layer stack (simplified):
  Resist (40-80 nm)
    ↓ [etch into]
  Hard Mask or Dielectric (20-500 nm)
    ↓ [etch into]
  Device Layer (Si, SiO₂, metal, etc.)

Etch process:
  - Plasma etches resist + hard mask + device layer
  - Resist is consumed progressively (etch rate ~5-20 nm/min)
  - Resist acts as mask until completely consumed
  - Selectivity between resist and hard mask: ~1-5:1 (resist consumes)

Time in plasma:
  - Hard mask etch: 30-120 seconds
  - Device layer etch: 30-300 seconds (deep features)
  - Total exposure: 1-10 minutes of resist in plasma
  - Dose: Ion bombardment ~10¹⁷ ions/cm² (very aggressive)
```

### 1.2.2 Resist Degradation During Etch

Exposure to plasma (ions, radicals, UV) fundamentally changes resist:

```
Plasma damage mechanisms:

Mechanism 1: Ion Sputtering
  - Ion bombardment (Ar⁺, O⁺, etc.)
  - Physical removal of material (50-100 eV typical ion energy)
  - Removes surface atoms, causes subsurface vacancies
  - Creates dangling bonds and radical sites

Mechanism 2: Radical Attack
  - F· (fluorine) attacks C-C and C-H bonds (for fluorine chemistries)
  - Cl· (chlorine) attacks similar bonds
  - O· (oxygen) oxidizes carbon, decomposes organic links
  - Result: Bond breakage, fragmentation

Mechanism 3: UV Photons
  - Deep UV photons (excimer lamp lines) dissociate bonds
  - Especially C-H bond scission
  - Creates reactive carbon radicals and fragmented products

Mechanism 4: Cross-Linking Enhancement
  - High energy density (UV + ions) promotes polymer cross-linking
  - Increases molecular weight and polymer network strength
  - Makes resist harder and less volatile
  - Complicates removal in post-etch ashing

Combined effect: Resist becomes
  - Chemically modified (fragmented, cross-linked)
  - Structurally weak (porous, fractured)
  - Difficult to remove (degradation products bond strongly)
  - Contaminated (ion implants, metal deposits from sputtering)
```

### 1.2.3 Post-Etch Resist Condition

After etch, the resist is in a very different state than pristine:

```
Post-etch resist characteristics:

Chemical composition (changed):
  - Original novolac: ~70%
  - Cross-linked polymers: ~15-20% (etch byproducts)
  - Oxide/ash residue: ~5-10% (oxidized carbon)
  - Metal contamination: ~0.1-1% (from sputtering, implantation)
  - Volatile fragments: Partially decomposed, still on surface

Physical structure (degraded):
  - Porosity increased: ~5-10% void fraction
  - Surface roughness increased: ~3-8 nm (damaged surface)
  - Tensile stress: ~100-300 MPa (ion implantation creates stress)
  - Adhesion: Still reasonable (polymer network remains)

Thickness remaining:
  - Hard mask etch: Resist may be 20-40 nm (25-50% consumed)
  - Very deep device etch: <10 nm remaining (90% consumed)
  - Some regions: Resist completely removed (no mask left)

Reactive sites:
  - Dangling bonds and radical sites from ion bombardment
  - Carbonyl groups from oxidation
  - Cross-linked network (difficult decomposition path)
```

---

## 1.3 Challenges in Selective Photoresist Removal

### 1.3.1 Why Resist Must Be Removed

After pattern transfer, the resist no longer serves a purpose and must be completely removed before the next process:

```
Process sequence (3D NAND example):

1. Lithography: Pattern resist
2. Etch (hard mask): Transfer resist pattern to carbon mask
3. Strip resist: Remove resist (THIS CHAPTER)
4. Etch (device layer): Deep etch using carbon as mask
5. Residue removal: Clean surfaces post-etch
6. ALD: Deposit dielectric layer
7. Repeat: Multiple patterning cycles

Why resist removal is essential:

- Contamination risk: Resist carbon and organics interfere with:
  * ALD nucleation (poor film quality)
  * Metal adhesion (delamination)
  * Subsequent lithography (pattern distortion)
  
- Thermal budget: Resist burns at ~300°C
  - Residual resist causes outgassing in downstream processing
  - Can degrade device performance

- Process fidelity: Resist on surface affects:
  * Etch uniformity in next layer
  * Electrical measurements (oxide integrity)
  * Lithography overlay (CD uniformity loss)

- Yield impact: Incomplete resist removal causes 1-5% yield loss
  - Defects in dielectric layer
  - Metallization failures
  - Device parametric loss
```

### 1.3.2 Selectivity Requirement: Core Challenge

The **central challenge** of photoresist ashing is **selectivity**: removing resist while protecting underlying layers.

```
Selectivity definitions:

Hard Mask (carbon, Si₃N₄, etc.) below resist:
  S = Rate_resist / Rate_hardmask
  Requirement: >3:1 (ideal >5:1)
  Why hard: Both resist and hardmask are organic/ceramic
  
Dielectric (SiO₂) below resist:
  S = Rate_resist / Rate_SiO₂
  Requirement: >5:1 (ideal >10:1)
  Why hard: Both contain C-O bonds
  
Metal (Cu, W, Al) below resist:
  S = Rate_resist / Rate_metal
  Requirement: >10:1 (ideal >20:1)
  Why hard: Metals are oxidation-prone (O₂ plasma)

Problem: These materials are chemically similar
  - Resist: C, H, O, N (organic polymer)
  - SiO₂: Si-O bonds (but O is also in resist)
  - Carbon hardmask: Pure C (compete with resist carbon)
  - Metals: M-O bonds form easily in O₂ plasma

Solution complexity:
  - Cannot use chemical selectivity alone (all oxidizable)
  - Must rely on:
    * Temperature effects (different activation energies)
    * Ion energy tuning (adjust sputtering contribution)
    * Pressure modulation (affect radical/ion balance)
    * Multi-step recipes (different conditions for each step)
```

### 1.3.3 Competing Goals in Ashing

Multiple requirements create trade-offs:

```
Requirement 1: Selectivity (protect underlayer)
  - Lower temperature → better selectivity (higher activation energy margin)
  - Lower ion energy → better selectivity (less physical sputtering)
  - Higher pressure → better selectivity (more radical, less ion)
  Trade-off: These conditions SLOW ashing rate

Requirement 2: Ashing Rate (maintain throughput)
  - Higher temperature → faster ashing
  - Higher ion energy → faster ashing
  - Lower pressure → faster ashing
  - Higher power → faster ashing
  Trade-off: These conditions REDUCE selectivity

Requirement 3: Uniformity (avoid thick/thin regions)
  - Careful pressure selection (~50-100 mTorr optimal for O₂)
  - Thermal stability (±2-3°C control)
  - Gas distribution (showerhead design)
  Trade-off: Uniformity adds cost

Requirement 4: Residue Control (minimize post-ashing cleanup)
  - Lower temperature → MORE residue (incomplete decomposition)
  - Higher selectivity → MORE residue (polymer accumulation)
  - Faster ashing → LESS residue (higher temperature)
  Trade-off: Residue vs. selectivity conflict

Requirement 5: Throughput (minimize time per wafer)
  - Faster ashing → better throughput
  - But faster = worse selectivity + more residue
  Trade-off: Cost/yield pressure vs. selectivity

Integration: Must balance ALL FIVE simultaneously
```

---

## 1.4 Technology Node Evolution & Why Ashing Became Critical

### 1.4.1 Historical Context

At older technology nodes (>32 nm), photoresist ashing was **not critical**:

```
32 nm and older nodes (2010s):

Hard mask thickness: 100-200 nm (thick, easy to protect)
Feature depth: 50-100 nm (shallow, low-AR)
Resist thickness: 80-150 nm (thick, easy to remove)
Selectivity requirement: ~2-3:1 (easy to achieve)
  - Simple O₂ plasma at moderate power
  - Recipe: Fixed P, W, T (no tuning needed)
  - Yield: 95%+ (resist ashing not a bottleneck)

Reason: Large feature size and thick masks provided margin
  - Hard to under-etch resist (remaining resist acceptable)
  - Easy to avoid over-etching hard mask (thick protection)
  - No aggressive selectivity tuning needed
```

### 1.4.2 Advanced Nodes (64L and Beyond)

Everything changed at 64L:

```
64L and beyond (2020s and forward):

Hard mask thickness: 20-50 nm (thin, difficult to protect)
Feature depth: 200-500 nm (deep, high-AR: 4:1 to 20:1+)
Resist thickness: 40-80 nm (thin, easy to over-etch)
Selectivity requirement: >5:1 minimum, >8:1 preferred
  - Complex recipe with temperature and power tuning
  - Multi-step approach (high rate + high selectivity)
  - Yield impact: 2-5% loss from over-etch or residue

Reason: Scaling has compressed all dimensions
  - Hard mask now ~20-50 nm (0.5-1× resist thickness)
  - Over-etch of 10 nm damages device seriously
  - Selectivity margin gone (must control perfectly)
  - ARDE must be compensated actively
  
Critical challenge: Simultaneous requirements
  - Fast enough: Maintain throughput (60-100 wafers/hour)
  - Selective enough: Protect hard mask to ±1-2 nm
  - Uniform enough: ±5% across 300mm wafer
  - Residue clean: <2-5 nm post-ashing residue
  - Cost-effective: Not add >15% to wafer cost
```

### 1.4.3 Why 3D NAND Particularly Demands Ashing Excellence

3D NAND architecture makes ashing **especially critical**:

```
3D NAND specifics (64L and beyond):

Architecture:
  - Vertical bit-lines (trenches): 50-100 nm diameter, 500-2000 nm deep
  - High-AR features: 5:1 to 40:1 common
  - String stacks: 64-128 layers, ~5 nm thick each
  
Pattern transfer uses carbon hard mask:
  Step 1: Lithography + resist etch (transfers pattern to resist)
  Step 2: Hard mask etch (transfers pattern to carbon, resist stripped)
  Step 3: DEEP device etch (carbon masks silicon etch, 2-5 µm deep)

Why photoresist ashing is critical in 3D NAND:

1. Selectivity critical: Carbon hardmask (20-50 nm) must not be damaged
   - Over-etch >10 nm = device failure
   - No margin for error

2. Deep trenches complicate residue: Post-ashing CₓOᵧ remains in trenches
   - High-AR features: 5-10 µm deep with <100 nm trench width
   - Residue removal becomes 2nd bottleneck
   - Must remove >95% of residue before ALD

3. Uniformity from dense to isolated: ARDE effects are severe
   - Ashing rate varies 5-10× from center (dense) to edge (isolated)
   - Compensation via multi-step recipes essential
   - Cannot use simple single-step approach

4. Thermal coupling: Multiple etch chambers in cluster
   - Adjacent hard-mask etch at 200°C heats ashing chamber
   - Thermal transient affects selectivity
   - Pre-conditioning required (adds 30-60 sec per wafer)

5. Yield impact: 2-5% loss directly traceable to ashing failures
   - Carbon hard mask damage: Open circuit / leakage
   - Residue in trenches: ALD defects → dielectric breakdown
   - Selectivity loss: Device shorts or opens
```

---

## 1.5 Resist Types & Variations

### 1.5.1 Lithography Technology Impact

Different lithography wavelengths use different resist types:

```
KrF (248 nm, older nodes):
  - Novolac + diazo compound
  - Thicker films (80-150 nm)
  - Better ashing properties (less cross-linking)
  - Largely phased out for 32 nm and below

ArF (193 nm, mainstream DUV):
  - Novolac + onium salt PAG
  - Intermediate thickness (50-100 nm)
  - Cross-linking moderate
  - Used for 32 nm down to ~7 nm (with resolution enhancement)

EUV (13.5 nm, next generation):
  - Methacrylate-based (more cross-linked than ArF)
  - Very thin (20-40 nm) due to absorption
  - Higher cross-linking density
  - Harder to ash (requires aggressive conditions)
  - Still evolving (not all variants characterized)
```

### 1.5.2 Ashing Behavior Variations

Different resist types ash at different rates:

```
Ashing rate comparison (same plasma, 80 mTorr, 2000W, 20°C):

KrF novolac: ~15 nm/min (reference)
ArF resist:  ~12 nm/min (8% slower, more cross-linked)
EUV resist:  ~8 nm/min (47% slower, much more cross-linked)

Selectivity variation:

           C / SiO₂    C / Carbon hardmask
KrF:       6:1         3:1
ArF:       5:1         2.5:1
EUV:       3:1         1.5:1 (worse selectivity!)

Implication:
  - EUV ashing is harder (slower, poorer selectivity)
  - Requires more aggressive ashing conditions
  - Higher risk of hard mask damage
  - Advanced selectivity tuning (temperature, ion energy) essential
  
EUV challenges:
  - Photon energy (92 eV) causes more damage than ArF (6.4 eV)
  - Resist becomes more cross-linked (carbonized)
  - More residue remains post-ashing
  - Higher thermal decomposition required (higher T risk)
```

---

## 1.6 Summary & Key Takeaways

1. **Resist Composition Simple, Behavior Complex** — Novolac + PAG is straightforward chemistry, but plasma damage creates cross-linked, fragmented material that is hard to remove.

2. **Post-Etch Resist Highly Degraded** — After pattern transfer (etch), resist is chemically modified, structurally weakened, and contaminated. Different material than pristine resist.

3. **Selectivity is the Central Challenge** — Removing resist while protecting hard mask, dielectric, and metal requires balancing chemical and ion-assisted mechanisms, temperature, and pressure.

4. **Advanced Nodes Demand Excellence** — 64L and beyond compressed all dimensions. Hard mask now thin (20-50 nm), margin gone (1% selectivity loss = 10 nm damage), uniformity critical, residue must be cleaned aggressively.

5. **3D NAND Makes Ashing Particularly Critical** — Carbon hard mask (20-50 nm) protecting deep trenches (500-2000 nm, high-AR) creates zero-margin selectivity requirement.

6. **Ashing Rate vs. Selectivity Trade-Off** — Conditions for fast ashing (high T, high power, low pressure) are opposite to conditions for high selectivity. Multi-step recipes or temperature tuning required.

7. **Temperature is Powerful Tuning Knob** — ~15%/10°C temperature dependence allows selectivity tuning without RF power changes (unique compared to fluorine etch).

8. **Residue Challenge Distinct** — Post-ashing residue (CₓOᵧ) is different from post-etch fluorocarbon residue. Removal essential for ALD nucleation and device yield.

---

**Next Chapter:** [Chapter 2 - Photoresist Decomposition Chemistry](./02-decomposition-chemistry.md)

---

**Chapter 1 Development Status:** Comprehensive foundational content complete  
**Version:** 1.0

