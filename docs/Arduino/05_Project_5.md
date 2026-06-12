### Project 5: Servo Aansturing

#### **(1)Beschrijving:**

Een servomotor is een rotatieactuator voor positiebeheer. Hij bestaat voornamelijk uit een behuizing, een printplaat, een kernloze motor, een tandwiel en een positiesensor. Het werkingsprincipe is dat de servo het signaal ontvangt van de MCU of ontvanger en een referentiesignaal genereert met een periode van 20ms en een breedte van 1,5ms. Vervolgens vergelijkt hij de verkregen DC-voorspanningsspanning met de spanning van de potentiometer en verkrijgt hij het spanningsverschil als uitvoer.

Wanneer de motorsnelheid constant is, wordt de potentiometer aangedreven via het getrapte reductietandwiel, waardoor het spanningsverschil 0 wordt en de motor stopt met draaien. Over het algemeen is het draaihoekbereik van een servo 0° --180°.

De draaihoek van de servomotor wordt geregeld door de duty cycle van het PWM-signaal (Pulse-Width Modulation) aan te passen. De standaardcyclus van het PWM-signaal is 20ms (50Hz). Theoretisch ligt de breedte tussen 1ms-2ms, maar in de praktijk is dit tussen 0,5ms-2,5ms. De breedte komt overeen met de draaihoek van 0° tot 180°. Let op: voor motoren van verschillende merken kan hetzelfde signaal tot verschillende draaihoeken leiden.

![](media/69be958142b773acdae33eeef12afed7.png)

Over het algemeen heeft een servo drie draden in bruin, rood en oranje. De bruine draad is de aardverbinding, de rode is de positieve pool en de oranje is de signaaldraad.

![](media/49467dfa70799401a5a5acc691014aee.png)

De hoek van de servo:

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Parameters:**

- Werkspanning: DC 4,8V \~ 6V

- Bedrijfshoekbereik: ongeveer 180° (bij 500 → 2500 μsec)

- Pulsbreedte bereik: 500 → 2500 μsec

- Onbelaste snelheid: 0,12 ± 0,01 sec / 60 (DC 4,8V) 0,1 ± 0,01 sec / 60 (DC 6V)

- Onbelaste stroom: 200 ± 20mA (DC 4,8V) 220 ± 20mA (DC 6V)

- Stoppend koppel: 1,3 ± 0,01kg · cm (DC 4,8V) 1,5 ± 0,1kg · cm (DC 6V)

- Stopstroom: ≦ 850mA (DC 4,8V) ≦ 1000mA (DC 6V)

- Stand-bystroom: 3 ± 1mA (DC 4,8V) 4 ± 1mA (DC 6V)

#### **(3)Aansluitschema:**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span> De bruine, rode en oranje draad van de servo worden respectievelijk aangesloten op Gnd(G), 5v(V) en 10 van het shield. Vergeet niet een externe voeding aan te sluiten vanwege de hoge stroom van de servo. Als u dit niet doet, kan het ontwikkelbord beschadigd raken.

#### **(4)Testcode 1:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruikmaakt van seriële communicatie, en er mogelijk conflicten ontstaan met de seriële Bluetooth-communicatie, waardoor het uploaden kan mislukken.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.1
Servo
http://www.keyestudio.com
*/

#define servoPin 10 //De pin van de servo

int pos; //De variabele voor de hoek van de servo
int pulsewidth; //De variabele voor de pulsbreedte van de servo

void setup() 
{
    pinMode(servoPin, OUTPUT); //Stel de pin van de servo in als uitvoer
    procedure(0); //Stel de hoek van de servo in op 0°
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  // Van 1° tot 180°
    {
    	// in stappen van 1 graad	
        procedure(pos); // Draai naar de hoek van 'pos'
        delay(15); //Beheers de rotatiesnelheid
    }
    for (pos = 180; pos >= 0; pos -= 1) // Van 180° naar 1°
    { 
        procedure(pos); // Draai naar de hoek van 'pos'
        delay(15);
    }
}
//De functie bestuurt de servo
void procedure(int myangle) 
{
    pulsewidth = myangle * 11 + 500; //Bereken de waarde van de pulsbreedte
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth); //De tijd in hoog niveau stelt de pulsbreedte voor
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000)); //Omdat de cyclus 20ms is, blijft de resterende tijd op laag niveau
}
```

Upload de code en de servo beweegt van 0° naar 180°. In de volgende hoofdstukken leggen we uit hoe u een servo aanstuurt. Daarnaast kunt u een servo aansturen met een servobibliotheek van Arduino.

<span style="color: rgb(255, 76, 65);">Opmerking:</span> Dit servobestand gebruikt timer 1, en de PWM-uitvoer van IO-poorten 9 en 10 gebruikt ook timer 1. Daarom kunnen we deze servobestand niet gebruiken wanneer we later de PWM-uitvoer van D9 en D10 gebruiken.

#### **(5)Testcode 2:**

(<span style="color: rgb(255, 76, 65);">Opmerking: </span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruikmaakt van seriële communicatie, en er mogelijk conflicten ontstaan met de seriële communicatie van de Bluetooth, waardoor het uploaden van de code kan mislukken.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.2
Servo
<http://www.keyestudio.com>
*/

#include <Servo.h>

Servo myservo; // maak servos aan
int pos = 0; // Sla de variabelen van de hoek op

void setup() 
{
	myservo.attach(10); //Verbind de servo met digitale poort 10
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  //Van 0° naar 180°
    {
    	//stapgrootte is 1
        myservo.write(pos); // Draai naar de hoek van 'pos'
        delay(15); // Wacht 15ms om de snelheid te regelen
    }

    for (pos = 180; pos >= 0; pos -= 1)  //Van 180° naar 0°
    {
        myservo.write(pos); // Draai naar de hoek van 'pos'
        delay(15); // Wacht 15ms om de snelheid te regelen
    }
}
```

#### **(6)Testresultaten:**

Upload de code, sluit de voeding aan en de servo beweegt binnen het bereik van 0° en 180°.

![](./media/img-20240117090810.png)

#### **(7)Codeuitleg:**

Arduino wordt geleverd met **\#include \<Servo.h\>** (servofunctie en -statements)

Hieronder staan enkele veelgebruikte statements van de servofunctie:

1\. **attach（interface）**——Stel de servo-interface in, poort 9 en 10 zijn beschikbaar

2\. **write（angle）**——Het statement om de draaihoek van de servo in te stellen, het hoekbereik is van 0° tot 180°

3\. **read（）**——Het statement om de hoek van de servo te lezen, leest de commandowaarde van "write()"

4\. **attached（）**——Controleer of de parameter van de servo naar de interface is verzonden

Opmerking: Het bovenstaande schrijfformaat is "servo variabelenaam, specifiek statement（）", bijvoorbeeld: myservo.attach(10)