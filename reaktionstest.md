# Reaktionstest

## Willkommen! @showdialog

⚡ **Wie schnell bist du?**

Drücke **A** zum Starten. Irgendwann erscheint ein Herz.
Drücke dann **so schnell wie möglich B**!
Der micro:bit zeigt dir, wie viele **Millisekunden** du gebraucht hast.

**Neu in diesem Spiel:** Zeit messen und mit Variablen **rechnen**.

## Starten mit Knopf A

- :circle: Ziehe aus ``||input:Eingabe||`` den Block ``||input:wenn Knopf A gedrückt||`` auf die Arbeitsfläche.
- :th: Ziehe aus ``||basic:Grundlagen||`` den Block ``||basic:Bildschirminhalt löschen||`` hinein.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
})
```

## Zufällig warten

Damit niemand schummeln kann, wartet der micro:bit eine **zufällige Zeit**.

- :th: Ziehe ``||basic:pausiere (ms)||`` unter ``||basic:Bildschirminhalt löschen||``.
- :calculator: Setze ``||math:wähle zufällig von 0 bis 10||`` ein und stelle **1000** bis **5000** ein.
- :th: Ziehe ``||basic:zeige Symbol||`` darunter und wähle das **Herz**.

```blocks
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.pause(randint(1000, 5000))
    basic.showIcon(IconNames.Heart)
})
```

~hint Warum zufällig? 💡
1000 bis 5000 Millisekunden sind **1 bis 5 Sekunden**. Weil es jedes Mal anders ist, kannst du nicht einfach mitzählen.
hint~

## Die Stoppuhr starten

Der micro:bit hat eine eingebaute Uhr: die **Laufzeit**. Sie zählt die Millisekunden, seit er eingeschaltet wurde.
Wir merken uns die Laufzeit genau dann, wenn das Herz erscheint.

- :align justify: Erstelle eine Variable ``start``.
- :mouse pointer: Ziehe ``||variables:setze start auf||`` unter ``||basic:zeige Symbol||``.
- :circle: Setze aus ``||input:Eingabe||`` den Block ``||input:Laufzeit (ms)||`` ein.

```blocks
let start = 0
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.pause(randint(1000, 5000))
    basic.showIcon(IconNames.Heart)
    start = input.runningTime()
})
```

## Die Zeit ausrechnen

Wenn du **B** drückst, rechnet der micro:bit: **jetzt – start**. Das ist deine Reaktionszeit!

- :circle: Ziehe ``||input:wenn Knopf B gedrückt||`` auf die Arbeitsfläche.
- :align justify: Erstelle eine Variable ``reaktion`` und ziehe ``||variables:setze reaktion auf||`` hinein.
- :calculator: Setze aus ``||math:Mathematik||`` den Minus-Block ``||math:0 - 0||`` ein.
- :circle: Links kommt ``||input:Laufzeit (ms)||``, rechts ``||variables:start||``.
- :th: Zeige das Ergebnis mit ``||basic:zeige Zahl||`` an.

```blocks
let reaktion = 0
let start = 0
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.pause(randint(1000, 5000))
    basic.showIcon(IconNames.Heart)
    start = input.runningTime()
})
input.onButtonPressed(Button.B, function () {
    reaktion = input.runningTime() - start
    basic.showNumber(reaktion)
})
```

## Ausprobieren @showdialog

Teste es im Simulator: Drücke **A**, warte auf das Herz und drücke dann schnell **B**.

Was ist deine Zeit? Schaffst du **unter 300**? 🏆

Aber Achtung: Was passiert, wenn du **B** drückst, **bevor** das Herz da ist? 🤔

## Schummeln verhindern

Wer zu früh drückt, schummelt! Wir merken uns deshalb, ob das Herz schon da ist.
Ist ``start`` noch **0**, war das Herz noch nicht da.

- :random: Ziehe ``||logic:wenn wahr dann sonst||`` in ``||input:wenn Knopf B gedrückt||``.
- :random: Prüfe mit ``||logic:0 > 0||``, ob ``||variables:start||`` größer als **0** ist.
- :mouse pointer: Verschiebe die beiden Blöcke von vorher in den **wenn**-Teil.
- :th: In den **sonst**-Teil kommt ``||basic:zeige Symbol||`` mit dem **X** (Nein).
- :align justify: Ganz unten: ``||variables:setze start auf 0||`` – dann ist die Runde vorbei.

```blocks
let reaktion = 0
let start = 0
input.onButtonPressed(Button.A, function () {
    basic.clearScreen()
    basic.pause(randint(1000, 5000))
    basic.showIcon(IconNames.Heart)
    start = input.runningTime()
})
input.onButtonPressed(Button.B, function () {
    if (start > 0) {
        reaktion = input.runningTime() - start
        basic.showNumber(reaktion)
    } else {
        basic.showIcon(IconNames.No)
    }
    start = 0
})
```

## Geschafft! @showdialog

🎉 Dein Reaktionstest ist fertig – und schummelsicher!

**Für Profis:** Kannst du dir mit einer Variable ``rekord`` die **beste Zeit** merken?
