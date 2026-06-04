# Kyria — ZMK Keymap Dokumentation

Dokumentation der Tastenbelegung für die kabellose SplitKB Kyria (rev3, je nice!nano v2). Konvertiert aus dem ursprünglichen QMK-Keymap. Es gibt **7 Ebenen**; das Keymap läuft auf der **zentralen (linken) Hälfte**.

## Tastenpositionen

Alle Ebenen nutzen dieselbe physische Nummerierung:

```
 0   1   2   3   4   5                 6   7   8   9  10  11
12  13  14  15  16  17                18  19  20  21  22  23
24  25  26  27  28  29  30  31    32  33  34  35  36  37  38  39
            40  41  42  43  44    45  46  47  48  49
```
Die **Encoder** sitzen baulich auf Position **31** (links, Tastendruck = Strg auf QWERTY) und Position **11** (rechts, Tastendruck = Bksp auf QWERTY). Drehen ist pro Ebene belegt (siehe unten); der Tastendruck ist die normale Belegung der jeweiligen Position.

## Notation

| Schreibweise | Bedeutung |
|---|---|
| `X` | normale Taste X |
| `Ct/Esc` | **Mod-Tap**: gehalten = Strg (Modifier), getippt = Esc |
| `Ct/'` | Mod-Tap: gehalten = Strg, getippt = `'` |
| `Spc→2` | **Layer-Tap**: gehalten = Ebene 2 (SPACED), getippt = Leertaste |
| `Adj→1`, `Fn→4`, `Sh→3` | **momentane Ebene**: nur solange gehalten aktiv |
| `Mac` | **rastende Umschaltung** der Ebene (toggle), bleibt an bis erneut gedrückt |
| `·` | transparent — reicht zur darunterliegenden Ebene (i. d. R. QWERTY) durch |
| `LMaus`/`RMaus`/`MMaus` | linke/rechte/mittlere Maustaste |
| `Maus↑↓←→`, `Rad↑↓` | Mauszeiger bewegen / Mausrad |

## Ebenen-Übersicht

| # | Ebene | Aktivierung | Encoder-Drehen (CW / CCW) |
|---|---|---|---|
| 0 | QWERTY | Basis (immer) | Pfeil ab / Pfeil auf |
| 1 | ADJUST | linker äußerer Daumen (40) halten | Alt+Tab / Alt+Shift+Tab |
| 2 | SPACED | Space-Daumen (43/46) halten | Bild ab / Bild auf |
| 3 | SHIFTED | rechter innerer Daumen (45) halten | Bild auf / Bild ab |
| 4 | FUNCTION | linker innerer Daumen (44) halten | Helligkeit + / − |
| 5 | FUNCSHIFT | FUNCTION + SHIFTED gemeinsam | Lautstärke + / − |
| 6 | macOS | ADJUST + M (rastend) | Pfeil ab / Pfeil auf |

## Daumencluster (Kern des Layouts)

Die fünf Daumentasten je Hälfte tragen die Ebenenlogik:

| Pos | Taste | Funktion |
|---|---|---|
| 40 | `Adj→1` | ADJUST halten |
| 41 | `LMaus` | linke Maustaste |
| 42 | `RGui` | rechte GUI/Super (auf macOS-Ebene → Strg) |
| 43 | `Spc→2` | tippen = Leertaste, halten = SPACED |
| 44 | `Fn→4` | FUNCTION halten |
| 45 | `Sh→3` | SHIFTED halten — der **Daumen-Shift** (Großschreibung) |
| 46 | `Spc→2` | tippen = Leertaste, halten = SPACED |
| 47 | `Bksp` | Backspace |
| 48 | `Del` | Entf |
| 49 | `MMaus` | mittlere Maustaste |

> **Daumen-Shift:** Ebene SHIFTED (45) enthält direkt die Groß-/Shift-Zeichen (`LS(...)`), statt einen Hardware-Modifier zu halten — daher zuverlässig. Für Shift+Klick / Shift+Pfeil (Auswahl) dienen die echten Shift-Tasten auf Pos 24 und 39.

## Ebene 0 · QWERTY (Basis)

Standard-Tippebene. Immer aktiv, sofern keine andere Ebene oben liegt.

```
  `      Q      W      E      R      T     ║    Y      U      I      O      P     Bksp 
Ct/Esc   A      S      D      F      G     ║    H      J      K      L      ;     Ct/' 
Shift    Z      X      C      V      B     ║    N      M      ,      .      /    Shift 

Innere Tasten:  30=Tab  31=Ctrl   ║   32=Alt  33=Enter
Daumen links :  40=Adj→1  41=LMaus  42=RGui  43=Spc→2  44=Fn→4
Daumen rechts:  45=Sh→3  46=Spc→2  47=Bksp  48=Del  49=MMaus
```

## Ebene 1 · ADJUST

Halten: linker äußerer Daumen (Pos 40). System-/RGB-/Mac-Umschaltung.

```
Sleep    ·      ·      ·      ·      ·     ║    ·      ·      ·      ·      ·      ·   
  ·      ·      ·      ·      ·      ·     ║    ·      ·      ·      ·      ·      ·   
  ·      ·      ·      ·      ·      ·     ║    ·     Mac     ·      ·      ·    Enter 

Innere Tasten:  30=Hell+  31=Laut+   ║   32=·  33=·
Daumen links :  40=·  41=RMaus  42=·  43=Hell-  44=Laut-
Daumen rechts:  45=·  46=·  47=·  48=·  49=·
```

## Ebene 2 · SPACED

Halten: eine der beiden Space-Daumentasten (Pos 43 / 46). Navigation, Pfeile, Maus.

```
  `     Esc   LMaus  Maus↑  RMaus   Rad↑   ║    ·      ·      ·      ·      -      ·   
  ·      `    Maus←  Maus↓  Maus→   Rad↓   ║    ←      ↓      ↑      →      =    BildAuf
 Caps   Esc   MMaus   Del    Bksp   Ins    ║    ·     Menu   Pos1   Ende    \\   BildAb

Innere Tasten:  30=·  31=·   ║   32=·  33=·
Daumen links :  40=·  41=·  42=·  43=·  44=·
Daumen rechts:  45=·  46=·  47=Del  48=Space  49=·
```

## Ebene 3 · SHIFTED

Halten: rechter innerer Daumen (Pos 45). Großbuchstaben + Shift-Zeichen.

```
  ~      Q      W      E      R      T     ║    Y      U      I      O      P      ·   
  ·      A      S      D      F      G     ║    H      J      K      L      :      "   
  ·      Z      X      C      V      B     ║    N      M      <      >      ?      ·   

Innere Tasten:  30=·  31=·   ║   32=·  33=·
Daumen links :  40=·  41=·  42=·  43=·  44=·
Daumen rechts:  45=·  46=·  47=·  48=·  49=·
```

## Ebene 4 · FUNCTION

Halten: linker innerer Daumen (Pos 44). Symbole (links) + Ziffernblock (rechts).

```
  `      &      %      ·      ^      |     ║    [      7      8      9      -      ·   
  ·      @      ·      ·      ·      #     ║    (      4      5      6      +      ·   
  ·      *      _      !      $      \\    ║    {      1      2      3      =    Enter 

Innere Tasten:  30=·  31=·   ║   32=·  33=·
Daumen links :  40=·  41=·  42=·  43=·  44=·
Daumen rechts:  45=·  46=0  47=.  48=,  49=Enter
```

## Ebene 5 · FUNCSHIFT

Halten: FUNCTION + SHIFTED gemeinsam (beide inneren Daumen). F-Tasten + schließende Klammern.

```
Power    ·      ·      ·      ·      ·     ║    ]      F7     F8     F9    F10     ·   
  ·      ·      ·      ·      ·      ·     ║    )      F4     F5     F6    F11     !   
  ·      ·      ·      ·      ·      ·     ║    }      F1     F2     F3    F12   Druck 

Innere Tasten:  30=·  31=·   ║   32=·  33=·
Daumen links :  40=·  41=·  42=·  43=·  44=·
Daumen rechts:  45=·  46=·  47=·  48=·  49=·
```

## Ebene 6 · macOS

Umschalten (rastend): ADJUST + M. Tauscht links Strg↔Cmd. Übersteht keinen Neustart.

```
  ·      ·      ·      ·      ·      ·     ║    ·      ·      ·      ·      ·      ·   
Cmd/Es   ·      ·      ·      ·      ·     ║    ·      ·      ·      ·      ·      ·   
  ·      ·      ·      ·      ·      ·     ║    ·      ·      ·      ·      ·      ·   

Innere Tasten:  30=·  31=Cmd   ║   32=·  33=·
Daumen links :  40=·  41=·  42=Ctrl  43=·  44=·
Daumen rechts:  45=·  46=·  47=·  48=·  49=·
```

## Sondertasten & Verhalten

- **Mod-Tap** (`Ct/Esc`, `Ct/'`): kurz tippen = Zeichen, halten = Modifier. Auf QWERTY: Pos 12 = Strg/Esc, Pos 23 = Strg/`'`.

- **Tri-Layer:** FUNCTION (4) und SHIFTED (3) gleichzeitig gehalten aktivieren automatisch FUNCSHIFT (5) — die Reihenfolge ist egal. Entspricht QMKs `update_tri_layer`.

- **Maus:** Klicks (`LMaus`/`RMaus`/`MMaus`), Zeigerbewegung (SPACED, linke Hand) und Mausrad. Benötigt `CONFIG_ZMK_POINTING`.

- **Encoder:** Drehbelegung ist pro Ebene gesetzt (Tabelle oben); beide Encoder verhalten sich gleich. Der Tastendruck des Encoders ist die jeweilige Positionsbelegung (links Pos 31, rechts Pos 11).

- **macOS-Modus (Ebene 6):** rastende Umschaltung über **ADJUST + M**. Tauscht auf der linken Seite Strg→Cmd (Pos 12 Mod-Tap, Pos 31 Encoder-Druck) und die linke GUI-Daumentaste → Strg (Pos 42). Alt/Option bleibt unverändert; die rechte Strg/`'`-Taste bleibt absichtlich unangetastet, damit Shift+`'` weiter `"` liefert. **Übersteht keinen Neustart** — für eine dauerhafte Lösung Strg/Cmd in den macOS-Systemeinstellungen tauschen.

## Flashen (Kurz-Erinnerung)

Bei einem ZMK-Split läuft das Keymap auf der **zentralen = linken** Hälfte. Für reine Keymap-Änderungen genügt es, die **linke** `.uf2` zu flashen. Die Meldung „NICENANO nicht korrekt ausgeworfen" ist normal: das Board startet nach dem Kopieren selbst neu — verschwindet das Laufwerk, war der Flash erfolgreich. Die Keymap-Datei muss `config/kyria_rev3.keymap` heißen (passend zum Shield-Namen), sonst baut ZMK still das Standard-Layout.
