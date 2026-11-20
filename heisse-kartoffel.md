# Heiße Kartoffel

## Willkommen! @showdialog

🥔 **Heiße Kartoffel** – das Spiel für die ganze Gruppe!

Der micro:bit ist die Kartoffel. Ihr gebt ihn im Kreis weiter.
Irgendwann „explodiert“ er – aber niemand weiß, wann!
Wer ihn dann in der Hand hält, hat verloren. 💀

**Neu in diesem Spiel:** die **Schleife** und die **Pause**.

## Start mit Knopf A

Das Spiel soll starten, wenn man **Knopf A** drückt.

- :circle: Ziehe aus ``||input:Eingabe||`` den Block ``||input:wenn Knopf A gedrückt||`` auf die Arbeitsfläche.

```blocks
input.onButtonPressed(Button.A, function () {
})
```

## Die Kartoffel zeigen

Jetzt soll eine Kartoffel auf dem Bildschirm erscheinen.

- :th: Ziehe aus ``||basic:Grundlagen||`` den Block ``||basic:zeige LEDs||`` in ``||input:wenn Knopf A gedrückt||``.
- :mouse pointer: Male eine Kartoffel – oder etwas anderes, das „heiß“ aussieht!

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . # # # .
        # # # # #
        # # # # #
        # # # # #
        . # # # .
        `)
})
```

## Eine geheime Zeit

Der micro:bit soll sich eine **geheime Zeit** ausdenken, wann die Kartoffel explodiert.

- :align justify: Erstelle in ``||variables:Variablen||`` eine Variable mit dem Namen ``zeit``.
- :mouse pointer: Ziehe ``||variables:setze zeit auf||`` unter den Block ``||basic:zeige LEDs||``.
- :calculator: Setze aus ``||math:Mathematik||`` den Block ``||math:wähle zufällig von 0 bis 10||`` ein und ändere die Zahlen auf **5** und **15**.

```blocks
let zeit = 0
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . # # # .
        # # # # #
        # # # # #
        # # # # #
        . # # # .
        `)
    zeit = randint(5, 15)
})
```

**Was bedeutet das? 💡**
Die Kartoffel explodiert nach **5 bis 15 Sekunden**. Das ist jedes Mal anders – niemand kann es wissen!

## Die Schleife

Jetzt kommt das Neue: eine **Schleife**. Sie wiederholt etwas immer wieder, **solange** etwas stimmt.

Solange die Zeit noch größer als 0 ist, soll der micro:bit 1 Sekunde warten und die Zeit um 1 kleiner machen.

- :refresh: Ziehe aus ``||loops:Schleifen||`` den Block ``||loops:während wahr||`` unter ``||variables:setze zeit auf||``.
- :random: Ersetze **wahr** durch den Vergleich ``||logic:0 > 0||`` aus ``||logic:Logik||``. Setze links ``||variables:zeit||`` ein.
- :align justify: Ziehe ``||variables:ändere zeit um 1||`` in die Schleife und mache aus der **1** eine **-1**.
- :th: Ziehe ``||basic:pausiere (ms) 100||`` darunter und stelle **1000** ein. (1000 ms = 1 Sekunde)

```blocks
let zeit = 0
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . # # # .
        # # # # #
        # # # # #
        # # # # #
        . # # # .
        `)
    zeit = randint(5, 15)
    while (zeit > 0) {
        zeit += -1
        basic.pause(1000)
    }
})
```

## BOOM!

Wenn die Schleife fertig ist, ist die Zeit abgelaufen. Jetzt explodiert die Kartoffel!

- :th: Ziehe aus ``||basic:Grundlagen||`` den Block ``||basic:zeige Symbol||`` **unter** die Schleife (nicht hinein!).
- :mouse pointer: Wähle den **Totenkopf** aus.

```blocks
let zeit = 0
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . # # # .
        # # # # #
        # # # # #
        # # # # #
        . # # # .
        `)
    zeit = randint(5, 15)
    while (zeit > 0) {
        zeit += -1
        basic.pause(1000)
    }
    basic.showIcon(IconNames.Skull)
})
```

## Ausprobieren @showdialog

Drücke im Simulator auf **A** und warte… 💀

Dann lade das Spiel auf deinen micro:bit und spielt es zusammen im Kreis!

**Für Profis:** Kannst du die Kartoffel kurz vor der Explosion **blinken** lassen?
