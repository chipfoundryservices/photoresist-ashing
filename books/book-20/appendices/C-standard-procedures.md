# Appendix C: Standard Operating Procedures

## C.1 Daily Pre-Ashing Equipment Check

```
Before starting production (performed each shift):

Time required: ~15 minutes
Performed by: Equipment technician or process engineer

Checklist:

1. Visual Inspection (5 min)
   ☐ Inspect chamber window for deposits/cloudiness
     - Clear = normal, proceed
     - Opaque/cloudy = electrode overdue for cleaning
     - Schedule maintenance before production
   
   ☐ Check electrode surface (remote camera, if available)
     - Look for corrosion pitting, discoloration
     - Compare to reference photo from last maintenance
     - If visible degradation: Stop, schedule service

2. RF System Check (5 min)
   ☐ Record reflected power baseline
     - Measure at low power (100 W coil, no bias)
     - Typical: 5-10 W reflected (normal)
     - >20 W reflected: Impedance problem, stop
     - Re-tune impedance matching network (±5 Ω)
   
   ☐ Verify tuning network status
     - Automated tuning ON (standard)
     - Manual tuning backup available
     - Document tuning range (should track <5% drift)

3. Thermal System Check (3 min)
   ☐ Check electrode temperature sensor
     - Read baseline temperature (should be ~20°C ambient)
     - Compare to setpoint (should agree ±2°C)
     - If drift >3°C: Recalibrate or replace sensor
   
   ☐ Verify cooling system operation
     - Chiller unit ON (green light)
     - No error codes displayed
     - Flow rate normal (visual check, if gauge available)

4. Gas Delivery System (2 min)
   ☐ Verify O₂ gas supply
     - Pressure regulator: 50-60 psi (upstream)
     - Flow controller: Set to recipe value (e.g., 200 sccm)
     - No visible leaks (listen for hissing)
   
   ☐ Check Ar purge gas (if used)
     - Pressure normal
     - Valve accessible (for chamber purge if needed)

Result: Pass/Fail Log
  PASS: Proceed to production
  FAIL: Note issue, notify maintenance, wait for clearance
```

## C.2 Recipe Setup & Qualification

```
Process: Establish new recipe or verify existing recipe

Time required: ~4 hours (including cool-down)
Performed by: Process engineer + equipment technician

Step 1: Baseline Characterization (30 min)

  a) Load control wafer stack into chamber
     - Resist: 80 nm ArF
     - Hard mask: 30 nm carbon
     - Dielectric: 200 nm SiO₂
     - Substrate: Si
  
  b) Set candidate recipe parameters:
     - Pressure: 70 mTorr (start conservative)
     - Coil power: 2000 W
     - Bias power: 400 W
     - Temperature: 20°C setpoint
  
  c) Run ashing for known time (e.g., 120 seconds)
  
  d) Remove wafer, allow cool-down (5 min in N₂)
  
  e) Measure remaining layers via cross-section TEM:
     - Photoresist thickness: Should be <2 nm (complete removal)
     - Carbon HM thickness: Should remain >25 nm (unattacked)
     - SiO₂ surface: No visible erosion

Step 2: Ashing Rate Determination (1 hour)

  Run series of 3-4 timed wafers:
    Time 60 sec: Measure remaining resist (mid-ashing sample)
    Time 90 sec: Measure remaining resist (near-endpoint)
    Time 120 sec: Measure final state
    Time 150 sec (if needed): Measure over-etch margin
  
  Plot: Remaining resist thickness vs. time
  Determine: Linear ashing rate R (nm/min)
  
  Example result:
    Time 60 sec: 50 nm resist remains → 30 nm removed
    Time 90 sec: 25 nm resist remains → 55 nm removed
    Time 120 sec: 2 nm resist remains → 78 nm removed
    Time 150 sec: 0 nm (complete) → all removed
    
    Ashing rate: (80-2) / 120 = 0.65 nm/sec ≈ 39 nm/min

Step 3: Selectivity Verification (1 hour)

  Use TEM cross-sections from Step 2:
  
  Calculate selectivity:
    S_C/SiO₂ = (Δt_resist / 120 sec) / (Δt_SiO₂ / 120 sec)
    
    Example:
      Resist removed: 78 nm
      SiO₂ eroded: 0 nm (no erosion)
      S = 78 / 0 = ∞ (perfect selectivity)
      
      Realistic: Resist 78 nm, SiO₂ 4 nm eroded
      S = 78 / 4 = 19.5:1 (excellent)
  
  Acceptance criteria:
    S_C/SiO₂ > 15:1 → PASS
    S_C/SiO₂ 10-15:1 → MARGINAL (acceptable, monitor)
    S_C/SiO₂ < 10:1 → FAIL (adjust recipe)
  
  If FAIL:
    Reduce bias power by 50 W
    Reduce temperature by 5°C
    Re-run Step 2 (ashing rate check)
    Verify selectivity improved

Step 4: Thermal Stability (30 min)

  Run back-to-back wafers (5 consecutive ashing steps)
  without cooling in-between:
  
  Ashing #1: T = 20°C (baseline)
  Ashing #2: T rises to ~25°C (transient heating)
  Ashing #3: T = ~28°C (steady-state heating)
  Ashing #4: T = ~28°C (stable)
  Ashing #5: T = ~28°C (stable, confirm)
  
  Measure thermal overshoot:
    Max temp rise: ~8°C typical (acceptable)
    Rate change: Should be <5% (within tolerance)
  
  If thermal overshoot >15°C:
    Increase electrode cooling flow
    Or reduce coil power
    Re-qualify recipe

Step 5: Documentation (30 min)

  Create recipe file with:
    - Process parameters locked
    - Ashing rate (nm/min)
    - Selectivity (C/SiO₂)
    - Thermal characteristics
    - Expected endpoint time
    - Safety margin (nm vs. hard mask)
  
  Create control wafer measurements:
    - Expected remaining resist: <2 nm
    - Expected HM thickness: >25 nm
    - TEM reference images (save for comparison)
  
  Approval sign-off:
    - Process engineer signature
    - Equipment technician approval
    - Date qualified
```

## C.3 Production Wafer Ashing Procedure

```
Standard procedure for production lots:

1. Wafer Loading (2 min)
   ☐ Load one wafer per run (most common)
   ☐ Wafer orientation: Flat mark aligned to reference mark
   ☐ Wafer centered on electrode
   ☐ No debris or particles on wafer surface

2. Chamber Closure & Pump-Down (3 min)
   ☐ Close chamber door, secure with automatic clamp
   ☐ Start vacuum pump (should reach <1 mTorr within 2 min)
   ☐ Verify chamber pressure < 1 mTorr before proceeding

3. Recipe Selection & Gas Flow Setup (2 min)
   ☐ Select locked recipe from database
   ☐ Verify recipe parameters on screen
   ☐ Open O₂ gas supply valve (manual safety valve)
   ☐ Set flow rate to recipe setpoint (e.g., 200 sccm)
   ☐ Wait for flow controller to stabilize (30 sec)

4. RF Plasma Initiation (1 min)
   ☐ Activate coil RF power (start at half setpoint, 1000 W)
   ☐ Wait 10 seconds for plasma ignition
   ☐ Verify plasma visible (glow discharge in window)
   ☐ Ramp coil power to full setpoint (2000 W) over 10 sec
   ☐ Turn ON bias power (ramp from 0 to 400 W over 5 sec)

5. Ashing Execution (2-3 min)
   ☐ Start timer (ashing begins when both RF and bias active)
   ☐ Monitor reflected power (should be <15 W)
   ☐ Monitor temperature setpoint (maintained by PID control)
   ☐ Watch optical endpoint monitor (C₂ signal trend)
   ☐ Listen for chamber acoustics (normal hum, no sparking)

6. Endpoint Detection & Plasma Stop (30 sec)
   ☐ At ~90% of nominal time, increase monitoring frequency
   ☐ Watch C₂ emission intensity:
     - Decreasing: Resist still present
     - Sharp drop: Endpoint approaching
     - Baseline level: Resist completely removed
   
   ☐ At endpoint confirmation:
     - Kill bias power (ramp to 0 over 2 sec)
     - Kill coil power (ramp to 0 over 2 sec)
     - Stop O₂ gas flow
     - Plasma extinguishes
   
   ☐ Log actual ashing time (compare to expected)

7. Wafer Cool-Down & Removal (3 min)
   ☐ Backfill chamber with Ar or N₂ (inert gas purge)
   ☐ Allow wafer to cool for 1-2 minutes
     (Prevents oxidation, maintains surface chemistry)
   ☐ Open chamber door when safe (no residual heat visible)
   ☐ Remove wafer carefully (use tweezers, clean room technique)
   ☐ Inspect wafer visually for defects (obvious damage?)

8. Wafer Transfer (2 min)
   ☐ Place wafer in transfer cassette
   ☐ Transport to next process (ideally <5 min in N₂ atmosphere)
   ☐ Log wafer ID, ashing time, chamber ID, date/time

Production Log (per wafer):
  Wafer ID: _________
  Lot ID: _________
  Ashing time: ______ seconds (target: 120 ± 5 sec)
  Coil power: ______ W (target: 2000 W)
  Bias power: ______ W (target: 400 W)
  Pressure: ______ mTorr (target: 70 mTorr)
  Temperature: ______ °C (target: 20°C ± 2°C)
  Reflected power: ______ W (should be <15 W)
  Endpoint signal: ______ (C₂ drop observed? YES / NO)
  Notes: ________________________________________
```

---

**Appendix C Complete: Standard Operating Procedures**

