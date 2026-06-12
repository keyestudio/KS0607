### Project 2: LED Helderheid Aanpassen

#### **(1)Beschrijving:**

In de vorige les hebben we de LED aan en uit gestuurd en laten knipperen.

In dit project regelen we de helderheid van de LED via PWM om een ademhalingseffect te simuleren. Op dezelfde manier kun je de stapgrootte en vertragingstijd in de code aanpassen om verschillende ademhalingseffecten te demonstreren.

PWM is een manier om analoge uitvoer via digitale middelen te regelen. Digitale sturing wordt gebruikt om blokgolven te genereren met verschillende duty cycles (een signaal dat voortdurend wisselt tussen hoge en lage niveaus) om de analoge uitvoer te regelen.

Over het algemeen zijn de ingangsspanningen van poorten 0V en 5V. Wat als 3V vereist is? Of een schakelaar tussen 1V, 3V en 3.5V? We kunnen niet voortdurend weerstanden wisselen. Daarom maken we gebruik van PWM.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Voor Arduino digitale poortspanningsuitgangen zijn er alleen LAGE en HOGE niveaus, die overeenkomen met de spanningsuitgangen van respectievelijk 0V en 5V. Je kunt LAAG definiëren als "0" en HOOG als "1", en de Arduino binnen 1 seconde vijfhonderd "0" of "1" laten uitvoeren. Als er vijfhonderd "1" worden uitgevoerd, is dat 5V; als het allemaal "0" is, is dat 0V; als er 250 01-patronen worden uitgevoerd, is dat 2.5V.

Dit proces kan worden vergeleken met het bekijken van een film. De films die we kijken zijn niet volledig continu. Eigenlijk worden er 25 beelden per seconde gegenereerd, wat het menselijk oog niet kan onderscheiden. Daarom zien we het als een continu proces. PWM werkt op dezelfde manier. Om verschillende spanningen uit te voeren, moeten we de verhouding van 0 en 1 regelen. Hoe meer "0" of "1" er per tijdseenheid worden uitgevoerd, hoe nauwkeuriger de regeling.

#### **(2)Parameters:**

![](./media/image-20250709104949184.png)

Besturingsinterface: Digitale poort 3

Werkspanning: DC 3.3-5V

Pinafstand: 2.54mm

LED weergavekleur: geel

#### **(3)Aansluitschema:**

PWM-pinnen van Arduino zijn verbonden met 3, 5, 6, 9, 10 en 11. Laat pin 9 ongewijzigd

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.1

pwm

http://www.keyestudio.com

*/

int LED = 9; // Definieer de pin van de LED als 9

void setup () 
{
	pinMode(LED, OUTPUT); // Stel de pin van de LED in op OUTPUT
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED AAN
		delay(5); // vertraging van 5ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // LED wordt dimmer
		delay(5); // vertraging van 5ms
	}
}
```

#### **(5)Testresultaten:**

Na het succesvol uploaden van de testcode verandert de LED geleidelijk van helder naar donker, zoals de ademhaling van een mens, in plaats van onmiddellijk aan en uit te gaan.

#### **(6)Codeuitleg:**

Om bepaalde instructies te herhalen, kunnen we de FOR-instructie gebruiken. Het formaat van de FOR-instructie is hieronder weergegeven:

![图1(1)](media/65da124bdd0ea488291c71c6b879fe95.jpeg)

FOR-cyclusvolgorde:

Ronde 1：1 → 2 → 3 → 4

Ronde 2：2 → 3 → 4

…

Totdat nummer 2 niet meer geldig is, is de "for"-lus afgelopen.

Na het kennen van deze volgorde, gaan we terug naar de code:

**for (int value = 0; value \< 255; value=value+1){**

**...}**

**for (int value = 255; value \>0; value=value-1){**

**...}**

De twee "for"-instructies zorgen ervoor dat de waarde toeneemt van 0 naar 255, vervolgens afneemt van 255 naar 0, daarna weer toeneemt naar 255,... oneindig in een lus.

Er is een nieuwe functie in het volgende ----- analogWrite()

We weten dat een digitale poort slechts twee toestanden heeft: 0 en 1. Maar hoe sturen we een analoge waarde naar een digitale waarde? Hiervoor is deze functie nodig. Laten we het Arduino-board bekijken en 6 pinnen vinden die zijn gemarkeerd met "\~", die PWM-signalen kunnen uitvoeren.

Functieformaat als volgt:

**analogWrite(pin,value)**

analogWrite() wordt gebruikt om een analoge waarde van 0\~255 te schrijven voor een PWM-poort, zodat de waarde in het bereik van 0\~255 ligt. Let op: je kunt alleen naar digitale pinnen schrijven met PWM-functionaliteit, zoals pin 3, 5, 6, 9, 10, 11.

PWM is een technologie om een analoge grootheid te verkrijgen via een digitale methode. Digitale sturing vormt een blokgolf, en het blokgolfsignaal heeft slechts twee toestanden: aan en uit (dat wil zeggen hoge of lage niveaus). Door de verhouding van de duur van aan en uit te regelen, kan een spanning variërend van 0 tot 5V worden gesimuleerd. De tijd dat het aan staat (academisch aangeduid als hoog niveau) wordt pulsbreedtte genoemd, dus PWM wordt ook pulsbreedte-modulatie genoemd.

Aan de hand van de volgende vijf blokgolven leren we meer over PWM.

![](media/553f3d1b6ca04e1aa0479841dd075fa2.png)

In de bovenstaande afbeelding vertegenwoordigt de groene lijn een periode, en de waarde van analogWrite() komt overeen met een percentage dat ook wel Duty Cycle (inschakelverhouding) wordt genoemd.

De duty cycle geeft aan dat de duur van het hoge niveau wordt gedeeld door de duur van het lage niveau in een cyclus. Van boven naar beneden is de duty cycle van de eerste blokgolf 0% en de bijbehorende waarde is 0. De LED-helderheid is het laagst, dat wil zeggen: lamp uit. Hoe langer het hoge niveau duurt, hoe helderder de LED. Daarom is de laatste duty cycle 100%, wat overeenkomt met 255, en is de LED het helderst. En 25% betekent donkerder.

PWM wordt voornamelijk gebruikt voor het regelen van de helderheid van LED's of de rotatiesnelheid van motoren.

Het speelt een cruciale rol bij het besturen van slimme robotauto's. Ik geloof dat je niet kunt wachten om het volgende project te leren.

#### **(7)Uitbreidingsoefening:**

Laten we de vertragingswaarde aanpassen terwijl de pin ongewijzigd blijft, en dan observeren hoe de LED verandert.

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.2

pwm-slow

http://www.keyestudio.com

*/

int LED = 9; // Definieer de pin van de LED als 9

void setup() 
{
	pinMode(LED, OUTPUT); // Stel de pin van de LED in op OUTPUT
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED AAN
		delay(30); // vertraging van 30ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // LED wordt dimmer
		delay (30); // vertraging van 30ms
	}
}
```

Upload de code naar het ontwikkelbord, de LED knippert langzamer.