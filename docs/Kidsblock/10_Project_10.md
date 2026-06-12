### Projekt 10: Lichtfolgendes Fahrzeug


#### **(1)Beschreibung:**

In den vorherigen Projekten haben wir die Verwendung verschiedener Sensoren, Module und Erweiterungsplatinen am Smart Car ausführlich vorgestellt. Nun wollen wir uns den Projekten des Smart Cars widmen. Das lichtfolgende Smart Car, wie der Name schon sagt, ist ein Smart Car, das dem Licht folgen kann.

Wir können das Wissen aus den Projekten über Fotowiderstände und Motorsteuerung kombinieren, um ein lichtsuchen des Smart Car zu bauen. In diesem Projekt verwenden wir zwei Fotowiderstandsmodule, um die Lichtintensität auf der linken und rechten Seite des Smart Cars zu messen, lesen die entsprechenden Analogwerte aus und steuern dann die Drehung der beiden Motoren basierend auf diesen zwei Datenwerten, um so die Bewegungen des Smart Cars zu kontrollieren.

Die spezifische Logik des lichtfolgenden Smart Cars ist wie folgt dargestellt.

![image-20230525113331422](media/image-20230525113331422.png)

#### **(2)Flussdiagramm:**

![](media/wps117.png)

#### **(3)Anschlussdiagramm:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Hinweis: </span>Die Pins „G", „V" und S des linken Fotowiderstandsmoduls sind mit G (GND), V (VCC) bzw. A1 verbunden;

Die Pins „G", „V" und S des rechten Fotowiderstandsmoduls sind mit G (GND), V (VCC) bzw. A2 verbunden.

Das 4-polige Kabel ist mit A, A1, B1 und B gekennzeichnet. Der rechte Hinterradmotor ist mit dem B-Anschluss der 8833-Motortreiber-Erweiterungsplatine verbunden und der linke Vorderradmotor ist mit dem A-Anschluss der 8833-Motortreiber-Erweiterungsplatine verbunden.

#### **(4)Testcode:**


Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt.

（1）![](media/9352e6447f9648efddc7d5a748618332.png)

（2）![](media/1d99d71f5fe52dd2145cb11d75cabb21.png)

（3）![](media/5004e509325dffb32c05afe25abedfc9.png)

（4）![](media/6c6f0492f657c4c78a0497bb86519561.png)

（5）![](media/b8fc70fa8b3f335dcdf0c8ad9ed998c6.png)

（6）![](media/9eb0e93fbd43aa24f2ce656191f7cd79.png)

(7) ![](media/9f023e6f571e597e661a8d71a7f803cb.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">Hinweis:</span> Der Schwellenwert 650 im Code kann entsprechend der spezifischen Lichtintensität angemessen angepasst werden.

Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Kommunikation des Bluetooth kommen kann, was dazu führen kann, dass das Hochladen des Codes fehlschlägt.)

![](media/6300174b85f63c05dbdcb3b77188f9dc.png)


#### **(5)Testergebnisse:**

Nach erfolgreichem Hochladen des Testcodes, Verkabelung herstellen, den DIP-Schalter auf die ON-Seite stellen und einschalten – das Smart Car folgt dem Licht und bewegt sich entsprechend.

![](./media/img-20240117093758.png)