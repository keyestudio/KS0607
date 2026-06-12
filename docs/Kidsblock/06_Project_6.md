### Project 6: Ultrasoonse Sensor

#### **(1)Beschrijving:**

![](media/0180b169a1c3b228394b43df704fac32.png)

De HC-SR04 ultrasoonse sensor gebruikt sonar om de afstand tot een object te bepalen, vergelijkbaar met hoe vleermuizen dat doen. Het biedt uitstekende contactloze afstandsdetectie met hoge nauwkeurigheid en stabiele metingen in een eenvoudig te gebruiken behuizing. Het wordt geleverd met ultrasone zender- en ontvangermodules.

De HC-SR04 of de ultrasoonse sensor wordt gebruikt in een breed scala aan elektronica-projecten voor het maken van obstakels detectie en afstandsmeting, evenals diverse andere toepassingen. Hier hebben we de eenvoudige methode beschreven om de afstand te meten met Arduino en een ultrasoonse sensor, en hoe je de ultrasoonse sensor met Arduino kunt gebruiken.

![](./media/image-20250709133626194.png)

#### **(2)Parameters:**

- Voedingsspanning: +5V DC

- Ruststroomverbruik: \<2mA

- Werkstroom: 15mA

- Effectieve hoek: \<15°

- Meetbereik: 2cm – 400 cm

- Resolutie: 0.3 cm

- Meethoek: 30 graden

- Breedte triggerpuls: 10uS

#### **(3)Het werkingsprincipe van de ultrasoonse sensor:**

Zoals op de bovenstaande afbeelding te zien is, lijkt het op twee ogen. De ene is het zenduiteinde, de andere is het ontvangsteinde.

De ultrasoonse module zendt ultrasoonse golven uit nadat een signaal is getriggerd. Wanneer de ultrasoonse golven een object tegenkomen en worden teruggekaatst, geeft de module een echoSignaal uit, zodat de afstand tot het object kan worden bepaald op basis van het tijdverschil tussen het triggersignaal en het echosignaal.

Hierbij is t de tijd vanaf het moment dat het uitgezonden signaal het obstakel ontmoet tot het terugkeert. De voortplantingssnelheid van geluid in de lucht is ongeveer 343m/s, en afstand = snelheid * tijd. Omdat de ultrasoonse golf echter naar het obstakel reist en terug, vertegenwoordigt de tijd tweemaal de afstand. Daarom moet het door 2 worden gedeeld. De door de **ultrasoonse golf gemeten afstand = (snelheid * tijd) / 2**.

1. Gebruiksmethode en tijdsdiagram van de ultrasoonse module:

2. Stel de vertragingstijd van de Trig-pin van de SR04 in op minimaal 10μs, wat het triggert om de afstand te detecteren.

3. Na het triggeren zendt de module automatisch acht ultrasoonse pulsen van 40KHz uit en detecteert of er een signaalterugkeer is. Deze stap wordt automatisch door de module uitgevoerd.

4. Als het signaal terugkeert, zal de Echo-pin een hoog niveau uitvoeren, en de duur van het hoge niveau is de tijd van de verzending van de ultrasoonse golf tot de terugkeer.

![](media/image-20230525110337646.png)

Schakelschema van de ultrasoonse sensor:

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4)Aansluitingsschema:**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Bedrading opmerking:</span> De VCC-pin van de ultrasoonse sensormodule is verbonden met de 5v(V) van het Keyestudio 8833 motoraandrijving uitbreidingsbord, de Trig-pin is verbonden met digitaal D12, de Echo-pin is verbonden met digitaal D13, en de Gnd-pin is verbonden met Gnd(G);

#### **(5)Testcode:**

Je kunt ook blokken slepen om je code te bewerken, zoals hieronder weergegeven.

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/128e0b4ee7d3448410d72312175bc6da.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/a6df8829b69f7faed26a73d01da8d50d.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/eca0805413af12957d319c706d3e7cdb.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth-seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/569aff5ff2cbd2f3605f217ebb5ed50b.png)

#### **(6)Testresultaten:**

Upload de testcode naar het ontwikkelbord, open de seriële monitor en stel de baudrate in op 9600. De gedetecteerde afstand wordt weergegeven in cm en inches. Wanneer je de ultrasoonse sensor met je hand blokkeert, wordt de weergegeven afstandswaarde kleiner.

![](media/4f77acbf5b226e20e3cdd70c0f90602e.png)

#### **(7)Uitbreidingsoefening:**

We hebben zojuist de door de ultrasoonse sensor gemeten afstand weergegeven. Hoe zit het met het aansturen van een LED met de gemeten afstand? Laten we het proberen en een LED-lichtmodule verbinden met de D9-pin.

![](media/291ac1db0f38418772d11bb1786b7314.png)


Je kunt ook blokken slepen om je code te bewerken, zoals hieronder weergegeven.

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/49d5523ae565e1d4dfc3504d1e1748d4.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/8d5fc923f5ded5305f36b1379c1ba38e.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/a6205e42e005084c33c247fe564bdcad.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth-seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/065eac0ad9cfa8f07aeb5e648698bdb5.png)

Upload de testcode naar het ontwikkelbord, beweeg je hand dichter naar de ultrasoonse sensor en controleer of de LED aangaat.

![](./media/img-20240117092413.png)