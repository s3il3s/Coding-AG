# Kipp-Sammler

## Willkommen! @showdialog

🌟 **Kipp-Sammler!**

Du steuerst einen Punkt, indem du den micro:bit **kippst** – ganz ohne Knöpfe!
Sammle so viele blinkende Sterne wie möglich, bevor die Zeit abläuft.

**Neu in diesem Spiel:** der **Beschleunigungssensor**. Er merkt, wie der micro:bit gehalten wird.

## Deine Spielfigur

- :align justify: Erstelle eine Variable ``spieler``.
- :mouse pointer: Ziehe ``||variables:setze spieler auf||`` in ``||basic:beim Start||``.
- :gamepad: Setze ``||game:erzeuge Sprite an Position x: 2 y: 2||`` ein.

```blocks
let spieler = game.createSprite(2, 2)
```

## Nach links und rechts kippen

Der Sensor liefert eine Zahl: Kippst du nach **rechts**, ist sie **größer als 0**. Kippst du nach **links**, ist sie **kleiner als 0**.

- :th: Ziehe ``||basic:dauerhaft||`` auf die Arbeitsfläche.
- :random: Ziehe ``||logic:wenn wahr dann||`` hinein und klicke auf **+**, damit es ein **sonst wenn** gibt.
- :random: Erste Bedingung: ``||logic:0 > 0||`` mit ``||input:Beschleunigung (mg) x||`` links und **200** rechts.
- :gamepad: Dann: ``||game:spieler ändere x um 1||``.
- :random: Bei **sonst wenn**: ``||logic:0 < 0||`` mit ``||input:Beschleunigung (mg) x||`` und **-200**.
- :gamepad: Dann: ``||game:spieler ändere x um -1||``.
- :th: Unter den ``||logic:wenn||``-Block: ``||basic:pausiere (ms)||`` mit **150**.

```blocks
let spieler = game.createSprite(2, 2)
basic.forever(function () {
    if (input.acceleration(Dimension.X) > 200) {
        spieler.change(LedSpriteProperty.X, 1)
    } else if (input.acceleration(Dimension.X) < -200) {
        spieler.change(LedSpriteProperty.X, -1)
    }
    basic.pause(150)
})
```

**Warum 200? 💡**
Ganz gerade liegt der Wert bei ungefähr **0**. Mit **200** muss man den micro:bit ein bisschen kippen – sonst würde der Punkt schon beim kleinsten Wackeln losflitzen.

## Nach vorne und hinten kippen

Jetzt dasselbe für **oben und unten**. Dafür gibt es die Richtung **y**.

- :mouse pointer: Klicke mit der rechten Maustaste auf den ``||logic:wenn||``-Block und wähle **Duplizieren**.
- :mouse pointer: Setze die Kopie darunter.
- :pencil: Ändere in der Kopie überall **x** in **y**.

```blocks
let spieler = game.createSprite(2, 2)
basic.forever(function () {
    if (input.acceleration(Dimension.X) > 200) {
        spieler.change(LedSpriteProperty.X, 1)
    } else if (input.acceleration(Dimension.X) < -200) {
        spieler.change(LedSpriteProperty.X, -1)
    }
    if (input.acceleration(Dimension.Y) > 200) {
        spieler.change(LedSpriteProperty.Y, 1)
    } else if (input.acceleration(Dimension.Y) < -200) {
        spieler.change(LedSpriteProperty.Y, -1)
    }
    basic.pause(150)
})
```

## Der Stern

Jetzt brauchen wir etwas zum Einsammeln: einen **blinkenden Stern** an einer zufälligen Stelle.

- :align justify: Erstelle eine Variable ``stern`` und setze sie in ``||basic:beim Start||``.
- :gamepad: Benutze ``||game:erzeuge Sprite an Position||`` und setze bei **x** und **y** jeweils ``||math:wähle zufällig von 0 bis 4||`` ein.
- :gamepad: Darunter: ``||game:stern setze blinken auf 300||``. So kann man Stern und Spieler unterscheiden.

```blocks
let spieler = game.createSprite(2, 2)
let stern = game.createSprite(randint(0, 4), randint(0, 4))
stern.set(LedSpriteProperty.Blink, 300)
basic.forever(function () {
    if (input.acceleration(Dimension.X) > 200) {
        spieler.change(LedSpriteProperty.X, 1)
    } else if (input.acceleration(Dimension.X) < -200) {
        spieler.change(LedSpriteProperty.X, -1)
    }
    if (input.acceleration(Dimension.Y) > 200) {
        spieler.change(LedSpriteProperty.Y, 1)
    } else if (input.acceleration(Dimension.Y) < -200) {
        spieler.change(LedSpriteProperty.Y, -1)
    }
    basic.pause(150)
})
```

## Einsammeln!

Wenn dein Punkt den Stern **berührt**, gibt es einen Punkt – und der Stern springt an eine neue Stelle.

- :random: Ziehe ``||logic:wenn wahr dann||`` über den Block ``||basic:pausiere||``.
- :gamepad: Bedingung: ``||game:spieler berührt stern?||``.
- :gamepad: Hinein: ``||game:ändere Spielstand um 1||``.
- :gamepad: Dann ``||game:stern setze x auf||`` und ``||game:stern setze y auf||`` – jeweils zufällig von **0 bis 4**.

```blocks
let spieler = game.createSprite(2, 2)
let stern = game.createSprite(randint(0, 4), randint(0, 4))
stern.set(LedSpriteProperty.Blink, 300)
basic.forever(function () {
    if (input.acceleration(Dimension.X) > 200) {
        spieler.change(LedSpriteProperty.X, 1)
    } else if (input.acceleration(Dimension.X) < -200) {
        spieler.change(LedSpriteProperty.X, -1)
    }
    if (input.acceleration(Dimension.Y) > 200) {
        spieler.change(LedSpriteProperty.Y, 1)
    } else if (input.acceleration(Dimension.Y) < -200) {
        spieler.change(LedSpriteProperty.Y, -1)
    }
    if (spieler.isTouching(stern)) {
        game.addScore(1)
        stern.set(LedSpriteProperty.X, randint(0, 4))
        stern.set(LedSpriteProperty.Y, randint(0, 4))
    }
    basic.pause(150)
})
```

## Gegen die Uhr

Damit es spannend wird, hast du nur **30 Sekunden**!

- :gamepad: Ziehe ``||game:starte Countdown (ms)||`` ans Ende von ``||basic:beim Start||`` und stelle **30000** ein.

```blocks
let spieler = game.createSprite(2, 2)
let stern = game.createSprite(randint(0, 4), randint(0, 4))
stern.set(LedSpriteProperty.Blink, 300)
game.startCountdown(30000)
basic.forever(function () {
    if (input.acceleration(Dimension.X) > 200) {
        spieler.change(LedSpriteProperty.X, 1)
    } else if (input.acceleration(Dimension.X) < -200) {
        spieler.change(LedSpriteProperty.X, -1)
    }
    if (input.acceleration(Dimension.Y) > 200) {
        spieler.change(LedSpriteProperty.Y, 1)
    } else if (input.acceleration(Dimension.Y) < -200) {
        spieler.change(LedSpriteProperty.Y, -1)
    }
    if (spieler.isTouching(stern)) {
        game.addScore(1)
        stern.set(LedSpriteProperty.X, randint(0, 4))
        stern.set(LedSpriteProperty.Y, randint(0, 4))
    }
    basic.pause(150)
})
```

**Was passiert am Ende? ⏱️**
Nach 30 Sekunden ist das Spiel vorbei und der micro:bit zeigt deinen **Spielstand** an.

## Ausprobieren @showdialog

Im Simulator kippst du den micro:bit, indem du die **Maus über ihm bewegst**. 🖱️

Richtig Spaß macht es aber mit dem echten micro:bit in der Hand!

## Geschafft! @showdialog

🎉 Super! Du hast einen **Sensor** benutzt, um ein Spiel zu steuern.

**Für Profis:** Baue eine **Bombe** ein, die du **nicht** berühren darfst – sonst ist **Game Over**!
