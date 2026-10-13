# UD12

**TWIN PINKS UD12** is a nonlinear two-pole state-variable filter based on
the Polivoks circuit. UD12 takes its name from the K140UD12, the Soviet
operational amplifier used in the Polivoks filter.

The model was developed through transistor-level simulations and measurements
of an original hardware filter.

## Ports

| Port | Function |
|---|---|
| **IN** | Audio input |
| **CV1** | Cutoff CV through the CV1 attenuverter |
| **CV2** | Cutoff CV, 1 V/oct |
| **BP** | Band-pass output |
| **LP** | Low-pass output |

The two cutoff CV inputs are summed. CV2 tracks 1 V/oct, and in self-oscillation
the filter plays in tune across the low and middle registers. CV1 runs through a
bipolar attenuverter; at ×3 a 5 V source such as an envelope can sweep the full
cutoff range, depending on where CUTOFF is set. The attenuverter starts at 0,
so CV1 has no effect until you turn it up.

Bypassing the module passes the input to both outputs.

## Controls

| Control | Range | Notes |
|---|---|---|
| **CUTOFF** | 5.1 Hz – 20.9 kHz | Non-linear taper, as on the hardware: center ≈ 650 Hz |
| **RES** | 0 – 100 % | Above ≈ 95 % the filter enters self-oscillation |
| **CV1** | ×−3 – ×3 | Attenuverter for the CV1 input |
| **GAIN** | −6 – +6 dB | Center is unity; extremes are exactly ×0.5 and ×2 |
| **OUTPUT** | 0 – 100 % | Default 83 % |

RES at 0 % does not remove the resonance completely: a slight peak at the
cutoff remains even with the knob all the way down, as on the original.

CV takes the cutoff beyond the range of the knob. Upward it reaches 26.5 kHz.
Downward there is no limit: CV can sweep the filter well into the sub-audio
range.

## Levels

The input expects eurorack-level signals, around **±4 to ±5 V**, as produced by
a typical VCO. This matters more than it may seem: the filter's character depends
on input level. A weak signal will not bring out the character, and an
excessively hot one will drive the filter into saturation before you hear the
resonance. If your source is louder, trim it with the **GAIN** control.

## Menu (right-click)

**CV limit** — what happens when CV pushes the cutoff past the ceiling:

* **Soft** (default) — the cutoff eases smoothly into the ceiling.
* **Fold (experimental)** — above the ceiling the cutoff reflects back down by
  the same number of octaves. A sound-design option, not a property of the
  hardware.

**Core rate** — UD12 uses oversampling; Core rate sets the internal processing
rate. A higher rate means more accuracy at the top of the range and more CPU:

| Mode | Rate | Use |
|---|---|---|
| High | 768 kHz | Maximum accuracy |
| **Normal** (default) | 384 kHz | The working choice: half the cost, no audible difference |
| Eco | 192 kHz | Economy mode |

On 44.1 kHz host families the labels are computed from the family and read
705.6 / 352.8 / 176.4 kHz — the rates actually running in your build.

## CPU

On a MacBook Air M2 running VCV Rack 2 Pro, one instance in Normal mode
measured approximately 2.7 % of one CPU core at a 48 kHz project rate with
default controls and no CV modulation. In the same test, CPU usage decreased to
approximately 2.0 % at 96 kHz and 1.6 % at 192 kHz. Results depend on the
computer, patch and processing mode.

## Patches

The module saves the Core rate and CV limit settings with your patch.

---

© TWIN PINKS. Filter model and code by Stepan Chernov.
