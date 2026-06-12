### Project 18: BT Snelheidsregeling Robot

#### (1)**Beschrijving:**

In het vorige project hebben we geleerd hoe we de slimme tank met Bluetooth kunnen besturen. De PWM-waarde van de motor die we eerder gebruikten is 200 (de snelheid is 200).

In deze les gebruiken we Bluetooth om de snelheid van de slimme auto aan te passen. Het is niet beperkt tot een vaste snelheid van 200. We definiëren twee variabelen om de snelheidswaarden van respectievelijk de linker- en rechtermotor op te slaan. Door het vorige onderzoek weten we dat het bereik van deze waarde alleen 0 tot 255 kan zijn.

#### **(2)Stroomdiagram:**

![](media/image-20230427102042028.png)

#### **(3)Aansluitingsschema:**

![](media/930a8024364e07505e845624a94c27bd.png)

De GND, VCC, SDA en SCL van de 8x16 LED dot matrix zijn respectievelijk verbonden met -(GND), + (VCC), SDA, SCL van het uitbreidingsbord;

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">Opmerking:</span> Bij het uploaden van de code moet de Bluetooth-module worden losgekoppeld. De Bluetooth kan opnieuw worden verbonden nadat het uploadproces is voltooid. Anders wordt de code mogelijk niet ingebrand.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 18
  bluetooth control speed tank
  http://www.keyestudio.com
*/

// Array, gebruikt om gegevens van afbeeldingen op te slaan, kan zelf worden berekend of verkregen via een modulustool
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char speed_a[] = {0x00, 0x00, 0x00, 0x20, 0x10, 0x08, 0x04, 0x02, 0xff, 0x02, 0x04, 0x08, 0x10, 0x20, 0x00, 0x00};
unsigned char speed_d[] = {0x00, 0x00, 0x00, 0x04, 0x08, 0x10, 0x20, 0x40, 0xff, 0x40, 0x20, 0x10, 0x08, 0x04, 0x00, 0x00};
#define SCL_Pin  A5  // stel de pin van de klok in op A5
#define SDA_Pin  A4  // stel de datapin in op A4

#define ML_Ctrl 4  // definieer de richtingsstuurpin van de linkermotor
#define ML_PWM 6   // definieer de PWM-stuurpinnen van de linkermotor
#define MR_Ctrl 2  // definieer de richtingsstuurpin van de rechtermotor
#define MR_PWM 5   // definieer de PWM-stuurpin van de rechtermotor
char ble_val;      // definieer de PWM-stuurpin van de rechtermotor
byte speeds_L = 200; // De beginsnelheid van de linkermotor is 200
byte speeds_R = 200; // De beginsnelheid van de rechtermotor is 200
String speeds_l, speeds_r; // Ontvang een tekenreeks van PWM om te converteren naar een geheel getal PWM-waarde

void setup() 
{
  Serial.begin(9600);

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // scherm wissen
  matrix_display(start01);  // toon de afbeelding om te starten
}

void loop() 
{
  if (Serial.available() > 0) 
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
    switch (ble_val) 
    {
      case 'F':  // het commando om vooruit te rijden
        Car_front();
        break;
      case 'B':  // het commando om achteruit te rijden
        Car_back();
        break;
      case 'L':  // het commando om links af te slaan
        Car_left();
        break;
      case 'R':  // het commando om rechts af te slaan
        Car_right();
        break;
      case 'S':  // het commando om te stoppen
        Car_Stop();
        break;
      case 'u':  // Ontvang een tekenreeks die begint met u en eindigt met #, en converteer deze naar een geheel getal waarde
        speeds_l = Serial.readStringUntil('#');
        speeds_L = String(speeds_l).toInt();
        break;
      case 'v':  // Ontvang een tekenreeks die begint met v en eindigt met #, en converteer deze naar een geheel getal waarde
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt();
        break;
    }
  }
}

/***************De functie om de motor te laten draaien***************/

void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  // Rijdt achteruit
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  // toon de afbeelding om vooruit te rijden
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  // toon de afbeelding om links af te slaan
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(right);  // toon de afbeelding om rechts af te slaan
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // toon de afbeelding om te stoppen
}

// Deze functie wordt gebruikt voor de weergave op het dot matrix scherm
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Functie om de startconditie voor gegevensoverdracht aan te roepen
  IIC_send(0xc0);  // Kies een adres
  for (int i = 0; i < 16; i++) // Patroongegevens hebben 16 bytes
  {
    IIC_send(matrix_value[i]); // patroongegevens overdragen
  }
  IIC_end();   // Beëindig de overdracht van patroongegevens
  IIC_start();
  IIC_send(0x8A);  // weergavebesturing, selecteer pulsbreedte als 4/16
  IIC_end();
}

// Condities voor het starten van gegevensoverdracht
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// het teken van het beëindigen van gegevensoverdracht
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

// gegevens overdragen
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // elk teken heeft 8 cijfers, die één voor één worden gedetecteerd
  {
    if (send_data & mask)  // stel hoge of lage niveaus in op basis van elk bit (0 of 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Trek de klokpin SCL_Pin hoog om gegevensoverdracht te stoppen
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // trek de klokpin SCL_Pin omlaag om signalen van SDA te wijzigen
  }
}
```

#### **(5)Testresultaten:**

Na het succesvol uploaden van de testcode, de DIP-schakelaar naar de rechterkant omzetten, de stroom inschakelen en de APP met Bluetooth koppelen, kan de slimme auto worden bestuurd om te bewegen via de APP. De snelheid van de auto kan worden geregeld door de snelheidsregelaars van de linker- en rechtermotor te verschuiven.

![](media/b9c902b937801f829b9ce2fd254b1849.jpeg)

(U kunt de functietabel in project 17 raadplegen)