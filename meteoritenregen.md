# Meteoritenregen

## Willkommen! @showdialog

☄️ **Meteoritenregen!**

Von oben fallen Meteoriten herunter. Du steuerst dein Raumschiff mit **A** (links) und **B** (rechts).
Weiche aus, so lange du kannst! Jeder Meteorit, dem du ausweichst, bringt einen Punkt.

**Neu in diesem Spiel:** Sprites **steuern**, Sprites **neu setzen** und **Zusammenstöße** erkennen.

## Dein Raumschiff

Dein Raumschiff steht ganz unten in der Mitte.

- :align justify: Erstelle eine Variable ``schiff``.
- :mouse pointer: Ziehe ``||variables:setze schiff auf||`` in ``||basic:beim Start||``.
- :gamepad: Setze ``||game:erzeuge Sprite an Position x: 2 y: 4||`` ein.

```blocks
let schiff = game.createSprite(2, 4)
```

~hint Warum y: 4? 💡
**y: 0** ist die oberste Zeile, **y: 4** die unterste. Dein Schiff steht also ganz unten.
hint~

## Steuern mit A und B

- :circle: Ziehe ``||input:wenn Knopf A gedrückt||`` auf die Arbeitsfläche.
- :gamepad: Ziehe ``||game:schiff ändere x um 1||`` hinein und mache daraus **-1** (nach links).
- :circle: Mache dasselbe mit ``||input:wenn Knopf B gedrückt||`` – aber mit **+1** (nach rechts).

```blocks
let schiff = game.createSprite(2, 4)
input.onButtonPressed(Button.A, function () {
    schiff.change(LedSpriteProperty.X, -1)
})
input.onButtonPressed(Button.B, function () {
    schiff.change(LedSpriteProperty.X, 1)
})
```

## Der Meteorit

Der Meteorit startet oben an einer **zufälligen** Stelle.

- :align justify: Erstelle eine Variable ``meteorit`` und setze sie in ``||basic:beim Start||``.
- :gamepad: Benutze wieder ``||game:erzeuge Sprite an Position||``. Bei **y** kommt **0**.
- :calculator: Bei **x** setzt du ``||math:wähle zufällig von 0 bis 4||`` ein.

```blocks
let schiff = game.createSprite(2, 4)
let meteorit = game.createSprite(randint(0, 4), 0)
input.onButtonPressed(Button.A, function () {
    schiff.change(LedSpriteProperty.X, -1)
})
input.onButtonPressed(Button.B, function () {
    schiff.change(LedSpriteProperty.X, 1)
})
```

## Der Meteorit fällt

Jetzt muss der Meteorit **fallen**. Ist er noch nicht unten, rutscht er eins nach unten.
Ist er unten angekommen, startet er **neu oben** – und du bekommst einen Punkt!

- :th: Ziehe ``||basic:dauerhaft||`` auf die Arbeitsfläche und darin ``||basic:pausiere (ms)||`` mit **300**.
- :random: Darunter kommt ``||logic:wenn wahr dann sonst||`` mit dem Vergleich ``||logic:0 < 0||``.
- :gamepad: Links ``||game:meteorit y||``, rechts **4**.
- :gamepad: Im **wenn**-Teil: ``||game:meteorit ändere y um 1||``.
- :gamepad: Im **sonst**-Teil: ``||game:meteorit setze y auf 0||``, ``||game:meteorit setze x auf||`` (zufällig 0 bis 4) und ``||game:ändere Spielstand um 1||``.

```blocks
let schiff = game.createSprite(2, 4)
let meteorit = game.createSprite(randint(0, 4), 0)
input.onButtonPressed(Button.A, function () {
    schiff.change(LedSpriteProperty.X, -1)
})
input.onButtonPressed(Button.B, function () {
    schiff.change(LedSpriteProperty.X, 1)
})
basic.forever(function () {
    basic.pause(300)
    if (meteorit.get(LedSpriteProperty.Y) < 4) {
        meteorit.change(LedSpriteProperty.Y, 1)
    } else {
        meteorit.set(LedSpriteProperty.Y, 0)
        meteorit.set(LedSpriteProperty.X, randint(0, 4))
        game.addScore(1)
    }
})
```

## Zusammenstoß!

Wenn der Meteorit dein Schiff **berührt**, ist das Spiel vorbei.

- :random: Ziehe einen neuen ``||logic:wenn wahr dann||``-Block **ganz unten** in ``||basic:dauerhaft||``.
- :gamepad: Setze ``||game:meteorit berührt schiff?||`` als Bedingung ein.
- :gamepad: Hinein kommt ``||game:Game Over||``.

```blocks
let schiff = game.createSprite(2, 4)
let meteorit = game.createSprite(randint(0, 4), 0)
input.onButtonPressed(Button.A, function () {
    schiff.change(LedSpriteProperty.X, -1)
})
input.onButtonPressed(Button.B, function () {
    schiff.change(LedSpriteProperty.X, 1)
})
basic.forever(function () {
    basic.pause(300)
    if (meteorit.get(LedSpriteProperty.Y) < 4) {
        meteorit.change(LedSpriteProperty.Y, 1)
    } else {
        meteorit.set(LedSpriteProperty.Y, 0)
        meteorit.set(LedSpriteProperty.X, randint(0, 4))
        game.addScore(1)
    }
    if (meteorit.isTouching(schiff)) {
        game.gameOver()
    }
})
```

## Ausprobieren @showdialog

Teste dein Spiel im Simulator! Wie viele Meteoriten schaffst du? ☄️

Zu leicht? Im nächsten Schritt wird es **immer schneller**.

## Immer schneller

- :align justify: Erstelle eine Variable ``tempo`` und setze sie in ``||basic:beim Start||`` auf **400**.
- :mouse pointer: Setze ``||variables:tempo||`` in ``||basic:pausiere (ms)||`` ein.
- :align justify: Ziehe ``||variables:ändere tempo um||`` mit **-10** unter ``||game:ändere Spielstand um 1||``.

```blocks
let tempo = 400
let schiff = game.createSprite(2, 4)
let meteorit = game.createSprite(randint(0, 4), 0)
input.onButtonPressed(Button.A, function () {
    schiff.change(LedSpriteProperty.X, -1)
})
input.onButtonPressed(Button.B, function () {
    schiff.change(LedSpriteProperty.X, 1)
})
basic.forever(function () {
    basic.pause(tempo)
    if (meteorit.get(LedSpriteProperty.Y) < 4) {
        meteorit.change(LedSpriteProperty.Y, 1)
    } else {
        meteorit.set(LedSpriteProperty.Y, 0)
        meteorit.set(LedSpriteProperty.X, randint(0, 4))
        game.addScore(1)
        tempo += -10
    }
    if (meteorit.isTouching(schiff)) {
        game.gameOver()
    }
})
```

## Geschafft! @showdialog

🚀 Dein erstes richtiges Videospiel ist fertig!

**Für Profis:** Kannst du einen **zweiten Meteoriten** einbauen?
