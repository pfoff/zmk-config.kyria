# Keymap reference

Auto-generated from `config/kyria_base.dtsi` (run `tools/gen_keymap_md.py`).
Each cell is one key; blank = transparent (falls through to the layer below).
The two inner keys on row 3 and the five thumb keys per half sit toward the centre.

**Legend:** `Ct/Esc` = Ctrl held / Esc tapped · `Spc/Spc`,`/2`,`/Spc` = layer-tap (hold = that layer) · `>Adj`,`>Fn`,`>Sft` = momentary layer while held · `tgMac` = toggle · `BT0..BT4` = BT profile · `BTclr`/`BTclA` = clear current/all · `USB`/`BLE`/`Out<>` = output · `RGB` = LEDs on/off · `Eff>` = next effect · `Bri+/-` = LED brightness · colour names = set underglow colour · `Vol+/-` = volume · `Scr+/-` = screen brightness · `Whl` = scroll wheel · `mUp`.. = mouse move · `A+S+Tb` = Alt+Shift+Tab · `S+Ent` = Shift+Enter.

> **Board differences:** the right-hand RGB block + colour presets on ADJUST are rev2.1 only (underglow board); on rev3 those keys are transparent. Encoders are rev3 only (see the README encoder table).

## Layer 0 - QWERTY (base)

```
  `     Q     W     E     R     T                                Y     U     I     O     P    Bksp

Ct/Esc  A     S     D     F     G                                H     J     K     L     ;    Ct/'

LShft   Z     X     C     V     B    Tab  LCtrl     LAlt Enter   N     M     ,     .     /   RShft
             >Adj  LClk  RGUI Spc/2  >Fn                  >Sft Spc/2  Bksp  Del   MClk
```

## Layer 1 - ADJUST (hold left-outer thumb)  <-- Bluetooth + RGB are here

```
Sleep  BT0   BT1   BT2   BT3   BT4                              RGB   Bri+  Red  Yellow Cyan Purple

       USB   BLE  Out<>                                         Eff>  Bri-  Org  Green  Blue White

      BTclr BTclA                    Scr+  Vol+                      tgMac                   Enter
                   RClk        Scr-  Vol-
```

## Layer 2 - SPACED (hold either Space thumb): mouse, arrows, navigation

```
  `    Esc   LClk  mUp   RClk WhlUp                                                      -

        `   mLeft mDown mRightWhlDn                             Left  Down   Up  Right   =    PgUp

 Caps  Esc   MClk  Del   Bksp  Ins                                    Menu  Home  End    \    PgDn
                                                                      Del  Space
```

## Layer 3 - SHIFTED (hold right thumb): shifted symbols; Tab = Alt+Shift+Tab, Enter = Shift+Enter

```
  ~     Q     W     E     R     T                                Y     U     I     O     P

        A     S     D     F     G                                H     J     K     L     :     "

        Z     X     C     V     B   A+S+Tb               S+Ent   N     M     <     >     ?

```

## Layer 4 - FUNCTION (hold right-outer thumb): numbers + symbols

```
  `     &     %           ^     |                                [     7     8     9     -

        @                       #                                (     4     5     6     +

        *     _     !     $     \                                {     1     2     3     =   Enter
                                                                 0     .     ,   Enter
```

## Layer 5 - FUNCSHIFT (FUNCTION + SHIFTED together): F-keys + brackets

```
Power                                                            ]     F7    F8    F9   F10

                                                                 )     F4    F5    F6   F11    !

                                                                 }     F1    F2    F3   F12  PrtSc

```

## Layer 6 - macOS (toggle with ADJUST + M): swaps Ctrl -> Cmd on the left modifiers

```


Gu/Esc

                                           LGUI
                        LCtrl
```
