### Project 20: Flame Sensor

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Beschrijving：**

De vlamsensor gebruikt een IR-ontvangstbuis om vlammen te detecteren. Het converteert de helderheid van de vlam naar hoog- en laagsignalen en voert deze in de centrale processor voor de bijbehorende programmaverwerking. De spanningswaarde van de analoge poort varieert afhankelijk van of er een vlam dichtbij is of helemaal geen vlam.

Als er geen vlam is, leest de analoge poort ongeveer 0,3V; wanneer er een vlam is, leest de analoge poort ongeveer 1,0V. Hoe dichter de vlam, hoe hoger de spanningswaarde. Het kan worden gebruikt om een vuurhaard te detecteren of om een slimme robot te bouwen.

Merk op dat de sonde van de vlamsensor alleen temperaturen tussen -25℃ en 85℃ kan verdragen.

Zorg er tijdens gebruik voor dat de vlamsensor op een veilige afstand van het vuur blijft om beschadiging te voorkomen.

#### **(2)Parameters：**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Werkspanning: 3,3V-5V (DC)

- Stroom: 100mA

- Maximaal vermogen: 0,5W

- Werktemperatuur: -10°C tot +50 graden Celsius

- Sensorafmetingen: 31,6mmx23,7mm

- Interface: 4pin naar 3PIN interface

- Uitgangssignaal: analoge signalen A0, A1



#### **(3)Aansluitingsschema:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

Vlamsensoren zijn aangesloten op A1 en A2.

Wanneer we ultrasone sensoren en fotoweerstandjes verwijderen en vervolgens vlamsensoren en ventilatormodules toevoegen,
wordt de brandblussende robot gecreëerd.

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
1）Dit experiment vereist het gebruik van een vuurhaard. Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment uit te voeren onder toezicht van een volwassene. Als u niet kunt bevestigen dat u veilig bent, stop dan met het experiment.
2）**De vlamsensor is niet vuurbestendig, verbrand hem niet direct met een vlam.**


#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.1

flame sensor

http://www.keyestudio.com

*/

int flame = A1; // Definieer de vlam-pin als analoge pin A1
int val = 0; // Definieer digitale variabelen

void setup() 
{
	pinMode(flame, INPUT); // Definieer de buzzer als een ingangsbron
    Serial.begin(9600); // Stel de baudrate in op 9600
}

void loop() 
{
	val = analogRead(flame); // Lees de analoge waarde van de vlamsensor
	Serial.println(val); // Geef de analoge waarde weer en druk deze af
	delay(100); // Vertraging van 100ms
}
```

#### **(5)Testresultaat：**

Sluit de componenten aan, upload de code, open de seriële monitor en stel de baudrate in op 9600.

U kunt de simulatiewaarde van de vlamsensor bekijken.

Hoe dichter de vlam, hoe kleiner de simulatiewaarde.

Pas de potentiometer op de module aan om D1 op het kritieke punt te houden. Wanneer de sensor geen vlam detecteert, zal D1 uit zijn, maar als de sensor een vlam detecteert, zal D1 aan zijn.

![](./media/img-20240117085629.png)

![](media/05db06b3e205dfca63c2ba3aa7ff528e.png)

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment uit te voeren onder toezicht van een volwassene. Als u niet kunt bevestigen dat u veilig bent, stop dan met het experiment. De vlamsensor is niet vuurbestendig, verbrand hem niet direct met een vlam.

#### **(6)Uitgebreide oefening:**

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
1）Dit experiment vereist het gebruik van een vuurhaard. Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment uit te voeren onder toezicht van een volwassene. Als u niet kunt bevestigen dat u veilig bent, stop dan met het experiment.
2）De vlamsensor is niet vuurbestendig, verbrand hem niet direct met een vlam.

Vervolgens sluiten we een LED aan op pin 9 en kunnen we deze bedienen met een vlamsensor, zoals hieronder weergegeven;

![](media/814c315d3bb44278b476a754d3681227.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.2

flame sensor

http://www.keyestudio.com

*/

int flame = A1; // Definieer de vlam-pin als analoge pin A1
int LED = 9; // Definieer de LED als digitale poort 9
int val = 0; // Definieer digitale variabelen

void setup() 
{
    pinMode(flame, INPUT); // Definieer de vlam als een ingangsbron
    pinMode(LED, OUTPUT); // Stel LED in op uitvoermodus
    Serial.begin(9600); // Stel de baudrate in op 9600
}

void loop() 
{
    val = analogRead(flame); // Lees de analoge waarde van de vlamsensor
    Serial.println(val); // Geef de analoge waarde weer en druk deze af
    if (val < 300)  // Wanneer de analoge waarde kleiner is dan 300, gaat de LED aan
    {
    	digitalWrite(LED, HIGH); // LED gaat aan
    } 
    else 
    {
    	digitalWrite(LED, LOW); // LED gaat uit
    }
    delay(50); // Vertraging van 50ms
}
```

#### **(8)Testresultaten：**

U kunt de vlam van een aansteker dicht bij de linker vlamsensor houden. Wanneer de vlamsensor een vlam detecteert, zal de LED-module oplichten als alarm.

![](./media/img-20240117085131.png)

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment uit te voeren onder toezicht van een volwassene. Als u niet kunt bevestigen dat u veilig bent, stop dan met het experiment. De vlamsensor is niet vuurbestendig, verbrand hem niet direct met een vlam.