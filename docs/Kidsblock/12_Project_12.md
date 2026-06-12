### Projekt 12: Ultraschall-Hindernisumfahrungs-Panzer

#### **(1)Beschreibung:**

Im vorherigen Projekt haben wir ein ultraschallgesteuertes Smart Car gebaut, das Objekten folgt. Tatsächlich müssen wir bei gleichen Bauteilen und gleicher Verkabelung nur den Testcode ändern, um daraus ein ultraschallgesteuertes Smart Car zu machen, das Hindernissen ausweicht. Dieses Smart Car kann sich mit der Bewegung der menschlichen Hände bewegen.

Wir verwenden Ultraschallsensoren, um den Abstand zwischen dem Smart Car und dem Hindernis vor ihm zu messen, und steuern dann die Drehung der beiden Motoren basierend auf diesen Daten, um die Bewegungen des Smart Cars zu kontrollieren.

|                          Erkennung                           |         |
| :----------------------------------------------------------: | :-----: |
| Vom Ultraschallsensor gemessener Abstand zwischen dem Auto und dem Hindernis vorne <br />（Servowinkel auf 90° einstellen） | a (cm)  |
| Vom Ultraschallsensor gemessener Abstand zwischen dem Auto und dem Hindernis rechts <br />（Servowinkel auf 0° einstellen） | a2 (cm) |
| Vom Ultraschallsensor gemessener Abstand zwischen dem Auto und dem Hindernis links <br />（Servowinkel auf 180° einstellen） | a1 (cm) |

**Einstellung: Startwinkel des Servos auf 90° einstellen**

| Bedingung 1 |        Bedingung 2         |      Bedingung 3       | Bewegung                                                     |
| :---------: | :------------------------: | :--------------------: | :----------------------------------------------------------- |
|    a＜20    |                            |                        | 500 ms anhalten; Servowinkel auf 180° einstellen, a1 lesen, 100 ms verzögern; Servowinkel auf 0° einstellen, a2 lesen, 0,1 s verzögern. |
|             | a1＜50<br />oder<br />a2＜50 | **a1 mit a2 vergleichen** |                                                              |
|             |                            |         a1＞a2         | Servowinkel auf 90° einstellen, 700 ms nach links drehen (PWM auf 255 setzen) und vorwärts fahren (PWM auf 200 setzen). |
|             |                            |         a1＜a2         | Servowinkel auf 90° einstellen, 700 ms nach rechts drehen (PWM auf 255 setzen) und vorwärts fahren (PWM auf 200 setzen). |
|             | a1≥50<br />und<br />a2≥50  |         Zufällig         | Servowinkel auf 90° einstellen, 500 ms nach links drehen (PWM auf 255 setzen) und vorwärts fahren (PWM auf 200 setzen).<br /><br />Servowinkel auf 90° einstellen, 500 ms nach rechts drehen (PWM auf 255 setzen) und vorwärts fahren (PWM auf 200 setzen). |
|    a≥20     |                            |                        | Vorwärts fahren (PWM auf 100 setzen)                               |

#### **(2)Flussdiagramm:**

![](media/wps119.png)

#### **(3)Anschlussdiagramm:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

(<span style="color: rgb(255, 76, 65);">Hinweis:</span> Die braunen, roten und orangefarbenen Kabel des Servos sind jeweils mit G (GND), V（5V）und D10 der Erweiterungsplatine verbunden; beim Ultraschallsensor ist der VCC-Pin mit 5V (V), der Trig-Pin mit digital 12 (S), der Echo-Pin mit digital 13 (S) und der Gnd-Pin mit Gnd (G) verbunden; wie im vorherigen Projekt.）

#### **(4)Testcode:**


Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt.![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/5dcbd405806b8e341505d7316246dbdd.png)

（3）![](media/996c8d4e5dd9620757dfb097329e7d5d.png)

（4）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

（10）![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

（11）![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/4360f9642a8c6b2488767c079d481482.png)

#### **(5)Testergebnisse:**

Nachdem der Testcode erfolgreich hochgeladen wurde, die Verkabelung vorgenommen, den DIP-Schalter auf die ON-Seite gestellt und das Gerät eingeschaltet wurde, fährt das Smart Car vorwärts und weicht automatisch Hindernissen aus.

![](./media/img-20240117093950.png)