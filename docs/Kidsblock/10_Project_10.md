### Project 10: Lichtvolgende Tank


#### **(1)Beschrijving:**

In vorige projecten hebben we het gebruik van verschillende sensoren, modules en uitbreidingsborden op de slimme auto in detail besproken. Nu gaan we verder met de projecten van de slimme auto. De lichtvolgende slimme auto is, zoals de naam al aangeeft, een slimme auto die het licht kan volgen.

We kunnen de kennis uit de projecten over de lichtweerstand en de motoraandrijving combineren om een lichtzoekende slimme auto te maken. In dit project gebruiken we twee lichtweerstandmodules om de lichtintensiteit aan de linker- en rechterkant van de slimme auto te meten, de bijbehorende analoge waarden te lezen en vervolgens de rotatie van de twee motoren te besturen op basis van deze twee gegevens, zodat de bewegingen van de slimme auto worden geregeld.

De specifieke logica van de lichtvolgende slimme auto wordt hieronder weergegeven.

![image-20230525113331422](media/image-20230525113331422.png)

#### **(2)Stroomdiagram:**

![](media/wps117.png)

#### **(3)Aansluitingsschema:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Opmerking: </span>De pinnen "G", "V" en S van de linker lichtweerstandmodule zijn verbonden met G (GND), V (VCC) en A1 respectievelijk;

De pinnen "G", "V" en S van de rechter lichtweerstandmodule zijn verbonden met G (GND), V (VCC) en A2 respectievelijk.

De 4-pins kabel is gemarkeerd met A, A1, B1 en B. De rechter achtermotor is verbonden met poort B van het 8833 motorrijder-uitbreidingsbord en de linker voormotor is verbonden met poort A van het 8833 motorrijder-uitbreidingsbord.

#### **(4)Testcode:**


U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.

（1）![](media/9352e6447f9648efddc7d5a748618332.png)

（2）![](media/1d99d71f5fe52dd2145cb11d75cabb21.png)

（3）![](media/5004e509325dffb32c05afe25abedfc9.png)

（4）![](media/6c6f0492f657c4c78a0497bb86519561.png)

（5）![](media/b8fc70fa8b3f335dcdf0c8ad9ed998c6.png)

（6）![](media/9eb0e93fbd43aa24f2ce656191f7cd79.png)

(7) ![](media/9f023e6f571e597e661a8d71a7f803cb.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">Opmerking:</span> De drempelwaarde 650 in de code kan naar behoefte worden aangepast op basis van de specifieke lichtintensiteit.

Sluit de Bluetooth-module niet aan voordat de code wordt geüpload, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er mogelijk conflicten ontstaan met de seriële communicatie van de Bluetooth, waardoor het uploaden van de code kan mislukken.)

![](media/6300174b85f63c05dbdcb3b77188f9dc.png)


#### **(5)Testresultaten:**

Na het succesvol uploaden van de testcode, de bedrading aansluiten, de DIP-schakelaar naar de ON-stand zetten en de stroom inschakelen, volgt de slimme auto het licht om te bewegen.

![](./media/img-20240117093758.png)