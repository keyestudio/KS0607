### Project 8: Motoraansturing en Snelheidsregeling

#### **(1)Beschrijving:**

Er zijn veel manieren om motoren aan te sturen. Onze slimme auto gebruikt de meest gebruikelijke oplossing genaamd L298P. L298P, geproduceerd door STMicroelectronics, is een uitstekende aandrijfchip speciaal ontworpen voor het aansturen van hoogvermogen motoren.

Het kan DC-motoren, twee-fase en vier-fase motoren direct aansturen met een aandrijfstroom die 2A bereikt. En de uitgangsaansluiting van de motor maakt gebruik van 8 hoge-snelheid Schottky-diodes als bescherming.

We hebben een uitbreidingsbord ontworpen op basis van het L298P-circuit, waarvan het gelaagde ontwerp direct in het UNO R3-bord gestoken kan worden voor gebruik, waardoor de technische moeilijkheden voor gebruikers bij het gebruiken en aansturen van de motor worden verminderd.

Stapel het uitbreidingsbord op het bord, sluit de BAT aan, zet de DIP-schakelaar naar het ON-uiteinde, en voed het uitbreidingsbord en het UNO R3-bord tegelijkertijd via externe voeding.

Om het bedraden te vergemakkelijken, is het uitbreidingsbord uitgerust met anti-omgekeerde interface (PH2.0 -2P -3P -4P -5P) en kan het dus direct worden aangesloten met motoren, voeding en sensoren/modules.

De Bluetooth-interface van het aandrijf-uitbreidingsbord is volledig compatibel met de Keyestudio HM-10 Bluetooth-module. Daarom hoeven we alleen de HM-10 Bluetooth-module in de bijbehorende interface te steken bij het aansluiten.

Tegelijkertijd gebruikt het aandrijf-uitbreidingsbord ook 2.54 pin-headers om enkele beschikbare digitale poorten en analoge poorten uit te breiden, zodat u andere sensoren kunt blijven toevoegen en uitbreidingsexperimenten kunt uitvoeren.

Het uitbreidingsbord kan worden aangesloten op 4 DC-motoren. In de standaard jumper-cap verbindingsmodus zijn de A- en A1-, B- en B1-interface-motoren parallel aangesloten, en hun bewegingspatroon is hetzelfde. 8 jumper-caps kunnen worden gebruikt om de rotatierichting van de 4 motorinterfaces te regelen.

Wanneer de twee jumper-caps voor de motor A-interface bijvoorbeeld worden veranderd van een horizontale verbinding naar een verticale verbinding, is de rotatierichting van motor A nu tegengesteld aan de oorspronkelijke rotatierichting.

![](media/image-20230427081635216.png)

![](media/5381c98d3be6da099ce43e841b8f736b.png)

#### **(2)Parameters：**

- Invoerspanning logisch deel: DC 5V

- Invoerspanning aandrijvingsdeel: DC 7-12V

- Werkstroom logisch deel: ≤36mA

- Werkstroom aandrijvingsdeel: ≤ 2A

- Maximaal dissipatiemogen: 25W (T=75℃)

- Ingangsniveau regelsignaal:
  
  ​	Hoog niveau: 2.3V ≤ Vin ≤ 5V
  
  ​	Laag niveau: 0V ≤ Vin ≤ 1.5V

- Werktemperatuur: -25℃～＋130℃

#### **(3)De robot laten bewegen**

De richtingspin van motor A is D2, de snelheidsregelingspin is D5; de richtingspin van motor B is D4 en de snelheidsregelingspin is D6.

Volgens de onderstaande tabel kunnen we zien hoe we de beweging van de robot kunnen regelen door de rotatie van twee motoren te besturen via de digitale poorten en PWM-poorten. Hierbij is het bereik van de PWM-waarde 0-255. Hoe groter de waarde, hoe sneller de motor roteert.

|     Functie      |  D4  | D6（PWM） | Motor （links）B |  D2  | D5（PWM） | Motor（Rechts）A |
| :--------------: | :--: | :-------: | :--------------: | :--: | :-------: | :--------------: |
|  Vooruit rijden  | HIGH |  255-200  |  Draait Links    | HIGH |  255-200  |  Draait Links    |
|  Achteruit gaan  | LOW  |    200    |  Draait Rechts   | LOW  |    200    |  Draait Rechts   |
|  Links draaien   | LOW  |    200    |  Draait Rechts   | HIGH |  255-200  |  Draait Links    |
|  Rechts draaien  | HIGH |  255-200  |  Draait Links    | LOW  |    200    |  Draait Rechts   |
|     Stoppen      | LOW  |     0     |      Stop        | LOW  |     0     |      Stop        |




#### **(4)Aansluitingsschema:**

![](media/3e53cf19ea5f85a931b955453b86304b.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span>

De 4-pins connector is gemarkeerd met A, A1, B1 en B. De rechter achtermotor is verbonden met B van het 8833-bord en de linker voormotor is verbonden met de A-poort.

#### **(5)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Verbind de Bluetooth-module niet voordat u de code uploadt, omdat het uploaden van de code ook seriële communicatie gebruikt, en er mogelijk conflicten zijn met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.1
motor driver
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // Definieer de richtingsregelingspin van de linker motor
#define ML_PWM 6 // Definieer de PWM-regelingspin van de linker motor
#define MR_Ctrl 2 // Definieer de richtingsregelingspin van de rechter motor
#define MR_PWM 5 // Definieer de PWM-regelingspin van de rechter motor

void setup()
{
    pinMode(ML_Ctrl, OUTPUT);// Definieer de richtingsregelingspin van de linker motor als OUTPUT
    pinMode(ML_PWM, OUTPUT);// Definieer de PWM-regelingspin van de linker motor als OUTPUT
    pinMode(MR_Ctrl, OUTPUT);// Definieer de richtingsregelingspin van de rechter motor als OUTPUT
    pinMode(MR_PWM, OUTPUT);// Definieer de PWM-regelingspin van de rechter motor als OUTPUT
}

void loop()
{
    // vooruit
    digitalWrite(ML_Ctrl, HIGH); // Stel richtingsregelingssnelheid van de linker motor in op HIGH
    analogWrite(ML_PWM, 55); // PWM-regelingssnelheid van de linker motor is 55
    digitalWrite(MR_Ctrl, HIGH); // Stel richtingsregelingssnelheid van de rechter motor in op HIGH
    analogWrite(MR_PWM, 55); // PWM-regelingssnelheid van de rechter motor is 55
    delay(2000);// vertraging van 2s

    // achteruit
    digitalWrite(ML_Ctrl, LOW); // Stel richtingsregelingssnelheid van de linker motor in op LOW
    analogWrite(ML_PWM, 200); // PWM-regelingssnelheid van de linker motor is 200
    digitalWrite(MR_Ctrl, LOW); // Stel richtingsregelingssnelheid van de rechter motor in op LOW
    analogWrite(MR_PWM, 200); // PWM-regelingssnelheid van de rechter motor is 200
    delay(2000);// vertraging van 2s

    // links draaien
    digitalWrite(ML_Ctrl, LOW); // Stel richtingsregelingssnelheid van de linker motor in op LOW
    analogWrite(ML_PWM, 200); // PWM-regelingssnelheid van de linker motor is 200
    digitalWrite(MR_Ctrl, HIGH); // Stel richtingsregelingssnelheid van de rechter motor in op HIGH
    analogWrite(MR_PWM, 55); // PWM-regelingssnelheid van de rechter motor is 55
    delay(2000);// vertraging van 2s

    // rechts draaien
    digitalWrite(ML_Ctrl, HIGH); // Stel richtingsregelingssnelheid van de linker motor in op HIGH
    analogWrite(ML_PWM, 55); // PWM-regelingssnelheid van de linker motor is 55
    digitalWrite(MR_Ctrl, LOW); // Stel richtingsregelingssnelheid van de rechter motor in op LOW
    analogWrite(MR_PWM, 200); // PWM-regelingssnelheid van de rechter motor is 200
    delay(2000);// vertraging van 2s

    // stoppen
    digitalWrite(ML_Ctrl, LOW);
    analogWrite(ML_PWM, 0); // PWM-regelingssnelheid van de linker motor is 0
    digitalWrite(MR_Ctrl, LOW);
    analogWrite(MR_PWM, 0); // PWM-regelingssnelheid van de rechter motor is 0
    delay(2000);// vertraging van 2s
}
```

#### **(6)Testresultaten:**

Na het bedraden volgens het schema, het uploaden van de testcode en het inschakelen.

![](./media/img-20240117082646.png)

rijdt de slimme auto 2s vooruit, 2s achteruit, 2s naar links, 2s naar rechts en stopt 2s en herhaalt deze volgorde.

#### **(7)Code-uitleg:**

**digitalWrite(ML_Ctrl,LOW);**

De wisseling tussen hoge en lage niveaus kan motoren clockwise of anticlockwise laten roteren. Algemene digitale pinnen kunnen worden gebruikt om deze bewegingen te besturen.

**analogWrite(ML_PWM,200);**

De snelheidsregeling van de motor wordt gerealiseerd door PWM, en de pin die de snelheid van de motor regelt moet de PWM-pin van Arduino zijn.

#### **(8)Uitbreidingsproject:**

We passen de snelheid van motoren aan door PWM te regelen en de bedrading blijft hetzelfde.

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Verbind de Bluetooth-module niet voordat u de code uploadt, omdat het uploaden van de code ook seriële communicatie gebruikt, en er mogelijk conflicten zijn met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.2
motor driver pwm
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // Definieer de richtingsregelingspin van de linker motor
#define ML_PWM 6 // Definieer de PWM-regelingspin van de linker motor
#define MR_Ctrl 2 // Definieer de richtingsregelingspin van de rechter motor
#define MR_PWM 5 // Definieer de PWM-regelingspin van de rechter motor

void setup() 
{
    pinMode(ML_Ctrl, OUTPUT);// Definieer de richtingsregelingspin van de linker motor als OUTPUT
    pinMode(ML_PWM, OUTPUT);// Definieer de PWM-regelingspin van de linker motor als OUTPUT
    pinMode(MR_Ctrl, OUTPUT);// Definieer de richtingsregelingspin van de rechter motor als OUTPUT
    pinMode(MR_PWM, OUTPUT);// Definieer de PWM-regelingspin van de rechter motor als OUTPUT
}

void loop() 
{
    // vooruit
    digitalWrite(ML_Ctrl, HIGH); // Stel richtingsregelingssnelheid van de linker motor in op HIGH
    analogWrite(ML_PWM, 155); // PWM-regelingssnelheid van de linker motor is 155
    digitalWrite(MR_Ctrl, HIGH); // Stel richtingsregelingssnelheid van de rechter motor in op HIGH
    analogWrite(MR_PWM, 155); // PWM-regelingssnelheid van de rechter motor is 155
    delay(2000);// vertraging van 2s

    // achteruit
    digitalWrite(ML_Ctrl, LOW); // Stel richtingsregelingssnelheid van de linker motor in op LOW
    analogWrite(ML_PWM, 100); // PWM-regelingssnelheid van de linker motor is 100
    digitalWrite(MR_Ctrl, LOW); // Stel richtingsregelingssnelheid van de rechter motor in op LOW
    analogWrite(MR_PWM, 100); // PWM-regelingssnelheid van de rechter motor is 100
    delay(2000);// vertraging van 2s

    // links
    digitalWrite(ML_Ctrl, LOW); // Stel richtingsregelingssnelheid van de linker motor in op LOW
    analogWrite(ML_PWM, 100); // PWM-regelingssnelheid van de linker motor is 100
    digitalWrite(MR_Ctrl, HIGH); // Stel richtingsregelingssnelheid van de rechter motor in op HIGH
    analogWrite(MR_PWM, 155); // PWM-regelingssnelheid van de rechter motor is 155
    delay(2000);// vertraging van 2s

    // rechts
    digitalWrite(ML_Ctrl, HIGH); // Stel richtingsregelingssnelheid van de linker motor in op HIGH
    analogWrite(ML_PWM, 155); // PWM-regelingssnelheid van de linker motor is 155
    digitalWrite(MR_Ctrl, LOW); // Stel richtingsregelingssnelheid van de rechter motor in op LOW
    analogWrite(MR_PWM, 100); // PWM-regelingssnelheid van de rechter motor is 100
    delay(2000);// vertraging van 2s

    // stoppen
    digitalWrite(ML_Ctrl, LOW); // Stel richtingsregelingssnelheid van de linker motor in op LOW
    analogWrite(ML_PWM, 0); // PWM-regelingssnelheid van de linker motor is 0
    digitalWrite(MR_Ctrl, LOW); // Stel richtingsregelingssnelheid van de rechter motor in op LOW
    analogWrite(MR_PWM, 0); // PWM-regelingssnelheid van de rechter motor is 0
    delay(2000);// vertraging van 2s
}
```

Upload de code, de snelheid van de motor is lager.

Een lage stroom zorgt ervoor dat de motor langzaam roteert.