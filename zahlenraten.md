# Zahlenraten

## Willkommen! @showdialog

🔢 **Zahlenraten!**

Der micro:bit denkt sich eine **geheime Zahl von 1 bis 10** aus.
Mit **A** stellst du deinen Tipp ein, mit **B** prüfst du ihn.
Der micro:bit zeigt dir mit einem Pfeil: **höher** ⬆️ oder **niedriger** ⬇️?

**Neu in diesem Spiel:** **eigene Funktionen** – du baust dir deine eigenen Blöcke!

## Geheime Zahl und Tipp

- :align justify: Erstelle die Variablen ``geheim`` und ``tipp``.
- :mouse pointer: Setze in ``||basic:beim Start||`` die Variable ``geheim`` auf ``||math:wähle zufällig von 1 bis 10||``.
- :align justify: Setze ``tipp`` auf **1**.
- :th: Zeige den Tipp mit ``||basic:zeige Zahl||`` an.

```blocks
let geheim = randint(1, 10)
let tipp = 1
basic.showNumber(tipp)
```

## Tipp einstellen mit A

Bei jedem Druck auf **A** wird der Tipp um 1 größer. Nach der 10 geht es wieder bei 1 los.

- :circle: Ziehe ``||input:wenn Knopf A gedrückt||`` auf die Arbeitsfläche.
- :align justify: Hinein: ``||variables:ändere tipp um 1||``.
- :random: Darunter: ``||logic:wenn wahr dann||`` mit der Bedingung ``||variables:tipp||`` **>** **10**.
- :align justify: Hinein: ``||variables:setze tipp auf 1||``.
- :th: Ganz unten: ``||basic:zeige Zahl||`` mit ``||variables:tipp||``.

```blocks
let geheim = randint(1, 10)
let tipp = 1
basic.showNumber(tipp)
input.onButtonPressed(Button.A, function () {
    tipp += 1
    if (tipp > 10) {
        tipp = 1
    }
    basic.showNumber(tipp)
})
```

## Deine erste Funktion

Jetzt bauen wir einen **eigenen Block** mit dem Namen ``pruefen``. Eine **Funktion** ist wie ein Rezept: Du schreibst es einmal auf und kannst es dann immer wieder benutzen.

- :code: Öffne ``||functions:Funktionen||`` und klicke auf **Erstelle eine Funktion...**
- :keyboard: Nenne sie ``pruefen`` und klicke auf **Fertig**.
- :random: In die Funktion: ``||logic:wenn wahr dann sonst||`` mit ``||variables:tipp||`` **=** ``||variables:geheim||``.
- :th: Im **wenn**-Teil: ``||basic:zeige Symbol||`` **fröhlich**.
- :th: Im **sonst**-Teil: ``||basic:zeige Symbol||`` **X**, dann ``||basic:pausiere (ms)||`` **1000** und ``||basic:zeige Zahl||`` mit ``||variables:tipp||``.
- :circle: Ziehe ``||input:wenn Knopf B gedrückt||`` auf die Arbeitsfläche und setze ``||functions:Aufruf pruefen||`` hinein.

```blocks
function pruefen () {
    if (tipp == geheim) {
        basic.showIcon(IconNames.Happy)
    } else {
        basic.showIcon(IconNames.No)
        basic.pause(1000)
        basic.showNumber(tipp)
    }
}
input.onButtonPressed(Button.A, function () {
    tipp += 1
    if (tipp > 10) {
        tipp = 1
    }
    basic.showNumber(tipp)
})
input.onButtonPressed(Button.B, function () {
    pruefen()
})
let tipp = 0
let geheim = 0
geheim = randint(1, 10)
tipp = 1
basic.showNumber(tipp)
```

## Höher oder niedriger?

Ein **X** hilft nicht viel. Besser: Der micro:bit zeigt, in welche Richtung du raten musst.

- :random: Ersetze das **X** durch einen neuen ``||logic:wenn wahr dann sonst||``-Block.
- :random: Bedingung: ``||variables:tipp||`` **<** ``||variables:geheim||``.
- :th: Dann ``||basic:zeige Pfeil||`` **Norden** ⬆️ (die Zahl ist höher).
- :th: Sonst ``||basic:zeige Pfeil||`` **Süden** ⬇️ (die Zahl ist niedriger).

```blocks
function pruefen () {
    if (tipp == geheim) {
        basic.showIcon(IconNames.Happy)
    } else {
        if (tipp < geheim) {
            basic.showArrow(ArrowNames.North)
        } else {
            basic.showArrow(ArrowNames.South)
        }
        basic.pause(1000)
        basic.showNumber(tipp)
    }
}
input.onButtonPressed(Button.A, function () {
    tipp += 1
    if (tipp > 10) {
        tipp = 1
    }
    basic.showNumber(tipp)
})
input.onButtonPressed(Button.B, function () {
    pruefen()
})
let tipp = 0
let geheim = 0
geheim = randint(1, 10)
tipp = 1
basic.showNumber(tipp)
```

## Noch eine Funktion: neues Spiel

Nach einem Treffer soll automatisch ein **neues Spiel** beginnen. Dafür bauen wir eine zweite Funktion.

- :code: Erstelle eine Funktion ``neuesSpiel``.
- :mouse pointer: Verschiebe die drei Blöcke aus ``||basic:beim Start||`` in die neue Funktion.
- :code: Setze ``||functions:Aufruf neuesSpiel||`` in ``||basic:beim Start||``.
- :code: In ``pruefen``, unter das fröhliche Gesicht: ``||basic:pausiere (ms)||`` **1000** und ``||functions:Aufruf neuesSpiel||``.

```blocks
function neuesSpiel () {
    geheim = randint(1, 10)
    tipp = 1
    basic.showNumber(tipp)
}
function pruefen () {
    if (tipp == geheim) {
        basic.showIcon(IconNames.Happy)
        basic.pause(1000)
        neuesSpiel()
    } else {
        if (tipp < geheim) {
            basic.showArrow(ArrowNames.North)
        } else {
            basic.showArrow(ArrowNames.South)
        }
        basic.pause(1000)
        basic.showNumber(tipp)
    }
}
input.onButtonPressed(Button.A, function () {
    tipp += 1
    if (tipp > 10) {
        tipp = 1
    }
    basic.showNumber(tipp)
})
input.onButtonPressed(Button.B, function () {
    pruefen()
})
let tipp = 0
let geheim = 0
neuesSpiel()
```

~hint Warum Funktionen? 💡
Jetzt steht „neues Spiel“ nur **einmal** im Programm, wird aber an **zwei** Stellen benutzt. Willst du etwas ändern (z. B. Zahlen bis 20), musst du es nur an **einer** Stelle tun!
hint~

## Versuche zählen

Wie viele Versuche hast du gebraucht?

- :align justify: Erstelle eine Variable ``versuche``.
- :align justify: In ``neuesSpiel``: ``||variables:setze versuche auf 0||``.
- :align justify: Ganz oben in ``pruefen``: ``||variables:ändere versuche um 1||``.
- :th: Nach dem fröhlichen Gesicht und der Pause: ``||basic:zeige Zahl||`` mit ``||variables:versuche||`` und noch einmal ``||basic:pausiere (ms)||`` **1000**.

```blocks
function neuesSpiel () {
    geheim = randint(1, 10)
    tipp = 1
    versuche = 0
    basic.showNumber(tipp)
}
function pruefen () {
    versuche += 1
    if (tipp == geheim) {
        basic.showIcon(IconNames.Happy)
        basic.pause(1000)
        basic.showNumber(versuche)
        basic.pause(1000)
        neuesSpiel()
    } else {
        if (tipp < geheim) {
            basic.showArrow(ArrowNames.North)
        } else {
            basic.showArrow(ArrowNames.South)
        }
        basic.pause(1000)
        basic.showNumber(tipp)
    }
}
input.onButtonPressed(Button.A, function () {
    tipp += 1
    if (tipp > 10) {
        tipp = 1
    }
    basic.showNumber(tipp)
})
input.onButtonPressed(Button.B, function () {
    pruefen()
})
let versuche = 0
let tipp = 0
let geheim = 0
neuesSpiel()
```

## Geschafft! @showdialog

🎉 Du hast deine **eigenen Blöcke** programmiert!

Spielt gegeneinander: Wer braucht die **wenigsten Versuche**?

**Für Profis:** Mache das Spiel schwerer – Zahlen von **1 bis 50**. Wo musst du dafür überall etwas ändern?
