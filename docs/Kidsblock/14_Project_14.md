### Projekt 14: Spurverfolgungs-Panzer


#### **(1)Beschreibung:**

Im vorherigen Projekt wurde erklärt, wie man das Smart Car dazu bringt, sich innerhalb eines bestimmten Bereichs zu bewegen. In diesem Projekt werden wir das bisher erlernte Wissen nutzen, um daraus ein spurverfolgendes Smart Car zu machen. Im Experiment verwenden wir den Spurverfolgungssensor, um zu erkennen, ob sich eine schwarze Linie in der Nähe des Smart Cars befindet, und steuern dann entsprechend den Erkennungsergebnissen die Drehung der beiden Motoren, damit das Smart Car der schwarzen Linie entlangfährt.

Die spezifische Logik des Smart Cars ist in der folgenden Tabelle dargestellt:

|               Sensor               |                          Erkennung                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Spurverfolgungssensor in der Mitte | Schwarze Linie erkannt: High-Pegel<br />Weiße Linie erkannt: Low-Pegel |
|  Spurverfolgungssensor links  | Schwarze Linie erkannt: High-Pegel<br />Weiße Linie erkannt: Low-Pegel |
| Spurverfolgungssensor rechts  | Schwarze Linie erkannt: High-Pegel<br />Weiße Linie erkannt: Low-Pegel |

|                         Bedingung 1                          |                         Bedingung 2                          |   Bewegung   |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------: |
| Spurverfolgungssensor <br />in der Mitte <br />erkennt die schwarze Linie | Spurverfolgungssensor links erkennt die schwarze Linie<br />der rechte erkennt weiße Linien | Links drehen  |
| Spurverfolgungssensor <br />in der Mitte <br />erkennt die schwarze Linie | Spurverfolgungssensor links erkennt weiße Linien<br />der rechte erkennt die schwarze Linie | Rechts drehen |
| Spurverfolgungssensor <br />in der Mitte <br />erkennt die schwarze Linie | Sowohl der linke als auch der rechte Spurverfolgungssensor erkennen weiße Linien<br />Sowohl der linke als auch der rechte Spurverfolgungssensor erkennen die schwarze Linie | Vorwärts fahren |
| Spurverfolgungssensor<br />in der Mitte <br />erkennt weiße Linien | Spurverfolgungssensor links erkennt die schwarze Linie<br />der rechte erkennt weiße Linien | Links drehen  |
| Spurverfolgungssensor<br />in der Mitte <br />erkennt weiße Linien | Spurverfolgungssensor links erkennt weiße Linien<br />der rechte erkennt die schwarze Linie | Rechts drehen |
| Spurverfolgungssensor<br />in der Mitte <br />erkennt weiße Linien | Sowohl der linke als auch der rechte Spurverfolgungssensor erkennen weiße Linien<br />Sowohl der linke als auch der rechte Spurverfolgungssensor erkennen die schwarze Linie |     Stopp     |

#### **(2)Flussdiagramm:**

![](media/wps11.png)

#### **(3)Anschlussdiagramm:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Testcode:**

Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

（7）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（8）![](media/fec93c7b8b089de709fd50575931519c.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

![](media/294ae4c01072e34b58a334912c90083a.png)


#### **(5)Testergebnisse:**

Nach dem erfolgreichen Hochladen des Testcodes und dem Einschalten der Stromversorgung fährt das Smart Car der schwarzen Linie entlang.

![](./media/img-20240117094129.png)