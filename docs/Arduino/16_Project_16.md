### Project 16: Bluetooth Afstandsbediening

![](./media/img-20240111140012.png)

#### **(1)Beschrijving:**

In de afgelopen decennia is Bluetooth de populairste draadloze communicatiemodule geworden omdat het eenvoudig te gebruiken is en brede toepassingen heeft gevonden in de meeste apparaten die op batterijen werken.

Om zich aan te passen aan de tijd, de realiteit en de behoeften van klanten, is Bluetooth meerdere keren geüpgraded. De afgelopen jaren heeft het veel transformaties ondergaan op het gebied van gegevensoverdrachtssnelheid, stroomverbruik van draagbare apparaten en IoT-apparaten, beveiligingssystemen en andere aspecten. Hier plannen we te leren over DX-BT24 met een Arduino-board.

#### **(2)Parameters:**

- Bluetooth-protocol: Bluetooth Specificatie V5.1 BLE

- Seriële poort verzenden en ontvangen zonder bytelimiet

- Communicatieafstand: 40m (open omgeving)

- Werkfrequentie: 2,4GHz ISM-band

- Modulatiemethode: GFSK (Gaussian Frequency Shift Keying)

- Beveiligingsfuncties: Authenticatie en encryptie

- Ondersteunde services: Central en Peripheral UUIDs FFE0, FFE1, FFE2

- Stroomverbruik: automatische slaapstand, stand-bystroomverbruik 400uA\~800uA, 8,5mA tijdens verzending.
  
- Voeding: 5V

- Bedrijfstemperatuur: –10 tot +65 graden Celsius

#### **(3)Aansluitschema:**

1.STATE is de statustest-pin verbonden met de interne lichtgevende diode en blijft gewoonlijk niet aangesloten.

2.RXD is de seriële poortinterface voor de ontvangstterminal.

3.TXD is de seriële poortinterface voor de verzendterminal.

4.GND is voor aarding.

5.VCC is de positieve pool.

6.EN/BRK: de verbreking hiervan staat voor de verbreking van de Bluetooth-verbinding en blijft gewoonlijk niet aangesloten.

(Opmerking: hier wordt de Bluetooth rechtstreeks verbonden met het V2-shield en **let op de richting**)

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)


#### **(4)APP downloaden en installeren:**

##### **Voor iOS-systeem**

1\. Open de App Store.

2\. Zoek <span style="color: rgb(61, 167, 66);">KeyesRobot</span> in de Apple Store en klik op downloaden.

![](./media/img-20240111141301.png)

3\. Nadat de app is geïnstalleerd, ziet u het volgende pictogram op het bureaublad van uw telefoon.

![](./media/img-20240111141412.png)

**Hoe iOS-telefoon verbinden met de Bluetooth-module:**

1\. Schakel Bluetooth en locatieservices in op de telefoon via instellingen.

![](./media/img-20240111141943.png)

2\. Sta KeyesRobot APP toe om toegang te krijgen tot Bluetooth via instellingen.

![](./media/img-20240111142052.png)

3\. Klik om de KeyesRobot App te openen.

![](./media/img-20240111142140.png)

4\. KeyesRobot App is een universele APP, die wordt toegepast op meerdere keyestudio-robots. Als de interface geen "TANK ROBOT" weergeeft, kunt u op de linker- en rechterknop klikken om "TANK ROBOT" te vinden.

5\. Klik op de <span style="color: rgb(61, 167, 66);">Bluetooth</span>-knop ![](./media/img-20240111142336.png) in de rechterbovenhoek om Bluetooth te scannen.

![](./media/img-20240111142415.png)

6\. U ziet een Bluetooth met de naam <span style="color: rgb(0, 209, 0);">**BT24**</span>, klik op de knop <span style="color: rgb(255, 169, 0);">Connect</span>.

![](./media/img-20240111142536.png)

7\. Als de ingebouwde LED op de Bluetooth-module stopt met knipperen en aan blijft, betekent dit dat uw telefoon succesvol is verbonden met de Bluetooth-module.

![](./media/img-20240111142702.png)


##### **Voor Android-systeem**

1\. Zoek <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> in Google Play, of open de volgende link om de app te downloaden en te installeren.

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Schakel Bluetooth en de locatieservices van de mobiele telefoon in.

![](./media/img-20240111143354.png)

3\. Zoek de KeyesRobot Bluetooth-app via instellingen, klik op de machtigingsopties van de app en schakel locatie- en nabijgelegen apparaatmachtigingen in. (<span style="color: rgb(255, 76, 65);">Opmerking:</span> Sommige mobiele telefoons hebben geen functie voor machtigingen voor nabijgelegen apparaten.)

![](./media/img-20240111143451.png)

4\. Klik om de KeyesRobot App te openen.

![](./media/img-20240111143529.png)

5\. KeyesRobot App is een universele APP, die wordt toegepast op meerdere keyestudio-robots. Als de interface geen "TANK ROBOT" weergeeft, kunt u op de linker- en rechterknop klikken om "TANK ROBOT" te vinden.

6\. Klik op de <span style="color: rgb(61, 167, 66);">Bluetooth</span>-knop ![](./media/img-20240111142336.png) in de rechterbovenhoek om Bluetooth te scannen.

![](./media/img-20240111142415.png)

7\. U ziet een Bluetooth met de naam <span style="color: rgb(0, 209, 0);">**BT24**</span>, klik op de knop <span style="color: rgb(255, 169, 0);">Connect</span>.

![](./media/img-20240111143910.png)

8\. Wanneer uw telefoon succesvol is verbonden met de Bluetooth-module, stopt de ingebouwde LED op de Bluetooth-module met knipperen en blijft aan.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(5)De Bluetooth APP testen:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.1
Bluetooth
http://www.keyestudio.com
*/

char ble_val; // Tekenvariabele (gebruikt om de waarde ontvangen door Bluetooth op te slaan)

void setup() 
{
	Serial.begin(9600);
}

void loop() 
{
    if (Serial.available() > 0) // Bepaal of er gegevens in de seriële poortbuffer zijn
    {
        ble_val = Serial.read(); // Lees de gegevens in de seriële poortbuffer
        Serial.println(ble_val); // Afdrukken
    }
}
```

Upload de code naar het ontwikkelbord, sluit vervolgens de Bluetooth-module aan en verbind daarna de mobiele telefoon met de Bluetooth-module.

Nadat de mobiele telefoon succesvol is verbonden met de Bluetooth-module, klikt u om de Bluetooth APP te openen en klikt u op de knop <span style="color: rgb(0, 252, 255);">Select</span> op de <span style="color: rgb(0, 252, 255);">startpagina</span>.

![](./media/img-20240111144744.png)

De hoofdinterface van de Bluetooth-app wordt weergegeven in de onderstaande afbeelding.

![](./media/img-20240111144859.png)

Nadat de bovenstaande code succesvol is geüpload, opent u de seriële monitor van de Arduino IDE en stelt u de baudrate in op 9600. Klik op het pictogram in de APP-interface en de seriële monitor geeft het commando weer dat door de knop is verzonden.

![](media/805f8ee5c8998a5d6cb8bcef9da09186.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Opmerking: De APP-verbindingsmethode is hetzelfde als hieronder.**</span>
<br>
<b>

#### **(6)Code-uitleg:**

**Serial.available()** vertegenwoordigt het aantal tekens dat momenteel overblijft in de seriële poortbuffer.

Deze functie wordt over het algemeen gebruikt om te bepalen of er gegevens in dit gebied zijn. Wanneer Serial.available()\>0, betekent dit dat de seriële poort gegevens heeft ontvangen en deze kunnen worden gelezen.

**Serial.read()** verwijst naar het uitnemen en lezen van een Byte aan gegevens uit de seriële poortbuffer. Als een apparaat bijvoorbeeld gegevens naar de Arduino verzendt via de seriële poort, kunnen we Serial.read() gebruiken om de verzonden gegevens te lezen.

#### **(7)Uitbreidingsproject:**

Hier gebruiken we het commando dat door de mobiele telefoon wordt verzonden om een LED-lamp aan of uit te zetten. Als we naar het bedradingsschema kijken, is een LED verbonden met de D9-pin.

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">Opmerking: </span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de seriële communicatie van de Bluetooth, waardoor het uploaden van de code kan mislukken.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.2
Bluetooth
http://www.keyestudio.com
*/

int LED = 9;
char ble_val; // Gehele getalvariabele gebruikt om de waarde ontvangen door Bluetooth op te slaan

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);
}

void loop() 
{

    if (Serial.available() > 0) // Bepaal of er gegevens in de seriële poortbuffer zijn
    {
        ble_val = Serial.read(); // Lees gegevens uit de seriële poortbuffer
        Serial.print("DATA RECEIVED:");
        Serial.println(ble_val);
        if (ble_val == 'a') 
        {
            digitalWrite(LED, HIGH);
            Serial.println("led on");
        }
        if (ble_val == 'b') 
        {
            digitalWrite(LED, LOW);
            Serial.println("led off");
        }
    }
}
```

![](media/3577f17c526b1dc55d4f587ef95f2d08.png)

Nadat de bovenstaande code succesvol is geüpload, opent u de seriële monitor van de Arduino IDE en stelt u de baudrate in op 9600. Klik op ![](media/3fd6c998c0f665fb607a5827794b9bfe.png) om de LED te bedienen. Wanneer u erop klikt, wordt het teken a verzonden en gaat de LED aan. Als deze knop opnieuw wordt ingedrukt, gaat de LED uit.

![](./media/img-20240117094533.png)

![](media/b45c3c46391467218fe07003dbb2f3e3.png)

U moet de BT-module verwijderen als u klaar bent met de projecten.