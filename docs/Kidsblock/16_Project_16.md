### Project 16: Bluetooth Afstandsbediening

![](./media/image-20250709134858245.png)

#### **(1)Beschrijving:**

In de afgelopen decennia is Bluetooth de populairste draadloze communicatiemodule geworden omdat het eenvoudig te gebruiken is en wijde toepassingen heeft gevonden in de meeste apparaten die op batterijen werken.

Om aan te passen aan de tijd, realiteit en de behoeften van klanten, is Bluetooth meerdere keren geüpgraded. In de afgelopen jaren heeft het veel transformaties ondergaan op het gebied van gegevensoverdrachtsnelheid, energieverbruik van wearable apparaten en IoT-apparaten, beveiligingssystemen en anderen. Hier plannen we om meer te leren over DX-BT24 met een Arduino-bord.

#### **(2)Parameter:**

- Bluetooth-protocol: Bluetooth Specification V5.1 BLE
- Werkafstand: In een open omgeving, bereik een ultra-lange afstand van 40m
- Communicatie-werkfrequentie: 2,4GHz ISM-band
- Communicatie-interface: UART
- Bluetooth-certificering: in overeenstemming met FCC CE ROHS REACH certificeringsnormen
- Seriële poortparameters: 9600, 8 databits, 1 stopbit, geen pariteitsbit, geen stroomregeling
- Voeding: 5V DC
- Werktemperatuur: –10 tot +65 graden Celsius


#### **(3)Toepassing:**

De DX-BT24-module ondersteunt ook het BT5.1 BLE-protocol, dat rechtstreeks verbinding kan maken met iOS-apparaten met BLE Bluetooth-functie, en ondersteunt het op de achtergrond draaien van programma's. Voornamelijk gebruikt op het gebied van draadloze gegevensoverdracht op korte afstand. Vermijdt omslachtige kabelverbindingen en kan seriële kabels direct vervangen. Succesvolle toepassingsgebieden van BT24-modules:

※ Draadloze Bluetooth-gegevensoverdracht; 

※ Mobiele telefoon, randapparatuur voor computers; 

※ Draagbare POS-apparatuur; 

※ Draadloze gegevensoverdracht van medische apparatuur;

※ Slimme thuisbediening; 

※ Bluetooth-printer; 

※ Bluetooth-afstandsbediening speelgoed; 

※ Gedeelde fietsen;

#### **(4)Beschrijving van pinnen:**

![](media/cd97cf79ff5cdd5bbd78f4cc960d38e5.png)

①STATE：statuspin

②RX：ontvangstpin

③TX：zendpin

④GND：geaard

⑤VCC：voedingspin

⑥EN：inschakelpin

Verbind Bluetooth met het ontwikkelbord

| Uno  | BT24 |
| :--: | :--: |
|  TX  |  RX  |
|  RX  |  TX  |
| VCC  |  5V  |
| GND  | GND  |

#### **(5)Aansluitschema:**

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)

#### **(6)Download APP:**

##### **Voor iOS-systeem**

1\. Open de App Store.

2\. Zoek <span style="color: rgb(61, 167, 66);">KeyesRobot</span> in de Apple Store en klik op downloaden.

![](./media/img-20240111141301.png)

3\. Nadat de app is geïnstalleerd, ziet u het volgende pictogram op het bureaublad van uw telefoon.

![](./media/img-20240111141412.png)

**Hoe iOS-telefoon verbinden met Bluetooth-module:**

1\. Schakel Bluetooth en locatiediensten in op de telefoon via instellingen.

![](./media/img-20240111141943.png)

2\. Sta toe dat de KeyesRobot APP toegang krijgt tot Bluetooth via instellingen.

![](./media/img-20240111142052.png)

3\. Klik om de KeyesRobot App te openen.

![](./media/img-20240111142140.png)

4\. KeyesRobot App is een universele APP, die wordt toegepast op meerdere keyestudio robots. Als de interface "TANK ROBOT" niet weergeeft, kunt u op de linker- en rechterknop klikken om "TANK ROBOT" te vinden.

5\. Klik op de <span style="color: rgb(61, 167, 66);">Bluetooth-knop</span>![](./media/img-20240111142336.png) in de rechterbovenhoek om Bluetooth te scannen

![](./media/img-20240111142415.png)

6\. U ziet een Bluetooth met de naam <span style="color: rgb(0, 209, 0);">**BT24**</span>, klik op de <span style="color: rgb(255, 169, 0);">Verbinden</span>-knop.

![](./media/img-20240111142536.png)

7\. Als de ingebouwde LED op de Bluetooth-module stopt met knipperen en aan blijft, betekent dit dat uw telefoon succesvol verbonden is met de Bluetooth-module.

![](./media/img-20240111142702.png)


##### **Voor Android-systeem**

1\. Zoek <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> in Google Play, of open de volgende link om de app te downloaden en te installeren. 

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Schakel de Bluetooth en de locatiediensten van de mobiele telefoon in

![](./media/img-20240111143354.png)

3\. Zoek de KeyesRobot Bluetooth-app in de instellingen, klik op de machtigingsopties van de app, en
schakel Locatie- en nabijgelegen apparaten-machtigingen in.(<span style="color: rgb(255, 76, 65);">Opmerking:</span> Sommige mobiele telefoons hebben geen functie voor nabijgelegen apparaten-machtigingen.)

![](./media/img-20240111143451.png)

4\. Klik om de KeyesRobot App te openen.

![](./media/img-20240111143529.png)

5\. KeyesRobot App is een universele APP, die wordt toegepast op meerdere keyestudio robots. Als de interface "TANK ROBOT" niet weergeeft, kunt u op de linker- en rechterknop klikken om "TANK ROBOT" te vinden.

6\. Klik op de <span style="color: rgb(61, 167, 66);">Bluetooth-knop</span>![](./media/img-20240111142336.png) in de rechterbovenhoek om Bluetooth te scannen

![](./media/img-20240111142415.png)

7\. U ziet een Bluetooth met de naam <span style="color: rgb(0, 209, 0);">**BT24**</span>, klik op de <span style="color: rgb(255, 169, 0);">Verbinden</span>-knop.![](./media/img-20240111143910.png)

8\. Wanneer uw telefoon succesvol verbonden is met de Bluetooth-module, stopt de ingebouwde LED op de Bluetooth-module met knipperen en blijft aan.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(7)BT Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/19a90ffb7565966f7d40462abed876a7.png)

（5）![](media/c8228c5040a43ae322612b312c995ac3.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth-seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/4766ada3bf48bb35522f292d9352bb78.png)


Upload de code naar het ontwikkelbord, sluit daarna de Bluetooth-module aan, en verbind vervolgens de mobiele telefoon met de Bluetooth-module.

Nadat de mobiele telefoon succesvol verbonden is met de Bluetooth-module, klik om de Bluetooth APP te openen en klik op de <span style="color: rgb(0, 252, 255);">Selecteer</span>-knop op de <span style="color: rgb(0, 252, 255);">startpagina</span>.

![](./media/img-20240111144744.png)

De hoofdinterface van de Bluetooth-app is weergegeven in de onderstaande afbeelding.

![](./media/img-20240111144859.png)

Klik op ![Img](./media/img-20240111171312.png) en stel de baudrate in op 9600. Klik op het pictogram in de APP-interface en de seriële monitor geeft het commando weer dat door de knop is verzonden.

![](media/f5004f5334fb4885ac0096f99e4133f9.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Opmerking: De APP-verbindingsmethode is hetzelfde als hieronder.**</span>
<br>
<br>


#### **(8)Uitbreidingsoefening:**

In het bovenstaande project ontvangt Bluetooth het signaal dat door de mobiele telefoon is verzonden en geeft het weer op de seriële poort van het ontwikkelbord. Hier gebruiken we het commando dat door de mobiele telefoon is verzonden om een LED aan of uit te zetten. Bekijk het aansluitschema, een LED is verbonden met pin D9,

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)


U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/aa78663af261ff1d9bc8ffa6ad7a65bc.png)

(5）![](media/c8228c5040a43ae322612b312c995ac3.png)

（6）![](media/4164bcf66d3d2415f43a0efcd1ce4243.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth-seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/91fd9d6f85e291fe90a63e5095ed7f44.png)

Nadat de bovenstaande code succesvol is geüpload. Klik op ![](media/d5e59839bafc63f8b35c78c60573d1fc.png) om de LED te bedienen.

![](./media/img-20240117094418.png)


Nadat u het BT-project heeft voltooid, verwijdert u het.