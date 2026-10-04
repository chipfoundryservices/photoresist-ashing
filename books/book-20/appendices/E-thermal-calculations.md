# Appendix E: Thermal Calculations & Modeling

## E.1 Arrhenius Model Quantification

```
Arrhenius equation for ashing rate:

R(T) = A × exp(-E_a / RT)

Where:
  R(T) = ashing rate (nm/min)
  A = pre-exponential factor (temperature-independent constant)
  E_a = activation energy (kcal/mol) ≈ 12 for photoresist
  R = gas constant = 1.987 × 10⁻³ kcal/mol·K
  T = absolute temperature (Kelvin)

Practical form (convert to linear):

ln[R(T)] = ln(A) - (E_a / R) × (1/T)

Plotting ln(R) vs. 1/T gives straight line:
  Slope = -E_a / R
  Intercept = ln(A)

Numerical calculation example:

Given:
  E_a = 12 kcal/mol (photoresist)
  R = 1.987 × 10⁻³ kcal/mol·K
  
Ratio: E_a / R = 12 / (1.987×10⁻³) = 6,036 K

Temperature dependence:

T = 293 K (20°C):  ln[R] = ln(A) - 6036 × (1/293) = ln(A) - 20.6
T = 283 K (10°C):  ln[R] = ln(A) - 6036 × (1/283) = ln(A) - 21.3
T = 303 K (30°C):  ln[R] = ln(A) - 6036 × (1/303) = ln(A) - 19.9

ΔT = 10°C:
  Δ[ln(R)] = 21.3 - 20.6 = 0.7
  R_ratio = exp(0.7) = 2.01 (factor of 2, matches ~15%/°C)

Calculation of A factor:

If you know: R(20°C) = 60 nm/min, E_a = 12 kcal/mol
  
  60 = A × exp(-20.6)
  A = 60 × exp(20.6) = 60 × 8.87×10⁸ = 5.32×10¹⁰
  
Then predict R at any temperature:

  R(0°C) = 5.32×10¹⁰ × exp(-21.3) ≈ 40 nm/min ✓ (matches table)
  R(40°C) = 5.32×10¹⁰ × exp(-19.9) ≈ 90 nm/min ✓
```

## E.2 Thermal Transient in Cluster Tool

```
Problem: Wafer arrives from deposition (hot, 200°C)
         Must cool before ashing (target 20°C)
         
Thermal transient modeling:

Heat transfer from electrode:

Equation: m × c_p × dT/dt = -h × A × (T - T_setpoint)

Where:
  m = wafer mass ≈ 50 g (for 300 mm wafer)
  c_p = heat capacity ≈ 0.9 J/g·K (Si)
  h = convection coefficient ≈ 50 W/m²·K (electrode cooling)
  A = wafer area ≈ 70,000 mm² ≈ 0.07 m²
  T = current temperature
  T_setpoint = electrode temperature (actively cooled to 20°C)

Time constant: τ = m×c_p / (h×A)
              τ = 50×0.9 / (50×0.07) = 45 / 3.5 ≈ 12.9 seconds

Transient response:

T(t) = T_setpoint + (T_initial - T_setpoint) × exp(-t/τ)

Example: T_initial = 200°C, T_setpoint = 20°C, τ = 13 sec

t = 0 sec:    T = 200°C (just loaded)
t = 13 sec:   T = 20 + (200-20)×exp(-1) = 20 + 180×0.368 = 86°C
t = 26 sec:   T = 20 + 180×exp(-2) = 20 + 24.3 = 44°C
t = 39 sec:   T = 20 + 180×exp(-3) = 20 + 8.9 = 29°C
t = 52 sec:   T = 20 + 180×exp(-4) = 20 + 3.3 = 23°C
t = 65 sec:   T = 20 + 180×exp(-5) = 20 + 1.2 = 21°C

Practical implications:

  After 30 seconds: T ≈ 35-45°C (still warm)
  After 60 seconds: T ≈ 20-25°C (nearly settled)
  
  If ashing starts at 30 sec after loading:
    Initial ashing at 35-45°C (higher rate than 20°C baseline)
    Rate error: ~10-20% faster than recipe assumed
    Endpoint detection compensates (C₂ signal), but marginal

Solutions:

  Option 1: Wait longer (60+ sec) before ashing
    Result: Wafer fully cooled, recipe matches
    Penalty: Throughput loss (~0.5-1 wafers/hour)
  
  Option 2: Dedicated pre-cooler chamber
    Wafer pre-cooled to 20°C in separate chamber
    Transfer to ashing chamber already cooled
    Result: Immediate proper temperature, no transient
    Cost: $750K capital, 1-year payback at production volume
  
  Option 3: Temperature-dynamic recipe
    Use higher temperature setpoint early (~30°C)
    As wafer cools, reduce setpoint toward 20°C
    Result: Rate stays approximately constant
    Complexity: Requires closed-loop control
```

## E.3 Thermal Stress Calculation

```
Thermal stress from coefficient-of-thermal-expansion (CTE) mismatch:

Given:
  Carbon CTE: α_C ≈ 5 ppm/°C
  Si substrate CTE: α_Si ≈ 2.6 ppm/°C
  Mismatch: Δα = 5 - 2.6 = 2.4 ppm/°C
  
  Young's modulus (carbon): E_C ≈ 100 GPa
  Young's modulus (Si): E_Si ≈ 170 GPa

Temperature change during ashing:

  Initial state: T_i = 20°C
  During ashing: T_f = 50°C (peak, due to plasma heating)
  ΔT = 30°C

Linear strain from CTE mismatch:

  ε = Δα × ΔT = 2.4×10⁻⁶/°C × 30°C = 72×10⁻⁶ = 72 ppm

Thermal stress (biaxial constraint):

  σ = E_eff × ε

  For thin carbon film on Si substrate:
  Effective modulus ≈ E_C (carbon limited)
  
  σ = 100 GPa × 72×10⁻⁶ = 7.2 MPa (compressive)

Safety margin:

  Carbon tensile strength: ~1-2 GPa
  Stress/strength ratio: 7.2 MPa / 1000 MPa = 0.007 = 0.7%
  Safety factor: ~140× (VERY SAFE for bulk carbon)
  
  BUT: At interfaces (adhesion), stress can concentrate
  Interface shear strength: ~100-200 MPa
  Stress concentration factor: ~10-20× (from edge effects)
  Effective stress at interface: 7.2 × 15 = 108 MPa
  Safety factor at interface: 200/108 = 1.85× (MARGINAL!)

Mitigation:

  Keep ΔT < 20°C: σ < 5 MPa (safer)
  Use gradual ramping: Avoid thermal shock
  Monitor wafer adhesion: TEM cross-sections quarterly
```

## E.4 Thermal Runaway Prevention

```
Scenario: Plasma ignites, electrode temperature rises

Feedback control system:

  Electrode temperature measured by thermocouple
  PID controller adjusts chiller to maintain setpoint
  
  Nominal setpoint: T_set = 20°C ± 2°C
  Acceptable range: 18-22°C
  
PID parameters (typical):

  Proportional gain (Kp): 10 W/°C
  Integral gain (Ki): 1 W/°C/sec
  Derivative gain (Kd): 50 W·sec/°C
  
  Control output: Q_cooling = Kp×error + Ki×∫error + Kd×d(error)/dt

Failure mode: Thermocouple fails or loses signal

  System response:
    No feedback → chiller assumes T rising
    Chiller activates maximum cooling
    Electrode overcools (could reach 0°C, damages wafer)
    OR chiller fails to activate → T rises uncontrolled
  
  Prevention:
    Redundant thermocouple (dual sensors)
    Backup manual temperature readout
    Watchdog timer (if no update from thermocouple in 10 sec, alarm)
    Safe default: Max cooling activated if signal lost

Failure mode: Setpoint accidentally increased

  Operator sets T_set = 80°C (thinking it's pressure setpoint!)
  Plasma runs hot
  Wafer overheats during ashing
  
  Prevention:
    Setpoint range-limited in software (min 10°C, max 50°C)
    Confirmation required for setpoint changes >5°C
    Alarm if T exceeds 45°C (high-temp alarm)
    Auto-shutdown if T exceeds 60°C (safety limit)
```

---

**Appendix E Complete: Thermal Calculations & Modeling**

