### Project 6: Ultrasone Sensor

#### **(1) Beschrijving:**

![](media/0180b169a1c3b228394b43df704fac32.png)

De HC-SR04 ultrasone sensor gebruikt sonar om de afstand tot een object te bepalen, net zoals vleermuizen dat doen. Het biedt uitstekende contactloze afstandsdetectie met hoge nauwkeurigheid en stabiele metingen in een gebruiksvriendelijk pakket. Het wordt geleverd compleet met ultrasone zender- en ontvangstmodules.

De HC-SR04 of de ultrasone sensor wordt gebruikt in een breed scala aan elektronicaprojecten voor het maken van obstakeldectectie en afstandsmeettoepassingen, evenals diverse andere toepassingen. Hier hebben we de eenvoudige methode gebracht om de afstand te meten met Arduino en de ultrasone sensor en hoe je de ultrasone sensor met Arduino gebruikt.

![](./media/image-20250709105712919.png)

#### **(2) Parameters:**

- Voedingsspanning: +5V DC

- Quiescent stroom: \<2mA

- Werkstroom: 15mA

- Effectieve hoek: \<15°

- Meetbereik: 2cm – 400 cm

- Resolutie: 0,3 cm

- Meethoek: 30 graden

- Triggerpuls breedte ingang: 10uS


#### **(3) Het principe van de ultrasone sensor:**

Zoals te zien is op de bovenstaande afbeelding, lijkt het op twee ogen. Één is het zendende uiteinde, het andere is het ontvangende uiteinde.

De ultrasone module zendt de ultrasone golven uit na het triggeren van een signaal. Wanneer de ultrasone golven een object tegenkomen en worden teruggekaatst, geeft de module een echosigsignaal uit, zodat de afstand tot het object kan worden bepaald op basis van het tijdsverschil tussen het triggersignaal en het echosignaal.

De t is de tijd dat het uitgestuurde signaal een obstakel ontmoet en terugkeert. De voortplantingssnelheid van geluid in de lucht is ongeveer 343m/s, en afstand = snelheid * tijd. De ultrasone golf wordt echter uitgestuurd en keert terug, wat 2 keer de afstand is. Daarom moet het worden gedeeld door 2, de afstand gemeten door **ultrasone golf = (snelheid * tijd)/2**

1. Gebruiksmethode en timingdiagram van de ultrasone module:

2. Stel de vertragingstijd van de Trig-pin van de SR04 in op minimaal 10μs, waarmee de afstandsmeting wordt getriggerd.

3. Na het triggeren stuurt de module automatisch acht 40KHz ultrasone pulsen uit en detecteert of er een signaal terugkomt. Deze stap wordt automatisch door de module uitgevoerd.

4. Als het signaal terugkeert, zal de Echo-pin een hoog niveau uitvoeren, en de duur van het hoge niveau is de tijd van de verzending van de ultrasone golf tot de terugkeer ervan.

![](media/image-20230426172540424.png)

Schakelschema van de ultrasone sensor:

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4) Aansluitingsdiagram:**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span> De pinnen VCC, Trig, Echo en Gnd van de ultrasone sensor zijn respectievelijk verbonden met 5v(V), 12(S), 13(S) en Gnd(G) van het shield.

#### **(5) Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook seriële communicatie gebruikt, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden mislukt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.1
Ultrasonic sensor
http://www.keyestudio.com
*/

int trigPin = 12; // Pin Trig is verbonden met 12
int echoPin = 13; // Pin Echo is verbonden met 13
long duration, cm, inches;

void setup() 
{
    // Seriële poort starten
    Serial.begin(9600);// Baudrate instellen op 9600
    // Invoer en uitvoer definiëren
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
}

void loop() 
{
    // Geef eerst een korte lage puls om een schone hoge puls te garanderen
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// Geef minimaal 10us hoog niveau trigger
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // De tijd op hoog niveau is gelijk aan het tijdsverschil tussen verzending en terugkeer van het ultrasone geluid
    duration = pulseIn(echoPin, HIGH);
    // Omzetten naar afstand
    cm = (duration / 2) / 29.1; // omzetten naar centimeters
    inches = (duration / 2) / 74; // omzetten naar inches
    // Seriële poort print uit
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    delay(50);
}
```

#### **(6) Testresultaten:**

Upload de testcode naar het ontwikkelbord, open de seriële monitor en stel de baudrate in op 9600. De gemeten afstand wordt weergegeven in cm en inches. Wanneer u de ultrasone sensor met uw hand blokkeert, wordt de weergegeven afstandswaarde kleiner.

![](media/2ff018e5d9d631a32fce99eb9b4778be.png)

#### **(7) Codeuitleg:**

**int trigPin = 12;** deze pin is gedefinieerd om ultrasone golven te verzenden, over het algemeen uitvoer.

**int echoPin = 13;** dit is gedefinieerd als de ontvangstpin, over het algemeen invoer

**cm = (duration/2) / 29.1; inches = (duration/2) / 74; met 0.0135**

We kunnen de afstand berekenen met behulp van de volgende formule:

afstand = (reistijd/2) x geluidssnelheid

De geluidssnelheid is: 343m/s = 0,0343 cm/uS = 1/29,1 cm/uS

Of in inches: 13503,9in/s = 0,0135in/uS = 1/74in/uS

We moeten de reistijd door 2 delen omdat we er rekening mee moeten houden dat de golf werd verzonden, het object raakte en vervolgens terugkeerde naar de sensor.

#### **(8) Uitbreidingsoefening:**


We hebben zojuist de afstand gemeten die door de ultrasone sensor wordt weergegeven. Hoe zit het met het besturen van de LED met de gemeten afstand? Laten we het proberen en een LED-lichtmodule aansluiten op de D9-pin.

![](media/291ac1db0f38418772d11bb1786b7314.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook seriële communicatie gebruikt, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden mislukt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.2
Ultrasonic LED
http://www.keyestudio.com
*/

int trigPin = 12; // Trig is verbonden met 12
int echoPin = 13; // Echo is verbonden met 13
int LED = 9;
long duration, cm, inches;

void setup() 
{
    // Seriële poort starten
    Serial.begin (9600);// baudrate instellen op 9600
    // invoer en uitvoer definiëren
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(LED, OUTPUT);
}

void loop() 
{
    // Geef eerst een korte lage puls om een schone hoge puls te garanderen
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// Geef minimaal 10us hoog niveau trigger
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // De duur van het hoge niveau is de tijd van het uitzenden tot de terugkeer van de ultrasone golf
    duration = pulseIn(echoPin, HIGH);
    // omzetten naar afstand
    cm = (duration / 2) / 29.1; // omzetten naar centimeters
    inches = (duration / 2) / 74; // omzetten naar inches
    // seriële poort print uit
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    if (cm >= 2 && cm <= 10) 
    {
    	digitalWrite(LED, HIGH);// LED aanzetten
    } 
    else 
    {
    	digitalWrite(LED, LOW); // LED uitzetten
    }
    delay(50);
}
```

Upload de testcode naar het ontwikkelbord en blokkeer de ultrasone sensor met uw hand, controleer dan of de LED aan is.

![](./media/img-20240117090734.png)