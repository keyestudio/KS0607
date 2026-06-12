### Project 7: IR Ontvangst

#### **(1)Beschrijving:**

![](media/8969111328604c5358f7c915ac94e474.png)

Het is onbetwistbaar dat infrarood afstandsbediening alomtegenwoordig is in het dagelijks leven. Het wordt gebruikt om verschillende huishoudelijke apparaten te bedienen, zoals tv's, stereo's, videorecorders en satellietontvangers. Infrarood afstandsbediening bestaat uit infrarood zend- en ontvangssystemen, dat wil zeggen een infrarood afstandsbediening en een infrarood ontvangstmodule en een microcontroller die kan decoderen.

Het 38K infrarood draaggolfsignaal dat door de afstandsbediening wordt uitgezonden, wordt gecodeerd door de coderingschip in de afstandsbediening. Het bestaat uit een stuk pilootcode, gebruikerscode, gebruikers inverse code, datacode en data inverse code. Het tijdsinterval van de puls wordt gebruikt om te onderscheiden of het een 0 of 1 signaal is, en de codering bestaat uit deze 0 en 1 signalen.

De gebruikerscode van dezelfde afstandsbediening blijft ongewijzigd, terwijl de datacode de toets kan onderscheiden.

Wanneer de knop van de afstandsbediening wordt ingedrukt, verzendt de afstandsbediening een infrarood draaggolfsignaal. Wanneer de IR-ontvanger het signaal ontvangt, zal het programma het draaggolfsignaal decoderen en bepalen welke toets is ingedrukt. De MCU decodeert het ontvangen 01-signaal en bepaalt daarmee welke toets op de afstandsbediening is ingedrukt.

![](media/image-20230426172824683.png)

De infrarood ontvanger is gesoldeerd op de motordriverkaart. Het integreert ontvangst, versterking en demodulatie, waarbij de interne IC al is afgesteld voor infrarood ontvangst en uitvoer, en werkt compatibel met TTL-signalen. Het geeft digitale signalen uit en is geschikt voor infrarood afstandsbediening en infrarood datatransmissie. Deze module heeft slechts drie pinnen, waaronder signaal, VCC en GND, waardoor het zeer eenvoudig is om te verbinden en te communiceren met microcontrollers zoals arduino.

#### **(2)Parameters:**

Bedrijfsspanning: 3.3-5V（DC）

Interface: 3PIN

Uitgangssignaal: Digitaal signaal

Ontvangsthoek: 90 graden

Frequentie: 38khz

Ontvangstafstand: 10m

Infrarood ontvanger geïntegreerd op de motordriverkaart：

![](./media/img-20240117082433.png)




#### **(3)Testcode:**

U moet eerst de IR-bibliotheek importeren.

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden mislukt.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 7.1

IRremote

http://www.keyestudio.com

*/

#include <IRremote.h> // IRremote bibliotheek declaratie

int RECV_PIN = 3; //definieer de pinnen van de IR-ontvanger als 3
IRrecv irrecv(RECV_PIN);
decode_results results; //decodeerresultaten staan in het "result" van "decode results"

void setup() 
{
    Serial.begin(9600);
    irrecv.enableIRIn(); //Ontvanger inschakelen
}

void loop() 
{
    if (irrecv.decode(&results))//succesvol gedecodeerd, een reeks infraroodsignalen ontvangen
    {
        Serial.println(results.value, HEX);//Woord in 16 HEX weergeven om ontvangen code te tonen
        irrecv.resume(); //Ontvang de volgende waarde
    }
    delay(100);
}
```

#### **(4)Testresultaten:**

Upload de testcode, open de seriële monitor en stel de baudrate in op 9600, richt de afstandsbediening op de IR-ontvanger. De bijbehorende waarde wordt dan weergegeven. Als u de toetsen een tijdje ingedrukt houdt, verschijnen er foutcodes.

![](media/a484b81d031c8d6e8addb169136fd45c.png)

Hieronder hebben we de waarde van elke knop van de keyestudio afstandsbediening vermeld. U kunt dit bewaren als naslagwerk.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

De IR-ontvanger is verbonden met D3, dus we hoeven geen bedrading aan te sluiten

#### **(5)Code Uitleg:**

**irrecv.enableIRIn():** na het inschakelen van IR-decodering worden de IR-signalen ontvangen, vervolgens zal de functie "decode()" continu controleren of het decoderen succesvol is.

**irrecv.decode(&results):** na succesvol decoderen zal deze functie "true" teruggeven en het resultaat opslaan in "results". Na het decoderen van een IR-signaal, voer de functie resume() uit en ontvang het volgende signaal.

#### **(6)Uitbreidingsoefening:**

We hebben de toetswaarde van de IR-afstandsbediening gedecodeerd. Wat dacht u ervan om de LED te bedienen met de gemeten waarde? We kunnen een experiment ontwerpen.

Sluit een LED aan op D9, druk vervolgens op de toetsen van de afstandsbediening om de LED aan en uit te zetten.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden mislukt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 7.2
IRremote
http://www.keyestudio.com
*/

#include <IRremote.h> //IRremote declaratie

int RECV_PIN = 3; //definieer de pin van LED als pin 3
int LED = 9;
bool flag = 0;
IRrecv irrecv(RECV_PIN);
decode_results results; //decodeerresultaten staan in het "result" van "decode results"

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);//stel LED in als uitgang
    irrecv.enableIRIn(); //Ontvanger inschakelen
}

void loop() 
{
    if (irrecv.decode(&results)) 
    {
        if (results.value == 0xFF02FD & flag == 0) //De bovenstaande toetscode, we gebruiken de OK-knop op de afstandsbediening, als u op de OK-knop drukt
        {
            digitalWrite(LED, HIGH); //LED aan
            flag = 1;
        }

        else if (results.value == 0xFF02FD & flag == 1) //opnieuw indrukken
        {
            digitalWrite(LED, LOW); //LED uit
            flag = 0;
        }
        irrecv.resume(); // Ontvang de volgende waarde
    }
}
```

Upload de code naar het ontwikkelbord en druk op de "OK" toets op de afstandsbediening om de LED aan en uit te zetten.

![](./media/img-20240117090645.png)