### Projekt 8: Motorsteuerung und Geschwindigkeitsregelung

#### **(1) Beschreibung:**

Es gibt viele Möglichkeiten, Motoren anzusteuern. Unser Smart Car verwendet die gängigste Lösung namens L298P. L298P, hergestellt von STMicroelectronics, ist ein hervorragender Ansteuerungschip, der speziell für den Antrieb von Hochleistungsmotoren entwickelt wurde.

Er kann DC-Motoren, zweiphasige und vierphasige Motoren direkt antreiben, wobei der Antriebsstrom 2A erreicht. Und der Ausgangsanschluss des Motors verwendet 8 schnelle Schottky-Dioden als Schutz.

Wir haben eine Erweiterungsplatine auf Basis der L298P-Schaltung entwickelt, die dank ihres gestapelten Designs direkt in das UNO R3-Board eingesteckt werden kann, was die technischen Schwierigkeiten für den Benutzer beim Einsatz und beim Antrieb des Motors reduziert.

Stecken Sie die Erweiterungsplatine auf das Board, versorgen Sie die BAT mit Strom, stellen Sie den DIP-Schalter auf die ON-Seite und versorgen Sie die Erweiterungsplatine und das UNO R3-Board gleichzeitig über eine externe Stromversorgung.

Um die Verkabelung zu vereinfachen, ist die Erweiterungsplatine mit verpolungssicheren Schnittstellen (PH2.0-2P-3P-4P-5P) ausgestattet, sodass sie direkt mit Motoren, Stromversorgung und Sensoren/Modulen verbunden werden kann.

Die Bluetooth-Schnittstelle der Antriebs-Erweiterungsplatine ist vollständig kompatibel mit dem Keyestudio HM-10 Bluetooth-Modul. Daher müssen wir beim Anschluss nur das HM-10 Bluetooth-Modul in die entsprechende Schnittstelle einstecken.

Gleichzeitig verwendet die Antriebs-Erweiterungsplatine auch 2,54-mm-Stiftleisten, um einige verfügbare digitale und analoge Ports zu erweitern, sodass Sie weitere Sensoren hinzufügen und Erweiterungsexperimente durchführen können.

Die Erweiterungsplatine kann mit 4 DC-Motoren verbunden werden. Im Standard-Jumper-Verbindungsmodus sind die Motoren an den Schnittstellen A und A1, B und B1 parallel geschaltet und ihr Bewegungsmuster ist gleich. 8 Jumper-Kappen können verwendet werden, um die Drehrichtung der 4 Motorschnittstellen zu steuern.

Wenn beispielsweise die beiden Jumper-Kappen vor der Motor-A-Schnittstelle von einer horizontalen auf eine vertikale Verbindung geändert werden, ist die Drehrichtung von Motor A nun entgegengesetzt zur ursprünglichen Drehrichtung.

![](media/image-20230427081635216.png)

![](media/5381c98d3be6da099ce43e841b8f736b.png)

#### **(2) Parameter:**

- Eingangsspannung Logikteil: DC 5V

- Eingangsspannung Antriebsteil: DC 7-12V

- Arbeitsstrom Logikteil: ≤36mA

- Arbeitsstrom Antriebsteil: ≤ 2A

- Maximale Verlustleistung: 25W (T=75℃)

- Eingangspegel Steuersignal:
  
  ​	Hoher Pegel: 2,3V ≤ Vin ≤ 5V
  
  ​	Niedriger Pegel: 0V ≤ Vin ≤ 1,5V

- Betriebstemperatur: -25℃～＋130℃

#### **(3) Den Roboter bewegen**

Der Richtungspin von Motor A ist D2, der Geschwindigkeitssteuerungspin ist D5; der Richtungspin von Motor B ist D4 und der Geschwindigkeitssteuerungspin ist D6.

Anhand der nachstehenden Tabelle können wir erkennen, wie die Bewegung des Roboters durch die Steuerung der Drehung zweier Motoren über die digitalen Ports und PWM-Ports gesteuert wird. Dabei liegt der PWM-Wertebereich bei 0-255. Je größer der Wert, desto schneller dreht sich der Motor.

|   Funktion   |  D4  | D6（PWM） | Motor（links）B |  D2  | D5（PWM） | Motor（rechts）A |
| :----------: | :--: | :-------: | :-------------: | :--: | :-------: | :-------------: |
| Vorwärts fahren | HIGH |  255-200  |   Dreht links   | HIGH |  255-200  |   Dreht links   |
|   Rückwärts fahren    | LOW  |    200    |  Dreht rechts   | LOW  |    200    |  Dreht rechts   |
| Links drehen  | LOW  |    200    |  Dreht rechts   | HIGH |  255-200  |   Dreht links   |
| Rechts drehen | HIGH |  255-200  |   Dreht links   | LOW  |    200    |  Dreht rechts   |
|     Stopp     | LOW  |     0     |      Stopp       | LOW  |     0     |      Stopp       |




#### **(4) Anschlussdiagramm:**

![](media/3e53cf19ea5f85a931b955453b86304b.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span>

Der 4-polige Anschluss ist mit A, A1, B1 und B gekennzeichnet. Der rechte hintere Motor ist mit B des 8833-Boards verbunden und der linke vordere Motor ist mit dem A-Port verbunden.

#### **(5) Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.1
motor driver
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // Richtungssteuerungspin des linken Motors definieren
#define ML_PWM 6 // PWM-Steuerungspin des linken Motors definieren
#define MR_Ctrl 2 // Richtungssteuerungspin des rechten Motors definieren
#define MR_PWM 5 // PWM-Steuerungspin des rechten Motors definieren

void setup()
{
    pinMode(ML_Ctrl, OUTPUT);// Richtungssteuerungspin des linken Motors als OUTPUT definieren
    pinMode(ML_PWM, OUTPUT);// PWM-Steuerungspin des linken Motors als OUTPUT definieren
    pinMode(MR_Ctrl, OUTPUT);// Richtungssteuerungspin des rechten Motors als OUTPUT definieren
    pinMode(MR_PWM, OUTPUT);// PWM-Steuerungspin des rechten Motors als OUTPUT definieren
}

void loop()
{
    // vorwärts
    digitalWrite(ML_Ctrl, HIGH); // Richtungssteuerungsgeschwindigkeit des linken Motors auf HIGH setzen
    analogWrite(ML_PWM, 55); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 55
    digitalWrite(MR_Ctrl, HIGH); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf HIGH setzen
    analogWrite(MR_PWM, 55); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 55
    delay(2000);// Verzögerung von 2s

    // rückwärts
    digitalWrite(ML_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des linken Motors auf LOW setzen
    analogWrite(ML_PWM, 200); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 200
    digitalWrite(MR_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf LOW setzen
    analogWrite(MR_PWM, 200); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 200
    delay(2000);// Verzögerung von 2s

    // links drehen
    digitalWrite(ML_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des linken Motors auf LOW setzen
    analogWrite(ML_PWM, 200); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 200
    digitalWrite(MR_Ctrl, HIGH); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf HIGH setzen
    analogWrite(MR_PWM, 55); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 55
    delay(2000);// Verzögerung von 2s

    // rechts drehen
    digitalWrite(ML_Ctrl, HIGH); // Richtungssteuerungsgeschwindigkeit des linken Motors auf HIGH setzen
    analogWrite(ML_PWM, 55); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 55
    digitalWrite(MR_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf LOW setzen
    analogWrite(MR_PWM, 200); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 200
    delay(2000);// Verzögerung von 2s

    // stopp
    digitalWrite(ML_Ctrl, LOW);
    analogWrite(ML_PWM, 0); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 0
    digitalWrite(MR_Ctrl, LOW);
    analogWrite(MR_PWM, 0); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 0
    delay(2000);// Verzögerung von 2s
}
```

#### **(6) Testergebnisse:**

Nach der Verkabelung gemäß dem Diagramm, dem Hochladen des Testcodes und der Stromversorgung.

![](./media/img-20240117082646.png)

fährt das Smart Car 2s vorwärts, 2s rückwärts, dreht 2s nach links, dreht 2s nach rechts und hält 2s an, und wiederholt diese Abfolge.

#### **(7) Code-Erklärung:**

**digitalWrite(ML_Ctrl,LOW);**

Der Wechsel zwischen hohen und niedrigen Pegeln lässt die Motoren im Uhrzeigersinn oder gegen den Uhrzeigersinn drehen. Allgemeine digitale Pins können verwendet werden, um diese Bewegungen zu steuern.

**analogWrite(ML_PWM,200);**

Die Geschwindigkeitsregelung des Motors wird durch PWM realisiert, und der Pin, der die Geschwindigkeit des Motors steuert, muss der PWM-Pin des Arduino sein.

#### **(8) Erweiterungsprojekt:**

Wir passen die Motorgeschwindigkeit durch die Steuerung von PWM an, die Verkabelung bleibt gleich.

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.2
motor driver pwm
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // Richtungssteuerungspin des linken Motors definieren
#define ML_PWM 6 // PWM-Steuerungspin des linken Motors definieren
#define MR_Ctrl 2 // Richtungssteuerungspin des rechten Motors definieren
#define MR_PWM 5 // PWM-Steuerungspin des rechten Motors definieren

void setup() 
{
    pinMode(ML_Ctrl, OUTPUT);// Richtungssteuerungspin des linken Motors als OUTPUT definieren
    pinMode(ML_PWM, OUTPUT);// PWM-Steuerungspin des linken Motors als OUTPUT definieren
    pinMode(MR_Ctrl, OUTPUT);// Richtungssteuerungspin des rechten Motors als OUTPUT definieren
    pinMode(MR_PWM, OUTPUT);// PWM-Steuerungspin des rechten Motors als OUTPUT definieren
}

void loop() 
{
    // vorwärts
    digitalWrite(ML_Ctrl, HIGH); // Richtungssteuerungsgeschwindigkeit des linken Motors auf HIGH setzen
    analogWrite(ML_PWM, 155); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 155
    digitalWrite(MR_Ctrl, HIGH); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf HIGH setzen
    analogWrite(MR_PWM, 155); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 155
    delay(2000);// Verzögerung von 2s

    // rückwärts
    digitalWrite(ML_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des linken Motors auf LOW setzen
    analogWrite(ML_PWM, 100); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 100
    digitalWrite(MR_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf LOW setzen
    analogWrite(MR_PWM, 100); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 100
    delay(2000);// Verzögerung von 2s

    // links
    digitalWrite(ML_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des linken Motors auf LOW setzen
    analogWrite(ML_PWM, 100); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 100
    digitalWrite(MR_Ctrl, HIGH); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf HIGH setzen
    analogWrite(MR_PWM, 155); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 155
    delay(2000);// Verzögerung von 2s

    // rechts
    digitalWrite(ML_Ctrl, HIGH); // Richtungssteuerungsgeschwindigkeit des linken Motors auf HIGH setzen
    analogWrite(ML_PWM, 155); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 155
    digitalWrite(MR_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf LOW setzen
    analogWrite(MR_PWM, 100); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 100
    delay(2000);// Verzögerung von 2s

    // stopp
    digitalWrite(ML_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des linken Motors auf LOW setzen
    analogWrite(ML_PWM, 0); // PWM-Steuerungsgeschwindigkeit des linken Motors ist 0
    digitalWrite(MR_Ctrl, LOW); // Richtungssteuerungsgeschwindigkeit des rechten Motors auf LOW setzen
    analogWrite(MR_PWM, 0); // PWM-Steuerungsgeschwindigkeit des rechten Motors ist 0
    delay(2000);// Verzögerung von 2s
}
```

Laden Sie den Code hoch, die Geschwindigkeit des Motors ist langsamer.

Ein niedriger Strom lässt den Motor langsamer drehen.