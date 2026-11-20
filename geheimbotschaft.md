# Geheimbotschaft

## Willkommen! @showdialog

✉️ **Geheimbotschaft!**

Du baust aus deinem micro:bit einen **Messenger**. Mit **A** blätterst du durch deine Nachrichten, mit **B** schickst du sie per Funk.
Alle micro:bits in deiner Funkgruppe sehen dann, **was** du geschrieben hast – und **wer** es war!

**Neu in diesem Spiel:** **Texte** per Funk senden und Texte **verbinden**.

## Die Funkgruppe

- :broadcast tower: Ziehe ``||radio:setze Funkgruppe 1||`` in ``||basic:beim Start||``.

```blocks
radio.setGroup(1)
```

**Wichtig! 💡**
Alle, die sich Nachrichten schicken wollen, brauchen **dieselbe** Funkgruppe. Fragt eure Lehrkraft, welche Zahl ihr nehmen sollt.

## Eine Nachricht senden

- :circle: Ziehe ``||input:wenn Knopf B gedrückt||`` auf die Arbeitsfläche.
- :broadcast tower: Ziehe ``||radio:sende Zeichenfolge über Funk||`` hinein und schreibe **HALLO**.

```blocks
radio.setGroup(1)
input.onButtonPressed(Button.B, function () {
    radio.sendString("HALLO")
})
```

## Eine Nachricht empfangen

Wenn ein anderer micro:bit eine Nachricht schickt, soll deiner sie anzeigen.

- :broadcast tower: Ziehe ``||radio:wenn Zeichenfolge empfangen receivedString||`` auf die Arbeitsfläche.
- :th: Hinein: ``||basic:zeige Text||``. Ziehe ``||variables:receivedString||`` aus dem Block heraus und setze es ein.

```blocks
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
})
radio.setGroup(1)
input.onButtonPressed(Button.B, function () {
    radio.sendString("HALLO")
})
```

## Eine Liste voller Nachrichten

Immer nur „HALLO“ ist langweilig. Wir legen eine **Liste mit Nachrichten** an und blättern mit **A** durch.

- :align justify: Erstelle die Variablen ``nachrichten`` und ``nummer``.
- :list: In ``||basic:beim Start||``: ``||arrays:setze nachrichten auf Array von||``. Klicke auf **+**, bis es 5 Felder gibt, und schreibe: **HALLO**, **JA**, **NEIN**, **KOMM HER**, **PAUSE?**
- :align justify: Setze ``nummer`` auf **0**.

```blocks
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
})
radio.setGroup(1)
let nachrichten = ["HALLO", "JA", "NEIN", "KOMM HER", "PAUSE?"]
let nummer = 0
input.onButtonPressed(Button.B, function () {
    radio.sendString("HALLO")
})
```

## Blättern mit A

- :circle: Ziehe ``||input:wenn Knopf A gedrückt||`` auf die Arbeitsfläche.
- :align justify: Hinein: ``||variables:ändere nummer um 1||``.
- :random: Darunter: ``||logic:wenn wahr dann||`` mit ``||variables:nummer||`` **≥** ``||arrays:Länge des Arrays nachrichten||``. Dann ``||variables:setze nummer auf 0||``.
- :th: Ganz unten: ``||basic:zeige Text||`` mit ``||arrays:nachrichten Wert an nummer||``.
- :broadcast tower: Ändere bei **B**: Statt „HALLO“ wird ``||arrays:nachrichten Wert an nummer||`` gesendet.

```blocks
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
})
input.onButtonPressed(Button.A, function () {
    nummer += 1
    if (nummer >= nachrichten.length) {
        nummer = 0
    }
    basic.showString(nachrichten[nummer])
})
input.onButtonPressed(Button.B, function () {
    radio.sendString(nachrichten[nummer])
})
let nummer = 0
let nachrichten: string[] = []
radio.setGroup(1)
nachrichten = ["HALLO", "JA", "NEIN", "KOMM HER", "PAUSE?"]
nummer = 0
```

**Warum „≥ Länge“? 💡**
Die Liste hat **5** Nachrichten an den Stellen **0 bis 4**. Kommt ``nummer`` bei **5** an, gibt es dort keine Nachricht mehr – also zurück zur **0**!

## Wer schreibt?

Damit man weiß, **von wem** die Nachricht kommt, hängen wir deinen Namen davor.

- :align justify: Erstelle eine Variable ``name`` und setze sie in ``||basic:beim Start||`` auf **deinen Namen** (zum Beispiel **MIA**).
- :text: Ziehe bei **B** aus ``||text:Text||`` den Block ``||text:verbinde||`` in ``||radio:sende Zeichenfolge||``.
- :plus: Klicke auf **+**, damit er **drei** Felder hat: ``||variables:name||``, **": "** und ``||arrays:nachrichten Wert an nummer||``.
- :th: Zeige nach dem Senden kurz ``||basic:zeige Symbol||`` **Häkchen** an, damit du weißt, dass es geklappt hat.

```blocks
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
})
input.onButtonPressed(Button.A, function () {
    nummer += 1
    if (nummer >= nachrichten.length) {
        nummer = 0
    }
    basic.showString(nachrichten[nummer])
})
input.onButtonPressed(Button.B, function () {
    radio.sendString("" + name + ": " + nachrichten[nummer])
    basic.showIcon(IconNames.Yes)
})
let nummer = 0
let nachrichten: string[] = []
let name = ""
radio.setGroup(1)
name = "MIA"
nachrichten = ["HALLO", "JA", "NEIN", "KOMM HER", "PAUSE?"]
nummer = 0
```

**Achtung, nicht zu lang! ⚠️**
Eine Funknachricht darf höchstens **19 Zeichen** lang sein. Wähle also einen kurzen Namen und kurze Nachrichten – sonst wird das Ende abgeschnitten.

## Ausprobieren @showdialog

Im Simulator siehst du **zwei** micro:bits. Blättere bei einem mit **A** und sende mit **B** – auf dem anderen erscheint deine Nachricht! 📡

Mit echten micro:bits: Alle in derselben Funkgruppe bekommen deine Nachricht.

## Geschafft! @showdialog

🎉 Du hast deinen eigenen **Messenger** programmiert!

**Für Profis:** Denkt euch eine **Geheimsprache** aus: Ersetzt die Nachrichten durch Codewörter, die nur eure Gruppe versteht. 🤫
