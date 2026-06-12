### Project 14: Lijnvolgend Pantservoertuig


#### **(1)Beschrijving:**

Het vorige project liet zien hoe je de slimme auto kunt beperken om binnen een bepaalde ruimte te bewegen. In dit project gebruiken we de eerder geleerde kennis om er een lijnvolgende slimme auto van te maken. In het experiment gebruiken we de lijnvolgsensor om te detecteren of er een zwarte lijn in de buurt van de slimme auto is, en vervolgens regelen we de rotatie van de twee motoren op basis van de detectieresultaten, zodat de slimme auto langs de zwarte lijn beweegt.

De specifieke logica van de slimme auto wordt weergegeven in de onderstaande tabel:

|               Sensor               |                          Detectie                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Lijnvolgsensor in het midden | Zwarte lijn gedetecteerd: hoog niveau<br />Witte lijn gedetecteerd: laag niveau |
|  Lijnvolgsensor aan de linkerkant  | Zwarte lijn gedetecteerd: hoog niveau<br />Witte lijn gedetecteerd: laag niveau |
| Lijnvolgsensor aan de rechterkant  | Zwarte lijn gedetecteerd: hoog niveau<br />Witte lijn gedetecteerd: laag niveau |

|                         Conditie 1                          |                         Conditie 2                          |   Beweging   |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------: |
| Lijnvolgsensor <br />in het midden <br />detecteert de zwarte lijn | Lijnvolgsensor aan de linkerkant detecteert de zwarte lijn<br />die aan de rechterkant detecteert witte lijnen | Draai links  |
| Lijnvolgsensor <br />in het midden <br />detecteert de zwarte lijn | Lijnvolgsensor aan de linkerkant detecteert witte lijnen<br />die aan de rechterkant detecteert de zwarte lijn | Draai rechts |
| Lijnvolgsensor <br />in het midden <br />detecteert de zwarte lijn | Beide linker- en rechter lijnvolgsensoren detecteren witte lijnen<br />Beide linker- en rechter lijnvolgsensoren detecteren de zwarte lijn | Vooruit rijden |
| Lijnvolgsensor<br />in het midden <br />detecteert witte lijnen | Lijnvolgsensor aan de linkerkant detecteert de zwarte lijn<br />die aan de rechterkant detecteert witte lijnen | Draai links  |
| Lijnvolgsensor<br />in het midden <br />detecteert witte lijnen | Lijnvolgsensor aan de linkerkant detecteert witte lijnen<br />die aan de rechterkant detecteert de zwarte lijn | Draai rechts |
| Lijnvolgsensor<br />in het midden <br />detecteert witte lijnen | Beide linker- en rechter lijnvolgsensoren detecteren witte lijnen<br />Beide linker- en rechter lijnvolgsensoren detecteren de zwarte lijn |     Stoppen     |

#### **(2)Stroomdiagram:**

![](media/wps11.png)

#### **(3)Aansluitingsschema:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Testcode:**

Je kunt ook blokken slepen om je code te bewerken, zoals hieronder weergegeven

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

（7）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（8）![](media/fec93c7b8b089de709fd50575931519c.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Let op:**</span> Sluit de Bluetooth-module niet aan voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er mogelijk conflicten kunnen ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden mislukt.)

![](media/294ae4c01072e34b58a334912c90083a.png)


#### **(5)Testresultaten:**

Na het succesvol uploaden van de testcode en het inschakelen van de voeding, beweegt de slimme auto langs de zwarte lijn.

![](./media/img-20240117094129.png)