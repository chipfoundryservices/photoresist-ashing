# Chapter 6: Gas Distribution & Ashing Uniformity

## Overview

Ashing uniformity—achieving consistent ashing rate across the 300mm wafer—depends critically on **gas distribution**. The showerhead (gas inlet) design, pressure regime, and radical transport dynamics determine whether ashing rates vary 10% or 200% from center to edge. This chapter covers showerhead design, CFD modeling, and uniformity optimization.

**Learning Objectives:**
- Understand showerhead design options and gas distribution mechanisms
- Calculate mean free path and identify transport regimes
- Model radical penetration into high-AR trenches
- Design for ±5-10% ashing uniformity
- Apply CFD modeling to predict gas flow patterns
- Use diagnostics (OES, mass spectrometry) to validate design
- Optimize pressure for both uniformity and rate

---

## 6.1 Showerhead Design

### 6.1.1 Showerhead Configurations

Several designs are used to distribute oxygen gas uniformly:

```
Design 1: Packed Orifice Showerhead

Configuration:
  Multiple small holes (0.5-1 mm diameter)
  Uniformly distributed across circular plate
  Typical: 100-300 holes covering 30-40 cm² area
  
Gas flow:
  Pressure drop from inlet to chamber: ~10-20 mTorr
  Gas velocity through holes: ~10-50 m/s (sonic/supersonic)
  Exit velocity: Highly directional downward
  
Characteristics:
  - Simple to manufacture
  - Uniform distribution if holes evenly spaced
  - Low pressure drop (high flow efficiency)
  
Uniformity:
  Center of wafer: Direct vertical flow from holes
  Edge of wafer: Tangential flow (at angle)
  Result: ±15-20% non-uniformity typical (edge slower)
  
Advantages:
  - Cost-effective
  - Easy to maintain/clean
  - Standard in production

Disadvantages:
  - Limited ability to adjust gas distribution
  - High-AR feature penetration challenging
  - Pressure-dependent uniformity
```

```
Design 2: Slit Jet Showerhead

Configuration:
  Narrow rectangular slit (1-3 mm wide, 200-300 mm long)
  Gas exits as high-velocity jet perpendicular to wafer
  Sometimes dual slits (one on each side)
  
Gas flow:
  Exit velocity: ~30-100 m/s (very high)
  Gas spreads after exiting jet
  Can reach all wafer areas with adjustable divergence
  
Characteristics:
  - Excellent uniformity control
  - High pressure drop (requires higher inlet pressure)
  - Complex geometry
  
Uniformity:
  ±5-10% achievable with proper design
  Flexible distribution by slit width/height
  
Advantages:
  - Excellent uniformity
  - Radical penetration better (directed flow)
  - Can adjust distribution by jet geometry

Disadvantages:
  - High cost ($50K-100K)
  - More maintenance (slit prone to clogging)
  - Higher pressure requirements
  - Complex gas inlet plumbing
```

```
Design 3: Multi-Ring Showerhead

Configuration:
  Multiple concentric rings of holes
  Inner ring, middle ring, outer ring
  Each ring fed separately or with flow baffles
  
Gas distribution:
  Inner ring: Lower flow (covers dense center)
  Middle ring: Moderate flow (covers intermediate)
  Outer ring: Higher flow (covers low-density edge)
  Flow ratio adjusted for target uniformity
  
Characteristics:
  - Moderate cost (~$30-50K)
  - Good uniformity control
  - Moderate complexity
  
Uniformity:
  ±8-12% achievable
  Flexible distribution by ring flow control
  
Advantages:
  - Good balance of cost and performance
  - Able to compensate for pattern effects
  - Adjustable via baffle design

Disadvantages:
  - Slightly more complex than packed orifice
  - Requires careful flow balancing
  - Maintenance moderate
```

---

## 6.2 Gas Transport Physics

### 6.2.1 Mean Free Path & Transport Regimes

Whether radicals reach deep trenches depends on **mean free path** (MFP):

```
Mean free path definition:

λ (MFP) = 1 / (√2 × π × d² × n)

where:
  d = molecular diameter (~3 Å for O₂)
  n = number density of molecules
  
Number density: n = P / (k_B × T)
  P = pressure (Pa)
  k_B = Boltzmann constant
  T = temperature (K)

Calculation example:

At P = 1 Torr = 133 Pa, T = 300 K:
  n = 133 / (1.38×10⁻²³ × 300) ≈ 3.2 × 10²¹ m⁻³
  
  λ = 1 / (√2 × π × (3×10⁻¹⁰)² × 3.2×10²¹)
  λ ≈ 100 µm

At P = 50 mTorr = 6.7 Pa, T = 300 K:
  n = 6.7 / (1.38×10⁻²³ × 300) ≈ 1.6 × 10²⁰ m⁻³
  λ ≈ 2 mm

At P = 100 mTorr:
  λ ≈ 1 mm
  
At P = 10 mTorr:
  λ ≈ 10 mm

Knudsen number: Kn = λ / L
  where L = characteristic dimension (trench depth, gap size)
  
  Kn < 0.01: Continuum regime (frequent collisions, diffusive)
  0.01 < Kn < 100: Transitional regime (mixed ballistic + diffusive)
  Kn > 100: Ballistic regime (rare collisions, straight-line paths)
```

### 6.2.2 Transport Regimes & Uniformity Impact

```
Regime 1: High Pressure (P > 100 mTorr, Kn < 0.01)

Characteristics:
  - MFP very short (<1 mm)
  - Frequent collisions
  - Radicals diffuse randomly (Brownian motion)
  
Gas distribution:
  - Uniform diffusive transport
  - All regions receive similar radical flux
  - High-AR trenches: Radical access good (diffusion penetrates)
  - Uniformity: Excellent (±3-5%)
  
Disadvantages:
  - Slower ashing rate (ions don't travel far either)
  - Ion flux reduced (ions lost to collisions)
  - Selectivity may suffer (reduced ion assistance)

Use: For high selectivity requirement (sacrifice rate)
```

```
Regime 2: Intermediate Pressure (P = 50-100 mTorr, Kn = 0.1-1)

Characteristics:
  - MFP comparable to gap size (~1-2 mm)
  - Mix of ballistic and diffusive transport
  - Some radicals travel straight, some collide
  
Gas distribution:
  - Directed flow from showerhead mixes with diffusive spreading
  - Better uniformity than pure ballistic
  - High-AR trenches: Radical access moderate (some diffusion + ballistic)
  - Uniformity: Good (±8-12%)
  - Rate: Moderate (better than high-P)
  - Ion flux: Moderate (better than high-P)
  
Characteristics:
  - Balanced performance
  - Most production tools operate here

Use: Production standard (best balance of uniformity, rate, selectivity)
```

```
Regime 3: Low Pressure (P < 50 mTorr, Kn > 1)

Characteristics:
  - MFP long (>2 mm)
  - Few collisions, mostly ballistic transport
  - Radicals travel in straight lines from showerhead
  
Gas distribution:
  - Strong directional bias (depends on showerhead orientation)
  - Center of wafer: Gets full radical flux (direct from showerhead)
  - Edge of wafer: Gets reduced flux (radicals miss edge, hit wall)
  - High-AR trenches: Radical access poor (ballistic, can't turn corners)
  - Uniformity: Poor (±30-50%)
  - Rate: Fast (ions also travel far, less collision)
  - Ion flux: High (ions reach surface readily)

Problems:
  - Center-to-edge uniformity degraded
  - ARDE effects severe (dense vs. isolated features very different)
  - Requires compensation (pressure modulation recipe)

Use: Only for high selectivity applications (accept poor uniformity, compensate)
```

### 6.2.3 Optimal Pressure for 3D NAND Ashing

```
Uniformity vs. Ashing Rate Trade-Off:

Pressure    Uniformity    Ashing Rate    Ion Flux    Selectivity
─────────────────────────────────────────────────────────────
150 mTorr   ±5%          35 nm/min      Low         Excellent
100 mTorr   ±8-10%       50 nm/min      Moderate    Good
80 mTorr    ±10-12%      60 nm/min      Moderate    Good
50 mTorr    ±15-20%      75 nm/min      High        Moderate
30 mTorr    ±30%         90 nm/min      Very high   Poor

For 3D NAND with high-AR trenches:

Requirement: Deep features (500-2000 nm) at 5-20:1 AR
Challenge: Radicals must penetrate deep while maintaining uniformity

Recommendation: 50-80 mTorr (intermediate regime)
  - Allows ballistic penetration to deep trenches
  - Retains adequate uniformity (±10-15%)
  - Moderate ashing rate (acceptable for selectivity recipe)
  - Ion flux sufficient for selectivity control

Multi-step approach:
  Step 1: High selectivity (80-100 mTorr, slow, uniform)
  Step 2: Transition (60-70 mTorr, moderate)
  Step 3: Fast finish (40-50 mTorr, if safe from selectivity risk)
```

---

## 6.3 High-AR Trench Penetration

### 6.3.1 Radical Penetration into Deep Trenches

3D NAND features often have extreme aspect ratios (500 nm deep, 20-50 nm wide = 10-25:1 AR):

```
Penetration challenge:

Trench geometry:
  Width: 20 nm (narrow)
  Depth: 500-1000 nm (very deep)
  Aspect ratio: 25-50:1 (extreme)
  
Radical transport into trench:

  Shallow: Top 100 nm
    - Direct access from showerhead
    - High radical flux: ~10¹⁵ radicals/(cm²·s)
    - Ashing rate: ~60-70 nm/min (fast)
  
  Middle: 100-300 nm depth
    - Diffusive transport becoming limited
    - Radical flux drops to ~5 × 10¹⁴
    - Ashing rate: ~40-50 nm/min (slower)
  
  Deep: >300 nm depth
    - Very limited radical access
    - Radical flux: ~10¹⁴ or less
    - Ashing rate: ~15-30 nm/min (very slow)
  
Extreme deep (>800 nm):
    - Radical starvation (depletion)
    - Ashing rate: <10 nm/min (near zero)
    - Risk: Trenches not fully etched, residue accumulation

Calculation of penetration depth:

  Radical diffusion into trench:
  
  Penetration depth ~ √(D × t)
  
  where:
    D = diffusion coefficient (~0.1 cm²/s typical)
    t = time (seconds)
  
  After 60 seconds ashing:
    Depth ~ √(0.1 × 60) ~ 2.4 cm (unrealistically large)
    
  But trench geometry limits:
    Trench width = 20 nm = 2 × 10⁻⁵ cm
    Effective diffusion in constrained geometry much slower
    
  Actual penetration: ~50-200 nm deep (orders of magnitude less)
```

### 6.3.2 Pressure Optimization for Deep Trench Ashing

```
Strategy 1: Low Pressure (Ballistic Penetration)

  P = 40-50 mTorr (high Kn)
  Radicals travel ballistically (straight lines)
  Can reach deep into trench if aimed at angle
  
  Penetration: Can reach ~500 nm deep (with angle)
  Uniformity: Poor (±30-50%)
  Solution: Accept poor uniformity, use ARDE compensation recipe

Strategy 2: Intermediate Pressure (Balanced)

  P = 60-80 mTorr (Kn ~ 0.5)
  Mix of ballistic and diffusive
  Some radicals reach deep (ballistic), some blocked by diffusion
  
  Penetration: ~300-400 nm (moderate)
  Uniformity: Better (±10-15%)
  Limitation: May not fill extremely deep trenches

Strategy 3: Multi-Step Approach (Recommended)

  Step 1: Low pressure (40-50 mTorr)
    - Fast ashing (80-90 nm/min)
    - Poor uniformity, but acceptable for removing bulk
    - Time: 30-40 seconds to remove 80% of resist
    
  Step 2: Higher pressure (80-100 mTorr)
    - Slower ashing (40-50 nm/min)
    - Better uniformity, cleans up remaining residue
    - Time: 20-30 seconds for final 20%
    - Ensures deep trench material doesn't remain
    
  Result: Balanced approach
    - Bulk ashing fast (maintains throughput)
    - Final pass with uniformity (ensures complete removal)
    - Deep trenches fully etched
```

---

## 6.4 CFD Modeling & Diagnostics

### 6.4.1 CFD Workflow for Showerhead Design

Computational Fluid Dynamics predicts gas distribution:

```
CFD modeling steps:

1. Geometry definition
   - Chamber dimensions (40 cm × 50 cm × 20 cm typical)
   - Showerhead holes/slits (exact position, size, orientation)
   - Wafer surface (300 mm diameter, 0.5 mm thick)
   - Electrode and chamber walls

2. Physics equations
   - Continuity equation (mass conservation)
   - Momentum equation (Navier-Stokes)
   - Energy equation (optional, if thermal effects matter)
   
3. Boundary conditions
   - Inlet: Pressure and temperature at showerhead
   - Outlet: Chamber pressure (e.g., 70 mTorr)
   - Walls: No-slip (molecules stick to wall)

4. Solver setup
   - Mesh generation (typically 100K-1M cells)
   - Convergence criteria (residuals < 1e-6)
   - Solver: Commercial (FLUENT, CFX) or open-source (OpenFOAM)

5. Results extraction
   - Velocity field (magnitude and direction at each point)
   - Pressure field (static pressure throughout domain)
   - Gas density (from ideal gas law)
   
6. Analysis
   - Radical flux to wafer surface = gas density × velocity × diffusivity
   - Compare center vs. edge flux (uniformity metric)
   - Adjust showerhead design if uniformity poor

Typical result: Uniformity ±10-15% with proper showerhead design
```

### 6.4.2 Spectroscopic Diagnostics (OES, Mass Spec)

Validate CFD predictions with actual measurements:

```
OES (Optical Emission Spectroscopy):

Principle:
  Atoms/ions in plasma emit photons at characteristic wavelengths
  Intensity ∝ species density
  
Measurement:
  Measure O (atomic oxygen) line at 703.7 nm
  Scan across wafer diameter at 10-20 points
  Record intensity at each location
  
Result:
  O density profile: Center vs. edge
  Expected from CFD: ±10% variation
  Observed: ±10-20% typical (some deviation from ideal)
  
Interpretation:
  If center > edge: Showerhead favors center (adjust holes)
  If edge > center: Showerhead favors edge (unusual, check design)
  If flat: Excellent uniformity design

Spectroscopy equipment cost: $30-50K
Measurement time: 10-20 minutes per run
```

```
Mass Spectrometry (Residual Gas Analysis):

Principle:
  Sample gas from chamber (very small amount)
  Ionize and measure mass-to-charge ratio
  Identify species (O₂, O, CO, etc.)
  
Measurement:
  During ashing, scan through m/z = 0-100
  Peaks at: m/z = 16 (O), m/z = 32 (O₂), m/z = 28 (CO), etc.
  Monitor peak heights to track ashing progress
  
Use for endpoint detection:
  O₂ peak height (m/z = 32): Constant (unreacted O₂)
  O peak height (m/z = 16): High during ashing, drops at endpoint
  CO peak height (m/z = 28): High during ashing, drops at endpoint
  
  Endpoint triggered when O and CO signals drop ~70%
  
Equipment cost: $50-100K
Measurement time: Continuous during ashing
```

---

## 6.5 Summary & Key Takeaways

1. **Showerhead Design Critical** — Packed orifice simple but limited uniformity; slit jet excellent but costly; multi-ring good compromise.

2. **Pressure Regime Determines Transport** — High P (>100 mTorr) diffusive/uniform but slow; low P (<50 mTorr) fast but poor uniformity; 60-80 mTorr optimal for 3D NAND.

3. **Mean Free Path Physics Essential** — Understanding Knudsen number predicts whether radicals reach deep trenches ballistically (low P) or diffusively (high P).

4. **Deep Trench Penetration Challenge** — Extreme AR (25-50:1) requires low pressure for ballistic access, but sacrifices uniformity. Multi-step recipe balances both.

5. **±10% Uniformity Achievable** — With good showerhead design and intermediate pressure (60-80 mTorr), center-to-edge uniformity ±10-15% is standard production spec.

6. **CFD Prediction vs. Reality** — Computational models predict distribution; actual uniformity typically ±10-20% due to manufacturing variations and nonlinear effects.

7. **Diagnostics Validate Design** — OES (optical) and mass spectrometry confirm radical distribution predictions and endpoint signals.

8. **Multi-Step Approach Optimal** — Fast low-pressure step for bulk removal, followed by higher-pressure step for uniformity ensures both throughput and deep trench coverage.

---

**Next Chapter:** [Chapter 7 - Pressure-Power-Temperature Phase Space](./07-pressure-power-temp.md)

---

**Chapter 6 Development Status:** Comprehensive gas distribution and uniformity framework  
**Version:** 1.0

