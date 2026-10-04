# Appendix F: Endpoint Detection Calibration

## F.1 Optical Emission (C₂ Swan Band) Calibration

```
Setup:

  Photomultiplier tube (PMT) or spectrometer views chamber
  Wavelength window: 510-520 nm (C₂ Swan band maximum)
  Reference: Background O emission at 777 nm (normalization)
  Sampling rate: 1-10 Hz (sufficient to catch changes)

Calibration procedure:

Step 1: Baseline measurement (no plasma)
  ─────────────────────────
  Chamber empty, no plasma running
  Record ambient light (room light leakage)
  Record dark signal (detector background)
  
  Typical values:
    Dark signal: 1-5 mV (PMT noise floor)
    Room light: 10-20 mV (if room lights visible)
    Baseline: ~5 mV (after room lights off)

Step 2: Plasma-only measurement (O₂, no resist)
  ──────────────────────────────────────
  Run recipe parameters with O₂ plasma
  Load dummy wafer (no resist on it)
  Run for 2-3 minutes
  Record C₂ signal (should be very low, almost baseline)
  
  Typical values:
    C₂ signal: 5-20 mV (O atom continuum, not C₂)
    This is "zero resist" baseline
    Save this as reference

Step 3: Full resist ashing characterization
  ────────────────────────────────────────
  Load wafer with full resist stack (80 nm resist on hard mask)
  Run recipe, record C₂ signal continuously
  
  Expected signal evolution:
    Time 0-10 sec: Low signal (~10-30 mV)
                   Resist surface still clean
    
    Time 10-60 sec: Rising signal (~50-200 mV)
                    Resist degrading, C fragments generated
                    
    Time 60-120 sec: High signal (~300-500 mV peak)
                     Heavy resist removal, maximum C₂ emission
                     
    Time 120-140 sec: Signal plateaus or rises further
                      Resist nearly depleted
                      
    Time 140-160 sec: SHARP DROP (50-100 mV/sec)
                      Last resist removed
                      Hard mask exposed, no more C₂ source
                      
    Time 160+ sec: Low signal (~20-30 mV baseline)
                   Over-etch: Hard mask exposed, C₂ gone
                   No more change (selectivity regime)

Step 4: Endpoint detection threshold setting
  ────────────────────────────────────────
  From Step 3 data:
    Peak C₂ signal during ashing: S_peak ≈ 400 mV
    Drop at endpoint: ΔS ≈ 250 mV (sharp)
    Baseline (hard mask only): S_baseline ≈ 25 mV
    
  Set alarm threshold:
    Trigger when dS/dt > 10 mV/sec (fast drop)
    AND absolute signal < 100 mV (crossed threshold)
    
  This reliably catches endpoint with ~1-2 sec precision

Step 5: Repeatability qualification
  ────────────────────────────────
  Repeat Step 3 with 10 wafers (test run)
  Record endpoint time for each
  Calculate mean and std dev:
    Mean endpoint: 138 sec
    Std dev: ±2 sec (excellent, <2% variation)
    Range: 135-141 sec
  
  Set safety timer:
    Nominal endpoint time: 138 sec
    Safety cutoff (max time): 138 + 10 sec = 148 sec
    If C₂ drop not detected by 148 sec, kill plasma anyway
    Prevents over-etch runaway

Calibration refresh schedule:

  Monthly: Re-run Step 3 on one control wafer
           Compare endpoint time to baseline
           If drift >5 sec, investigate cause
           Possible cause: PMT aging, optics dirt
  
  Quarterly: Full recalibration (Steps 1-5)
             Update software thresholds if needed
             Regenerate C₂ signal profile plots
```

## F.2 Electrical Endpoint Detection (Reflected Power)

```
Alternative method: Monitor RF impedance change

Setup:

  RF power generator measures reflected power in real-time
  As plasma parameters change, impedance changes
  Endpoint causes impedance shift

Impedance change mechanism:

  Early ashing (resist present):
    Chamber filled with C and O fragments
    Plasma density relatively constant
    Impedance stable
    Reflected power: ~10-15 W (low, matched load)
  
  Near endpoint (last resist):
    Resist fragments nearly gone
    Ion density starts to drop (less electron-resist collision)
    Impedance increases
    Reflected power rises: ~15-20 W (increasing)
  
  Hard mask exposed (endpoint):
    No more resist fragments
    Plasma significantly less dense
    Impedance mismatch larger
    Reflected power jumps: 20-40 W (large change)

Electrical endpoint detection:

  Monitor: dP_reflected / dt (change in reflected power rate)
  
  Threshold: If dP/dt > 2 W/sec for 0.5 sec
             → Endpoint signal
  
  Backup timer: 150 sec (ensure stop even if electrical detection fails)

Advantages over optical (C₂):

  ✓ No optics needed (less prone to chamber buildup)
  ✓ Robust signal (electrical is fast, MHz response)
  ✓ No line-of-sight requirement
  
  ✗ Less selective (doesn't distinguish resist from O₂ changes)
  ✗ Requires good RF coupling (not all tools have this sensor)
  ✗ Sensitive to tuning network drift

Best practice: Dual sensing

  Primary: Optical (C₂ signal) - most reliable
  Confirmatory: Electrical (reflected power) - verifies
  Backup: Timer (blind endpoint if both fail)
  
  All three together provide very high confidence
```

## F.3 Endpoint Detection Under ARDE Conditions

```
Problem: High-aspect-ratio (AR) features ash differently than open areas
         Optical endpoint detection sees average signal
         But deep trenches may not be finished
         
ARDE effect on endpoint:

  Open area (low AR):
    C₂ signal strong (radical accessible)
    Endpoint arrives at nominal time (e.g., 140 sec)
  
  Deep trench (high AR, 50:1 aspect ratio):
    C₂ signal weak locally (radical depletion, shadowing)
    Resist in trench takes 2-3× longer to ash
    True completion time: 200-250 sec
  
  Optical endpoint:
    Sees average of open + trench signals
    Detects when OPEN area is done (140 sec)
    But trenches still 50% full!
    Result: UNDER-ETCH in deep features → device failure

Solutions:

Method 1: Pressure-based ARDE compensation
  Use multi-step recipe:
    Step 1: Standard pressure (70 mTorr) - fast open areas
    Step 2: High pressure (100 mTorr) - slower, helps deep AR
    Step 3: Lower pressure (50 mTorr) - finishing open areas
  
  Result: More uniform ashing, endpoint detection more reliable
  Penalty: Longer total time (~+15%)

Method 2: Pulsed plasma ARDE compensation
  Use duty-cycle modulation:
    On 50 sec: Plasma runs (50% duty cycle)
    Off 50 sec: Plasma off (pressure drops, radicals diffuse deep)
    Repeat 2-3 cycles
  
  Result: Better penetration into deep features
  Penalty: Much longer total time (~+50%)

Method 3: Blind time endpoint (conservative)
  Don't rely on optical detection for ARDE-heavy recipes
  Set timer for worst-case (deep trenches) + 20% margin
  Example: 250 sec estimated for deep AR, set timer 300 sec
  
  Result: Guaranteed completion even in worst features
  Penalty: Over-etch risk in open areas

Practical recommendation:

  For AR < 10:1 (standard logic):
    Use optical endpoint (C₂ detection)
    Minimal over-etch risk, reliable
  
  For AR 10-20:1 (aggressive 3D or 3D NAND):
    Use optical + pressure compensation
    Better uniformity, still optical endpoint
  
  For AR > 30:1 (extreme 3D NAND):
    Use pressure compensation + pulsed plasma
    Blind timer as backup
    Highest complexity, but highest yield
```

---

**Appendix F Complete: Endpoint Detection Calibration**

