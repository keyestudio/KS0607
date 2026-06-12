### Project 11: Ultrasonic Volgend Pantservoertuig


#### **(1)Beschrijving:**

In de vorige les hebben we geleerd over de lichtvolgende slimme auto. En in deze les kunnen we de kennis combineren om een ultrasone volgende auto te maken. In het project gebruiken we ultrasone sensoren om de afstand tussen de auto en het obstakel voor hem te detecteren, en vervolgens de rotatie van de twee motoren te regelen op basis van deze gegevens om zo de bewegingen van de slimme auto te besturen.

De specifieke logica van de ultrasone volgende slimme auto wordt weergegeven in de onderstaande tabel:

|                        Detectie                        |              Instelling              |
| :-----------------------------------------------------: | :-------------------------------: |
| De afstand (cm) tussen de auto en het obstakel ervoor | Stel de hoek van de servo in op 90° |
|                      **Conditie**                      |           **Beweging**            |
|               afstand≥20 en afstand≤50               |             Vooruit rijden              |
|            10＜afstand＜20<br/>afstand＞50            |               Stoppen                |
|                       afstand≤10                       |              Achteruit rijden              |

#### **(2)Stroomdiagram:**

![](media/wps118.png)

#### **(3)Aansluitingsdiagram:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span> De bedrading van de ultrasone sensor, de servo en de motor is hetzelfde als het vorige projectexperiment. De GND, VCC, SDA en SCL van het 8x16 LED-paneel zijn respectievelijk verbonden met G (GND), V (VCC), A4 en A5 op het uitbreidingsbord.

#### **(4)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.

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

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/b895ca60e3249e09d4c15c356c60099a.png)


#### **(5)Testresultaat:**

Upload de code, zet de stroom aan en zet de DIP-schakelaar op ON. De servo zal 90° roteren, het 8X16 LED-paneel toont ![](media/fdd4ae50b3372cc9c4ef27f6bddda387.png), en de auto zal het obstakel volgen om te bewegen.

![](./media/img-20240117093900.png)