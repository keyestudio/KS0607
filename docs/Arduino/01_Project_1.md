### Project 1: LED Knippert

#### **(1)Beschrijving:**

![](media/64b0b431d58473408ac46b39d2dc2ad0.jpeg)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Voor beginners en enthousiastelingen is LED Knipperen een fundamenteel programma. LED, de afkorting van lichtgevende diodes, bestaat uit Ga, As, P, N chemische verbindingen enzovoort. De LED kan in verschillende kleuren knipperen door de vertragingstijd in de testcode te wijzigen. Bij bediening wordt stroom aangesloten op GND en VCC. De LED gaat aan als het S-uiteinde op een hoog niveau is; anders gaat hij uit.

#### **(2)Parameters:**

![](./media/image-20250709104606457.png)

- Besturingsinterface: digitale poort
- Werkspanning: DC 3.3-5V
- Pinafstand: 2.54mm
- LED weergavekleur: geel

#### **(3)Benodigde Componenten:**

![](media/img-20240117081416.png)


#### **(4)8833 Motor driver uitbreidingsbord:**

Het Keyestudio 8833 motor driver uitbreidingsbord is compatibel met het Arduino UNO ontwikkelbord. Stapel het gewoon op het ontwikkelbord wanneer u het gebruikt.

![](./media/image-20250709104749140.png)

#### **(5)Aansluitdiagram:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](media/d68e6475a7c9ed55bb057b75d1b11689.png)

<span style="color: rgb(255, 76, 65);">**LET OP:**</span> De LED is aangesloten op de D9 poort. Vergeet niet om jumperkapjes op het shield te plaatsen.

#### **(6)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.1

Blink

http://www.keyestudio.com

*/

int LED = 9; //Definieer de pin van de LED om te verbinden met digitale poort 9

void setup()
{
	pinMode(LED, OUTPUT); //Initialiseer de LED-pin naar uitvoermodus
}

void loop() //oneindige lus
{
	digitalWrite(LED, HIGH); //Geef hoog niveau uit en zet de LED aan
	delay(1000); //Wacht 1s
	digitalWrite(LED, LOW); //Geef laag niveau uit en zet de LED uit
	delay(1000); //Wacht 1s
}
```

#### **(7)Testresultaten:**

Upload het programma, de LED knippert met een interval van 1s.

#### **(8)Code Uitleg:**

**pinMode(LED，OUTPUT) -** Deze functie kan aangeven dat de pin INPUT of OUTPUT is

**digitalWrite(LED，HIGH) -** Wanneer de pin OUTPUT is, kunnen we deze instellen op HIGH (5V uitvoer) of LOW (0V uitvoer)

#### **(9)Uitbreidingsoefening:**

We hebben de LED succesvol laten knipperen. Laten we nu observeren wat er met de LED gebeurt als we pins en vertragingstijd wijzigen.

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.2

Blink

http://www.keyestudio.com

*/

int LED = 9; //Definieer de pin van de LED als 9

void setup()
{
	pinMode(LED, OUTPUT); //Stel de pin van de LED in op OUTPUT
}

void loop() //Oneindige lus
{
    digitalWrite(LED, HIGH); //geef hoge niveaus uit, zet LED aan
	delay(100); //Wacht 0.1s
	digitalWrite(LED, LOW); //LED geeft lage niveaus uit, zet LED uit
	delay(100); //Wacht 0.1s

}
```

Het testresultaat toont aan dat de LED sneller knippert. Daarom kunnen we concluderen dat pins en vertragingstijd de knipperfrequentie beïnvloeden.