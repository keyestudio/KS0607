### Projekt 8: Motorsteuerung und Geschwindigkeitsregelung

#### **(1) Beschreibung:**

Es gibt viele Möglichkeiten, Motoren anzusteuern. Unser Smart Car verwendet die gängigste Lösung namens L298P. L298P, hergestellt von STMicroelectronics, ist ein hervorragender Ansteuerungschip, der speziell für den Antrieb von Hochleistungsmotoren entwickelt wurde. Er kann DC-Motoren, zweiphasige und vierphasige Motoren direkt ansteuern, wobei der Antriebsstrom bis zu 2A erreicht. Der Ausgangsanschluss des Motors verwendet 8 schnelle Schottky-Dioden als Schutz. Wir haben eine Erweiterungsplatine basierend auf dem L298P-Schaltkreis entwickelt, die durch ihr gestapeltes Design direkt auf das UNO R3-Board gesteckt werden kann und so die technischen Schwierigkeiten für Benutzer bei der Verwendung und dem Antrieb des Motors reduziert.

Stecken Sie die Erweiterungsplatine auf das Board, versorgen Sie BAT mit Strom, drehen Sie den DIP-Schalter auf die ON-Seite und versorgen Sie die Erweiterungsplatine und das UNO R3-Board gleichzeitig über eine externe Stromversorgung. Um die Verkabelung zu erleichtern, ist die Erweiterungsplatine mit verpolungssicheren Schnittstellen (PH2.0 -2P -3P -4P -5P) ausgestattet, sodass Motoren, Stromversorgung und Sensoren/Module direkt angesteckt werden können. Die Bluetooth-Schnittstelle der Antriebserweiterungsplatine ist vollständig kompatibel mit dem Keyestudio HM-10 Bluetooth-Modul. Daher müssen wir das HM-10 Bluetooth-Modul beim Anschließen nur in die entsprechende Schnittstelle stecken. Gleichzeitig verwendet die Antriebserweiterungsplatine auch 2,54-mm-Stiftleisten, um einige verfügbare Digital- und Analogports zu erweitern, sodass Sie weitere Sensoren hinzufügen und Erweiterungsexperimente durchführen können.

Die Erweiterungsplatine kann mit 4 DC-Motoren verbunden werden. Im Standard-Jumper-Verbindungsmodus sind die Schnittstellen A und A1 sowie B und B1 parallel geschaltet, und ihr Bewegungsmuster ist identisch. Mit 8 Jumperkappen kann die Drehrichtung der 4 Motorschnittstellen gesteuert werden. Wenn beispielsweise die zwei Jumperkappen vor der Motorschnittstelle A von einer horizontalen auf eine vertikale Verbindung geändert werden, ist die Drehrichtung von Motor A nun entgegengesetzt zur ursprünglichen Drehrichtung.

![](media/6c3731f639e113c8f32fe1829f239898.png)

![](media/62ee9578858ecc8e27b824af65fb22bb.png)

#### **(2) Parameter:**

-   Eingangsspannung des Logikteils: DC 5V

-   Eingangsspannung des Antriebsteils: DC 7-12V

-   Betriebsstrom des Logikteils: ≤36mA

-   Betriebsstrom des Antriebsteils: ≤ 2A

-   Maximale Verlustleistung: 25W (T=75℃)

-   Eingangspegel des Steuersignals:

    High-Pegel: 2,3V ≤ Vin ≤ 5V

    Low-Pegel: 0V ≤ Vin ≤ 1,5V

-   Betriebstemperatur: -25℃～＋130℃

#### **(3) Den Roboter bewegen:**

Der Richtungspin von Motor A ist D2, der Geschwindigkeitssteuerungspin ist D5; der Richtungspin von Motor B ist D4 und der Geschwindigkeitssteuerungspin ist D6.

Anhand der folgenden Tabelle können wir erkennen, wie die Bewegung des Roboters durch die Steuerung der Drehung zweier Motoren über die Digitalports und PWM-Ports gesteuert wird. Der Wertebereich des PWM-Werts liegt dabei zwischen 0 und 255. Je größer der Wert ist, desto schneller dreht sich der Motor.

|   Funktion    |  D4  | D6（PWM） | Motor （links）B |  D2  | D5（PWM） | Motor（rechts）A |
| :-----------: | :--: | :-------: | :--------------: | :--: | :-------: | :--------------: |
| Vorwärts fahren | HIGH |     0     |   Dreht links   | HIGH |     0     |   Dreht links   |
|  Rückwärts fahren   | LOW  |    255    |  Dreht rechts   | LOW  |    255    |  Dreht rechts   |
| Links drehen  | LOW  |    255    |  Dreht rechts   | HIGH |    100    |   Dreht links   |
| Rechts drehen | HIGH |    100    |   Dreht links   | LOW  |    255    |  Dreht rechts   |
|    Stopp      | LOW  |     0     |      Stopp       | LOW  |     0     |      Stopp       |

#### **(4) Anschlussdiagramm:**

![](./media/image-20250709134029403.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span>

Der 4-polige Stecker ist mit A, A1, B1 und B gekennzeichnet. Der rechte hintere Motor ist mit B des 8833-Boards verbunden und der linke vordere Motor ist mit dem A-Port verbunden.

#### **(5) Testcode:**

Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt.

（1）![](media/7cbc4d14c2e2dac956f2e9f145f01f31.png)

（2）![](media/0067d367772d4e3005bfc097ba3b59b0.png)

（3）![](media/f0c505e8268454c7996b755f97c6322b.png)

（4）![](media/b7215c8a4997a188947e80fdee1a8cd9.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/332229f3dc01a38de898367f52531b28.png)


#### **(6) Testergebnisse:**

Nach der Verkabelung gemäß dem Diagramm, dem Hochladen des Testcodes und der Inbetriebnahme.

![](./media/img-20240117092625.png)

fährt das Smart Car 2 Sekunden vorwärts, 2 Sekunden rückwärts, dreht 2 Sekunden nach links, dreht 2 Sekunden nach rechts und stoppt für 2 Sekunden.