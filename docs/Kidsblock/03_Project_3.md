### Project 3: Fotoweerstand

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Beschrijving:**

De lichtgevoelige weerstand is een speciale weerstand gemaakt van een halfgeleidermateriaal zoals een sulfide of seleen, en is ook bedekt met een vochtwerende hars met een fotogeleiding-effect. De lichtgevoelige weerstand reageert het meest op het omgevingslicht; bij verschillende verlichtingssterkte is de weerstand van de lichtgevoelige weerstand verschillend. We gebruiken de lichtgevoelige weerstand om de lichtgevoelige weerstandsmodule te ontwerpen.

Het modulesignaal is verbonden met de analoge poort van de microcontroller. Wanneer de lichtintensiteit sterker is, is de spanning op de analoge poort groter, dat wil zeggen dat de simulatiewaarde van de microcontroller ook groter is; omgekeerd, wanneer de lichtintensiteit zwakker is, is de spanning op de analoge poort kleiner, dat wil zeggen dat de simulatiewaarde van de microcontroller ook kleiner is.

Op deze manier kunnen we de overeenkomstige analoge waarde uitlezen met behulp van de lichtgevoelige weerstandsmodule, en de intensiteit van het licht in de omgeving bepalen.

![](./media/image-20250709122809574.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Parameters:**

- Weerstandswaarde lichtgevoelige weerstand: 5K Ohm-0.5m

- Type interface: simulatiepoort A0, A1

- Werkspanning: 3.3V-5V

- Pinafstand: 2.54mm

#### **(3)Aansluitdiagram:**

Wat we hierna gaan testen is de fotoweerstandsmodule aan de linkerkant van de robot.

![](./media/img-20240117091730.png)

De linker fotoweerstand is verbonden met A1/P3 van het motoraanstuurschild.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)


#### **(4)Testcode:**

Je kunt ook blokken slepen om je code te bewerken, zoals hieronder weergegeven.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Verbind de Bluetooth-module niet voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er mogelijk conflicten zijn met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/f29c7da2238bcc2bc70cb4b2c773b50d.png)

#### **(5)Testresultaten:**

Upload de code naar het ontwikkelbord. Klik op ![](media/9011f20d83897d7a5936793c4ae142fc.png) om de baudrate in te stellen op 9600. Wanneer je het afdekt met je hand, wordt de waarde kleiner; zo niet, dan wordt de waarde groter.

![](media/53e2fc37ee5bb2c6ec187c309c431c47.png)



#### **(6)Uitbreidingsoefening:**

De bovenstaande code leest alleen de waarde van de fotoweerstand. We kunnen de lichtgevoelige weerstand en LED combineren om de LED te wijzigen. Wat dacht je ervan om de helderheid van de LED hiermee te regelen?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

PWM kan de lichthelderheid veranderen, dat wil zeggen dat de LED moet worden aangesloten op de PWM van het ontwikkelbord.

Verbind de LED met D9 en laat de andere pinnen ongewijzigd, dan bewerken we de code.

Je kunt ook blokken slepen om je code te bewerken, zoals hieronder weergegeven.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/b94c3789429c5fed4fd38467cb9792dd.png)

![](media/9ecdfd77e2a69dea5a8df04e7d56a13a.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Verbind de Bluetooth-module niet voordat je de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er mogelijk conflicten zijn met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/b23bcae806e8e27382b162909d30f3c0.png)

Upload de code naar het ontwikkelbord, we drukken op de fotoweerstand om te zien of de helderheid van het LED-lampje is veranderd.

![](./media/img-20240117091759.png)