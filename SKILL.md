---
name: formant-diphthong-dynamics
description: Generates exhaustive Formant & Diphthong Dynamics reports specifying time-varying formant trajectories (onset, nucleus, offset in ms) for FACE, PRICE, GOAT, MOUTH, CHOICE, consonant locus equations for /b d g/, and Euclidean Vowel Space Area (VSA). Trigger with 'formant dynamics for', 'diphthong trajectories of', 'locus equations for', or '/formant-dynamics'.
disable-model-invocation: true
---

# Formant & Diphthong Dynamics

## Purpose & Scope

This skill models the **dynamic, time-varying trajectories of speech formants**. Static formant averages (e.g., "F1 = 500, F2 = 1500") fail to capture the true essence of human vocal identity because personal identity lives in the **glides, transition slopes, and coarticulatory locus equations**. This skill maps the millisecond-by-millisecond trajectories of diphthongs and the mathematical slopes of consonant-vowel transitions.

This skill owns:
- Dynamic formant trajectories (F1, F2, F3 time-series at 20%, 50%, 80% duration) for all diphthongs (FACE, PRICE, GOAT, MOUTH, CHOICE, NEAR, SQUARE)
- Diphthong offglide duration, trajectory velocity (Hz/ms), and Euclidean vector length
- Consonant-vowel locus equations for stops (/b, d, g/) defining $F2_{	ext{onset}} = m \cdot F2_{	ext{vowel}} + k$
- Euclidean Vowel Space Area (VSA in $	ext{Hz}^2$) and Formant Centralization Ratio (FCR)
- Dynamic coarticulation resistance indices

This skill does **not** own fundamental frequency intonation curves (owned by `prosodic-grammar-intonation-os`).

---

## Activation Triggers

Activate automatically when:
- User asks for formant trajectories, diphthong glide dynamics, or locus equations (e.g., *"formant dynamics for [speaker]"*, *"diphthong curves of [subject]"*).
- User triggers `/formant-dynamics [subject]`.
- Calibrating formant synthesis engines (KlattGrid, CHANT) or training high-fidelity neural vocoders.
- Documenting dialect-specific vowel shifts that depend on glide direction rather than target quality.

---

## Mandatory Report Schema & Structure

### 1. Diphthong Trajectory Time Series
For FACE, PRICE, GOAT, MOUTH, CHOICE, NEAR, and SQUARE, record:
- **Onset Formants (20% duration):** F1, F2, F3 in Hz.
- **Nucleus Formants (50% duration):** F1, F2, F3 in Hz.
- **Offset / Target Formants (80% duration):** F1, F2, F3 in Hz.
- **Trajectory Length (TL):** Euclidean distance in Bark or Hz between onset and offset.
- **Glide Duration (ms) & Velocity:** Transition speed in Hz per millisecond.

### 2. Consonant Locus Equations
Linear regression parameters predicting F2 onset from following vowel F2 ($F2_{	ext{onset}} = m \cdot F2_{	ext{vowel}} + k$):
- **Bilabial /b/:** Slope ($m$), intercept ($k$ in Hz), correlation ($r^2$).
- **Alveolar /d/:** Slope ($m$), intercept ($k$ in Hz), correlation ($r^2$).
- **Velar /g/:** Slope ($m$), intercept ($k$ in Hz), correlation ($r^2$).
- **Articulatory Coarticulation Degree:** High slope ($m 	o 1.0$) indicates high coarticulation; low slope ($m 	o 0$) indicates articulatory rigidity.

### 3. Vowel Space Area (VSA) & Acoustic Dispersion
- **Euclidean VSA ($	ext{Hz}^2$):** Calculated from triangular or quadrilateral corner vowels (/i, æ, ɑ, u/).
- **Formant Centralization Ratio (FCR):** Ratio assessing vowel space expansion vs. hypo-articulatory compression.
- **Vowel Centralization Tendency:** Degree of schwa-ward drift during rapid speech.

### 4. Coarticulation & Transition Durations
- **Formant Transition Duration (ms):** Mean millisecond duration of formant transitions from stop release into vowel steady state (typically 30–70 ms).
- **Anticipatory Coarticulation:** Spread of lip rounding or nasalization across syllable boundaries.

---

## Machine Output Block

```json
{
  "$schema": "https://json-schemas.voice/formant-dynamics.v1.json",
  "speaker_id": "SPEAKER_ID",
  "diphthong_trajectories": {
    "PRICE": {
      "t20_f1_f2_f3": [740, 1220, 2450],
      "t50_f1_f2_f3": [650, 1540, 2480],
      "t80_f1_f2_f3": [480, 1920, 2550],
      "duration_ms": 175,
      "glide_velocity_hz_per_ms": 4.0
    },
    "MOUTH": {
      "t20_f1_f2_f3": [710, 1380, 2420],
      "t50_f1_f2_f3": [640, 1210, 2400],
      "t80_f1_f2_f3": [490, 1020, 2380],
      "duration_ms": 160,
      "glide_velocity_hz_per_ms": 2.25
    },
    "GOAT": {
      "t20_f1_f2_f3": [520, 1080, 2380],
      "t50_f1_f2_f3": [490, 1010, 2390],
      "t80_f1_f2_f3": [440, 920, 2410],
      "duration_ms": 145,
      "glide_velocity_hz_per_ms": 1.1
    }
  },
  "locus_equations": {
    "b": {"slope": 0.72, "intercept_hz": 420, "r2": 0.91},
    "d": {"slope": 0.41, "intercept_hz": 1180, "r2": 0.88},
    "g": {"slope": 0.85, "intercept_hz": 310, "r2": 0.94}
  },
  "vowel_space": {
    "euclidean_vsa_hz2": 285400,
    "fcr_ratio": 1.04,
    "coarticulation_resistance": "MODERATE_HIGH"
  }
}
```

---

## Biometric & Personality Crosswalk

| Dynamics Parameter | Core Biometric Section | Personality Profile Section | Synthesis Compiler Target |
| :--- | :--- | :--- | :--- |
| Diphthong Trajectories | §3 Formant Frequencies & Vowel Space | §3.4 Cultural Vernacular | Klatt Time-Varying Formant Tiers |
| Locus Equation Slopes | §6 Articulatory Precision | §5.2 Articulatory Search | Coarticulation Transition Interpolator |
| VSA & Centralization | §3 Spectral Characteristics | §4.1 Dominant Attitude | Dynamic Formant Bandwidth / Area |
| Transition Duration | §2 Waveform Properties | §5.1 Turn-Taking Cadence | Phoneme Boundary Morph Timers |

---

## Calibration Reference Example: Queens Orator Baseline

- **PRICE Trajectory:** Starts fronted at F2 ~1220 Hz and glides rapidly toward 1920 Hz with a steep 4.0 Hz/ms velocity, maintaining crisp dialectal separation.
- **GOAT Monophthongization Tendency:** Shallow glide slope (1.1 Hz/ms), exhibiting near-monophthongal backing [oː] during rapid extemporaneous speech.
- **Alveolar Locus (/d/):** High intercept (1180 Hz) and low slope ($m = 0.41$), signaling high coarticulation resistance and crisp alveolar tongue placement.
- **Vowel Space Area:** VSA is expansive in formal addresses ($285,400	ext{ Hz}^2$), compressing by ~18% during rapid rally storytelling.

---

## Generation Rules

1. Provide complete 3-point time-series coordinates (20%, 50%, 80%) in Hz for all primary diphthongs.
2. Formulate consonant locus equations with explicit slope ($m$) and intercept ($k$).
3. Every profile must output the machine-readable `diphthong_trajectories.json` block.
