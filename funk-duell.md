# Funk-Duell: Schere, Stein, Papier

## Willkommen! @showdialog

📡 **Schere, Stein, Papier – per Funk!**

Zwei micro:bits spielen gegeneinander. Ihr schüttelt **gleichzeitig**.
Jeder micro:bit schickt seine Hand per **Funk** an den anderen und rechnet aus, **wer gewonnen hat**!

Ihr braucht für dieses Spiel **zwei micro:bits** – im Simulator erscheint der zweite automatisch.

**Neu in diesem Spiel:** **Funk** und Bedingungen mit **und** / **oder**.

## Die Funkgruppe

Damit sich nur eure zwei micro:bits unterhalten, braucht ihr eine **eigene Funkgruppe** – wie einen eigenen Kanal beim Walkie-Talkie.

- :broadcast tower: Ziehe aus ``||radio:Funk||`` den Block ``||radio:setze Funkgruppe 1||`` in ``||basic:beim Start||``.

```blocks
radio.setGroup(1)
```

~hint Wichtig in der AG! 💡
Jedes Paar braucht eine **andere Zahl** (zum Beispiel Team 1, Team 2, Team 3 …). Sonst funken alle durcheinander!
Beide micro:bits eines Paares brauchen aber **dieselbe** Zahl.
hint~

## Schütteln und senden

Wie beim ersten Schere-Stein-Papier würfelt der micro:bit eine Zahl. Neu ist: Er **schickt** sie per Funk.

**1 = Papier, 2 = Stein, 3 = Schere**

- :circle: Ziehe ``||input:wenn geschüttelt||`` auf die Arbeitsfläche.
- :align justify: Erstelle eine Variable ``hand`` und setze sie auf ``||math:wähle zufällig von 1 bis 3||``.
- :broadcast tower: Ziehe ``||radio:sende Zahl 0 über Funk||`` darunter und setze ``||variables:hand||`` ein.

```blocks
let hand = 0
radio.setGroup(1)
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    radio.sendNumber(hand)
})
```

## Die eigene Hand zeigen

Jetzt zeigt der micro:bit, was er gewählt hat. Diesmal nehmen wir fertige Symbole.

- :random: Ziehe ``||logic:wenn wahr dann sonst||`` unter ``||radio:sende Zahl||`` und klicke auf **+**, damit es ein **sonst wenn** gibt.
- :random: Prüfe ``||variables:hand||`` = **1** und ``||variables:hand||`` = **2**.
- :th: Zeige mit ``||basic:zeige Symbol||``: **Quadrat** für Papier, **kleine Raute** für Stein und die **Schere** im **sonst**-Teil.

```blocks
let hand = 0
radio.setGroup(1)
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    radio.sendNumber(hand)
    if (hand == 1) {
        basic.showIcon(IconNames.Square)
    } else if (hand == 2) {
        basic.showIcon(IconNames.SmallDiamond)
    } else {
        basic.showIcon(IconNames.Scissors)
    }
})
```

## Die Hand des Gegners empfangen

Wenn der andere micro:bit seine Zahl schickt, merken wir sie uns.

- :broadcast tower: Ziehe ``||radio:wenn Zahl empfangen receivedNumber||`` auf die Arbeitsfläche.
- :align justify: Erstelle eine Variable ``gegner``.
- :mouse pointer: Setze ``||variables:gegner||`` auf ``||variables:receivedNumber||`` (die empfangene Zahl – ziehe sie aus dem Block heraus).
- :th: Danach: ``||basic:pausiere (ms)||`` mit **1500**, damit man die eigene Hand noch sieht.

```blocks
let gegner = 0
let hand = 0
radio.setGroup(1)
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    radio.sendNumber(hand)
    if (hand == 1) {
        basic.showIcon(IconNames.Square)
    } else if (hand == 2) {
        basic.showIcon(IconNames.SmallDiamond)
    } else {
        basic.showIcon(IconNames.Scissors)
    }
})
radio.onReceivedNumber(function (receivedNumber) {
    gegner = receivedNumber
    basic.pause(1500)
})
```

## Unentschieden?

Jetzt wird es knifflig: Wer hat gewonnen? Zuerst der einfachste Fall – **beide haben dasselbe**.

- :random: Ziehe ``||logic:wenn wahr dann sonst||`` unter ``||basic:pausiere||`` und klicke auf **+** für ein **sonst wenn**.
- :random: Erste Bedingung: ``||variables:hand||`` = ``||variables:gegner||``.
- :th: Dann zeige das Symbol **Meh** 😐 (unentschieden).

```blocks
let gegner = 0
let hand = 0
radio.setGroup(1)
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    radio.sendNumber(hand)
    if (hand == 1) {
        basic.showIcon(IconNames.Square)
    } else if (hand == 2) {
        basic.showIcon(IconNames.SmallDiamond)
    } else {
        basic.showIcon(IconNames.Scissors)
    }
})
radio.onReceivedNumber(function (receivedNumber) {
    gegner = receivedNumber
    basic.pause(1500)
    if (hand == gegner) {
        basic.showIcon(IconNames.Meh)
    } else if (false) {

    } else {

    }
})
```

## Gewonnen oder verloren?

Du gewinnst in **drei** Fällen:

- **Papier (1)** gegen **Stein (2)**
- **Stein (2)** gegen **Schere (3)**
- **Schere (3)** gegen **Papier (1)**

Dafür brauchst du **und** und **oder** aus ``||logic:Logik||``.

- :random: Baue im **sonst wenn** drei ``||logic:und||``-Blöcke, z. B. ``hand = 1`` **und** ``gegner = 2``.
- :random: Verbinde die drei mit ``||logic:oder||``.
- :th: Gewonnen: Symbol **fröhlich** 😀. Im **sonst**-Teil: Symbol **traurig** 😢.

```blocks
let gegner = 0
let hand = 0
radio.setGroup(1)
input.onGesture(Gesture.Shake, function () {
    hand = randint(1, 3)
    radio.sendNumber(hand)
    if (hand == 1) {
        basic.showIcon(IconNames.Square)
    } else if (hand == 2) {
        basic.showIcon(IconNames.SmallDiamond)
    } else {
        basic.showIcon(IconNames.Scissors)
    }
})
radio.onReceivedNumber(function (receivedNumber) {
    gegner = receivedNumber
    basic.pause(1500)
    if (hand == gegner) {
        basic.showIcon(IconNames.Meh)
    } else if (hand == 1 && gegner == 2 || (hand == 2 && gegner == 3 || hand == 3 && gegner == 1)) {
        basic.showIcon(IconNames.Happy)
    } else {
        basic.showIcon(IconNames.Sad)
    }
})
```

~hint Tipp: Zusammenbauen 🧩
Baue zuerst **einen** ``||logic:und||``-Block fertig. Dann rechtsklick → **Duplizieren** und nur die Zahlen ändern. Das spart viel Zeit!
hint~

## Ausprobieren @showdialog

Im Simulator siehst du jetzt **zwei** micro:bits. Klicke bei **beiden** schnell nacheinander auf **SHAKE**.

Mit echten micro:bits: Ladet das Programm auf beide, stellt **dieselbe Funkgruppe** ein – und schüttelt gleichzeitig! 📡

## Geschafft! @showdialog

🏆 **Super!** Das war das schwierigste Spiel bisher – du hast mit Funk und komplizierten Bedingungen programmiert!

**Für Profis:** Kannst du mit einer Variable ``siege`` zählen, wie oft du gewonnen hast, und sie mit **Knopf A** anzeigen?
