# Audio / FPGA / Inductive Chaos System — EMC & Stability README

## Overview

This system deliberately blends:
- Fast digital logic (FPGA control domain)
- Sensitive analog audio paths
- Magnetic/inductive elements
- Nonlinear components (saturation, clipping, opto or vactrol control)
- Physical field interaction (coils, ferrofluid, spatial geometry)

This creates a design space where **electromagnetic coupling is not just noise risk, but a functional variable**.

However, without constraints, the same mechanisms become uncontrolled instability, hiss, modulation artefacts, and unpredictable behaviour.

This document outlines:

1. Primary sources of electromagnetic and circuit-level chaos  
2. Failure modes they cause  
3. Explicit design “do nots” to avoid collapse into uncontrolled behaviour  

---

# 1. FPGA DOMAIN CHAOS SOURCES

## 1.1 Fast edge transitions (primary RF source)

### What causes chaos
- GPIO switching edges (rise/fall times in ns range)
- Internal PLL clocks and fabric toggling
- PWM or sigma-delta style modulation
- High fan-out parallel switching

### Failure modes
- RF noise injection into analog stages
- Audible “digital hash” on outputs
- In-band modulation of audio via ground bounce
- Coil excitation from unintended harmonics

### DO NOT
- Do not route FPGA signals near analog inputs
- Do not allow unbuffered FPGA pins to directly drive anything analog-sensitive
- Do not run high-frequency PWM near audio bandwidth intentionally unless isolated
- Do not share return paths between FPGA I/O current and audio ground

---

## 1.2 Power rail switching noise

### What causes chaos
- Simultaneous switching outputs (SSO)
- Internal core current spikes
- DC/DC converter ripple coupling

### Failure modes
- Low frequency “motorboating” modulation
- Dynamic distortion tied to FPGA activity
- Instability when logic load changes

### DO NOT
- Do not power analog and FPGA from shared unfiltered rails
- Do not rely on decoupling capacitors alone for domain separation
- Do not route analog reference from digital regulator outputs

---

# 2. GROUNDING & RETURN PATH CHAOS

## 2.1 Shared ground impedance

### What causes chaos
- Analog and digital currents sharing copper paths
- Long ground loops between modules
- Inductor current return mixing with signal return

### Failure modes
- Audio distortion dependent on digital processing load
- Hum that changes with FPGA activity
- Channel cross-modulation

### DO NOT
- Do not use a single undifferentiated ground plane for everything
- Do not daisy-chain analog ground through FPGA ground
- Do not route coil return currents through audio reference ground

---

## 2.2 Ground bounce coupling

### What causes chaos
- High di/dt switching in FPGA I/O banks
- Insufficient local return capacitance
- Long interconnect inductance

### Failure modes
- Random clicks or ticks in audio
- “Breathing” noise floor
- Unstable threshold behaviour in analog control paths

### DO NOT
- Do not rely on long ribbon cables for FPGA I/O
- Do not route high-speed signals without adjacent return paths
- Do not assume ground is equipotential across the system

---

# 3. INDUCTOR / COIL CHAOS DOMAIN

## 3.1 Electromagnetic radiation

### What causes chaos
- Time-varying current through large coils
- Poor shielding or open geometry coils
- Interaction with enclosure materials

### Failure modes
- Coil behaves as transmitter and receiver simultaneously
- Audio picks up digital clock harmonics
- Unintended feedback loops through air

### DO NOT
- Do not place inductors near FPGA or DC/DC converters
- Do not assume coil fields are localized
- Do not leave coil wiring unshielded at long distances

---

## 3.2 Mutual inductance between system elements

### What causes chaos
- Multiple coils in proximity
- Parallel wiring runs
- Shared magnetic cores or structures

### Failure modes
- Cross-channel modulation
- Unstable stereo imaging
- Motion/geometry-dependent tonal shifts

### DO NOT
- Do not run multiple coil drive lines in parallel bundles
- Do not assume channels are electrically independent if physically close
- Do not ignore enclosure geometry as part of the circuit

---

## 3.3 Core nonlinearity unpredictability

### What causes chaos
- Ferrite or mu-metal saturation curves
- Hysteresis effects
- Temperature-dependent permeability shifts

### Failure modes
- Non-reproducible distortion characteristics
- Drift over time or heat
- “Memory” effects in sound

### DO NOT
- Do not assume linear response from inductive elements
- Do not calibrate system without thermal considerations
- Do not treat magnetic cores as static components

---

# 4. ANALOG AUDIO DOMAIN CHAOS

## 4.1 High impedance nodes

### What causes chaos
- Op-amp feedback networks with large resistances
- Vactrol or opto-controlled gain stages
- Floating filter nodes

### Failure modes
- RF pickup from digital subsystem
- Audible hiss modulation
- Sensitivity to physical layout changes

### DO NOT
- Do not leave high impedance nodes unshielded near digital traces
- Do not route sensitive nodes across board boundaries
- Do not assume PCB layout is electrically irrelevant

---

## 4.2 Nonlinear feedback paths

### What causes chaos
- Saturating inductors in feedback loops
- Variable resistance elements (vactrols, digital pots)
- Frequency-dependent feedback gains

### Failure modes
- Oscillation at unpredictable frequencies
- Sudden regime shifts in tone
- “Alive” or unstable behaviour under load

### DO NOT
- Do not place nonlinear elements inside uncontrolled high-gain loops
- Do not combine multiple nonlinear feedback paths without damping
- Do not assume stability from small-signal analysis alone

---

# 5. DIGITAL ↔ ANALOG INTERFACE CHAOS

## 5.1 Direct coupling without isolation

### What causes chaos
- FPGA pins directly biasing analog nodes
- Shared ADC/DAC references without filtering
- Mixed-domain routing

### Failure modes
- Digital clock bleed into audio band
- Parameter control affecting signal path unintentionally
- Loss of repeatability

### DO NOT
- Do not connect FPGA outputs directly to op-amp summing nodes
- Do not share reference voltages without filtering/isolation
- Do not treat digital control as “DC-only”

---

## 5.2 Control-rate aliasing into audio domain

### What causes chaos
- Low-rate parameter modulation from FPGA
- PWM or stepped control signals
- Insufficient smoothing of control voltage

### Failure modes
- Aliasing artifacts in audio band
- Stepped or “grainy” modulation textures
- Unintended rhythmic artefacts

### DO NOT
- Do not modulate analog gain directly with raw digital PWM
- Do not skip reconstruction filtering on control signals
- Do not assume “slow control” is automatically safe

---

# 6. ENCLOSURE / PHYSICAL GEOMETRY CHAOS

## 6.1 Electromagnetic boundary effects

### What causes chaos
- Metal enclosures forming partial Faraday cages
- Open plastic structures allowing radiation
- Asymmetrical layouts

### Failure modes
- Frequency response changes depending on enclosure
- Spatial dependency of sound character
- Sensitivity to nearby objects or cables

### DO NOT
- Do not assume enclosure is neutral
- Do not change physical layout without expecting electrical consequences
- Do not ignore cable routing as part of circuit design

---

# 7. SYSTEM-WIDE CHAOS INTERACTIONS

## 7.1 Feedback between domains

### Key risk
The system is not linear. It contains multiple feedback paths:

- FPGA activity → EMI → coil response → analog modulation → FPGA sensing loop
- Coil field → analog gain shift → feedback instability
- Ground bounce → control signal drift → unintended modulation

### DO NOT
- Do not assume separation of “control path” and “audio path” is absolute
- Do not introduce feedback loops without explicit damping
- Do not test subsystems independently and assume system-level stability

---

# DESIGN PRINCIPLES (SAFE OPERATING MODE)

These are not constraints — they are stabilisation strategies:

- Separate domains physically first, electrically second
- Treat inductors as both emitters and sensors
- Assume every wire is an antenna unless proven otherwise
- Filter control signals even if they seem “slow”
- Design grounding as current routing, not voltage reference
- Expect enclosure geometry to affect signal behaviour

---

# FINAL NOTE

This system is intentionally close to the boundary between:
- controlled analog synthesis
- and electromagnetic instability

The goal is not to eliminate chaos.

The goal is to **decide where chaos is allowed to exist — and where it is forbidden**.
