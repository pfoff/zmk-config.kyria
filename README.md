# Kyria ZMK config

ZMK firmware for two SplitKB Kyria keyboards from a single shared keymap,
converted from a QMK `keymap.c`.

- **rev3** — wireless (nice!nano v2), rotary encoders, no underglow.
- **rev2.1** — wireless (nice!nano v2), RGB underglow LEDs, no encoders.

Pinned to ZMK **v0.3.0** so upstream `main` changes can't break the build.

## Repo layout

```
.github/workflows/build.yml   GitHub Actions build (pinned @v0.3.0)
build.yaml                    all four targets (two halves x two revisions)
config/west.yml               ZMK dependency, pinned to v0.3.0
config/kyria_base.dtsi        the keymap - single source of truth for BOTH boards
config/kyria_rev3.keymap      thin wrapper: #define HAS_ENCODERS  + include base
config/kyria_rev2.keymap      thin wrapper: #define HAS_UNDERGLOW + include base
config/kyria_rev3.conf        rev3 features (encoders, mouse, sleep)
config/kyria_rev2.conf        rev2.1 features (underglow, mouse, sleep)
```

## One source, two boards

Both keyboards share `kyria_base.dtsi`. The per-revision `.keymap` files are
one-line switches that set a `#define` and include the base:

- `HAS_ENCODERS`  -> encoder `sensor-bindings` are compiled in.
- `HAS_UNDERGLOW` -> the RGB keys on the Adjust layer become real `&rgb_ug`
  controls; without it they collapse to `&trans`, so the layout is identical.

Edit the keymap once in `kyria_base.dtsi`; both boards pick it up. Per-board
hardware differences live in the two `.conf` files.

## Building & flashing

1. Push to GitHub. The **Actions** tab builds on every push.
2. One run produces four `.uf2` files (rev3 L/R, rev2 L/R) in the artifacts zip.
3. Per board, flash the **left** half - it is the central half that runs the
   keymap. Double-tap reset, the nice!nano mounts as a USB drive, copy the
   matching `.uf2` on. Then the right half the same way.

No local toolchain needed.

## Layers

`0 QWERTY · 1 ADJUST · 2 SPACED · 3 SHIFTED · 4 FUNCTION · 5 FUNCSHIFT · 6 macOS · 7 Spaced(Mac)`

- **FUNCTION + SHIFTED** held together activate **FUNCSHIFT** (QMK tri-layer, via
  a `conditional_layers` node).
- **macOS (6)** is an optional toggle (ADJUST + M) that swaps Ctrl->Cmd on the
  left-side modifiers. Press-to-toggle, does not survive a reboot - for a
  permanent swap use macOS System Settings > Keyboard > Modifier Keys.
- **Spaced(Mac) (7)** is automatic (SPACED + macOS): the SPACED encoders then
  task-switch with Cmd+Tab instead of Alt+Tab.

### Encoders (rev3), per layer

| Layer | Left encoder | Right encoder |
| --- | --- | --- |
| QWERTY / Adjust | cursor left/right | cursor up/down |
| Spaced | Alt+Tab task switch | Alt+Tab task switch |
| Shifted / Function / FuncShift | Volume | Brightness |

Alt-Tab is `&inc_dec_kp`, i.e. it taps the combo each detent (toggles between the
two most-recent windows rather than scrolling through all).

### Adjust layer

- **Left hand:** sleep, Bluetooth profiles 0-4 (`&bt BT_SEL`), output select
  (`&out OUT_USB/BLE/TOG`), and BT clear (`&bt BT_CLR` / `BT_CLR_ALL`).
- **Right hand (rev2.1 only):** RGB underglow - on/off, effect cycle
  (solid -> breathe -> spectrum -> swirl), brightness +/-, and 8 colour presets
  (red, orange, yellow, green, cyan, blue, purple, white). Presets set the active
  colour, which solid/breathe show; spectrum/swirl cycle hues on their own.
- **ADJUST + M:** toggle the macOS layer.

## Notes

- **Thumb-shift (right thumb)** is a plain `&mo SHIFTED` momentary layer that
  carries pre-shifted keycodes (no hardware modifier held). Capitals and shifted
  symbols come from those keycodes. **Exception:** thumb-shift + Enter sends
  **Shift+Enter** (pos 33 on SHIFTED is `&kp LS(RET)`), so it does not submit in
  chat apps.
- **rev2.1 underglow** defaults to the swirl gradient and is **capped at 30%**
  brightness to save battery (`CONFIG_ZMK_RGB_UNDERGLOW_BRT_MAX=30`). ZMK has no
  battery-only dimming, so this is a global ceiling.
- **Mouse emulation** (`&mkp`/`&mmv`/`&msc`) is on the SPACED layer; needs
  `CONFIG_ZMK_POINTING=y` (set in both `.conf` files).
- **Leader-key sequences and OLED art** from the QMK file are not ported.
