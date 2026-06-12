### Project 23: Brandblussende Robot Meerdere Functies


#### **(1)Beschrijving:**

De slimme auto heeft in elk vorig project een enkele functie uitgevoerd.

Kan hij meerdere functies tegelijk weergeven? Ja.

In dit laatste grote project willen we een volledige code gebruiken om de slimme auto te bedienen zodat alle functies die in eerdere projecten zijn besproken worden getoond. We gebruiken de knoppen op de Bluetooth-app om automatisch tussen verschillende functies te wisselen, heel eenvoudig en handig.



#### **(2)Stroomdiagram:**

<span style="color: rgb(255, 76, 65);">**Raadpleeg Project 16 voor het installeren en configureren van de Bluetooth-app**</span>

![](media/image-20230427102547633.png)

#### **(3)Aansluitschema:**

![](media/e7ac834ba04aa2e8862995d2d33ce9356.jpg)

1\. GND, VCC, SDA, en SCL van het 8x16-bord zijn verbonden met G (GND), + (VCC), A4, en A5 van het uitbreidingsbord.

2\. VCC, IN+, IN-, en Gnd van de ventilatormodule zijn verbonden met 5V (V), 12 (S), 13 (S), en Gnd (G).

3\. De bruine draad, rode draad, en oranje draad van de servo zijn verbonden met Gnd (G), 5v (V), en D10.

4\. RXD, TXD, GND, en VCC van de BT-module zijn verbonden met TX, RX, G (GND), en 5V (VCC). STATE en BRK hoeven niet te worden aangesloten.

5\. De pinnen "G", "V", en A van de linker vlamsensor zijn verbonden met respectievelijk G (GND), V (VCC), en A1; De rechter vlamsensor is verbonden met G (GND), V (VCC), en A2.

6\. De distale poorten van de lijnvolgensor zijn 11, 7, en 8.

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 23
  Fire Extinguishing Robot Multiple Functions
  http://www.keyestudio.com
*/
#include <IRremote.h>
IRrecv irrecv(3);  //
decode_results results;
long ir_rec;  // gebruikt om de IR-waarde op te slaan

/***********/
#define USE_FAN_FUNCTION   1

// Array, gebruikt om gegevens van afbeeldingen op te slaan, kan zelf berekend worden of verkregen via modulustool
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

unsigned char Smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};
unsigned char Disgust[] = {0x00, 0x00, 0x02, 0x02, 0x02, 0x12, 0x08, 0x04, 0x08, 0x12, 0x22, 0x02, 0x02, 0x00, 0x00, 0x00};
unsigned char Happy[] = {0x02, 0x02, 0x02, 0x02, 0x08, 0x18, 0x28, 0x48, 0x28, 0x18, 0x08, 0x02, 0x02, 0x02, 0x02, 0x00};
unsigned char Squint[] = {0x00, 0x00, 0x00, 0x41, 0x22, 0x14, 0x48, 0x40, 0x40, 0x48, 0x14, 0x22, 0x41, 0x00, 0x00, 0x00};
unsigned char Despise[] = {0x00, 0x00, 0x06, 0x04, 0x04, 0x04, 0x24, 0x20, 0x20, 0x26, 0x04, 0x04, 0x04, 0x04, 0x00, 0x00};
unsigned char Heart[] = {0x00, 0x00, 0x0C, 0x1E, 0x3F, 0x7F, 0xFE, 0xFC, 0xFE, 0x7F, 0x3F, 0x1E, 0x0C, 0x00, 0x00, 0x00};

unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  // stel de pin van de klok in op A5
#define SDA_Pin  A4  // stel de datapen in op A4

#define ML_Ctrl 4  // definieer de richtingsbesturingspin van de linkermotor als 4
#define ML_PWM 6   // definieer de PWM-besturingspin van de linkermotor
#define MR_Ctrl 2  // definieer de richtingsbesturingspin van de rechtersensor
#define MR_PWM 5   // definieer de PWM-besturingspin van de rechtermotor
char ble_val;      // gebruikt om de Bluetooth-waarde op te slaan
byte speeds_L = 200; // de beginsnelheid van de linkermotor is 200
byte speeds_R = 200; // de beginsnelheid van de rechtermotor is 200
String speeds_l, speeds_r; // ontvang PWM-tekens en converteer ze naar PWM-waarde

// bedrading van de lijnvolgensor
#define L_pin  11  // links
#define M_pin  7  // midden
#define R_pin  8  // rechts
int L_val, M_val, R_val;

#if USE_FAN_FUNCTION  /****gebruik ventilator*******/
int flame_L = A1; // definieer de analoge poort van de linker vlamsensor als A1
int flame_R = A2; // definieer de analoge poort van de rechter vlamsensor als A2
int flame_valL, flame_valR;

// de pin van de 130-motor
int INA = 12;
int INB = 13;

#else /****gebruik de ultrasone sensor*******/
#define servoPin    10  // servo Pin
#define light_L_Pin A1   // definieer de pin van de linker lichtgevoelige weerstand
#define light_R_Pin A2   // definieer de pin van de rechter lichtgevoelige weerstand
int left_light;
int right_light;

#define Trig 12
#define Echo 13
float distance;// Sla de afstandswaarden op die door ultrasoon worden gedetecteerd voor volgfunctie

// Sla de afstandswaarden op die door ultrasoon worden gedetecteerd voor hindernisontwijking
int a;
int a1;
int a2;

#endif

bool flag;  // vlag variabele, gebruikt om een modus te betreden en te verlaten

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  // Initialiseer de bibliotheek van de IR-afstandsbediening

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(L_pin, INPUT); // definieer de pinnen van sensoren als INPUT
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);

  matrix_display(clear);    // scherm wissen
  matrix_display(start01);  // start tonen

#if USE_FAN_FUNCTION/****gebruik de ventilator*******/
  pinMode(INA, OUTPUT);// stel INA in als OUTPUT
  pinMode(INB, OUTPUT);// stel INB in als OUTPUT

  // definieer ingangen van de vlamsensor
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
#else/****gebruik de ultrasone sensor*******/
  pinMode(servoPin, OUTPUT);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);

  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  procedure(90); // stel de hoek van de servo in op 90°
#endif
}

void loop() 
{
  if (Serial.available()) // als er gegevens in de seriële buffer zijn
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
    switch (ble_val) 
    {
      case 'F': Car_front(); break; // het commando om vooruit te gaan

      case 'B': Car_back(); break;  // het commando om achteruit te gaan

      case 'L': Car_left(); break;  // het commando om links af te slaan

      case 'R': Car_right(); break; // het commando om rechts af te slaan

      case 'S': Car_Stop();  break; // stoppen

      case 'e': Tracking();  break; // de lijnvolgmodus activeren

      case 'f': Confinement(); break;  // de inperkingsmodus activeren

#if USE_FAN_FUNCTION/****gebruik ventilator*******/
      case 'j': Fire(); break;  // brandblussingsmodus inschakelen

      case 'c': fan_begin(); break;  // de ventilator inschakelen

      case 'd': fan_stop();  break;  // de ventilator uitschakelen

#else/****gebruik de ultrasone sensor*******/
      case 'g': Avoid(); break;  // hindernisontwijkingsmodus activeren

      case 'h': Follow(); break;  // volgmodus activeren

      case 'i': Light_following();  break;  // lichtvolg modus activeren
#endif
      case 'u': 
        speeds_l = Serial.readStringUntil('#'); 
        speeds_L = String(speeds_l).toInt(); 
        break; // begin met ontvangen van u, eindig met ontvangen van tekens # en converteer naar het geheel getal

      case 'v': 
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt(); 
        break; // begin met ontvangen van u, eindig met ontvangen van tekens # en converteer naar het geheel getal

      case 'k': matrix_display(Smile);    break;  // toon "glimlach" gezicht
      case 'l': matrix_display(Disgust);  break;  // toon "walging" gezicht
      case 'm': matrix_display(Happy);    break;  // toon "blij" gezicht
      case 'n': matrix_display(Squint);   break;  // toon "verdrietig" gezicht
      case 'o': matrix_display(Despise);  break;  // toon "minachting" gezicht
      case 'p': matrix_display(Heart);    break;  // toon de hartslag afbeelding
      case 'z': matrix_display(clear);    break;  // afbeeldingen wissen

      default: break;
    }
  }

#if (USE_FAN_FUNCTION != 1)/****de functie om de ventilator niet te gebruiken*******/
  // De volgende drie signalen worden voornamelijk gebruikt voor cyclisch afdrukken
  if (ble_val == 'x') 
  {
    distance = checkdistance(); Serial.println(distance);
    delay(50);
  } 
  else if (ble_val == 'w') 
  {
    left_light = analogRead(light_L_Pin);
    Serial.println(left_light);
    delay(50);
  } 
  else if (ble_val == 'y') 
  {
    right_light = analogRead(light_R_Pin);
    Serial.println(right_light);
    delay(50);
  }
#endif

  if (irrecv.decode(&results))  // Infrarood afstandsbedieningswaarde ontvangen
  {
    ir_rec = results.value;
    Serial.println(ir_rec, HEX);
    switch (ir_rec) 
    {
      case 0xFF629D: Car_front();   break;   // vooruit gaan
      case 0xFFA857: Car_back();    break;   // achteruit gaan
      case 0xFF22DD: Car_left();    break;   // naar links draaien
      case 0xFFC23D: Car_right();   break;   // naar rechts draaien
      case 0xFF02FD: Car_Stop();    break;   // stoppen
      default: break;
    }
    irrecv.resume();
  }
}

#if (USE_FAN_FUNCTION != 1)/****gebruik de ultrasone sensor*******/

// Bedien de ultrasone sensor
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //
  delay(10);
  return distance;
}


// de functie om de servo te bedienen
void procedure(int myangle) 
{
  int pulsewidth;
  pulsewidth = map(myangle, 0, 180, 500, 2000);  // Bereken de pulsbreedtewaarde, dit moet de afbeeldingswaarde zijn van 500 tot 2500. Rekening houdend met de invloed van de infraroodbibliotheek wordt hier 500~2000 gebruikt.
  for (int i = 0; i < 5; i++) 
  {
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   // De duur van het hoge niveau is de pulsbreedte
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  // De periode is 20ms, dus het lage niveau duurt de rest van de tijd
  }
}

/*****************hindernisontwijking******************/
void Avoid()
{
  flag = 0;
  while (flag == 0)
  {
    a = checkdistance();  // de voorste afstand wordt ingesteld op a
    if (a < 20) // Wanneer de afstand voor minder dan 20cm is
    {
      Car_Stop();  // stoppen
      delay(500); // vertraging van 500ms
      procedure(180);  // servo draait naar links
      delay(500); // vertraging van 500ms
      a1 = checkdistance();  // de linkerafstand wordt ingesteld op a1
      delay(100); // waarde lezen

      procedure(0); // servo draait naar rechts
      delay(500); // vertraging van 500ms
      a2 = checkdistance(); // de rechterafstand wordt ingesteld op a2
      delay(100); // waarde lezen

      procedure(90);  // terug naar 90°
      delay(500);
      if (a1 > a2)  // Wanneer de afstand links groter is dan de afstand rechts
      {
        Car_left();  // de robot draait naar links
        delay(700);  // draai 700ms naar links
      } 
      else 
      {
        Car_right(); // naar rechts draaien
        delay(700);
      }
    }
    else  // als de voorste afstand ≥20cm is, gaat de robot vooruit
    {
      Car_front(); // vooruit gaan
    }
    // ontvang de Bluetooth-waarde om de lus te verlaten
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S')  // ontvang S
      {
        flag = 1;  // Stel vlag in op 1 om de lus te verlaten
        Car_Stop();
      }
    }
  }
}

/*******************volgen***************/
void Follow() 
{
  flag = 0;
  while (flag == 0) 
  {
    distance = checkdistance();  // stel de afstandswaarde in op distance
    if (distance >= 20 && distance <= 60) // vooruit gaan
    {
      Car_front();
    }
    else if (distance > 10 && distance < 20)  // stoppen
    {
      Car_Stop();
    }
    else if (distance <= 10)  // achteruit gaan
    {
      Car_back();
    }
    else  // stoppen
    {
      Car_Stop();
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S')
      {
        flag = 1;  // verlaat de lus
        Car_Stop();
      }
    }
  }
}

/****************licht volgen******************/
void Light_following() 
{
  flag = 0;
  while (flag == 0) 
  {
    left_light = analogRead(light_L_Pin);
    right_light = analogRead(light_R_Pin);
    if (left_light > 650 && right_light > 650) // vooruit gaan
    {
      Car_front();
    }
    else if (left_light > 650 && right_light <= 650)  // naar links draaien
    {
      Car_left();
    }
    else if (left_light <= 650 && right_light > 650) // naar rechts draaien
    {
      Car_right();
    }
    else  // anders, stoppen
    {
      Car_Stop();
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

#else/****gebruik de ventilator*******/
/***************ventilator inschakelen*****************/
void fan_begin() 
{
  digitalWrite(INA, LOW);
  digitalWrite(INB, HIGH);
}

/***************ventilator stoppen*****************/
void fan_stop() 
{
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

/***************brand blussen****************/
void Fire() 
{
  flag = 0;
  while (flag == 0) 
  {
    // Lees de analoge waarde van de vlamsensor
    flame_valL = analogRead(flame_L);
    flame_valR = analogRead(flame_R);
    if (flame_valL <= 700 || flame_valR <= 700) 
    {
      Car_Stop();
      fan_begin();
    } 
    else 
    {
      fan_stop();
      L_val = digitalRead(L_pin); // Lees de waarde van de linker sensor
      M_val = digitalRead(M_pin); // Lees de waarde van de linker sensor
      R_val = digitalRead(R_pin); // Lees de waarde van de rechter sensor
```

```
      if (M_val == 1)  //de middelste detecteert zwarte lijnen
      {
        if (L_val == 1 && R_val == 0)  //Als een zwarte lijn links wordt gedetecteerd, maar niet rechts, draai links
        {
          Car_left();
        }
        else if (L_val == 0 && R_val == 1)  //Als een zwarte lijn rechts wordt gedetecteerd, niet links, draai rechts
        {
          Car_right();
        }
        else //ga vooruit
        { 
          Car_front();
        }
      }
      else //de middelste detecteert zwarte lijnen
      { 
        if (L_val == 1 && R_val == 0) //Als een zwarte lijn links wordt gedetecteerd, maar niet rechts, draai links
        { 
          Car_left();
        }
        else if (L_val == 0 && R_val == 1) //Als een zwarte lijn rechts wordt gedetecteerd, niet links, draai rechts
        { 
          Car_right();
        }
        else //anders stoppen
        { 
          Car_Stop();
        }
      }
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

#endif

/***************lijnvolgen*****************/
void Tracking() 
{
  flag = 0;
  while (flag == 0) 
  {
    L_val = digitalRead(L_pin); //Lees de waarde van de linkersensor
    M_val = digitalRead(M_pin); //Lees de waarde van de middelste sensor
    R_val = digitalRead(R_pin); //Lees de waarde van de rechtssensor
    if (M_val == 1)  //de middelste detecteert zwarte lijnen
    {
      if (L_val == 1 && R_val == 0) //Als een zwarte lijn links wordt gedetecteerd, maar niet rechts, draai links
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1) //Als een zwarte lijn rechts wordt gedetecteerd, niet links, draai rechts
      { 
        Car_right();
      }
      else //ga vooruit
      { 
        Car_front();
      }
    }
    else //de middelste sensor detecteert geen zwarte lijnen
    { 
      if (L_val == 1 && R_val == 0) //Als een zwarte lijn links wordt gedetecteerd, maar niet rechts, draai links
      { 
        Car_left();
      }
      else if (L_val == 0 && R_val == 1) //Als een zwarte lijn rechts wordt gedetecteerd, niet links, draai rechts
      { 
        Car_right();
      }
      else //anders stoppen
      { 
        Car_Stop();
      }
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

/***************Begrenzing*****************/
void Confinement() 
{
  flag = 0;
  while (flag == 0) 
  {
    L_val = digitalRead(L_pin); //Lees de waarde van de linkersensor
    M_val = digitalRead(M_pin); //Lees de waarde van de middelste sensor
    R_val = digitalRead(R_pin); //Lees de waarde van de rechtssensor
    if ( L_val == 0 && M_val == 0 && R_val == 0 ) //Ga vooruit wanneer er geen zwarte lijnen worden gedetecteerd   
    {    
        Car_front();
    }
    else 
    { 
      Car_back();
      delay(700);
      Car_left();
      delay(800);
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}


/***************puntmatrix******************/
//deze functie wordt gebruikt voor de weergave van de puntmatrix 
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  //gebruik de functie om gegevensoverdracht te starten
  IIC_send(0xc0);  //selecteer een adres
  for (int i = 0; i < 16; i++) //afbeeldingsgegevens hebben 16 tekens
  {
    IIC_send(matrix_value[i]); //gegevens om afbeeldingen te verzenden
  }
  IIC_end();   //beëindig de gegevensoverdracht van afbeeldingen
  IIC_start();
  IIC_send(0x8A);  //toon besturing en selecteer pulsbreedte 4/16
  IIC_end();
}

//de conditie waaronder gegevensoverdracht begint
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

//gegevens verzenden
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) //elk teken heeft 8 cijfers, die één voor één worden gedetecteerd
  {
    if (send_data & mask)  //stel hoge of lage niveaus in op basis van elk bit (0 of 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); //trek de klokpin SCL_Pin omhoog om de gegevensoverdracht te beëindigen
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); //trek de klokpin SCL_Pin omlaag om signalen van SDA te wijzigen 
  }
}

//het teken dat gegevensoverdracht eindigt
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

/***************motor rijdt****************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  //toon de afbeelding van achteruitrijden
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  //toon de afbeelding van vooruitrijden
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  //toon de afbeelding van links afslaan
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(right);  //toon de afbeelding van rechts afslaan
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  //toon de stopafbeelding
}
```

#### (5)Testresultaat

Voordat de programmacode wordt geüpload, moet de Bluetooth-module worden verwijderd; anders mislukt het uploaden van de code.

Na het succesvol uploaden van de code, schakel de locatieservices in op uw apparaat en verbind vervolgens de Bluetooth-module.

Zodra de Bluetooth-module is aangesloten en ingeschakeld, en de mobiele APP succesvol verbonden is met de Bluetooth, kunnen we de mobiele APP gebruiken om de tankrobot te besturen.

U kunt de robot ook bedienen met de afstandsbediening.

![](media/13656cfee75dc5acbeba18a90a084e159.jpg)