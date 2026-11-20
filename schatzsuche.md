# Funk-Schatzsuche

## Willkommen! @showdialog

💎 **Funk-Schatzsuche!**

Ein micro:bit wird zum **Schatz** und wird irgendwo im Raum versteckt. Er sendet die ganze Zeit ein Funksignal.
Alle anderen sind **Schatzsucher**: Ihr micro:bit zeigt, wie **stark** das Signal ist – je näher, desto mehr Lichter leuchten!

**Neu in diesem Spiel:** **Signalstärke** messen, ein **Balkendiagramm** und ein Programm mit **zwei Rollen**.

## Funkgruppe und Rolle

Alle bekommen **dasselbe** Programm. Erst ist jeder micro:bit ein **Sucher**. Die Variable ``istSchatz`` merkt sich, ob er zum Schatz geworden ist.

- :broadcast tower: Ziehe ``||radio:setze Funkgruppe 1||`` in ``||basic:beim Start||``.
- :align justify: Erstelle eine Variable ``istSchatz``.
- :random: Setze sie mit ``||variables:setze istSchatz auf||`` auf ``||logic:falsch||`` (aus ``||logic:Logik||``).

```blocks
radio.setGroup(1)
let istSchatz = false
```

~hint Wahr oder falsch? 💡
Eine Variable kann nicht nur Zahlen oder Texte speichern, sondern auch **wahr** oder **falsch** – wie ein Lichtschalter: an oder aus.
hint~

## Zum Schatz werden

Wer **A und B gleichzeitig** drückt, macht seinen micro:bit zum Schatz.

- :circle: Ziehe ``||input:wenn Knopf A gedrückt||`` auf die Arbeitsfläche und stelle **A+B** ein.
- :align justify: Hinein: ``||variables:setze istSchatz auf||`` ``||logic:wahr||``.
- :broadcast tower: Darunter: ``||radio:setze Sendeleistung||`` auf **1**. (Damit reicht das Signal nicht so weit – das macht die Suche spannender!)
- :th: Zum Schluss: ``||basic:zeige Symbol||`` **Diamant** 💎.

```blocks
input.onButtonPressed(Button.AB, function () {
    istSchatz = true
    radio.setTransmitPower(1)
    basic.showIcon(IconNames.Diamond)
})
let istSchatz = false
radio.setGroup(1)
istSchatz = false
```

## Der Schatz sendet

Der Schatz soll **ständig** ein Signal senden – fünfmal pro Sekunde.

- :th: Ziehe ``||basic:dauerhaft||`` auf die Arbeitsfläche.
- :random: Hinein: ``||logic:wenn wahr dann||`` mit ``||variables:istSchatz||`` als Bedingung.
- :broadcast tower: Hinein: ``||radio:sende Zahl 0 über Funk||``.
- :th: Unter den ``||logic:wenn||``-Block: ``||basic:pausiere (ms)||`` **200**.

```blocks
input.onButtonPressed(Button.AB, function () {
    istSchatz = true
    radio.setTransmitPower(1)
    basic.showIcon(IconNames.Diamond)
})
let istSchatz = false
radio.setGroup(1)
istSchatz = false
basic.forever(function () {
    if (istSchatz) {
        radio.sendNumber(0)
    }
    basic.pause(200)
})
```

## Das Signal messen

Jetzt kommen die Sucher dran. Wenn ihr micro:bit das Signal empfängt, misst er, **wie stark** es ist.

- :broadcast tower: Ziehe ``||radio:wenn Zahl empfangen receivedNumber||`` auf die Arbeitsfläche.
- :align justify: Erstelle eine Variable ``staerke`` und setze sie auf ``||radio:empfangenes Paket Signalstärke||``.
- :lightbulb: Darunter: ``||led:zeichne Balkendiagramm von||``.
- :calculator: Bei **von** kommt ``||math:0 + 0||`` mit ``||variables:staerke||`` und **100**. Bei **bis** kommt **60**.

```blocks
input.onButtonPressed(Button.AB, function () {
    istSchatz = true
    radio.setTransmitPower(1)
    basic.showIcon(IconNames.Diamond)
})
radio.onReceivedNumber(function (receivedNumber) {
    staerke = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    led.plotBarGraph(staerke + 100, 60)
})
let staerke = 0
let istSchatz = false
radio.setGroup(1)
istSchatz = false
basic.forever(function () {
    if (istSchatz) {
        radio.sendNumber(0)
    }
    basic.pause(200)
})
```

~hint Warum plus 100? 💡
Die Signalstärke ist eine **negative** Zahl: etwa **-95**, wenn der Schatz weit weg ist, und etwa **-42**, wenn er direkt daneben liegt.
Mit **+ 100** wird daraus eine Zahl zwischen **5** und **58** – genau richtig für das Balkendiagramm bis **60**.
hint~

## Gefunden!

Wenn das Signal **sehr stark** ist, steht der Sucher direkt neben dem Schatz. Dann gibt es ein fröhliches Gesicht!

- :random: Ziehe ``||logic:wenn wahr dann sonst||`` unter ``||variables:setze staerke auf||``.
- :random: Bedingung: ``||variables:staerke||`` **>** **-50**.
- :th: Dann: ``||basic:zeige Symbol||`` **fröhlich** 😀.
- :mouse pointer: Verschiebe ``||led:zeichne Balkendiagramm||`` in den **sonst**-Teil.

```blocks
input.onButtonPressed(Button.AB, function () {
    istSchatz = true
    radio.setTransmitPower(1)
    basic.showIcon(IconNames.Diamond)
})
radio.onReceivedNumber(function (receivedNumber) {
    staerke = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    if (staerke > -50) {
        basic.showIcon(IconNames.Happy)
    } else {
        led.plotBarGraph(staerke + 100, 60)
    }
})
let staerke = 0
let istSchatz = false
radio.setGroup(1)
istSchatz = false
basic.forever(function () {
    if (istSchatz) {
        radio.sendNumber(0)
    }
    basic.pause(200)
})
```

## So wird gespielt @showdialog

1. Ladet das Programm auf **alle** micro:bits eurer Gruppe.
2. Einer drückt **A+B** – das ist jetzt der Schatz 💎. Er wird versteckt, während die anderen rausgehen oder die Augen zumachen.
3. Die Sucher laufen herum und beobachten die Lichter. **Mehr Lichter = näher dran!**
4. Wer zuerst das fröhliche Gesicht sieht, hat den Schatz gefunden! 🏆

**Tipp:** Wände, Schränke und sogar Menschen schwächen das Signal. Das macht die Suche knifflig!

## Geschafft! @showdialog

🎉 Du hast ein echtes **Ortungsgerät** gebaut – so ähnlich funktioniert auch die Suche nach verlorenen Kopfhörern mit dem Handy!

**Für Profis:** Lass den Sucher **piepen** – und zwar umso **schneller**, je näher er am Schatz ist.
