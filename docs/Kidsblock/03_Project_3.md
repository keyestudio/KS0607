### Projekt 3: Fotowiderstand

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Beschreibung:**

Der lichtempfindliche Widerstand ist ein spezieller Widerstand, der aus einem Halbleitermaterial wie Sulfid oder Selen hergestellt wird, und zusätzlich mit einem feuchtigkeitsbeständigen Harz mit fotoleitendem Effekt beschichtet ist. Der Fotowiderstand reagiert am empfindlichsten auf das Umgebungslicht; bei unterschiedlicher Lichtstärke ist der Widerstandswert des Fotowiderstands unterschiedlich. Wir verwenden den lichtempfindlichen Widerstand, um das Fotowiderstandsmodul zu entwerfen.

Das Modulsignal ist mit dem analogen Port des Mikrocontrollers verbunden. Wenn die Lichtintensität stärker ist, ist die Spannung am analogen Port größer, d.h. der Simulationswert des Mikrocontrollers ist ebenfalls größer; umgekehrt gilt: Wenn die Lichtintensität schwächer ist, ist die Spannung am analogen Port kleiner, d.h. der Simulationswert des Mikrocontrollers ist ebenfalls kleiner.

Auf diese Weise können wir den entsprechenden Analogwert mithilfe des Fotowiderstandsmoduls auslesen und die Lichtintensität in der Umgebung erfassen.

![](./media/image-20250709122809574.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Parameter:**

- Widerstandswert des Fotowiderstands: 5K Ohm-0,5m

- Schnittstellentyp: Simulationsport A0, A1

- Betriebsspannung: 3,3V-5V

- Pin-Abstand: 2,54mm

#### **(3)Anschlussdiagramm:**

Als nächstes testen wir das Fotowiderstandsmodul auf der linken Seite des Roboters.

![](./media/img-20240117091730.png)

Der linke Fotowiderstand ist mit A1/P3 des Motorantriebsshields verbunden.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)


#### **(4)Testcode:**

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/f29c7da2238bcc2bc70cb4b2c773b50d.png)

#### **(5)Testergebnisse:**

Laden Sie den Code auf das Entwicklungsboard hoch. Klicken Sie auf ![](media/9011f20d83897d7a5936793c4ae142fc.png), um die Baudrate auf 9600 einzustellen. Wenn Sie den Sensor mit der Hand abdecken, wird der Wert kleiner; wenn nicht, wird der Wert größer.

![](media/53e2fc37ee5bb2c6ec187c309c431c47.png)



#### **(6)Erweiterungsübung:**

Der obige Code liest lediglich den Wert des Fotowiderstands. Wir können den Fotowiderstand und die LED kombinieren, um die LED zu steuern. Was wäre, wenn wir die Helligkeit der LED damit steuern würden?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

PWM kann die Lichthelligkeit ändern, d.h. die LED sollte mit dem PWM des Entwicklungsboards verbunden werden.

Verbinden Sie die LED mit D9 und lassen Sie die anderen Pins unverändert, dann bearbeiten wir den Code.

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/b94c3789429c5fed4fd38467cb9792dd.png)

![](media/9ecdfd77e2a69dea5a8df04e7d56a13a.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/b23bcae806e8e27382b162909d30f3c0.png)

Laden Sie den Code auf das Entwicklungsboard hoch. Wir drücken auf den Fotowiderstand, um zu sehen, ob sich die Helligkeit der LED verändert hat.

![](./media/img-20240117091759.png)