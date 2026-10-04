# Appendix D: Ashing Rate Lookup Tables

## D.1 Photoresist Ashing Rate vs. Process Parameters

```
Table: Ashing Rate (nm/min) for ArF Photoresist
Varying Temperature, Coil Power, Bias Power
Pressure fixed at 70 mTorr, O₂ 200 sccm

Temperature: -10°C

Coil Power (W)  W_bias=300W  W_bias=400W  W_bias=500W  W_bias=600W
────────────────────────────────────────────────────────────
1800            28           33           38           42
2000            32           37           43           48
2200            36           41           47           53
2400            40           46           52           58

Temperature: 0°C

Coil Power (W)  W_bias=300W  W_bias=400W  W_bias=500W  W_bias=600W
────────────────────────────────────────────────────────────
1800            31           37           43           48
2000            36           43           50           56
2200            41           48           56           62
2400            46           54           62           69

Temperature: 10°C

Coil Power (W)  W_bias=300W  W_bias=400W  W_bias=500W  W_bias=600W
────────────────────────────────────────────────────────────
1800            35           42           49           55
2000            41           49           57           64
2200            47           56           65           72
2400            53           63           73           81

Temperature: 20°C (STANDARD)

Coil Power (W)  W_bias=300W  W_bias=400W  W_bias=500W  W_bias=600W
────────────────────────────────────────────────────────────
1800            40           48           56           63
2000            47           56           65           73
2200            54           65           75           84
2400            61           73           85           95

Temperature: 30°C

Coil Power (W)  W_bias=300W  W_bias=400W  W_bias=500W  W_bias=600W
────────────────────────────────────────────────────────────
1800            46           55           64           72
2000            54           65           75           84
2200            62           75           86           97
2400            71           85           99           111

Temperature: 40°C

Coil Power (W)  W_bias=300W  W_bias=400W  W_bias=500W  W_bias=600W
────────────────────────────────────────────────────────────
1800            53           64           74           83
2000            63           76           87           98
2200            72           87           101          113
2400            82           99           114          128

Usage example:
  To ash 80 nm photoresist at T=20°C, W_coil=2000W, W_bias=400W:
  From table: Rate = 56 nm/min
  Time = 80 nm / 56 nm/min = 1.43 min = 86 seconds
  Safety margin: Add 10% buffer → 95 seconds ashing time
```

## D.2 Temperature Coefficient Correction

```
Quick adjustment factor for temperature variations:

If your fab operates at different T than tabulated:

Correction factor: f(T) = R(T_actual) / R(T_standard)

Example: Tables are at T_standard = 20°C
         Your fab operates at T_actual = 25°C
         Correction = 1.08 (8% faster)
         
         If table says 56 nm/min at 20°C:
         At 25°C → 56 × 1.08 = 60.5 nm/min

Temperature adjustment table:

ΔT from 20°C    Correction Factor    Notes
────────────────────────────────────────
-10°C            0.71              (~30% slower)
-5°C             0.84              (~15% slower)
 0°C             0.93              (~7% slower)
+5°C             1.08              (~8% faster)
+10°C            1.22              (~22% faster)
+15°C            1.39              (~39% faster)
+20°C            1.57              (~57% faster)

Application:

  Adjusted rate = Base rate × Correction factor
  
  Example:
    Base (20°C): 60 nm/min
    Actual T: 5°C (cooler)
    Correction: 0.93
    Adjusted: 60 × 0.93 = 55.8 nm/min
    Time for 80 nm: 80/55.8 = 1.43 min = 86 seconds
```

## D.3 Selectivity Lookup Table (C/SiO₂)

```
Table: C/SiO₂ Selectivity Ratio
Varying Temperature and Effective Ion Energy

Note: Ion energy E_ion ≈ 0.3 × V_bias
  V_bias = 200 V → E_ion ≈ 60 eV
  V_bias = 300 V → E_ion ≈ 90 eV
  V_bias = 400 V → E_ion ≈ 120 eV

Temperature: -10°C (High Selectivity)

E_ion (eV)   60 eV    90 eV    120 eV   150 eV
──────────────────────────────────────
Selectivity  28:1     22:1     17:1     14:1

Temperature: 0°C

E_ion (eV)   60 eV    90 eV    120 eV   150 eV
──────────────────────────────────────
Selectivity  25:1     20:1     15:1     12:1

Temperature: 10°C

E_ion (eV)   60 eV    90 eV    120 eV   150 eV
──────────────────────────────────────
Selectivity  23:1     18:1     14:1     11:1

Temperature: 20°C (STANDARD)

E_ion (eV)   60 eV    90 eV    120 eV   150 eV
──────────────────────────────────────
Selectivity  20:1     16:1     12:1     10:1

Temperature: 30°C

E_ion (eV)   60 eV    90 eV    120 eV   150 eV
──────────────────────────────────────
Selectivity  17:1     14:1     11:1     8:1

Temperature: 40°C

E_ion (eV)   60 eV    90 eV    120 eV   150 eV
──────────────────────────────────────
Selectivity  15:1     12:1     9:1      7:1

Production decision:

  For 30 nm carbon hard mask (minimum ~3 nm margin safe):
    Minimum selectivity required: (80-3)/30 = 2.57:1
    (This is actually achievable but risky!)
    
    For safety margin (5 nm acceptable):
      Required selectivity: (80-5)/(30-5) = 3:1
      Possible in production, but tight
    
    For generous margin (10 nm acceptable):
      Required selectivity: (80-10)/(30-10) = 3.5:1
      Comfortably achievable
    
  Recommendation:
    Use parameters that give selectivity 15-20:1
    Provides huge safety (5+ nm selectivity margin)
    Standard production-safe recipe
```

## D.4 Time-to-Etch Calculator

```
Quick lookup: Ashing time for given thickness

Fill in your baseline rate from experiment:
  My baseline rate: _______ nm/min (at my conditions)
  My standard thickness: _______ nm
  
Calculation: Time (sec) = Thickness (nm) / Rate (nm/min) × 60

Common thickness scenarios:

For 80 nm resist at 50 nm/min: Time = 80/50 × 60 = 96 sec
For 80 nm resist at 60 nm/min: Time = 80/60 × 60 = 80 sec
For 80 nm resist at 70 nm/min: Time = 80/70 × 60 = 69 sec
For 100 nm resist at 50 nm/min: Time = 100/50 × 60 = 120 sec
For 100 nm resist at 60 nm/min: Time = 100/60 × 60 = 100 sec
For 100 nm resist at 70 nm/min: Time = 100/70 × 60 = 86 sec

Thickness (nm) | Rate=50 nm/min | Rate=60 nm/min | Rate=70 nm/min
───────────────────────────────────────────────────────────────
     50        |    60 sec      |    50 sec      |    43 sec
     75        |    90 sec      |    75 sec      |    64 sec
     80        |    96 sec      |    80 sec      |    69 sec
     90        |   108 sec      |    90 sec      |    77 sec
    100        |   120 sec      |   100 sec      |    86 sec
    110        |   132 sec      |   110 sec      |    94 sec
    120        |   144 sec      |   120 sec      |   103 sec

Endpoint time with safety margin (add 10%):

     80        |   106 sec      |    88 sec      |    76 sec
    100        |   132 sec      |   110 sec      |    95 sec
    120        |   158 sec      |   132 sec      |   113 sec
```

---

**Appendix D Complete: Ashing Rate Lookup Tables**

