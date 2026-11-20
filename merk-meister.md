# Merk-Meister

## Willkommen! @showdialog

🧠 **Merk-Meister!**

Der micro:bit zeigt dir eine Reihe von Pfeilen: ⬅️ ➡️ ➡️ ⬅️ …
Drücke danach die Knöpfe in **genau derselben Reihenfolge**: **A** für links, **B** für rechts.
Jede Runde kommt ein Pfeil dazu. Wie lange kannst du dir die Reihe merken?

**Neu in diesem Spiel:** **Listen** und **Funktionen mit Parametern**.

## Eine Liste

Eine **Liste** ist eine Variable, in die **viele Werte** hineinpassen – wie eine Einkaufsliste.
In unserer Liste ``folge`` steht: **0 = links**, **1 = rechts**.

- :align justify: Erstelle eine Variable ``folge``.
- :list: Ziehe aus ``||arrays:Arrays||`` den Block ``||arrays:setze folge auf leeres Array||`` in ``||basic:beim Start||``.

```blocks
let folge: number[] = []
```

## Eine neue Runde

Jede Runde hängt der micro:bit einen zufälligen Pfeil **ans Ende der Liste**.

- :code: Erstelle eine Funktion ``neueRunde``.
- :list: Ziehe ``||arrays:füge Wert am Ende von folge hinzu||`` hinein.
- :calculator: Als Wert: ``||math:wähle zufällig von 0 bis 1||``.
- :circle: Ziehe ``||input:wenn geschüttelt||`` auf die Arbeitsfläche. Hinein: ``||arrays:setze folge auf leeres Array||`` und ``||functions:Aufruf neueRunde||``.

```blocks
function neueRunde () {
    folge.push(randint(0, 1))
}
input.onGesture(Gesture.Shake, function () {
    folge = []
    neueRunde()
})
let folge: number[] = []
```

**Warum schütteln? 💡**
Schütteln **startet** das Spiel: Die Liste wird geleert und die erste Runde beginnt.

## Die Pfeile zeigen

Jetzt soll der micro:bit **jeden Wert** der Liste nacheinander als Pfeil zeigen. Dafür gibt es eine besondere Schleife.

- :refresh: Ziehe ``||loops:für jedes Element wert von folge||`` unter ``||arrays:füge Wert am Ende hinzu||``.
- :random: Hinein: ``||logic:wenn wahr dann sonst||`` mit ``||variables:wert||`` **=** **0**.
- :th: Dann ``||basic:zeige Pfeil||`` **Westen** ⬅️, sonst ``||basic:zeige Pfeil||`` **Osten** ➡️.
- :th: Unter den ``||logic:wenn||``-Block: ``||basic:pausiere (ms)||`` **400**, ``||basic:Bildschirminhalt löschen||`` und ``||basic:pausiere (ms)||`` **200**.

```blocks
function neueRunde () {
    folge.push(randint(0, 1))
    for (let wert of folge) {
        if (wert == 0) {
            basic.showArrow(ArrowNames.West)
        } else {
            basic.showArrow(ArrowNames.East)
        }
        basic.pause(400)
        basic.clearScreen()
        basic.pause(200)
    }
}
input.onGesture(Gesture.Shake, function () {
    folge = []
    neueRunde()
})
let folge: number[] = []
```

**Warum die kurze Pause mit leerem Bildschirm? 💡**
Kommen zwei gleiche Pfeile hintereinander, sieht man sonst nicht, dass es **zwei** waren!

## Eine Funktion mit Parameter

Wenn du einen Knopf drückst, prüft der micro:bit: Ist das der **richtige** Pfeil an dieser **Stelle** der Liste?
Die Variable ``position`` merkt sich, beim wievielten Pfeil du gerade bist.

Wir bauen dafür **eine** Funktion ``pruefe`` mit einem **Parameter** ``taste``. Ein Parameter ist ein Wert, den man der Funktion mitgibt.

- :align justify: Erstelle eine Variable ``position`` und setze sie am Ende von ``neueRunde`` auf **0**.
- :code: Erstelle eine Funktion ``pruefe``. Klicke dabei auf **Zahl**, um einen Parameter hinzuzufügen, und nenne ihn ``taste``.
- :random: In ``pruefe``: ``||logic:wenn wahr dann sonst||`` mit ``||variables:taste||`` **=** ``||arrays:folge Wert an 0||``. Statt der 0 kommt ``||variables:position||``.
- :align justify: Dann: ``||variables:ändere position um 1||``. Sonst: ``||game:Game Over||``.
- :circle: ``||input:wenn Knopf A gedrückt||`` → ``||functions:Aufruf pruefe 0||``, ``||input:wenn Knopf B gedrückt||`` → ``||functions:Aufruf pruefe 1||``.

```blocks
function pruefe (taste: number) {
    if (taste == folge[position]) {
        position += 1
    } else {
        game.gameOver()
    }
}
function neueRunde () {
    folge.push(randint(0, 1))
    for (let wert of folge) {
        if (wert == 0) {
            basic.showArrow(ArrowNames.West)
        } else {
            basic.showArrow(ArrowNames.East)
        }
        basic.pause(400)
        basic.clearScreen()
        basic.pause(200)
    }
    position = 0
}
input.onButtonPressed(Button.A, function () {
    pruefe(0)
})
input.onGesture(Gesture.Shake, function () {
    folge = []
    neueRunde()
})
input.onButtonPressed(Button.B, function () {
    pruefe(1)
})
let position = 0
let folge: number[] = []
```

**Wie zählt eine Liste? 💡**
Computer fangen bei **0** an zu zählen! Der **erste** Pfeil steht an Stelle **0**, der zweite an Stelle **1** und so weiter.

## Runde geschafft!

Wenn ``position`` so groß ist wie die **Länge der Liste**, hast du alle Pfeile richtig gedrückt. Dann kommt die nächste Runde!

- :random: Ziehe in ``pruefe`` unter ``||variables:ändere position um 1||`` einen ``||logic:wenn wahr dann||``-Block.
- :random: Bedingung: ``||variables:position||`` **=** ``||arrays:Länge des Arrays folge||``.
- :th: Hinein: ``||basic:zeige Symbol||`` **Häkchen**, ``||basic:pausiere (ms)||`` **500** und ``||functions:Aufruf neueRunde||``.

```blocks
function pruefe (taste: number) {
    if (taste == folge[position]) {
        position += 1
        if (position == folge.length) {
            basic.showIcon(IconNames.Yes)
            basic.pause(500)
            neueRunde()
        }
    } else {
        game.gameOver()
    }
}
function neueRunde () {
    folge.push(randint(0, 1))
    for (let wert of folge) {
        if (wert == 0) {
            basic.showArrow(ArrowNames.West)
        } else {
            basic.showArrow(ArrowNames.East)
        }
        basic.pause(400)
        basic.clearScreen()
        basic.pause(200)
    }
    position = 0
}
input.onButtonPressed(Button.A, function () {
    pruefe(0)
})
input.onGesture(Gesture.Shake, function () {
    folge = []
    neueRunde()
})
input.onButtonPressed(Button.B, function () {
    pruefe(1)
})
let position = 0
let folge: number[] = []
```

## Punkte zählen

Bei **Game Over** soll der micro:bit zeigen, wie viele Runden du geschafft hast. Das ist die Länge der Liste **minus 1** (die letzte Runde hast du ja nicht geschafft).

- :gamepad: Ziehe ``||game:setze Spielstand auf||`` über ``||game:Game Over||``.
- :calculator: Setze ``||math:0 - 0||`` ein: links ``||arrays:Länge des Arrays folge||``, rechts **1**.

```blocks
function pruefe (taste: number) {
    if (taste == folge[position]) {
        position += 1
        if (position == folge.length) {
            basic.showIcon(IconNames.Yes)
            basic.pause(500)
            neueRunde()
        }
    } else {
        game.setScore(folge.length - 1)
        game.gameOver()
    }
}
function neueRunde () {
    folge.push(randint(0, 1))
    for (let wert of folge) {
        if (wert == 0) {
            basic.showArrow(ArrowNames.West)
        } else {
            basic.showArrow(ArrowNames.East)
        }
        basic.pause(400)
        basic.clearScreen()
        basic.pause(200)
    }
    position = 0
}
input.onButtonPressed(Button.A, function () {
    pruefe(0)
})
input.onGesture(Gesture.Shake, function () {
    folge = []
    neueRunde()
})
input.onButtonPressed(Button.B, function () {
    pruefe(1)
})
let position = 0
let folge: number[] = []
```

## Ausprobieren @showdialog

Klicke im Simulator auf **SHAKE**, schau dir die Pfeile genau an und drücke dann **A** und **B** in der richtigen Reihenfolge.

Wer in der AG schafft die **längste Reihe**? 🏆

## Geschafft! @showdialog

🎉 Du kannst jetzt mit **Listen** und **Funktionen mit Parametern** programmieren – das machen auch echte Programmierer jeden Tag!

**Für Profis:** Mache das Spiel mit jeder Runde **schneller**, indem die Pause beim Zeigen der Pfeile kürzer wird.
