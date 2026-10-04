# Glossary: Photoresist Ashing in 3D NAND

## A

**Activation Energy (E_a):** The minimum energy required for a chemical reaction to proceed. For photoresist ashing in O₂ plasma, E_a ≈ 12 kcal/mol. Higher E_a materials (SiO₂ ~38 kcal/mol) etch slower at low temperature, creating selectivity.

**Ashing:** The process of removing photoresist via plasma oxidation, typically in O₂-based discharges. Distinct from "stripping" (wet chemical removal).

**Aspect Ratio (AR):** The ratio of feature depth to width in a semiconductor device. High-AR features (depth/width > 20:1) present challenges for uniform resist removal due to radical depletion and ion shadowing.

**Arrhenius Equation:** Mathematical model describing temperature dependence of reaction rates: R(T) = A×exp(-E_a/RT). Photoresist ashing rate increases ~15% per 10°C temperature rise.

**ARDE** (Aspect Ratio Dependent Etching): Non-uniform ashing rate across features of different aspect ratios. Deep trenches etch slower than wide openings due to ion/radical depletion and shadowing. Variation: 5-10× rate difference possible without compensation.

---

## B

**Bias Power (W_bias):** RF power applied to the wafer (electrode) in a capacitive discharge, ranging 200-600 W typically. Higher bias increases ion energy and ashing rate but reduces selectivity. Related to ion energy by E_ion ≈ 0.3×V_bias (eV).

**Byproducts:** Gaseous decomposition products from ashing: CO₂, CO, and volatile fragments. Unlike hard-mask etch, O₂ ashing produces primarily CO/CO₂ (no fluorine byproducts).

---

## C

**Carbon Hard Mask (CHM):** Dense carbon film (~30 nm) deposited below photoresist to control etch selectivity and prevent damage to underlying layers. Challenging selectivity target: C/CHM only ~2.7:1.

**C₂ Swan Band:** Optical emission from diatomic carbon molecules (wavelength ~516 nm, visible as green light) during resist ashing. Used for real-time endpoint detection: C₂ signal drops sharply when resist is depleted.

**Capacitive Discharge:** RF plasma generation mode where electrode and chamber walls form a capacitor. Lower plasma density than inductive discharge; typical chamber design for resist ashing.

**Cluster Tool:** Multi-chamber integrated system where wafers undergo sequential processes (deposition, ashing, ALD, metallization) without air exposure. Thermal coupling between chambers creates challenges for ashing uniformity.

**CTE** (Coefficient of Thermal Expansion): Material's fractional length change per degree temperature change (ppm/°C). Carbon CTE ~5 ppm/°C, Si CTE ~2.6 ppm/°C. Mismatch causes thermal stress during ashing.

---

## D

**Dissociation:** Breaking of chemical bonds by electron impact in plasma. O₂ dissociation requires ~5.1 eV from electron collision, producing atomic oxygen (O·) radicals.

---

## E

**Electron Cyclotron Resonance (ECR):** Plasma generation mode not typically used for resist ashing; mentioned for comparison to standard CCP/ICP designs.

**Electron Impact:** Process where energetic electrons collide with gas molecules, causing excitation, ionization, or dissociation. Electron energy ~1-2 eV in O₂ plasma (effective temperature ~10,000-20,000 K).

**Endpoint Detection:** Real-time monitoring to determine when resist removal is complete. Methods: (1) Optical (C₂ Swan band emission), (2) Electrical (reflected RF power), (3) Timer backup (blind endpoint).

---

## F

**Fluorocarbon Polymer:** Protective polymer layer (CF_x, from trace fluorine or byproducts) that accumulates during ashing in some processes. In O₂ ashing, residual polymer is CₓOᵧ (carbon-oxygen), not fluorinated.

---

## G

**Gas-Phase Chemistry:** Reactions occurring in the plasma bulk (not at surface). Includes O· radical formation, O₂ dissociation, and ion generation. Competes with surface chemistry.

---

## H

**Hard Mask Etch:** Preceding step to resist ashing; removes hard-mask material (carbon) through deeper trenches. Different chemistry (often fluorine-based); ashing is separate downstream step for resist removal.

---

## I

**IED** (Ion Energy Distribution): Statistical distribution of ion kinetic energies entering the wafer. In CCP discharges, IED is narrow (~20-30% FWHM) with peak at ~0.3×V_bias eV.

**Impedance Matching:** RF network tuning to maximize power transfer from generator to plasma. L-match or π-match networks adjust capacitance/inductance to achieve 50 Ω load impedance, minimizing reflected power.

**Inductive Discharge:** Plasma generation mode using coil coupling (ICP). Higher plasma density than CCP; not standard for resist ashing (CCP more common).

**Inert Gas Purge:** Nitrogen or argon gas flow used to prevent oxidation or cool chamber after ashing. N₂ purge standard in cluster tools to protect wafer surface post-ashing.

**Integrated Process Module (IPM):** Multi-chamber tool architecture with deposition, ashing, and ALD integrated. Thermal management critical due to ~110-130°C transients between chambers.

**Ion Bombardment:** Physical damage to wafer surface by energetic ions (~50-150 eV). Contributes to ashing rate but also to roughness and selectivity loss. Controllable via bias power.

**Ion Flux (φ_ion):** Number of ions reaching wafer per unit area per unit time, typically ~10¹⁴-10¹⁵ ions/cm²·s. Related to bias current and dictates ion-assisted ashing contribution.

---

## L

**LWR** (Line Width Roughness): Stochastic variation in resist line width along the trench sidewall. Ashing increases apparent LWR by ~1-3 nm due to resist surface roughening during ion bombardment.

---

## M

**Mean Free Path (λ):** Average distance a gas molecule travels before collision. At 70 mTorr, λ ≈ 100 µm (much larger than ~1 cm chamber gap); determines transition between ballistic and diffusive transport.

**Metastable:** Excited atom/molecule with long lifetime (>100 ms) that can participate in chemical reactions. O₂(¹Δ) (singlet delta) is important metastable state in O₂ plasma.

**Microloading:** Non-uniform ashing rate depending on feature density. Dense features etch slower due to local radical depletion. Achievable uniformity: ±10-15% with proper pressure tuning.

---

## N

**Native Oxide:** Spontaneous oxidation of carbon surface when exposed to air/oxygen. Forms ~10-20 Å in first minute, ~80-100 Å after 1 hour (saturates, self-passivating). Affects ALD nucleation quality.

**Notching:** Undercutting at oxide-resist interface during ashing. Resist below oxide undercuts, oxide overhangs. Depth: 10-20 nm typical. Reduced by lower ion energy or two-step endpoint approach.

**Novolac:** Base polymer in ArF photoresist; phenolic resin with weakly cross-linked aromatic rings. Molecular weight ~200-500 g/mol per repeating unit.

---

## O

**Optical Emission Spectroscopy (OES):** Monitoring of plasma light emission to diagnose plasma state. Key lines: O 777 nm (oxygen atoms), O₂⁺ 427 nm (ions), C₂ 516 nm (resist signature).

**Over-etch:** Continuation of plasma ashing after resist is completely removed. In optimized processes: <5 nm over-etch (within selectivity margin). Excessive over-etch damages hard mask and underlying layers.

---

## P

**PAG** (Photo-Acid Generator): Chemical component in ArF/EUV resist; onium salt or diazonium that generates proton (H⁺) upon UV exposure. Proton catalyzes resist deprotection reactions during lithography.

**Pulsed Plasma:** Discontinuous RF power application (duty cycle <100%) to improve ARDE by allowing radical diffusion into deep features during off-time. Reduces ARDE by 2-3× but increases total time.

---

## R

**Radical:** Neutral species with unpaired electron (e.g., O·). Highly reactive; responsible for majority of resist ashing in O₂ plasma. Lifetime ~1-10 ms in bulk gas.

**Reflectance:** Fraction of RF power reflected back from load (plasma + chamber). Related to impedance mismatch; typical <10% reflected (good matching), >20% reflected (poor matching, mistuned).

**Residue:** Partially oxidized carbon polymer (CₓOᵧ) remaining after ashing, typically 10-15 nm thick. Must be removed via thermal annealing or O₂ plasma before ALD/metallization.

**RF** (Radio Frequency): Electromagnetic wave at MHz frequencies (13.56 MHz standard for ashing). Applied to electrodes to sustain plasma via capacitive coupling (CCP) or inductive coil (ICP).

---

## S

**SAC** (Self-Aligned Contact): Process where metal (typically tungsten) is deposited directly on carbon hard mask in trench bottom, self-aligned to feature sidewalls. Sensitive to resist contamination and native oxide.

**Selectivity:** Ratio of ashing rates between two materials. C/SiO₂ ~15-20:1 (excellent), C/CHM ~2.7:1 (challenging), C/Si ~20:1 (good). Temperature and ion energy control selectivity.

**Sputtering:** Physical ejection of atoms from surface by ion impact. Yield (atoms/ion) varies with material: carbon ~0.8, SiO₂ ~0.3, Si ~0.2. Contributes to ashing rate and surface roughening.

**Substrate:** Silicon wafer or lower layer beneath all process layers. Generally protected by hard mask and SiO₂ during ashing; selectivity to Si naturally very high (>20:1).

---

## T

**TEM** (Transmission Electron Microscopy): Cross-sectional imaging technique used for post-etch verification. Shows resist remaining, hard-mask damage, selectivity, and residue thickness with ~0.5 nm resolution.

**Thermal Annealing:** Post-ashing residue removal by heating to 120-150°C for 30-60 minutes. Residue (CₓOᵧ) decomposes into volatile CO₂/CO. Slower but safer than plasma removal.

**Thermal Overshoot:** Electrode temperature rise above setpoint during continuous ashing due to plasma heating. Typical: 8°C rise after 200+ sec; PID feedback control maintains setpoint ±2-3°C.

**Threshold Energy (E_th):** Minimum ion energy required for sputtering. Carbon: ~10 eV, SiO₂: ~20 eV, Si: ~25 eV. Below threshold, ion bombardment doesn't cause sputtering (only chemical reaction matters).

---

## U

**Under-etch:** Incomplete resist removal in some regions (especially deep AR features due to radical depletion). Risk: Resist remains and contaminates downstream processes, causing yield loss.

---

## V

**Vf-Vp Profile:** Plasma sheath profile (voltage floating to bias voltage). Typical: V_f ~ 0-10 V, V_p ~ -200 to -500 V. Ion acceleration through sheath produces energetic ions.

---

## W

**Wafer Loading Density:** Number of wafers processed per chamber per hour. Standard: ~25 wafers/hour (2.4 min per wafer including pumpdown/vent/cooling). Limited by thermal transients in cluster tools.

---

## X

**XPS** (X-ray Photoelectron Spectroscopy): Surface composition analysis technique. Can measure residue thickness (CₓOᵧ layer) and native oxide (SiO₂ layer) to <1 nm precision. Destructive (damages sample).

---

## Y

**YSZ** (Yttria-Stabilized Zirconia): Standard electrode coating material for O₂ plasma ashing. Chemical formula ZrO₂+Y₂O₃; very corrosion-resistant, typical life ~20,000 wafers.

---

## Z

**Zero-crossing Endpoint:** Alternative endpoint detection method where RF waveform zero-crossing characteristics change as plasma impedance shifts. Less common than C₂ optical detection.

---

**End of Glossary: 60+ Production-Level Definitions**

