### Projekt 21: Feuerlösch-Panzer

#### **(1) Beschreibung:**

Die Spurverfolgungs-Funktion des Smart-Panzers wurde im vorherigen Projekt erläutert. In diesem Projekt verwenden wir den Flammensensor, um einen Feuerlöschroboter zu bauen.

Wenn das Fahrzeug auf Flammen trifft, dreht sich der Motor des Lüfters, um das Feuer auszublasen. Natürlich müssen wir zuerst den Ultraschallsensor und die beiden Fotowiderstände durch ein Lüftermodul und Flammensensoren ersetzen.

Die spezifische Logik des Smart Cars ist in der folgenden Tabelle dargestellt:

| Linker Flammensensor | Rechter Flammensensor | Status                                                        |
| :------------------: | :-------------------: | :------------------------------------------------------------ |
|        ≤700          |         ≤700          | Auto stoppt, Lüfter beginnt zu drehen, um die Flamme auszublasen |
|        ≥700          |         ≥700          | Auto stoppt, Lüfter beginnt zu drehen, um die Flamme auszublasen |
|        ≥700          |         ≥700          | Auto stoppt, Lüfter beginnt zu drehen, um die Flamme auszublasen |
|        ＞700         |         ＞700         | Lüfter stoppt, Auto bewegt sich                               |

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
1） Dieses Experiment erfordert die Verwendung einer Feuerquelle. Bitte halten Sie Abstand von brennbaren Gegenständen, um Brände zu verhindern. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie sich nicht sicher sind, dass Sie sicher sind, verzichten Sie bitte auf das Experiment.
2） Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.
Wir können eine externe LED mit dem Flammensensor steuern. Die LED ist weiterhin mit D9 verbunden. Wenn Feuer erkannt wird, leuchtet die LED auf.


#### **(2) Flussdiagramm:**

![](media/wps120.png)

#### **(3) Anschlussdiagramm:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span>

GND, VCC, SDA und SCL des 8x16-LED-Panels sind mit G（GND), V（VCC), A4 und A5 verbunden.

G, V und A der beiden Flammensensoren sind mit G（GND), V（VCC), A1 und A2 des Erweiterungsboards verbunden.

#### **(4) Testcode:**


Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/2e3d4904d9605dfecb5736b4bf235ab2.png)

（4） ![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（5） ![](media/4b40151c7482ff9371570978b8ef9c77.png)

（6）![](media/c0365237fa7ec7de10e9fc465353fae1.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/c07c09e5533a37838722b8c2b513646d.png)

#### **(5) Testergebnisse:**

Nachdem der Testcode erfolgreich hochgeladen wurde, schalten Sie die Stromversorgung ein und stellen Sie den DIP-Schalter auf die ON-Seite. Das Smart Car löscht das Feuer, wenn es eine Flamme erkennt.

![](media/2de5f1d832d40c0fc94274f1d87443c6.jpeg)

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
Bitte halten Sie Abstand von brennbaren Gegenständen, um Brände zu verhindern. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie sich nicht sicher sind, dass Sie sicher sind, verzichten Sie bitte auf das Experiment. Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.