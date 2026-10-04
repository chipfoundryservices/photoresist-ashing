# Appendix G: Chamber Maintenance & Seasoning

## G.1 Electrode Coating Corrosion Management

```
Electrode material degradation in O₂ plasma:

Coating material (YSZ - Yttria-Stabilized Zirconia):

  Chemical composition: ZrO₂ + Y₂O₃ (~8% Y)
  Crystal structure: Cubic fluorite (dense, hard)
  Hardness: ~1200 Vickers (very hard)
  
  Reaction in O₂ plasma:
    YSZ + O₂ → Minimal reaction (oxide already, inert)
    Y₂O₃ component can oxidize slightly
    But net corrosion rate extremely low
    
  Corrosion rate (typical): 0.1-0.5 nm/wafer
  Per 100 wafers: 10-50 nm cumulative loss
  Time to failure (thinning to 50% thickness): ~10,000 wafers

Alternative coating (Al₂O₃ - Alumina):

  Chemical composition: Al₂O₃
  Hardness: ~2000 Vickers (even harder than YSZ)
  
  Corrosion in O₂ plasma:
    Al₂O₃ very stable (already fully oxidized)
    Actual corrosion rate: ~0.01-0.1 nm/wafer
    Much slower than YSZ
    
  Time to failure: ~100,000 wafers (10× longer!)
  
  Trade-off: Al₂O₃ more expensive ($5K vs $2K coating)
             But longer life justifies cost

Competing coating (SiO₂ - Silicon Dioxide):

  Corrosion in O₂ plasma:
    SiO₂ relatively stable but less than Al₂O₃
    Corrosion rate: ~0.2-1 nm/wafer
    Time to failure: ~5,000 wafers (fast failure)
  
  Not recommended for O₂ plasma (poor choice)
  Better for other chemistries (Cl₂, CF₄)
```

## G.2 Preventive Maintenance Schedule

```
Monthly maintenance (every 500-1000 wafers):

Step 1: Visual inspection (10 min)
  ─────────────────────────────────
  ☐ Check electrode via chamber window
    Look for:
      - Orange/brown discoloration (YSZ corrosion starting)
      - White deposits (salt buildup - ionic contamination)
      - Cracks or pitting (catastrophic failure beginning)
    
    If significant discoloration:
      Continue production but schedule service
      Monitor performance trending
    
    If white deposits visible:
      STOP production immediately
      Schedule emergency cleaning
      Risk: Ionic contamination → wafer defects

Step 2: Impedance trending (5 min)
  ─────────────────────────────────
  ☐ Measure reflected power at standard recipe
    Compare to baseline (from last month)
    
    Normal: Reflected power same ±10% (within tolerance)
    
    If reflected power increases >15%:
      Impedance mismatch increasing
      Possible cause: Electrode coating thinning
      Action: Clean electrode or replace
    
    If reflected power becomes erratic (±20% variation):
      Tuning network having trouble
      Possible cause: Electrode becoming lossy
      Action: Check tuner, may need service

Step 3: Gas system check (5 min)
  ───────────────────────────────
  ☐ Verify gas line pressures
    O₂ supply: 50-60 psi (normal)
    Regulator output: 5-10 psi (normal)
    Check for leaks (listen, smell)
  
  ☐ Purge gas (Ar/N₂) accessibility
    Emergency purge capability verified

Quarterly maintenance (every 2000-3000 wafers):

  Deep cleaning procedure:
  
  Step 1: Cool chamber, power down all systems
  
  Step 2: Remove electrode
    Carefully unscrew electrode assembly
    Inspect coating condition (visual + profilometry if available)
    Take reference photographs
  
  Step 3: Clean electrode surfaces
    If only light deposits (orange tint):
      Soak in distilled water + ultrasonic, 10 min
      Gently scrub with soft brush (no scratching)
      Rinse with DI water
      Dry with N₂ blow-off
    
    If heavy deposits (white, crusty):
      Use mild acid (2% HCl in DI water), 5-10 min soak
      WARNING: Don't over-etch coating (limit to 1-2 min if yikes!)
      Rinse thoroughly with DI water (10+ rinses)
      Neutralize with dilute NaOH if needed
      Final rinse with DI water
      Dry with N₂
  
  Step 4: Chamber wall inspection
    Visually inspect chamber walls (ceramic)
    Look for erosion, deposits, cracks
    If wall coating also degraded, plan replacement
  
  Step 5: Reinstall electrode
    Re-mount electrode assembly
    Verify thermal couple connection
    Verify gas lines connected
    Vacuum test (pump to <1 mTorr, hold 1 hour)
    If pressure rises: Leak detected, troubleshoot

Annual maintenance (every 10,000+ wafers):

  Full system overhaul:
  
  ☐ Replace electrode coating if worn
    Typical life: 15,000-30,000 wafers depending on coating
    Cost: $5-10K for new coating
    Downtime: 1 week for coating + qualification
  
  ☐ Replace RF chamber if severely pitted
    Typical life: 30,000-50,000 wafers
    Cost: $50-100K for new chamber
    Downtime: 2-3 weeks for replacement + qualification
  
  ☐ Recalibrate all sensors
    Thermocouples: Thermal resistance check
    Pressure transducers: Compare to reference gauge
    RF power monitors: Zero/full calibration
  
  ☐ Regenerate process window
    Run full 2³ factorial DOE
    Update ashing rate tables
    Validate recipe performance
    Update SOP documentation
```

## G.3 Chamber Seasoning (Break-in Procedure)

```
After electrode replacement or chamber rebuild:

Problem: New electrode has different properties
         Ashing rate higher/lower than expected
         Selectivity different
         Requires conditioning before production use

Seasoning procedure (3-5 production days):

Day 1-2: High-power "burn-in" conditioning
  ─────────────────────────────────
  ☐ Run dummy wafers (bare Si, no patterned resist)
  
  Step 1: Run at 50% higher coil power than recipe
          W_coil_recipe = 2000 W
          W_coil_burnin = 3000 W (50% higher)
          Duration: 5 min per dummy wafer
          Purpose: Create oxidation layer, stabilize surface
  
  Step 2: Cool chamber (2 min)
  
  Step 3: Repeat 10 times (total 50 min burn-in)
  
  Result: New electrode surface oxidizes
          Resistance stabilizes
          Ready for next stage

Day 2-3: Process window characterization
  ────────────────────────────────────
  ☐ Run control wafers at recipe conditions
  
  Step 1: Baseline ashing rate measurement
          Load control wafer stack (resist + HM)
          Run for known time (e.g., 120 sec)
          TEM cross-section to measure removal
          Calculate ashing rate
          Compare to historical baseline
  
  Step 2: If rate significantly higher (>10%):
          New electrode more active
          Adjust recipe (reduce coil power or lower T)
          Re-run measurement
          Iterate until rate matches baseline
  
  Step 3: If rate significantly lower (<-10%):
          New electrode less active (unlikely)
          Check tuning network (manual tune may be needed)
          Verify plasma quality
  
  Expected result:
    Ashing rate within 5-10% of baseline
    Selectivity within 10-15% of baseline

Day 3-5: Production trial run
  ──────────────────────────
  ☐ Resume normal production
  
  Step 1: First wafer lot with new electrode
          Extra scrutiny:
            - Monitor endpoint signal closely
            - Log all ashing times
            - Compare to statistical control limits
  
  Step 2: After first 50 wafers:
          Verify selectivity still good (TEM or XRR)
          If selectivity drifts >10%:
            Adjust recipe parameters
            Document changes
  
  Step 3: After 200 wafers:
          Full control wafer validation
          Confirm ashing rate and selectivity stable
          If stable: Clear for full production
          If unstable: Continue seasoning, don't full ramp

Typical seasoning outcome:

  After seasoning:
    Ashing rate: Within ±5% of baseline (good)
    Selectivity: Within ±5% of baseline (good)
    Thermal stability: Equivalent to baseline
    Ready for normal production rate (~25 wafers/hour)
  
  If seasoning unsuccessful:
    Ashing rate still outside ±10% tolerance
    Selectivity drifting or poor
    Possible problems:
      - Electrode contamination (requires deep cleaning)
      - RF tuning issue (requires specialist diagnosis)
      - Chamber leak (requires helium leak test)
    Action: Stop production, troubleshoot root cause
```

---

**Appendix G Complete: Chamber Maintenance & Seasoning**

