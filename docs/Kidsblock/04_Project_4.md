### Project 4: Lijnvolgingssensor

#### **(1)Beschrijving:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

De lijnvolgingssensor is eigenlijk een infraroodsensor. Het hier gebruikte component is de TCRT5000 infraroodbuis.

Het werkingsprincipe is gebaseerd op het gebruik van de verschillende reflectiviteit van infraroodlicht op kleuren, waarbij de sterkte van het gereflecteerde signaal wordt omgezet in een stroombandssignaal.

Tijdens het detectieproces is zwart actief op HOOG niveau en wit op LAAG niveau. De detectiehoogte is 0-3 cm.

De Keyestudio 3-kanaals lijnvolgingsmodule heeft 3 sets TCRT5000 infraroodbuizen geïntegreerd op één printplaat, wat handiger is voor bedrading en bediening.

Als de lijnvolgingssensor niet werkt zoals verwacht, moet u een schroevendraaier gebruiken om de potentiometer aan te passen om deze gevoeliger te maken. Wanneer uw vinger dicht bij de sensor is, gaat het ingebouwde LED-lampje aan, en wanneer uw vinger wegbeweegt, gaat het ingebouwde LED-lampje uit. Op dat moment is de gevoeligheid relatief goed.

![](./media/img-20240117091947.png)

#### **(2)Parameters:**

- Werkspanning: 3.3-5V (DC)
- Interface: 5PIN
- Uitgangssignaal: Digitaal signaal
- Detectiehoogte: 0-3 cm

Speciale opmerking: draai vóór het testen aan de potentiometer op de sensor om de detectiegevoeligheid aan te passen. Wanneer de LED is ingesteld op de drempelwaarde tussen AAN en UIT, is de gevoeligheid het best.

<span style="color: rgb(255, 76, 65);">Opmerking:</span> de lijnvolgingssensor is bevestigd onder de bodem van de robot.

#### **(3)Aansluitschema:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/700cb0ecc14cbccd6e367c5098360f08.png)

![](media/271423c55b5f147796beb344eed7e9cf.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan vóór het uploaden van de code, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, wat conflicten kan veroorzaken met de Bluetooth seriële communicatie en het uploaden kan doen mislukken.)

![](media/5298cdfb6fd7c71df155c969c80450cd.png)

#### **(5)Testresultaten:**

Upload de code naar het ontwikkelbord, open de seriële monitor op 9600 en controleer de lijnvolgingssensoren. De weergegeven waarde is 1 (hoog niveau) wanneer er geen signalen worden ontvangen. De waarde verandert naar 0 wanneer de sensor wordt afgedekt met papier.

![](media/5630032421adf9446d51b770f0e7f8af.png)

#### **(6)Uitbreiding:**

We kunnen een LED bedienen met deze sensor. De LED is verbonden met D9. Als we de sensor afdekken, zal de LED oplichten.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/574854f4d96c40a85e1db549d85f14f4.png)

![](media/9077c0d059f7a4d3277f10ccb4e962fb.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

![](media/80e9c514357c63f4791c72220829b673.png)

![](media/b10e1897e99af2c1ade6c09da6c30dba.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan vóór het uploaden van de code, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, wat conflicten kan veroorzaken met de Bluetooth seriële communicatie en het uploaden kan doen mislukken.)

![](media/b5a4b5a04cdee9f79d6e18a5c48cbe48.png)

Wanneer een object (zoals papier of een vinger) de lijnvolgingssensor nadert, detecteert de sensor het terugkerende signaal dat door zichzelf wordt uitgezonden, en gaat de LED-module aan. Wanneer de sensor geen terugkerend signaal detecteert, gaat de LED-module uit.

![](./media/img-20240117092116.png)