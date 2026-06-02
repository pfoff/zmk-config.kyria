# Kyria ZMK config

ZMK firmware config for a wireless SplitKB Kyria (nice!nano v2 in both halves),
converted from a QMK `keymap.c`.

## Repo layout

```
.github/workflows/build.yml   GitHub Actions build (produces the .uf2 files)
build.yaml                    which board + shields to build
config/west.yml               ZMK build dependencies
config/kyria_rev3.keymap           the keymap (6 layers + encoders)
config/kyria_rev3.conf             feature flags (encoders, mouse, RGB, sleep)
```

## Building

1. Create a new **empty** GitHub repository and push these files to it.
2. Open the **Actions** tab — a build starts automatically on push.
3. When it finishes, download the **artifacts** zip. It contains two files:
   `kyria_rev3_left-nice_nano_v2-zmk.uf2` and `...right...uf2`.
4. Flash each half: put the nice!nano into bootloader mode (double-tap reset),
   it mounts as a USB drive, copy the matching `.uf2` onto it. Repeat for the
   other half.

No local toolchain needed — the build runs in the cloud.

## Hardware assumptions

- **Controllers:** nice!nano v2, both halves.
- **Revision:** targets `kyria_rev3_*` (your old QMK OLED said "Kyria rev 2").
  If it's a rev3, change both shield lines in `build.yaml` to `kyria_rev3_left`
  / `kyria_rev3_right`. A wrong revision usually shows up as a dead/scrambled
  column.
- **Encoders:** one per half. Left encoder sits on the Ctrl key, right encoder
  on Backspace. Rotation is handled by the per-layer `sensor-bindings`; the
  encoder push is just the key it sits on (Ctrl / Backspace). Enabled via
  `CONFIG_EC11=y` in `kyria_rev3.conf`.
- **No OLED.** No display config is included.
- **RGB underglow** is enabled so the `RGB_*` keys on the ADJUST layer work. It
  compiles fine even with no LEDs soldered; delete `CONFIG_ZMK_RGB_UNDERGLOW=y`
  from `kyria_rev3.conf` if you don't want it.

## Layers

`0 QWERTY · 1 ADJUST · 2 SPACED · 3 SHIFTED · 4 FUNCTION · 5 FUNCSHIFT`

FUNCTION + SHIFTED held together activate FUNCSHIFT (QMK tri-layer, done here
with a `conditional_layers` node).

## Notes carried over from the QMK conversion

- **Right thumb (`SSHFT`)** is a plain `&mo SHIFTED` momentary layer. In QMK it
  also held Left-Shift; that's dropped to keep the FUNCSHIFT F-keys clean.
  Capitals come from the dedicated LSHFT/RSHFT keys on the bottom row. An
  optional `&sshft` macro that restores hold-Shift is included (commented) in
  `kyria_rev3.keymap`.
- **Encoder Alt-Tab** (ADJUST layer) is approximated with `&inc_dec_kp` — it
  cycles windows but taps Alt each detent instead of holding it.
- **Both encoders currently do the same thing per layer** (matching the QMK
  code). To split them, the first binding in each `sensor-bindings` pair is the
  left encoder, the second is the right.
- **Leader-key sequences and OLED art** from the QMK file are not ported (no ZMK
  equivalent / no display).
