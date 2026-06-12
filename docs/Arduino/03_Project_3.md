### Projekt 3: Fotowiderstand

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Beschreibung:**

Der lichtempfindliche Widerstand ist ein spezieller Widerstand, der aus einem Halbleitermaterial wie Sulfid oder Selen hergestellt wird, und eine feuchtigkeitsbeständige Beschichtung mit einem fotoleitenden Effekt ist ebenfalls aufgetragen. Der Fotowiderstand reagiert am empfindlichsten auf das Umgebungslicht; bei unterschiedlicher Beleuchtungsstärke ist der Widerstandswert des Fotowiderstands verschieden. Wir verwenden den Fotowiderstand, um das Fotowiderstandsmodul zu entwerfen.

Das Modulsignal ist mit dem Analogport des Mikrocontrollers verbunden. Wenn die Lichtintensität stärker ist, ist die Spannung am Analogport größer, d. h. der Analogwert des Mikrocontrollers ist ebenfalls größer; umgekehrt, wenn die Lichtintensität schwächer ist, ist die Spannung am Analogport kleiner, d. h. der Analogwert des Mikrocontrollers ist ebenfalls kleiner.

Auf diese Weise können wir den entsprechenden Analogwert mithilfe des Fotowiderstandsmoduls auslesen und die Lichtintensität in der Umgebung erfassen.

![](media/7784e14e15402644cdbe674d500327c4.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Parameter:**

Widerstandswert des Fotowiderstands: 5K Ohm-0,5m

Schnittstellentyp: Simulationsport A0, A1

Betriebsspannung: 3,3V-5V

Pinabstand: 2,54mm


#### **(3)Anschlussdiagramm:**

Was wir als nächstes testen werden, ist das Fotowiderstandsmodul auf der linken Seite des Roboters.

![](./media/img-20240117091559.png)

Der linke Fotowiderstand ist mit A1/P3 des Motorantriebsboards verbunden.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls die serielle Kommunikation nutzt und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.1

photocell

http://www.keyestudio.com

*/

int sensorPin = A1; // A1 ist der Eingangspin des Fotowiderstands

int sensorValue = 0; // Speichert den Wert des Fotowiderstands

void setup() 
{
	Serial.begin(9600); // Seriellen Monitor öffnen und Baudrate auf 9600 setzen
}

void loop() 
{
	sensorValue = analogRead(sensorPin); // Analogwert vom Fotowiderstandssensor lesen
	Serial.println(sensorValue); // Serieller Monitor gibt den Wert des Fotowiderstands aus
	delay(500); // Verzögerung von 500ms
}
```

#### **(5)Testergebnisse:**

![](media/54b92578e3210999e23f5fb8138f0fa0.png)

Wenn man ihn abdeckt, wird der Wert kleiner; wenn nicht, wird der Wert größer.

#### **(6)Code-Erklärung:**

**analogRead(sensorPin)**: liest den Analogwert des Fotowiderstands

**Serial.begin(9600)**: initialisiert den seriellen Port und setzt die Baudrate auf 9600

**Serial.println**: serielle Ausgabe

#### **(7)Erweiterungsübung:**

Der obige Code liest nur den Wert des Fotowiderstands. Wir können den Fotowiderstand und eine LED kombinieren, um die LED zu steuern. Wie wäre es, die Helligkeit der LED damit zu regeln?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

Die Helligkeit der LED wird durch PWM gesteuert. Daher verbinden wir die LED mit dem PWM-Pin (Pin 9) des Boards.

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls die serielle Kommunikation nutzt und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

```c
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.2

photocell-analog output

http://www.keyestudio.com

*/

int analogInPin = A1; // A1 ist der Eingangspin des Fotowiderstands

int analogOutPin = 9; // Digitalport 9 ist der PWM-Ausgang

int sensorValue = 0; // Speichert die Variable des Widerstandswerts des Fotowiderstands

int outputValue = 0; // Wert, der an PWM ausgegeben wird

void setup() 
{
	Serial.begin(9600); // Seriellen Monitor öffnen und Baudrate auf 9600 setzen
}

void loop() 
{
    sensorValue = analogRead(analogInPin); // Analogwert vom Fotowiderstandssensor lesen
    // Analogwerte 0\~1023 auf PWM-Ausgabewerte 255\~0 abbilden
    outputValue = map(sensorValue, 0, 1023, 255, 0);
    // Analogen Ausgang ändern
    analogWrite(analogOutPin, outputValue);
    Serial.println(sensorValue); // Serieller Monitor gibt den Wert des Fotowiderstands aus
    delay(2);
}
```

Laden Sie den Code auf das Entwicklungsboard hoch, decken Sie dann den Fotowiderstand ab und beobachten Sie die Helligkeit der LED.

![](./media/img-20240117091105.png)