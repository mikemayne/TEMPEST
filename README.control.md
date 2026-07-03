# FPGA-Controlled Passive Inductor EQ — Full Control & Build Overview

## Overview

This document describes a hybrid audio system where a passive LC (inductor-capacitor) EQ network performs all frequency shaping, while an FPGA provides dynamic control over how that network behaves over time.

The system is intentionally not a fixed EQ. It is a **resonant analog network whose behavior is continuously reconfigured by digital control signals**.

---

# 1. SYSTEM ARCHITECTURE

The audio path is fully analog and passive in character:

- Input is buffered by a low impedance driver
- Signal passes through passive LC networks (inductors and capacitors)
- Damping elements shape resonance and Q
- Output is recovered by a buffer stage

The FPGA does not process audio directly. It only controls parameters that affect the analog network.

---

# 2. PASSIVE EQ CORE BEHAVIOUR

The EQ is built from LC resonant networks:

- Inductors control frequency-dependent impedance
- Capacitors define resonance and frequency separation
- The interaction between L and C creates peaks, dips, and shelving behaviour

Unlike digital EQ, the response is not perfectly fixed. It depends on:
- source impedance
- load impedance
- signal level
- magnetic core behaviour

This makes the EQ inherently interactive and non-linear.

---

# 3. INDUCTOR DESIGN AND CORE MATERIALS

## Core types

### MnZn ferrite rod cores
These are the recommended baseline for musical behaviour. They provide smooth saturation, gentle hysteresis, and predictable but musical nonlinear response.

### Iron powder cores (-26 / -52 material)
These offer tighter low-frequency control and more defined saturation behaviour. They are more linear at low levels but compress more abruptly under load.

### Experimental ferrite / ceramic rods
These introduce strong character and unpredictability. They are less consistent but can produce highly expressive and unique tonal behaviour.

## Wire selection

- 0.3 mm enamelled copper is the general-purpose choice
- 0.2 mm wire increases impedance and sensitivity
- 0.4 mm or thicker improves current handling and reduces resistive loss

## Winding approach

Uniform winding produces stable and predictable EQ behaviour.

Segmented winding creates distributed frequency behaviour along a single core, allowing one inductor to act like multiple interacting spectral regions.

---

# 4. BASIC EQ STRUCTURE

## Resonant behavior

An inductor and capacitor form a resonant system that can emphasize or attenuate specific frequencies. The exact behavior depends on damping and load conditions.

## Shelving behavior

By altering how inductors interact with resistive elements, the system can produce broad frequency tilts rather than sharp peaks. This gives a more natural and musical tonal shaping effect.

## Multi-band interaction

Multiple LC branches can operate in parallel, creating overlapping resonances. This produces complex, organic EQ curves that are highly dependent on impedance and signal level.

---

# 5. DAMPING AND RESONANCE CONTROL

Without damping, LC circuits become overly resonant and unstable.

Fixed damping uses resistors to control resonance sharpness and stabilize the system.

Variable damping introduces dynamic control of resonance using electronically controlled resistance elements. This allows the system to transition between:
- tight, controlled EQ
- open resonant shaping
- unstable, expressive behaviour

Damping is one of the most important controls in the system.

---

# 6. FPGA CONTROL LAYER

The FPGA operates entirely in the control domain.

## What it controls

### Damping
Adjusts resonance sharpness and Q-factor dynamically.

### Topology switching
Enables or disables LC branches, effectively changing the EQ structure in real time.

### Gain staging
Controls how strongly the passive network is driven, influencing saturation and harmonic generation.

### Modulation sources
Generates time-based control signals such as LFOs, envelopes, random variation, or external sidechain-driven modulation.

---

## Control signal implementation

The FPGA output is converted into analog control signals using either PWM (filtered) or DAC-based systems.

These control signals drive:
- optocouplers
- MOSFET variable resistors
- switching elements for topology changes

The audio signal is never directly processed by the FPGA.

---

# 7. NONLINEAR MAGNETIC BEHAVIOUR

Inductors are not linear components in this system.

## Saturation

As signal level increases, inductance effectively decreases. This causes:
- low frequencies to compress first
- harmonic content to increase naturally
- softening of high-frequency transients

## Hysteresis

Magnetic cores retain a short-term memory of past signals. This causes the system to respond not only to current input but also to recent signal history, creating a form of temporal tonal shaping.

---

# 8. PHYSICAL LAYOUT CONSIDERATIONS

Inductor placement and system layout significantly affect performance.

Inductors should be physically separated unless intentional coupling is desired. Rotation of adjacent coils can reduce unintended magnetic interaction.

The FPGA and switching electronics should be physically isolated from analog inductive elements to prevent noise coupling.

Grounding must be carefully structured to avoid shared return currents between digital and analog domains.

---

# 9. WHAT NOT TO DO

- Do not route audio directly through FPGA logic
- Do not leave PWM control signals unfiltered
- Do not share analog and digital ground paths without structure
- Do not assume inductors behave linearly under all conditions
- Do not place inductors near switching regulators or high-speed digital traces
- Do not assume EQ behaviour is independent of signal level or load

---

# 10. SYSTEM BEHAVIOUR SUMMARY

This system behaves as a hybrid between:

- a passive analog resonant filter network
- a nonlinear magnetic tone-shaping system
- a digitally modulated control environment

It does not behave like a conventional EQ. It behaves like a **physically interactive spectral system whose response evolves over time**.

---

# FINAL DESIGN INTENT

The FPGA defines movement and structure.

The LC network defines tone and resonance.

The inductors define character and nonlinearity.

Together they form a system that is not a static processor, but a **dynamic, physically grounded audio instrument**.
