### Project 15: IR Afstandsbediening Tank

![](./media/image-20250709134800790.png)

#### **(1)Beschrijving:**

Infrarood afstandsbediening is een van de meest voorkomende toepassingen voor afstandsbediening, te vinden in elektrische motoren, elektrische ventilatoren en vele andere huishoudelijke apparaten. In dit project gebruiken we de eerder opgedane kennis om een infrarood afstandsbediende slimme auto te maken.

In les 9 hebben we de overeenkomstige toetswaarde van elke toets van de infrarood afstandsbediening getest. In dit project kunnen we de code (toetswaarde) instellen zodat de bijbehorende knop de bewegingen van de slimme auto bestuurt en de bewegingspatronen worden weergegeven op de 8X16 LED-dotmatrix.

De specifieke logica van de slimme auto wordt weergegeven in de onderstaande tabel:

|                 Ultrasone toets                 | Toetswaarde | Instructies van toetsen                                      |
| :---------------------------------------------: | :---------: | ------------------------------------------------------------ |
| ![](media/b11dc5ffa6cccebc6088e5d557d76daf.png) |   FF629D    | Vooruit rijden（PWM instellen op 200）<br />het patroon van vooruit rijden weergeven |
| ![](media/ae8110034aacb083151cfd882ee599ba.png) |   FFA857    | Achteruit rijden（PWM instellen op 200）<br />het patroon van achteruit rijden weergeven |
| ![](media/bce9cba2c6d2465fbcce570ad4210eba.png) |   FF22DD    | Links afslaan<br />het patroon "STOP" weergeven              |
| ![](media/ad907a618af86f30d52986bbbd57ba76.png) |   FFC23D    | Rechts afslaan<br />het patroon van links afslaan weergeven  |
| ![](media/9716a4ed61a4064d2f47a7b73eccaf87.png) |   FF02FD    | Stoppen<br />het patroon "STOP" weergeven                    |

**Begininstelling: 8X16 LED-dotmatrix toont het patroon"![](media/dc59c5fcb4fcf6af4d4a5ebb14b7a919.png)"**



#### **(2)Stroomdiagram:**

![](media/wps121.png)

#### **(3)Aansluitingsschema:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span>

GND, VCC, SDA en SCL van het 8x16 LED-paneel zijn verbonden met G（GND), V（VCC). A4 en A5 van het uitbreidingsbord.

Omdat het 8833-bord de IR-ontvanger integreert, hoeft u deze niet aan te sluiten. De pinnen van de IR-ontvanger zijn G（GND), V（VCC) en D3.

#### **(4)Testcode:**

U kunt blokken bewerken om uw code samen te stellen

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/a9042e77ebe3009fbb7653bef3429b66.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6）![](media/51e30aa2aca3a7da67ee4f0f81c7dad1.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/7ab62148fa2a23259b8039475978d8fc.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/fae6c22640ced038daca9cb6721ab95e.png)

#### **(5)Testresultaten:**

Nadat de testcode succesvol is geüpload en de stroom is ingeschakeld, kan de slimme auto worden bestuurd met de IR-afstandsbediening en toont de 8\*16 de bijbehorende patronen van de bewegingen.

![](./media/img-20240117094223.png)