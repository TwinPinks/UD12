# UD12

**TWIN PINKS UD12** is a nonlinear two-pole state-variable filter based on
the Polivoks circuit and its K140UD12 operational amplifiers. It is built from
the circuit itself — the amplifier nonlinearity, the sag and bump of the transfer
characteristic, and the behaviour of the loop at its limit are all computed in
real time, not reproduced from a table of presets.

## Ports

| Port | Function |
|---|---|
| **IN** | Audio input |
| **CV1** | Cutoff modulation via the CV1 attenuverter |
| **CV2** | Cutoff modulation, 1 V/oct, no attenuverter |
| **BP** | Band-pass output |
| **LP** | Low-pass output |

Bypassing the module passes the input to both outputs.

## Controls

| Control | Range | Notes |
|---|---|---|
| **CUTOFF** | 5.1 Hz – 20.9 kHz | Non-linear taper, as on the hardware: center ≈ 650 Hz |
| **RES** | 0 – 100 % | Above ≈ 92 % the filter enters self-oscillation |
| **CV1** | −3 – +3 | Attenuverter for the CV1 input |
| **INPUT** | −6 – +6 dB | Center is unity; extremes are exactly ×0.5 and ×2 |
| **OUTPUT** | 0 – 100 % | Default 83 % |

CV is summed into the cutoff at 1 V/oct. Cutoff will not travel above 26.5 kHz —
this ceiling is set by the circuit (the saturation current of the first stage).

## Levels

The input expects eurorack-level signals, around **±4 to ±5 V**, as produced by
a typical VCO. This matters more than it may seem: the circuit's nonlinearities
respond to level. A weak signal will not bring out the character, and an
excessively hot one will drive the filter into limiting before you hear the
resonance. If your source is louder, trim it with the **INPUT** control.

## Menu (right-click)

**CV limit** — what happens when CV pushes the cutoff past the ceiling:

* **Soft** (default) — the cutoff eases smoothly into the ceiling.
* **Fold (experimental)** — above the ceiling the cutoff reflects back down by
  the same number of octaves. A sound-design option, not a property of the
  hardware.

**Core rate** — the internal processing rate. The model runs at its own rate and
is resampled to the host rate by an output filter. A higher rate means more
accuracy at the top of the range and more CPU:

| Rate | Use |
|---|---|
| 768 kHz | Maximum accuracy |
| **384 kHz** (default) | The working choice: half the cost, no audible difference |
| 192 kHz | Economy mode |

On 44.1 kHz host families the labels are computed from the family and read
705.6 / 352.8 / 176.4 kHz — the rates actually running in your build.

## What to expect

* **Resonance up to ~92 %** — normal filter operation.
* **Above that** — the filter begins to sound on its own. This is the hardware's
  behaviour, not a fault: the Polivoks' self-oscillation was measured from the
  instrument and reproduced along with its threshold and the character of its
  onset.
* **In the bass** at high resonance the loop is limited harder than a simple
  drop in level — a dedicated law, derived from the decay of the free
  oscillation on the hardware. It engages only when a signal is present at the
  input, so it stays out of the way when the module is used as an oscillator.
* **Cutoff above 17 kHz at a 44.1 kHz host** rolls off honestly: there is no
  room above it at that host rate. At 48 kHz and higher this does not occur.

## CPU

One voice at the defaults (384 kHz core, 48 kHz host) costs about 2.5 % of one
core on an Apple M-series CPU. The 768 kHz core costs roughly twice as much,
192 kHz roughly half.

## Patches

The module stores the core rate and the CV limit mode in the patch. Patches
made with earlier versions open correctly: control positions are carried over
by their own laws, and the nearest available core rate is selected.

---

© TWIN PINKS. Filter model and code by Stepan Chernov.
