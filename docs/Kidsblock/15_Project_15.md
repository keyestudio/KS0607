### Projekt 15: Infrarot-Ferngesteuerter Panzer

![](./media/image-20250709134800790.png)

#### **(1)Beschreibung:**

Infrarot-Fernsteuerung ist eine der häufigsten Fernsteuerungsanwendungen in Elektromotoren, Elektrolüftern und vielen anderen Haushaltsgeräten. In diesem Projekt nutzen wir das zuvor erlernte Wissen, um ein infrarot-ferngesteuertes Smart Car zu bauen.

In der 9. Lektion haben wir den entsprechenden Tastenwert jeder Taste der Infrarot-Fernbedienung getestet. In diesem Projekt können wir den Code (Tastenwert) festlegen, damit die entsprechende Taste die Bewegungen des Smart Cars steuert und die Bewegungsmuster auf der 8X16 LED-Punktmatrix anzeigt.

Die spezifische Logik des Smart Cars ist in der folgenden Tabelle dargestellt:

|                 Ultraschall-Taste                  | Tastenwert | Anweisungen der Tasten                                       |
| :---------------------------------------------: | :-------: | ------------------------------------------------------------ |
| ![](media/b11dc5ffa6cccebc6088e5d557d76daf.png) |  FF629D   | Vorwärts fahren（PWM auf 200 setzen）<br />Muster für Vorwärtsfahren anzeigen |
| ![](media/ae8110034aacb083151cfd882ee599ba.png) |  FFA857   | Rückwärts fahren（PWM auf 200 setzen）<br />Muster für Rückwärtsfahren anzeigen |
| ![](media/bce9cba2c6d2465fbcce570ad4210eba.png) |  FF22DD   | Links abbiegen<br />Muster „STOP" anzeigen                     |
| ![](media/ad907a618af86f30d52986bbbd57ba76.png) |  FFC23D   | Rechts abbiegen<br />Muster für Links abbiegen anzeigen          |
| ![](media/9716a4ed61a4064d2f47a7b73eccaf87.png) |  FF02FD   | Anhalten<br />Muster „STOP" anzeigen                          |

**Anfangseinstellung: 8X16 LED-Punktmatrix zeigt das Muster"![](media/dc59c5fcb4fcf6af4d4a5ebb14b7a919.png)"**



#### **(2)Ablaufdiagramm:**

![](media/wps121.png)

#### **(3)Anschlussdiagramm:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span>

GND, VCC, SDA und SCL des 8x16 LED-Panels sind mit G（GND), V（VCC), A4 und A5 der Erweiterungsplatine verbunden.

Da die 8833-Platine den IR-Empfänger bereits integriert hat, muss dieser nicht extra verdrahtet werden. Die Pins des IR-Empfängers sind G（GND), V（VCC) und D3.

#### **(4)Testcode:**

Sie können Blöcke bearbeiten, um Ihren Code aufzubauen

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/a9042e77ebe3009fbb7653bef3429b66.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6）![](media/51e30aa2aca3a7da67ee4f0f81c7dad1.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/7ab62148fa2a23259b8039475978d8fc.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/fae6c22640ced038daca9cb6721ab95e.png)

#### **(5)Testergebnisse:**

Nachdem der Testcode erfolgreich hochgeladen und das Gerät eingeschaltet wurde, kann das Smart Car durch die Infrarot-Fernbedienung gesteuert werden, und das 8\*16-Display zeigt die entsprechenden Bewegungsmuster an.

![](./media/img-20240117094223.png)