### Projekt 7: IR-Empfang

#### **(1) Beschreibung:**

![](./media/image-20250709133757050.png)

Zweifellos ist die Infrarot-Fernbedienung im täglichen Leben allgegenwärtig. Sie wird zur Steuerung verschiedener Haushaltsgeräte verwendet, wie z. B. Fernseher, Stereoanlagen, Videorekorder und Satellitenempfänger. Die Infrarot-Fernbedienung besteht aus einem Infrarot-Sende- und einem Infrarot-Empfangssystem, d. h. einer Infrarot-Fernbedienung, einem Infrarot-Empfangsmodul und einem Mikrocontroller, der zur Decodierung fähig ist.

Das vom Fernbedienungsgerät ausgesendete 38K-Infrarot-Trägersignal wird vom Codierchip in der Fernbedienung codiert. Es besteht aus einem Pilotcode, einem Benutzercode, einem invertierten Benutzercode, einem Datencode und einem invertierten Datencode. Das Zeitintervall der Impulse wird verwendet, um zu unterscheiden, ob es sich um ein 0- oder 1-Signal handelt, und die Codierung wird aus diesen 0- und 1-Signalen zusammengesetzt.

Der Benutzercode derselben Fernbedienung bleibt unverändert, während der Datencode die Taste unterscheiden kann.

Wenn die Fernbedienungstaste gedrückt wird, sendet die Fernbedienung ein Infrarot-Trägersignal aus. Wenn der IR-Empfänger das Signal empfängt, decodiert das Programm das Trägersignal und bestimmt, welche Taste gedrückt wurde. Der Mikrocontroller decodiert das empfangene 01-Signal und ermittelt dadurch, welche Taste der Fernbedienung gedrückt wurde.

![](media/5ad0f889b39646ecb13664511479efc8.png)

Der von uns verwendete Infrarotempfänger ist ein Infrarot-Empfangsmodul. Es besteht hauptsächlich aus einem Infrarot-Empfangskopf, einem Gerät, das Empfang, Verstärkung und Demodulation integriert. Der interne IC hat die Demodulation abgeschlossen und kann den Infrarotempfang bis zur Ausgabe realisieren und ist mit TTL-Signalen kompatibel. Außerdem ist es für Infrarot-Fernsteuerung und Infrarot-Datenübertragung geeignet. Das vom Empfänger hergestellte Infrarot-Empfangsmodul hat nur drei Pins: Signalleitung, VCC und GND. Es ist sehr praktisch, mit Arduino und anderen Mikrocontrollern zu kommunizieren.

#### **(2) Parameter:**

- Betriebsspannung: 3,3–5 V (DC)
- Schnittstelle: 3PIN
- Ausgangssignal: Digitalsignal
- Empfangswinkel: 90 Grad
- Frequenz: 38 kHz
- Empfangsreichweite: 10 m

Auf der Motorsteuerplatine integrierter Infrarotempfänger:

![](./media/image-20250709133832650.png)

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Da der IR-Empfänger in die Keyestudio 8833 Motorantriebs-Erweiterungsplatine integriert ist, ist keine zusätzliche Verkabelung erforderlich. Die Pins des IR-Empfängers auf der Keyestudio 8833 Motorantriebs-Erweiterungsplatine sind G (GND), V (VCC) und D3.

#### **(4) Testcode:**

Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt

![](media/cfe0841bcc9404c29519ed623195ca6a.png)

![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

![](media/5a48421831518ea8e0c00be83cf4edf4.png)

![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was zu einem Fehlschlagen des Uploads führen kann.)

![](media/90978855cddd94c161f9ed02f85b0674.png)

#### **(5) Testergebnisse:**

Laden Sie den Code auf die Entwicklungsplatine hoch und stellen Sie die Baudrate auf 9600 ein. Nehmen Sie die Fernbedienung heraus, richten Sie sie auf den Infrarot-Empfangssensor und drücken Sie eine Taste, um das Signal zu senden. Sie sehen den entsprechenden Tastenwert. Wenn die Taste zu lange gedrückt wird, kann leicht ein unlesbares „FFFFFFFF" erscheinen.

![](media/5c01c594a5a11511cf52466eb5f27e45.png)

Nachfolgend haben wir jeden Tastenwert der Keyestudio-Fernbedienung aufgelistet. Sie können ihn als Referenz aufbewahren.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

#### **(6) Erweiterungsübung:**

Wir haben gerade die Tastenwerte der IR-Fernbedienung decodiert. Nun wollen wir damit eine LED-Leuchte ein- und ausschalten. Wir müssen ein LED-Leuchtmodul an den D9-Pin anschließen, während die Pin-Position des Infrarotempfängers unverändert bleibt. Wenn die OK-Taste auf der Fernbedienung gedrückt wird, leuchtet die an D9 angeschlossene LED auf, und wenn die OK-Taste erneut gedrückt wird, erlischt die LED.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)


Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt

（1）![](media/cfe0841bcc9404c29519ed623195ca6a.png)

（2）![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

（3）![](media/ba67c48d67b1c9753fca82964c9dddc7.png)

(4) ![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

（5）![](media/f8b75df8ccea3efe1cd3ea383b0f88f2.png)

（6）![](media/7406d60c93cdba0b13ded27cba718ec7.png)

（7）![](media/d7be3fa06a1456d46472fffd61823c73.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was zu einem Fehlschlagen des Uploads führen kann.)

![](media/57149c79243ff22aa00ff2c54dd4f70b.png)

Laden Sie den Code auf die Entwicklungsplatine hoch und drücken Sie die „OK"-Taste auf der Fernbedienung, um die LED ein- und auszuschalten.

![](./media/img-20240117092532.png)