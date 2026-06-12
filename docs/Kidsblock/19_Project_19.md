### Project 19: Vlamsensor

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Beschrijving:**

De vlamsensor gebruikt een IR-ontvangstbuis om vlammen te detecteren. Het zet de helderheid van de vlam om in hoog- en laagsignalen en stuurt deze naar de centrale processor voor bijbehorende programmaverwerking. De spanningswaarde van de analoge poort varieert afhankelijk van of er een vlam dichtbij is of helemaal geen vlam.

Als er geen vlam is, leest de analoge poort ongeveer 0,3V; wanneer er een vlam is, leest de analoge poort ongeveer 1,0V. Hoe dichter de vlam, hoe hoger de spanningswaarde. Het kan worden gebruikt om een vuurbron te detecteren of om een slimme robot te bouwen.

Let op: de sonde van de vlamsensor kan alleen temperaturen tussen -25℃ en 85℃ verdragen.

Zorg er tijdens gebruik voor dat de vlamsensor op een veilige afstand van het vuur blijft om beschadiging te voorkomen.

#### **(2)Parameters:**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Werkspanning: 3,3V-5V (DC)

- Stroom: 100mA

- Maximaal vermogen: 0,5W

- Werktemperatuur: -10°C tot +50 graden Celsius

- Sensorafmetingen: 31,6mmx23,7mm

- Interface: 4pin naar 3PIN interface

- Uitgangssignaal: analoge signalen A0, A1

#### **(3)Aansluitschema:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

Pin A van twee fotoresistoren zijn verbonden met A1 en A2. We verbinden de vlamsensor met A1 en A2. We vervangen twee fotoresistoren en de ultrasone sensor door twee vlamsensoren en een ventilator, waarmee een bluswagen wordt gecreëerd.

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
1）Dit experiment vereist het gebruik van een vuurbron. Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment onder toezicht van een volwassene uit te voeren. Als u niet kunt bevestigen dat u veilig bent, verlaat dan het experiment.
2）**De vlamsensor is niet vuurbestendig, verbrand hem niet rechtstreeks met een vlam.**

#### **(4)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook seriële communicatie gebruikt, en er mogelijk conflicten zijn met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/4bc6c8a4d6e964fd078a6aeb0dd51ff4.png)

#### **(5)Testresultaten:**

Sluit de componenten aan, upload de code, open de seriële monitor en stel de baudrate in op 9600.

U kunt de simulatiewaarde van de vlamsensor bekijken.

Hoe dichter de vlam, hoe kleiner de simulatiewaarde.

Stel de potentiometer op de module af om de LED op het kritieke punt te houden. Wanneer de sensor geen vlam detecteert, gaat de LED uit, maar als de sensor een vlam detecteert, gaat de LED aan.

![](./media/img-20240117100139.png)

![](media/60d0ce2044a504135af3b1113a1a4c7d.png)

#### **(6)Uitbreidingsoefening:**

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
1）Dit experiment vereist het gebruik van een vuurbron. Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment onder toezicht van een volwassene uit te voeren. Als u niet kunt bevestigen dat u veilig bent, verlaat dan het experiment.
2）De vlamsensor is niet vuurbestendig, verbrand hem niet rechtstreeks met een vlam.
We kunnen een externe LED besturen met de vlamsensor. De LED is nog steeds verbonden met D9. Wanneer vuur wordt gedetecteerd, gaat de LED aan.

![](media/814c315d3bb44278b476a754d3681227.png)

U kunt blokken slepen om uw code te bewerken, zoals hieronder weergegeven

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook seriële communicatie gebruikt, en er mogelijk conflicten zijn met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/9d2f5915e4a6991ed4549b39ec853fa5.png)

U kunt de vlam van een aansteker in de buurt van de linker vlamsensor houden. Wanneer de vlamsensor een vlam detecteert, zal de LED-module oplichten als alarm.

![](./media/img-20240117100333.png)

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment onder toezicht van een volwassene uit te voeren. Als u niet kunt bevestigen dat u veilig bent, verlaat dan het experiment. De vlamsensor is niet vuurbestendig, verbrand hem niet rechtstreeks met een vlam.