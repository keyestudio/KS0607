### Project 4: Lijnvolgingssensor

#### **(1)Beschrijving:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

De lijnvolgingssensor is eigenlijk een infraroodsensor. Het hier gebruikte onderdeel is de TCRT5000 infraroodbuis.

Het werkingsprincipe is gebaseerd op het gebruik van de verschillende reflectiviteit van infraroodlicht op kleuren, en vervolgens het omzetten van de sterkte van het gereflecteerde signaal naar een stromsignaal.

Tijdens het detectieproces is zwart actief op HOOG niveau terwijl wit actief is op LAAG niveau. De detectiehoogte is 0-3 cm.

De Keyestudio 3-kanaals lijnvolgingsmodule heeft 3 sets TCRT5000 infraroodbuizen geïntegreerd op één printplaat, wat de bedrading en besturing eenvoudiger maakt.

Als de lijnvolgingssensor niet werkt zoals verwacht, moet u een schroevendraaier gebruiken om de potentiometer aan te passen om hem gevoeliger te maken. Wanneer uw vinger dicht bij de sensor komt, gaat het ingebouwde LED-lampje aan, en wanneer uw vinger wegbeweegt, gaat het ingebouwde LED-lampje uit. Op dat moment is de gevoeligheid relatief goed.

![](./media/img-20240117090858.png)

#### **(2)Parameters:**

- Bedrijfsspanning: 3.3-5V (DC)

- Interface: 5PIN

- Uitgangssignaal: Digitaal signaal

- Detectiehoogte: 0-3 cm


Speciale opmerking: voor het testen, draai de potentiometer op de sensor om de detectiegevoeligheid aan te passen. Wanneer de LED wordt ingesteld op de drempel tussen AAN en UIT, is de gevoeligheid het beste.

<span style="color: rgb(255, 76, 65);">Opmerking:</span> de lijnvolgingssensor is gemonteerd onder de bodem van de robot.

#### **(3)Aansluitschema:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.1

Line Track sensor

http://www.keyestudio.com

*/

// De bedrading van de lijnvolgingssensoren

#define L_pin 11 // links
#define M_pin 7 // midden
#define R_pin 8 // rechts

void setup()
{
    Serial.begin(9600); // Stel de baudrate in op 9600
    pinMode(L_pin, INPUT); // Stel alle pinnen van de lijnvolgingssensoren in op invoermodus
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); // Lees de waarde van de linkersensor
    int M_val = digitalRead(M_pin); // Lees de waarde van de middelste sensor
    int R_val = digitalRead(R_pin); // Lees de waarde van de rechtssensor

    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); // vertraging van 100ms
}
```

#### **(5)Testresultaten:**

Upload de code op het ontwikkelbord, open de seriële monitor om de lijnvolgingssensoren te controleren. De weergegeven waarde is 1 (hoog niveau) wanneer er geen signalen worden ontvangen. De waarde verandert naar 0 wanneer de sensor wordt bedekt met papier.

![](./media/img-20240117090920.png)


![](media/b9319753c148f66aabc9bf648ed93da1.png)

#### **(6)Codeuitleg:**

**Serial.begin(9600)**- Initialiseer de seriële poort, stel de baudrate in op 9600

**pinMode-** Definieer de pin als invoer- of uitvoermodus

**digitalRead-** Lees de toestand van de pin, dit zijn over het algemeen HOOG en LAAG niveau

#### **(7)Uitgebreide oefening:**

Na het kennen van het werkingsprincipe kunt u een LED verbinden met D9, zodat u de LED kunt bedienen via de lijnvolgingssensor.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.2

Line Track sensor

http://www.keyestudio.com

*/

// LED pin

#define LED 9
// De bedrading van de lijnvolgingssensoren
#define L_pin 11 // links
#define M_pin 7 // midden
#define R_pin 8 // rechts

void setup()
{
    Serial.begin(9600); // Stel de baudrate in op 9600
    pinMode(LED, OUTPUT); // Stel LED in op uitvoermodus
    pinMode(L_pin, INPUT); // Stel alle pinnen van de lijnvolgingssensoren in op invoermodus
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); // Lees de waarde van de linkersensor
    int M_val = digitalRead(M_pin); // Lees de waarde van de middelste sensor
    int R_val = digitalRead(R_pin); // Lees de waarde van de rechtssensor
    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); // Vertraging in

    if (L_val == 0 || M_val == 0 || R_val == 0) 
    {
    	digitalWrite(LED, HIGH);
    }
    else 
    {
    	digitalWrite(LED, LOW);
    }
}
```