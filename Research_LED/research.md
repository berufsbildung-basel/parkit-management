# LED Matrix Research

## LED Matrix

Eine RGB LED matrix ist wie ein display. Es besteht aus vielen Pixeln.  
RGB steht für Rot Grün Blau.  
In jedem Pixel befinden sich Rote, Grüne und Blaue LEDs.

In dem man die helligkeit von den RGB LEDs anpasst verändert sich die Farbe z.b Rot und Grün an, Blau aus => Gelb.  
Wenn alle drei Farben mit voller Helligkeit leuchten entsteht Weiss. Wenn alle aus sind ist der Pixel Schwarz bzw. aus.  
Durch unterschiedliche Helligkeiten von Rot, Grün und Blau können sehr viele verschiedene Farben erzeugt werden.

Man kann die LED matrizen in diese Haupttypen unterscheiden:

- Single Color LED matrix
- RGB LED matrix
- Adressierbare RGB LED matrix

Die Single color matrix kann nur genau eine Farbe anzeigen man kann nichts an der Farbe ändern sondern nur sagen ob ein Pixel an oder aus ist.  
Bei einer RGB matrix können verschiedene Farben dargestellt werden, indem Rot, Grün und Blau unterschiedlich kombiniert werden.  
Bei einer Adressierbaren RGB matrix kann man jedes pixel einzeln ansteuern und sagen in welcher Farbe und Helligkeit es leuchten soll.

Es gibt verschiedene Arten wie eine LED matrix angesteuert werden kann.

Bei kleinen adressierbaren Matrizen werden oft LEDs wie WS2812B verwendet. Diese LEDs besitzen bereits einen kleinen Chip und die Daten werden von LED zu LED weitergegeben. Dadurch braucht man nur wenige Datenleitungen.

Bei grösseren RGB Panels wird häufig HUB75 verwendet. Hier werden mehrere Reihen und Spalten sehr schnell nacheinander angesteuert. Das passiert so schnell, dass es für das menschliche Auge so aussieht als würden alle LEDs gleichzeitig leuchten.

### Normale Grössen

Die normalen Grössen sind z.b folgende:

- 8x8
- 16x16
- 32x32
- 64x32
- 64x64

z.b bei einer 8x8 matrix gibt es 8 mal 8 pixel => 64pixel  
Bei einer 64x64 matrix sind es bereits 4096 pixel.

Man kann diese auch zu grösseren kombinieren z.b 2x 8x8 => entweder 16x8 oder 8x16.  
Auch grössere Panels können miteinander verbunden werden. Dadurch kann man z.b aus mehreren 64x64 Panels ein deutlich grösseres Display bauen.

### Pixel Pitch

Neben der Auflösung gibt es bei LED matrizen auch den Pixel Pitch. Dieser gibt den Abstand zwischen den einzelnen Pixeln an.

z.b P2.5 bedeutet, dass zwischen den Pixeln ungefähr 2.5mm Abstand liegt.  
Ein kleinerer Pixel Pitch bedeutet, dass die Pixel näher zusammenliegen und das Bild aus kurzer Entfernung detaillierter aussieht.

### Benötigte Hardware

Um eine LED matrix zu nutzen braucht es normalerweise diese Hardware:

- Controller
- Netzteil / Power kabel z.b 5V
- LED matrix
- Datenkabel

Der Controller kann z.b ein Arduino, ESP32, Raspberry Pi oder ein spezieller LED Controller sein.  
Der Controller bekommt die Daten die angezeigt werden sollen und sendet die richtigen Signale an die LED matrix.

Welcher Controller benötigt wird hängt von der Matrix ab. Eine kleine 8x8 Matrix benötigt deutlich weniger Leistung vom Controller als mehrere grosse Panels.

Das Netzteil versorgt die LEDs mit Strom.  
Die benötigte Spannung hängt von der Matrix ab, häufig werden z.b 5V verwendet.

Wichtig ist aber auch wie viel Strom das Netzteil liefern kann. Je mehr LEDs gleichzeitig und mit hoher Helligkeit leuchten, desto mehr Strom wird benötigt.  
Bei grossen Matrizen kann deshalb ein deutlich stärkeres Netzteil notwendig sein.

### Typischer Aufbau

Ein typischer aufbau sieht z.b so aus:

- Applikation/Server/Computer
- Controller
- LED matrix

**Applikation/Computer/Server** (Sendet was angezeigt werden soll)  
↓  
**Controller** (Bekommt die gewünschte information von der Applikation und verwandelt diese in für die Matrix verständliche signale)  
↓  
**LED matrix** (Bekommt die Signale und gibt das Bild/Text aus)

Die LED matrix wird zusätzlich über ein Netzteil mit Strom versorgt.

Die Verbindung zwischen Applikation/Computer und Controller kann z.b über USB, WLAN oder Ethernet erfolgen.

Dabei muss die Applikation nicht unbedingt direkt wissen wie die einzelnen LEDs angesteuert werden. Sie kann z.b ein Bild, Text oder andere Daten an den Controller senden. Der Controller übernimmt danach die eigentliche Ansteuerung der LEDs.

Ein Beispiel könnte so aussehen:

`Computer mit einer Applikation` → `WLAN/Ethernet` → `ESP32/LED Controller` → `Datenkabel` → `LED matrix`

Der Controller aktualisiert die Matrix normalerweise sehr oft pro Sekunde. Dadurch können nicht nur Bilder und Text sondern auch Animationen und Videos dargestellt werden.

> **Gehe zu `./Screenshots/Options` um mögliche realistische Setups anzuschauen die zu unserem Projekt passen könnten.**

> Formatierung wurde mit Chatgpt gemacht
---

# English Version

> **Translated with AI**

## LED Matrix

An RGB LED matrix is like a display. It consists of many pixels.  
RGB stands for Red Green Blue.  
Each pixel contains red, green and blue LEDs.

By adjusting the brightness of the RGB LEDs, the color changes. For example, red and green on, blue off => Yellow.  
If all three colors are at full brightness, they create white. If all of them are off, the pixel is black or turned off.  
By using different brightness levels of red, green and blue, many different colors can be created.

LED matrices can be divided into these main types:

- Single Color LED matrix
- RGB LED matrix
- Addressable RGB LED matrix

A Single Color matrix can only display one color. The color cannot be changed, you can only control whether a pixel is on or off.  
An RGB matrix can display different colors by combining red, green and blue in different ways.  
With an Addressable RGB matrix, each pixel can be controlled individually. You can control which color and brightness each pixel should have.

There are different ways an LED matrix can be controlled.

Small addressable matrices often use LEDs like the WS2812B. These LEDs already contain a small chip and the data is passed from one LED to the next. Because of this, only a few data lines are needed.

Larger RGB panels often use HUB75. Here, multiple rows and columns are controlled very quickly one after another. This happens so fast that to the human eye it looks like all LEDs are on at the same time.

### Common Sizes

Common sizes are for example:

- 8x8
- 16x16
- 32x32
- 64x64
- 64x32

For example, an 8x8 matrix has 8 times 8 pixels => 64 pixels.  
A 64x64 matrix already has 4096 pixels.

They can also be combined to create larger matrices, for example 2x 8x8 => either 16x8 or 8x16.

Larger panels can also be connected together. For example, multiple 64x64 panels can be used to build a much larger display.

### Pixel Pitch

In addition to the resolution, LED matrices also have a pixel pitch. This describes the distance between the individual pixels.

For example, P2.5 means that the distance between the pixels is approximately 2.5mm.  
A smaller pixel pitch means that the pixels are closer together and the image looks more detailed from a short distance.

### Required Hardware

To use an LED matrix, the following hardware is normally needed:

- Controller
- Power supply / power cable, for example 5V
- LED matrix
- Data cable

The controller can for example be an Arduino, ESP32, Raspberry Pi or a dedicated LED controller.  
The controller receives the data that should be displayed and sends the correct signals to the LED matrix.

Which controller is needed depends on the matrix. A small 8x8 matrix requires much less performance from the controller than multiple large panels.

The power supply provides power to the LEDs.  
The required voltage depends on the matrix, but for example 5V is commonly used.

It is also important how much current the power supply can provide. The more LEDs that are on at the same time and at high brightness, the more current is needed.  
For large matrices, a much more powerful power supply may therefore be necessary.

### Typical Setup

A typical setup could look like this:

- Application/Server/Computer
- Controller
- LED matrix

**Application/Computer/Server** (Sends what should be displayed)  
↓  
**Controller** (Receives the information from the application and converts it into signals that the matrix can understand)  
↓  
**LED matrix** (Receives the signals and displays the image/text)

The LED matrix is additionally connected to a power supply.

The connection between the application/computer and the controller can for example use USB, Wi-Fi or Ethernet.

The application does not necessarily need to know how each individual LED is controlled. It can for example send an image, text or other data to the controller. The controller then handles the actual control of the LEDs.

An example could look like this:

`Computer with an application` → `Wi-Fi/Ethernet` → `ESP32/LED Controller` → `Data cable` → `LED matrix`

The controller normally updates the matrix many times per second. This makes it possible to display not only images and text but also animations and videos.