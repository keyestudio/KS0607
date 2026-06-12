### Project 2: LED Helderheid Aanpassen

#### **(1)Beschrijving:**

In de vorige les hebben we de LED aan- en uitgeschakeld en laten knipperen.

In dit project regelen we de helderheid van de LED via PWM om een ademhalingseffect te simuleren. Op dezelfde manier kun je de staplengte en vertragingstijd in de code aanpassen om verschillende ademhalingseffecten te demonstreren.

PWM is een methode om de analoge uitvoer via digitale middelen te regelen. Digitale besturing wordt gebruikt om blokgolven te genereren met verschillende duty cycles (een signaal dat voortdurend wisselt tussen hoog en laag niveau) om de analoge uitvoer te regelen.

Over het algemeen zijn de ingangsspanningen van poorten 0V en 5V. Maar wat als 3V vereist is? Of een wisseling tussen 1V, 3V en 3,5V? We kunnen niet voortdurend weerstanden vervangen. Daarom maken we gebruik van PWM.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Voor Arduino digitale poort spanningsuitvoer zijn er alleen LAAG en HOOG niveaus, die overeenkomen met spanningsuitvoer van respectievelijk 0V en 5V. Je kunt LAAG definiëren als "0" en HOOG als "1", en de Arduino binnen 1 seconde vijfhonderd "0" of "1" laten uitvoeren. Als vijfhonderd "1" worden uitgevoerd, is dat 5V; als het allemaal "0" is, is dat 0V; als 250 01-patronen worden uitgevoerd, is dat 2,5V.

Dit proces kan worden vergeleken met het bekijken van een film. De films die we bekijken zijn niet volledig continu. Eigenlijk worden er 25 beelden per seconde gegenereerd, wat het menselijk oog niet kan onderscheiden. Daarom beschouwen we het als een continu proces. PWM werkt op dezelfde manier. Om verschillende spanningen uit te voeren, moeten we de verhouding van 0 en 1 regelen. Hoe meer "0" of "1" per tijdseenheid wordt uitgevoerd, hoe nauwkeuriger de regeling.

#### **(2)Parameters:**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Regelinterface: Digitale poort 3

- Werkspanning: DC 3,3-5V

- Pinafstand: 2,54mm

- LED weergavekleur: geel

#### **(3)Aansluitingsschema**

PWM-pinnen van de Arduino zijn verbonden met 3, 5, 6, 9, 10 en 11. Houd pin9 ongewijzigd.

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4)Testcode:**

Je kunt ook blokken slepen om je code te bewerken, zoals hieronder weergegeven

![](media/de8ccd3cb6621f0eb89a8514a9fd8452.png)

![](media/659b8a45b8e8d271226d9a25034aedfd.png)

![](media/3157917e305c01f1920cf4d06aff4ff9.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/aaab53a06684ab078936ee61f9abcbb3.png)


#### **(5)Testresultaten**

Na het succesvol uploaden van de testcode verandert de LED geleidelijk van helder naar donker, zoals de ademhaling van een mens, in plaats van onmiddellijk aan en uit te gaan.

#### **(6)Uitbreidingsoefening:**

Laten we de vertragingswaarde aanpassen en de pin ongewijzigd laten, en dan observeren hoe de LED verandert.

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/2ff0d71c2688d39695b760a1d0f76965.png)

Upload de code naar het ontwikkelbord, de LED knippert langzamer.