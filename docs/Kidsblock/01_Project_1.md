### Project 1: LED Knippert

#### (1)Beschrijving：

![](./media/image-20250709122631704.png)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Voor beginners en enthousiastelingen is LED Knipperen een fundamenteel programma. LED, de afkorting van light emitting diodes (lichtgevende diodes), bestaat uit Ga, As, P, N chemische verbindingen enzovoort. De LED kan in diverse kleuren knipperen door de vertragingstijd in de testcode te wijzigen. Bij bediening wordt stroom aangesloten op GND en VCC. De LED gaat aan als het S-uiteinde op een hoog niveau staat; anders gaat hij uit.

#### **(2)Parameters:**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Besturingsinterface: digitale poort
- Werkspanning: DC 3.3-5V
- Pinafstand: 2.54mm
- LED weergavekleur: geel

#### (3)Benodigde Componenten:

![](./media/image-20250709122437613.png)

#### **(4)8833 Motor Driver Expansiebord:**

Het Keyestudio 8833 motor driver expansiebord is compatibel met het Arduino UNO ontwikkelbord. Stapel het gewoon op het ontwikkelbord bij gebruik.

![](media/d8696e83ade31f2b7c56cc5911eacbd7.GIF)

#### **(5)Aansluitschema:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](./media/image-20250709122655936.png)

<span style="color: rgb(255, 76, 65);">**OPMERKING:**</span> De LED is verbonden met de D9 poort. Vergeet niet om jumperkapjes op het shield te installeren.

#### **(6)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.

![](media/cc43ba357acb68a4961adb7e5041b6fe.png)

![](media/26b69cd46ad24e1c900c4fb316430353.png)

![](media/21dc3c24da4271aa7ec2bfdac732eeb3.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/ba4723bab640078eccbe1811da138bc3.png)

#### **(7)Testresultaten:**

Upload het programma, de LED knippert met een interval van 1s.

#### **(8)Uitbreidingsoefening:**

We weten nu hoe we de LED moeten besturen, laten we dan de frequentie van de LED wijzigen.

We kunnen de frequentie van de LED wijzigen zonder de pin van de LED te veranderen. Laten we de code aanpassen.

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/58c76be4c719a885afb500e8f3b80b85.png)

Het testresultaat toont aan dat de LED sneller knippert. Daarom kunnen we concluderen dat pinnen en vertragingstijd de knipperfrequentie beïnvloeden.