# Schere, Stein, Papier

## Willkommen! @showdialog

Heute baust du aus deinem micro:bit ein **Schere-Stein-Papier-Spiel**! ✂️🪨📄

Wenn du den micro:bit schüttelst, zeigt er zufällig **Schere**, **Stein** oder **Papier** an.
Spiele dann gegen deine Nachbarin oder deinen Nachbarn!

## Schütteln erkennen

Zuerst muss der micro:bit merken, wenn er **geschüttelt** wird.

- :circle: Öffne die Kategorie ``||input:Eingabe||``.
- :mouse pointer: Ziehe den Block ``||input:wenn geschüttelt||`` auf die Arbeitsfläche.

```blocks
input.onGesture(Gesture.Shake, function () {
})
```

## Eine Variable für die Hand

Der micro:bit braucht einen „Zettel“, auf dem er sich merkt, was er zeigt. So einen Zettel nennt man **Variable**.

- :align justify: Öffne ``||variables:Variablen||`` und klicke auf **Erstelle eine Variable...**
- :keyboard: Nenne die Variable ``hand`` und klicke auf **OK**.
- :mouse pointer: Ziehe ``||variables:setze hand auf||`` in den Block ``||input:wenn geschüttelt||``.

```blocks
let hand = 0
input.onGesture(Gesture.Shake, function () {
    hand = 0
})
```

## Eine Zufallszahl würfeln

Jetzt soll der micro:bit **zufällig** eine Zahl von 1 bis 3 auswählen – wie ein Würfel mit nur drei Seiten.

- :calculator: Öffne ``||math:Mathematik||``.
- :mouse pointer: Ziehe ``||math:wähle zufällig von 0 bis 10||`` in das Feld mit der **0** im Block ``||variables:setze hand auf||``.
- :keyboard: Ändere die Zahlen auf **1** und **3**.

```blocks
let hand = 0
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
})
```

~hint Warum 1 bis 3? 💡
Es gibt drei Möglichkeiten: Schere, Stein und Papier. Jede bekommt eine Zahl:
**1 = Papier**, **2 = Stein**, **3 = Schere**.
hint~

## Wenn die Zahl 1 ist: Papier

Jetzt prüfen wir, welche Zahl gewürfelt wurde. Ist es eine **1**, zeigen wir **Papier**.

- :random: Ziehe aus ``||logic:Logik||`` den Block ``||logic:wenn wahr dann||`` unter ``||variables:setze hand auf||``.
- :random: Ziehe aus ``||logic:Logik||`` den Vergleich ``||logic:0 = 0||`` in das Feld **wahr**.
- :align justify: Ziehe ``||variables:hand||`` in das **linke** Feld und tippe rechts eine **1** ein.
- :th: Ziehe aus ``||basic:Grundlagen||`` den Block ``||basic:zeige LEDs||`` in den ``||logic:wenn||``-Block und male ein Blatt Papier.

```blocks
let hand = 0
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showLeds(`
            # # # # #
            # . . . #
            # . . . #
            # . . . #
            # # # # #
            `)
    }
})
```

## Wenn die Zahl 2 ist: Stein

Ist die Zahl eine **2**, soll ein **Stein** erscheinen.

- :plus: Klicke **zweimal** auf das kleine **+** unten am ``||logic:wenn||``-Block. Jetzt gibt es ein **sonst wenn** und ein **sonst**.
- :random: Ziehe wieder ``||logic:0 = 0||`` in das Feld bei **sonst wenn**.
- :align justify: Setze ``||variables:hand||`` links ein und tippe rechts eine **2**.
- :th: Ziehe ``||basic:zeige LEDs||`` unter **sonst wenn** und male einen Stein.

```blocks
let hand = 0
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showLeds(`
            # # # # #
            # . . . #
            # . . . #
            # . . . #
            # # # # #
            `)
    } else if (hand == 2) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    } else {

    }
})
```

## Sonst: Schere

Wenn es weder 1 noch 2 ist, bleibt nur noch die **3** übrig – das ist die **Schere**!

- :th: Ziehe ``||basic:zeige LEDs||`` in den Teil **sonst** und male eine Schere.

```blocks
let hand = 0
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    if (hand == 1) {
        basic.showLeds(`
            # # # # #
            # . . . #
            # . . . #
            # . . . #
            # # # # #
            `)
    } else if (hand == 2) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    } else {
        basic.showLeds(`
            # # . . #
            # # . # .
            . . # . .
            # # . # .
            # # . . #
            `)
    }
})
```

~hint Eigene Bilder 🎨
Du musst die Bilder nicht genau so malen. Denk dir deine eigene Schere, deinen eigenen Stein und dein eigenes Papier aus!
hint~

## Ausprobieren im Simulator @showdialog

Teste dein Spiel im **Simulator** links! 🎮

Klicke auf den Knopf **SHAKE** (Schütteln) über dem micro:bit.
Erscheint jedes Mal Schere, Stein oder Papier? Super!

## Auf den micro:bit laden @showdialog

Schließe deinen micro:bit mit dem USB-Kabel an den Computer an und klicke auf **Herunterladen**. 💾

Jetzt kannst du den micro:bit in die Hand nehmen, schütteln und gegen andere spielen!

## Bonus: Punkte zählen

Wer hat gewonnen? Der micro:bit soll deine **Punkte** zählen.

- :align justify: Erstelle in ``||variables:Variablen||`` eine neue Variable mit dem Namen ``punkte``.
- :circle: Ziehe aus ``||input:Eingabe||`` den Block ``||input:wenn Knopf A gedrückt||`` auf die Arbeitsfläche.
- :align justify: Ziehe ``||variables:ändere punkte um 1||`` hinein.
- :th: Ziehe aus ``||basic:Grundlagen||`` den Block ``||basic:zeige Zahl||`` darunter und setze ``||variables:punkte||`` ein.

```blocks
let punkte = 0
input.onButtonPressed(Button.A, function () {
    punkte += 1
    basic.showNumber(punkte)
})
```

~hint So wird gespielt 🏆
Hast du eine Runde gewonnen? Dann drücke **Knopf A**. Der micro:bit zählt einen Punkt dazu und zeigt deinen Punktestand an.
hint~

## Geschafft! @showdialog

🎉 **Super gemacht!** Dein Schere-Stein-Papier-Spiel ist fertig.

Für Profis: Kannst du mit **Knopf B** die Punkte wieder auf **0** setzen?
