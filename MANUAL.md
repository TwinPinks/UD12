# UD12

**TWIN PINKS UD12** is a nonlinear two-pole state-variable filter based on
the Polivoks circuit. UD12 takes its name from the K140UD12, the Soviet
operational amplifier used in the Polivoks filter.

The model comes from transistor-level simulation of that circuit and from
measurements of a hardware Polivoks filter.

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

The input expects eurorack levels, around **±4 to ±5 V**, as produced by a
typical VCO. Input level changes how the resonance responds and how the filter
sounds. A quiet signal keeps it in its linear range; a very hot one saturates it
before the resonance comes through. Trim a loud source with **GAIN**.

## Menu (right-click)

**CV limit** — what happens when CV pushes the cutoff past the ceiling:

* **Soft** (default) — the cutoff slows as it nears the ceiling and stops there.
* **Fold (experimental)** — above the ceiling the cutoff reflects back down by
  the same number of octaves. A sound-design option, not a property of the
  hardware.

**Core rate** — UD12 uses oversampling; Core rate sets the internal processing
rate. A higher rate means more accuracy at the top of the range and more CPU:

| Mode | Rate | CPU | Use |
|---|---|---|---|
| Extreme | 768 kHz | ×4 | Maximum accuracy |
| High | 384 kHz | ×2 | Steadier pitch and level under cutoff FM at high resonance |
| **Normal** (default) | 192 kHz | — | The working choice |

At 44.1 kHz project rates the menu reads 705.6 / 352.8 / 176.4 kHz instead,
and the default is 176.4 kHz.

## Patches

The module saves the Core rate and CV limit settings with your patch.

---

Audio examples and details: [twinpinksmusic.com/ud12-vcv](https://twinpinksmusic.com/ud12-vcv)

© TWIN PINKS. Filter model and code by Stepan Chernov.
