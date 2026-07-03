# Passive Inductor EQ Build Guide (Hybrid Audio System)

## Overview

This guide describes how to build a passive inductor-based EQ for a hybrid analog + FPGA-controlled audio system.

It is not a precision mastering EQ. It is a **musical resonant network** designed for:
- broad tone shaping
- nonlinear magnetic behaviour
- level-dependent spectral change
- optional digital modulation of damping and topology

---

# 1. SYSTEM ARCHITECTURE

A passive EQ stage consists of:

- Low impedance input buffer (driver)
- LC networks for frequency shaping
- Resistive damping elements for Q control
- Output buffer for impedance recovery
- Optional FPGA-controlled variable resistance elements

### Core behaviour

- Inductors control current flow vs frequency
- Capacitors define voltage-based frequency separation
- Together they form resonant or shelving responses
- Actual EQ curve depends strongly on source/load impedance

---

# 2. INDUCTOR CORE SELECTION

## Recommended core types

### Best musical baseline
- MnZn ferrite rods (AM radio style cores)
- smooth saturation
- gentle hysteresis
- musically forgiving nonlinear response

### More aggressive response
- iron powder cores (-26 or -52 material)
- tighter low-end behaviour
- more defined saturation knee

### Experimental / character-heavy
- ceramic ferrite rods (unknown grade)
- unpredictable hysteresis
- strong tonal “voice”
- useful for expressive systems

---

## Do not use

- air cores (no saturation behaviour, too linear)
- mu-metal (unstable mechanical/magnetic behaviour)
- generic steel cores (noisy hysteresis, inconsistent response)

---

# 3. INDUCTOR WINDING DESIGN

## Wire choice

- 0.2 mm enamelled copper → high impedance coils
- 0.3 mm enamelled copper → general audio use (recommended)
- 0.4 mm+ → higher current, lower resistance coils

---

## Core geometry guidance

Typical experimental scale:
- ~150 mm rod length
- ~8 mm diameter

This supports:
- audible-range inductance values
- distributed field behaviour
- strong interaction with nonlinear effects

---

## Winding strategies

### Uniform winding (stable EQ)
Even spacing across full core length.

Result:
- predictable resonance
- stable EQ curves
- repeatable behaviour

---

### Segmented winding (recommended)

Divide core into functional zones:

- Low-frequency zone: tighter winding
- Mid-frequency zone: medium spacing
- High-frequency zone: sparse winding

Result:
- one coil behaves like multiple EQ bands
- natural frequency-dependent response shaping
- more organic spectral behaviour

---

## Turn count guidance

- 50–150 turns → high-frequency shaping
- 150–400 turns → general EQ behaviour (recommended range)
- 400–800 turns → strong low-frequency shaping / resonance emphasis

---

# 4. BASIC PASSIVE EQ TOPOLOGIES

## Resonant band cell

A single frequency-selective energy storage network:

- inductor in series with signal path
- capacitor to ground forming resonance

Behaviour:
- produces a resonant peak or dip depending on loading
- frequency determined by LC relationship
- response strongly affected by damping

---

## Shelving / tilt EQ cell

- inductor used as frequency-dependent impedance element
- resistor sets damping and tilt shape

Behaviour:
- broad tonal shaping
- smooth frequency slope
- more “musical EQ” than surgical filtering

---

## Multi-band passive network

Multiple resonant branches operating in parallel:

- each LC pair defines a spectral region
- interactions create overlapping resonances

Behaviour:
- complex EQ curves
- non-surgical tonal shaping
- highly dependent on impedance interactions

---

# 5. DAMPING AND Q CONTROL

Without damping, the system becomes overly resonant and unstable.

## Fixed damping

- resistors in series or parallel with LC elements
- typical range: 10Ω to 10kΩ

Effects:
- controls resonance sharpness
- stabilises frequency response
- reduces uncontrolled ringing

---

## Variable damping (FPGA-controlled)

Damping can be dynamically controlled using:
- optocouplers
- digital potentiometers
- MOSFET-based linear resistance control

Effects:
- resonance becomes performable
- EQ curves evolve over time
- spectral shape becomes time-dependent

---

# 6. DRIVER AND LOAD REQUIREMENTS

## Input stage

- must be low impedance
- must isolate source from reactive LC loading

Without this:
- EQ curve shifts unpredictably
- resonance becomes unstable
- frequency response depends on source device

---

## Output stage

- must be high impedance or buffered
- prevents external load from collapsing EQ behaviour

Without this:
- tonal balance changes with downstream gear
- resonance characteristics become inconsistent

---

# 7. NONLINEAR MAGNETIC BEHAVIOUR

## Core saturation

As signal level increases:

- inductance decreases effectively
- low frequencies compress first
- harmonic content increases naturally

Musical result:
- bass tightens under load
- mids gain harmonic density
- highs soften instead of hard clipping

---

## Hysteresis (magnetic memory)

Core materials retain short-term magnetic state:

- recent audio influences current response
- transient history affects tonal balance
- system exhibits short-term “memory EQ”

---

# 8. FPGA CONTROL LAYER (OPTIONAL)

The FPGA should not directly process audio.

It should control:

- damping elements
- switching of EQ branches
- modulation depth of nonlinear elements
- gain staging around LC networks

Musical result:
- EQ curves morph over time
- resonance shifts dynamically
- spectral balance becomes animated rather than static

---

# 9. PHYSICAL LAYOUT GUIDELINES

## Coil placement

- keep inductors physically separated unless intentional coupling is desired
- rotate adjacent coils 90 degrees to reduce unintended coupling
- avoid proximity to switching regulators or FPGA clocks

---

## Shielding

- shield digital/FPGA section
- avoid fully shielding inductors unless measuring baseline response
- allow controlled electromagnetic interaction where musically useful

---

## Grounding

- use star or split-ground architecture
- isolate analog and digital return paths
- avoid shared high-current ground segments

---

# 10. EXPECTED AUDIO BEHAVIOUR

If implemented correctly, the system behaves as:

- broad, musical EQ shaping rather than surgical filtering
- frequency response that shifts with signal level
- resonances that respond dynamically to load and drive
- subtle harmonic enhancement from magnetic components
- evolving spectral character under modulation

---

# 11. DESIGN INTENT

This system is designed for:

- expressive tone shaping
- nonlinear spectral movement
- physically grounded sound design
- controlled instability as a creative parameter

It is NOT designed for:

- transparent mastering EQ
- fixed frequency correction
- precision surgical filtering

---

# SUMMARY

This is a passive LC-based EQ system where:

- inductors define frequency behaviour
- capacitors define resonance structure
- magnetic cores introduce nonlinear dynamics
- FPGA elements add time-based modulation

The result is a **living spectral network rather than a static EQ device**.
