# Fang den Punkt

## Willkommen! @showdialog

🎯 **Fang den Punkt!**

Ein Punkt saust hin und her. Drücke **A** genau dann, wenn er in der **Mitte** ist!
Triffst du, bekommst du einen Punkt – und es wird **schneller**.
Verpasst du ihn: **Game Over**!

**Neu in diesem Spiel:** **Sprites** (bewegliche Figuren), die **dauerhaft**-Schleife und der **Spielstand**.

## Einen Sprite erzeugen

Ein **Sprite** ist ein einzelnes Licht, das sich bewegen kann – wie eine Spielfigur.

- :align justify: Erstelle eine Variable ``punkt``.
- :mouse pointer: Ziehe ``||variables:setze punkt auf||`` in ``||basic:beim Start||``.
- :gamepad: Setze aus ``||game:Spiel||`` den Block ``||game:erzeuge Sprite an Position x: 2 y: 2||`` ein.

```blocks
let punkt = game.createSprite(2, 2)
```

~hint Was bedeuten x und y? 💡
Der Bildschirm hat 5 × 5 Lichter. **x** ist die Spalte von links (0 bis 4), **y** die Zeile von oben (0 bis 4).
**x: 2, y: 2** ist genau die **Mitte**.
hint~

## Hin und her

Jetzt soll der Punkt sich **immer** bewegen. Dafür gibt es die Schleife ``||basic:dauerhaft||`` – sie hört nie auf.

- :th: Ziehe ``||basic:dauerhaft||`` auf die Arbeitsfläche (falls er nicht schon da ist).
- :gamepad: Ziehe ``||game:punkt bewege um 1||`` hinein.
- :gamepad: Darunter: ``||game:punkt pralle ab, wenn am Rand||``.
- :th: Zum Schluss: ``||basic:pausiere (ms)||`` mit **300**.

```blocks
let punkt = game.createSprite(2, 2)
basic.forever(function () {
    punkt.move(1)
    punkt.ifOnEdgeBounce()
    basic.pause(300)
})
```

## Treffer oder daneben?

Wenn du **A** drückst, prüft der micro:bit: Ist der Punkt in der Mitte (**x = 2**)?

- :circle: Ziehe ``||input:wenn Knopf A gedrückt||`` auf die Arbeitsfläche.
- :random: Ziehe ``||logic:wenn wahr dann sonst||`` hinein.
- :random: Setze den Vergleich ``||logic:0 = 0||`` ein.
- :gamepad: Links kommt ``||game:punkt x||``, rechts eine **2**.
- :gamepad: Im **wenn**-Teil: ``||game:ändere Spielstand um 1||``.
- :gamepad: Im **sonst**-Teil: ``||game:Game Over||``.

```blocks
let punkt = game.createSprite(2, 2)
basic.forever(function () {
    punkt.move(1)
    punkt.ifOnEdgeBounce()
    basic.pause(300)
})
input.onButtonPressed(Button.A, function () {
    if (punkt.get(LedSpriteProperty.X) == 2) {
        game.addScore(1)
    } else {
        game.gameOver()
    }
})
```

## Ausprobieren @showdialog

Teste im Simulator! Drücke **A**, wenn der Punkt in der Mitte ist.

Bei **Game Over** zeigt der micro:bit deinen Spielstand an. 🏆

Ist es dir noch zu leicht? Dann machen wir es jetzt **schneller**!

## Immer schneller

Bei jedem Treffer soll die Pause **kürzer** werden. Dafür brauchen wir eine Variable ``tempo``.

- :align justify: Erstelle eine Variable ``tempo`` und setze sie in ``||basic:beim Start||`` auf **300**.
- :mouse pointer: Ziehe ``||variables:tempo||`` in den Block ``||basic:pausiere (ms)||`` statt der 300.
- :align justify: Ziehe ``||variables:ändere tempo um||`` unter ``||game:ändere Spielstand um 1||`` und mache daraus **-20**.

```blocks
let tempo = 300
let punkt = game.createSprite(2, 2)
basic.forever(function () {
    punkt.move(1)
    punkt.ifOnEdgeBounce()
    basic.pause(tempo)
})
input.onButtonPressed(Button.A, function () {
    if (punkt.get(LedSpriteProperty.X) == 2) {
        game.addScore(1)
        tempo += -20
    } else {
        game.gameOver()
    }
})
```

## Geschafft! @showdialog

🎉 Dein Geschicklichkeitsspiel ist fertig!

Wer in der AG schafft den **höchsten Spielstand**?

**Für Profis:** Wenn ``tempo`` zu klein wird, ist das Spiel unmöglich. Kannst du dafür sorgen, dass ``tempo`` nie unter **80** fällt?
