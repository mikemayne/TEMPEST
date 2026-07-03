# System Audio & EQ Behaviour — Musical / Spectral Design README

## Overview

This system behaves less like a conventional EQ or processor and more like a **field-driven spectral sculptor**.

It combines:
- Passive / semi-passive filter networks
- Inductor-based frequency shaping
- Nonlinear magnetic elements (core saturation, hysteresis)
- FPGA-controlled modulation of gain, damping, and topology
- Optional spatial / mechanical interaction (ferrofluid / geometry)

The result is not a fixed EQ curve, but a **continuously morphing frequency response that depends on signal level, time, and control state**.

---

# 1. CORE EQ ARCHITECTURE

## 1.1 Passive inductor-based shaping

The base EQ behaviour is dominated by LC-style networks:

- Inductors act as **frequency-dependent resistive elements**
- Capacitive elements define resonance boundaries
- Source impedance (op-amp or passive drive) defines damping

### Musical effect
- Broad, musical tilt rather than surgical filtering
- “Weighted” frequency zones instead of fixed bands
- Natural resonance peaks that feel program-dependent

### Character
- Low frequencies: thick, slightly elastic
- Mids: dynamically coloured depending on saturation state
- Highs: soft roll-off with occasional resonant lift rather than sharp EQ cuts

---

## 1.2 Damping as a first-class control

Unlike conventional EQ, Q-factor is not fixed.

Damping is controlled by:
- FPGA-driven variable resistance (digital pot / opto / VCA-like element)
- Coil core losses (temperature + flux state)
- Feedback network impedance changes

### Musical effect
- EQ bands feel “alive” rather than static
- Peaks can widen or collapse dynamically
- Resonances behave like “breathing formants”

---

# 2. NONLINEAR MAGNETIC EQ BEHAVIOUR

## 2.1 Core saturation as spectral compression

Inductors are not linear:

- At low levels → behave like clean reactive filters
- At moderate levels → introduce harmonic redistribution
- At high levels → compress low frequencies magnetically

### Musical effect
- Bass becomes denser rather than louder
- Midrange gains harmonic texture under drive
- High frequency transients soften instead of clipping harshly

This creates a **frequency-selective compression curve**:
- lows = compression
- mids = harmonic generation
- highs = smoothing / damping

---

## 2.2 Hysteresis (memory of sound)

Magnetic cores retain state briefly:

### Musical effect
- Recent transients influence current tonal balance
- Kick drums subtly affect following bass tone
- Sustained material “charges” the EQ curve

This is not distortion in the traditional sense — it is **temporal EQ biasing**.

---

# 3. FPGA-CONTROLLED SPECTRAL MOTION

## 3.1 Macro EQ morphing

The FPGA does not “EQ” in a static sense. It controls:

- Band center drift
- Q modulation
- Gain staging per band or region
- Cross-coupling between channels (mid/side or stereo field)

### Musical effect
- EQ curves slowly evolve over time
- Spectral “tilt” shifts like moving light through a lens
- No two moments sound identical under modulation

---

## 3.2 Time-domain spectral animation

Control sources may include:
- LFOs
- Envelope followers
- Audio-rate modulation (carefully filtered)
- External sidechain signals

### Musical effect
- Frequency response behaves like motion rather than setting
- Percussive elements “scan through” tonal space
- Pads develop shifting harmonic emphasis

---

# 4. MID / SIDE AND SPATIAL EQ BEHAVIOUR

## 4.1 Mid/Side spectral decoupling

The system naturally supports splitting:

- Mid channel → core inductive / nonlinear processing
- Side channel → more filtered / constrained / spatially stable path

### Musical effect
- Center becomes dense, harmonic, and dynamic
- Sides remain airy and stable
- Perceived width changes with frequency content

---

## 4.2 Spatial frequency instability (intentional)

Because of inductive coupling and modulation:

- Left/right channels may not respond identically under extreme conditions
- Slight phase and tonal divergence occurs

### Musical effect
- “Enlarged” stereo image under modulation
- Subtle movement in spatial perception without explicit panning
- Organic width that is frequency-dependent

---

# 5. DYNAMIC EQ BEHAVIOUR (LEVEL-DEPENDENT SHAPING)

## 5.1 Signal-dependent frequency response

The EQ curve is not static; it changes with amplitude:

- Low level: more linear, open bandwidth
- Medium level: harmonic shaping engages
- High level: compression + resonance damping dominates

### Musical effect
- Quiet signals sound clean and extended
- Loud signals become dense, focused, and saturated
- Natural “mix glue” without explicit bus compression

---

## 5.2 Program-dependent tone shaping

Different material produces different EQ behaviour:

- Percussive input → sharper transient-controlled shaping
- Sustained tones → resonance build-up and drift
- Complex mixes → self-balancing spectral redistribution

---

# 6. SYSTEM-WIDE MUSICAL CHARACTER

## 6.1 Not an EQ, but a “spectral organism”

The system behaves like:

- A resonant filter network
- A nonlinear magnetic medium
- A slowly evolving modulation field

Rather than:
- fixed bands
- predictable gain curves
- static frequency correction

---

## 6.2 Core sonic traits

### Frequency domain
- Soft, wide EQ bands
- Organic resonance rather than surgical peaks
- Level-dependent tonal balance

### Time domain
- Memory effects (hysteresis)
- Slow spectral drift
- Feedback-like “aftertaste” of transients

### Spatial domain
- Mid/side divergence under modulation
- Frequency-dependent stereo width changes

---

## 7. DESIGN INTENT (IMPORTANT)

This system is designed to behave like:

> “EQ that reacts to music rather than corrects it.”

It is not intended for:
- transparent mastering correction
- surgical frequency removal
- linear, repeatable filtering

It *is* intended for:
- tone shaping that feels alive
- evolving spectral textures
- physically informed harmonic colour

---

## SUMMARY

Conventional EQ:
- static bands
- predictable gain curves
- linear response

This system:
- dynamic frequency field
- nonlinear magnetic coloration
- time-dependent spectral memory
- spatially responsive tone shaping
