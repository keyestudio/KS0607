### Projekt 5: Servo-Steuerung

#### **(1)Beschreibung:**

Ein Servomotor ist ein positionsgesteuerter Drehantrieb. Er besteht hauptsächlich aus einem Gehäuse, einer Leiterplatte, einem kernlosen Motor, einem Getriebe und einem Positionssensor. Das Funktionsprinzip besteht darin, dass der Servo das vom MCU oder Empfänger gesendete Signal empfängt und ein Referenzsignal mit einer Periode von 20 ms und einer Breite von 1,5 ms erzeugt. Anschließend wird die erfasste DC-Offsetspannung mit der Spannung des Potentiometers verglichen und die Spannungsdifferenz am Ausgang ermittelt.

Wenn die Motorgeschwindigkeit konstant ist, wird das Potentiometer über das nachgeschaltete Untersetzungsgetriebe zur Rotation angetrieben, wodurch die Spannungsdifferenz 0 wird und der Motor stoppt. Im Allgemeinen liegt der Drehwinkelbereich des Servos bei 0° bis 180°.

Der Drehwinkel des Servomotors wird durch die Regelung des Tastverhältnisses des PWM-Signals (Pulsweitenmodulation) gesteuert. Der Standardzyklus des PWM-Signals beträgt 20 ms (50 Hz). Theoretisch liegt die Breite zwischen 1 ms und 2 ms, aber tatsächlich liegt sie zwischen 0,5 ms und 2,5 ms. Die Breite entspricht dem Drehwinkel von 0° bis 180°. Zu beachten ist, dass bei verschiedenen Motormarken dasselbe Signal zu unterschiedlichen Drehwinkeln führen kann.

![](media/69be958142b773acdae33eeef12afed7.png)

Im Allgemeinen hat ein Servo drei Leitungen in Braun, Rot und Orange. Die braune Leitung ist die Masse, die rote ist der Pluspol und die orange ist die Signalleitung.

![](media/49467dfa70799401a5a5acc691014aee.png)

Der Winkel des Servos:

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Parameter:**

- Betriebsspannung: DC 4,8V \~ 6V

- Betriebswinkelbereich: ca. 180° (bei 500 → 2500 μsec)

- Pulsbreitenbereich: 500 → 2500 μsec

- Leerlaufgeschwindigkeit: 0,12 ± 0,01 sec / 60 (DC 4,8V) 0,1 ± 0,01 sec / 60 (DC 6V)

- Leerlaufstrom: 200 ± 20mA (DC 4,8V) 220 ± 20mA (DC 6V)

- Haltemoment: 1,3 ± 0,01kg · cm (DC 4,8V) 1,5 ± 0,1kg · cm (DC 6V)

- Haltestrom: ≦ 850mA (DC 4,8V) ≦ 1000mA (DC 6V)

- Ruhestrom: 3 ± 1mA (DC 4,8V) 4 ± 1mA (DC 6V)

#### **(3)Anschlussdiagramm:**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Die braunen, roten und orangefarbenen Leitungen des Servos werden jeweils mit Gnd(G), 5v(V) und D10 des Shields verbunden. Denken Sie daran, eine externe Stromversorgung anzuschließen, da der Servo einen hohen Strom benötigt. Andernfalls wird das Entwicklungsboard beschädigt.

#### **(4)Testcode:**

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten dargestellt

![](media/5b04350e0310955ee2ecd48338f556a3.png)

![](media/7dd97d17b785de17e6c9362fa32e2a74.png)

![](media/69724a2063fa25e0f142e1eb48efd40f.png)

![](media/e149b45054fe94196dea220b319cb0bf.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

![](media/26e37037daf84d69320b76dd13346cd1.png)

#### **(6)Testergebnisse:**

Code hochladen, Stromversorgung anschließen und der Servo bewegt sich im Bereich von 0° bis 180°.

![](./media/img-20240117092225.png)