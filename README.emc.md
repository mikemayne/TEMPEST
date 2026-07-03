Passive Inductor EQ with Magnetic Non-Linearity

Overview

This project is a mono passive equaliser built around hand-wound ferrite rod inductors. Unlike conventional passive EQs that aim for transparency, the goal is to exploit the non-ideal behaviour of real inductors to produce musically interesting colouration, harmonic distortion and dynamic frequency response.

The EQ is intended to become part of a stereo processor, operating primarily on the Mid (mono) channel while allowing the Side channel to be processed separately.

⸻

Design Goals

* Simple passive LC equaliser topology.
* Use custom wound ferrite inductors.
* Accept imperfect frequency response.
* Encourage magnetic saturation.
* Allow electronic control of the magnetic operating point.
* Produce behaviour somewhere between passive EQ, tape saturation and transformer colour.

⸻

Signal Path

Input Buffer
      │
      │
Passive LC Network
      │
Output Make-up Gain

The passive network always attenuates.

An output amplifier restores the lost gain and can optionally add additional clipping or saturation.

⸻

Passive EQ Section

The EQ consists of one or more resonant sections.

Each section contains:

* Ferrite rod inductor
* Capacitor
* Resistor for Q control

Typical configurations are:

Low Shelf

Signal
 │
 L
 │
 C
 │
Ground

Changing L or C changes turnover frequency.

⸻

Mid Bell

Signal
 │
 ├────L────┐
 │         │
 │         C
 │         │
 └──R──────┘
 │
Output

The resistor controls resonance.

Because the inductor is non-ideal, the centre frequency and Q change slightly with signal level.

⸻

High Shelf

Capacitor in series
followed by
inductor to ground

Again, the ferrite characteristics modify behaviour as current increases.

⸻

Why the Inductors Matter

Conventional EQ inductors attempt to behave ideally.

These inductors intentionally do not.

The custom ferrite rods exhibit:

* Variable inductance with current
* Core losses
* Hysteresis
* Saturation
* Eddy current effects (depending on material)
* Frequency dependent permeability

This means:

* EQ frequency shifts with programme material.
* Resonance changes dynamically.
* Harmonics are generated naturally.
* Loud signals compress slightly.

The result should be a much more animated sound than a conventional passive EQ.

⸻

Magnetic Bias Coil

Each audio inductor has a second winding.

This winding carries DC or low-frequency current only.

            Audio winding
Signal ─────────████████─────
               Ferrite Core
Bias Current ───████████─────

The bias winding never carries audio.

Instead it changes the magnetic operating point of the ferrite.

Changing bias alters:

* Inductance
* Saturation point
* Distortion character
* Harmonic balance
* Compression
* Resonant frequency

⸻

FPGA Control

An FPGA generates control signals that influence the bias winding through a simple current source (for example, a 2N2222A transistor with an emitter resistor).

Possible modulation sources include:

* Envelope follower
* LFO
* Sidechain level
* Mid/Side ratio
* User controls
* Preset automation
* Random modulation

The FPGA does not process the audio directly in this stage.

It only controls the magnetic state of the core.

⸻

Saturation Behaviour

As audio level increases:

1. Core permeability falls.
2. Inductance decreases.
3. EQ frequency shifts.
4. Harmonic distortion increases.
5. Compression occurs naturally.
6. Resonance softens.

Additional DC bias changes where this transition occurs.

The processor therefore behaves as both an EQ and a dynamically changing analogue colour device.

⸻

Output Stage

Because passive EQ introduces insertion loss, the output stage provides make-up gain.

Potential additions include:

* Op-amp gain stage
* Soft clipping
* Diode feedback clipping
* Vactrol-controlled clipping depth
* Variable drive control

This stage can provide further analogue character while preserving the passive EQ’s frequency shaping.

⸻

Expected Sonic Character

The processor is not intended to emulate any specific vintage unit exactly.

Instead it should offer:

* Tape-like saturation
* Transformer-style harmonic enrichment
* Dynamic EQ movement
* Level-dependent tonal balance
* Magnetic compression
* Slowly evolving timbral changes through FPGA modulation

Each hand-wound inductor will have slightly different characteristics, making every build unique.

⸻

Future Extensions

Potential enhancements include:

* Switchable inductors for multiple EQ bands
* Relay-switched capacitor banks
* Digitally controlled magnetic bias presets
* Stereo linking of bias modulation
* Mid/Side independent EQ
* Envelope-controlled resonance
* Audio-rate bias modulation for experimental effects
* Ferrofluid visualiser driven from the same sidechain, creating a physical display that reflects the processor’s behaviour

The overall vision is an analogue signal processor whose frequency response, distortion and dynamics are all influenced by controllable magnetic components, with the FPGA acting as a flexible modulation engine rather than replacing the analogue audio path.
