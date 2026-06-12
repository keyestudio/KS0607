### Projekt 19: Flammensensor

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Beschreibung:**

Der Flammensensor verwendet eine IR-Empfangsröhre zur Erkennung von Flammen. Er wandelt die Helligkeit der Flamme in High- und Low-Pegel-Signale um und gibt diese an den Zentralprozessor zur entsprechenden Programmverarbeitung weiter. Der Spannungswert am Analogport variiert je nachdem, ob eine Flamme in der Nähe ist oder nicht.

Wenn keine Flamme vorhanden ist, liest der Analogport etwa 0,3V; wenn eine Flamme vorhanden ist, liest der Analogport etwa 1,0V. Je näher die Flamme ist, desto höher ist der Spannungswert. Er kann verwendet werden, um eine Feuerquelle zu erkennen oder einen intelligenten Roboter zu bauen.

Beachten Sie, dass die Sonde des Flammensensors nur Temperaturen zwischen -25℃ und 85℃ standhält.

Achten Sie während der Verwendung darauf, den Flammensensor in einem sicheren Abstand zum Feuer zu halten, um Schäden zu vermeiden.

#### **(2)Parameter:**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Betriebsspannung: 3,3V-5V (DC)

- Strom: 100mA

- Maximale Leistung: 0,5W

- Betriebstemperatur: -10°C bis +50 Grad Celsius

- Sensorgröße: 31,6mm x 23,7mm

- Schnittstelle: 4-poliger auf 3-poliger Anschluss

- Ausgangssignal: Analogsignale A0, A1

#### **(3)Schaltplan:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

Pin A der beiden Fotowiderstände ist mit A1 und A2 verbunden. Wir verbinden den Flammensensor mit A1 und A2. Indem wir die beiden Fotowiderstände und den Ultraschallsensor durch zwei Flammensensoren und einen Lüfter ersetzen, entsteht ein Löschfahrzeug.

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
1）Dieses Experiment erfordert den Einsatz einer Feuerquelle. Bitte halten Sie diese von brennbaren Gegenständen fern, um Brände zu verhindern. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie nicht sicher sind, ob Sie sicher sind, verzichten Sie bitte auf das Experiment.
2）**Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.**

#### **(4)Testcode:**

Sie können auch Blöcke per Drag & Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, wodurch der Upload fehlschlagen kann.)

![](media/4bc6c8a4d6e964fd078a6aeb0dd51ff4.png)

#### **(5)Testergebnisse:**

Verkabeln Sie die Komponenten, brennen Sie den Code, öffnen Sie den seriellen Monitor und stellen Sie die Baudrate auf 9600 ein.

Sie können den Simulationswert des Flammensensors anzeigen.

Je näher die Flamme ist, desto kleiner ist der Simulationswert.

Stellen Sie das Potentiometer am Modul so ein, dass die LED am kritischen Punkt bleibt. Wenn der Sensor keine Flamme erkennt, ist die LED ausgeschaltet. Wenn der Sensor jedoch eine Flamme erkennt, leuchtet die LED auf.

![](./media/img-20240117100139.png)

![](media/60d0ce2044a504135af3b1113a1a4c7d.png)

#### **(6)Erweiterungsübung:**

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
1）Dieses Experiment erfordert den Einsatz einer Feuerquelle. Bitte halten Sie diese von brennbaren Gegenständen fern, um Brände zu verhindern. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie nicht sicher sind, ob Sie sicher sind, verzichten Sie bitte auf das Experiment.
2）Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.
Wir können eine externe LED mit dem Flammensensor steuern. Die LED ist weiterhin mit D9 verbunden. Wenn Feuer erkannt wird, leuchtet die LED auf.

![](media/814c315d3bb44278b476a754d3681227.png)

Sie können Blöcke per Drag & Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, wodurch der Upload fehlschlagen kann.)

![](media/9d2f5915e4a6991ed4549b39ec853fa5.png)

Sie können die Flamme eines Feuerzeugs in die Nähe des linken Flammensensors halten. Wenn der Flammensensor eine Flamme erkennt, leuchtet das LED-Modul als Alarm auf.

![](./media/img-20240117100333.png)

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
Bitte halten Sie diese von brennbaren Gegenständen fern, um Brände zu verhindern. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie nicht sicher sind, ob Sie sicher sind, verzichten Sie bitte auf das Experiment. Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.