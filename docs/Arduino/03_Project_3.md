### Project 3: Fotoweerstand

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Beschrijving:**

De lichtgevoelige weerstand is een speciale weerstand gemaakt van een halfgeleidermateriaal zoals een sulfide of seleen, en is ook gecoat met een vochtbestendige hars met een fotogeleiding-effect. De lichtgevoelige weerstand is het meest gevoelig voor het omgevingslicht; bij verschillende verlichtingssterktes is de weerstand van de lichtgevoelige weerstand anders. We gebruiken de lichtgevoelige weerstand om de fotoweerstandsmodule te ontwerpen.

Het signaalpunt van de module is verbonden met de analoge poort van de microcontroller. Wanneer de lichtintensiteit sterker is, is de spanning op de analoge poort groter, dat wil zeggen dat de simulatiewaarde van de microcontroller ook groter is; omgekeerd, wanneer de lichtintensiteit zwakker is, is de spanning op de analoge poort kleiner, dat wil zeggen dat de simulatiewaarde van de microcontroller ook kleiner is.

Op deze manier kunnen we de overeenkomstige analoge waarde lezen met behulp van de fotoweerstandsmodule, en de intensiteit van het licht in de omgeving bepalen.

![](media/7784e14e15402644cdbe674d500327c4.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Parameters:**

Weerstandswaarde fotoweerstand: 5K Ohm - 0.5M

Interfacetype: simulatiepoort A0, A1

Werkspanning: 3.3V-5V

Pinafstand: 2.54mm


#### **(3)Aansluitingsschema:**

Wat we hierna gaan testen is de fotoweerstandsmodule aan de linkerkant van de robot.

![](./media/img-20240117091559.png)

De linker fotoweerstand is verbonden met A1/P3 van de motoraansturingshield.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.1

photocell

http://www.keyestudio.com

*/

int sensorPin = A1; // A1 is de invoerpin van de fotoweerstand

int sensorValue = 0; // sla de waarde van de fotoweerstand op

void setup() 
{
	Serial.begin(9600); // Open de seriële poortmonitor en stel de baudrate in op 9600
}

void loop() 
{
	sensorValue = analogRead(sensorPin); // Lees de analoge waarde van de fotoweerstands sensor
	Serial.println(sensorValue); // De seriële poort drukt de waarde van de fotoweerstand af
	delay(500); // Vertraging van 500ms
}
```

#### **(5)Testresultaten:**

![](media/54b92578e3210999e23f5fb8138f0fa0.png)

Wanneer u de sensor afdekt, wordt de waarde kleiner; als u dat niet doet, wordt de waarde groter.

#### **(6)Code-uitleg:**

**analogRead(sensorPin)**: lees de analoge waarde van de fotoweerstand

**Serial.begin(9600)**: initialiseer de seriële poort en stel de baudrate in op 9600

**Serial.println**: serieel afdrukken

#### **(7)Uitbreidingsoefening:**

De bovenstaande code leest alleen de waarde van de fotoweerstand. We kunnen de lichtgevoelige weerstand en een LED combineren om de LED te bedienen. Wat dacht u van het besturen van de helderheid van de LED hiermee?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

De helderheid van de LED wordt geregeld door PWM. Daarom verbinden we de LED met de PWM-pin (pin 9) van de shield.

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```c
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.2

photocell-analog output

http://www.keyestudio.com

*/

int analogInPin = A1; // A1 is de invoerpin van de fotoweerstand

int analogOutPin = 9; // Digitale poort 9 is de uitvoer van PWM

int sensorValue = 0; // sla de variabele op van de weerstandswaarde van de fotoweerstand

int outputValue = 0; // Waarde uitgevoerd naar PWM

void setup() 
{
	Serial.begin(9600); // Open de seriële poortmonitor en stel de baudrate in op 9600
}

void loop() 
{
    sensorValue = analogRead(analogInPin); // Lees de analoge waarde van de fotoweerstands sensor
    // Wijs de analoge waarden 0\~1023 toe aan de PWM-uitvoerwaarden 255\~0
    outputValue = map(sensorValue, 0, 1023, 255, 0);
    // Wijzig de analoge uitvoer
    analogWrite(analogOutPin, outputValue);
    Serial.println(sensorValue); // De seriële poort drukt de waarde van de fotoweerstand af
    delay(2);
}
```

Upload de code naar het ontwikkelbord, dek vervolgens de fotoweerstand af en observeer de helderheid van de LED.

![](./media/img-20240117091105.png)