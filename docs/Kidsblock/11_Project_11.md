### Projekt 11: Ultraschall-Folge-Tank


#### **(1)Beschreibung:**

In der vorherigen Lektion haben wir etwas über das lichtfolgende Smart-Car gelernt. In dieser Lektion können wir das Wissen kombinieren, um ein ultraschallfolgendes Auto zu bauen. In diesem Projekt verwenden wir Ultraschallsensoren, um den Abstand zwischen dem Auto und dem Hindernis vorne zu messen, und steuern dann die Drehung der beiden Motoren basierend auf diesen Daten, um die Bewegungen des Smart-Cars zu kontrollieren.

Die spezifische Logik des ultraschallfolgenden Smart-Cars ist in der folgenden Tabelle dargestellt:

|                        Erkennung                        |              Einstellung              |
| :-----------------------------------------------------: | :-----------------------------------: |
| Der Abstand (cm) zwischen dem Auto und dem Hindernis vorne | Servowikel auf 90° einstellen |
|                      **Bedingung**                      |           **Bewegung**            |
|               Abstand≥20 und Abstand≤50               |             Vorwärts fahren              |
|            10＜Abstand＜20<br/>Abstand＞50            |               Stopp                |
|                       Abstand≤10                       |              Rückwärts fahren              |

#### **(2)Flussdiagramm:**

![](media/wps118.png)

#### **(3)Anschlussdiagramm:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span> Die Verkabelung des Ultraschallsensors, des Servos und des Motors ist dieselbe wie beim vorherigen Projektexperiment. GND, VCC, SDA und SCL des 8x16-LED-Panels sind jeweils mit G (GND), V (VCC), A4 und A5 auf der Erweiterungsplatine verbunden.

#### **(4)Testcode:**

Sie können auch Blöcke per Drag & Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt.

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/f6fb93211f786d023eb77eb210eae454.png)

（3）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

(7) ![](media/4b40151c7482ff9371570978b8ef9c77.png)

(8) ![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

(9) ![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

(10) ![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es möglicherweise zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/b895ca60e3249e09d4c15c356c60099a.png)


#### **(5)Testergebnis:**

Laden Sie den Code hoch, schalten Sie die Stromversorgung ein und stellen Sie den DIP-Schalter auf ON. Der Servo dreht sich um 90°, das 8X16-LED-Panel zeigt ![](media/fdd4ae50b3372cc9c4ef27f6bddda387.png) an, und das Auto folgt dem Hindernis.

![](./media/img-20240117093900.png)