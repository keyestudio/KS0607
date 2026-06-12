### Project 15: IR Afstandsbediening Tank

![](./media/image-20250709113214889.png)


#### **(1)Beschrijving:**

Infrarood afstandsbediening is een van de meest voorkomende toepassingen van afstandsbediening in elektrische motoren, elektrische ventilatoren en vele andere huishoudelijke apparaten. In dit project gebruiken we de kennis die we eerder hebben geleerd om een infrarood afstandsbediening slimme auto te maken.

In les 9 hebben we de bijbehorende toetswaarde van elke toets van de infrarood afstandsbediening getest. In het project kunnen we de code (toetswaarde) instellen om de bijbehorende knop de bewegingen van de slimme auto te laten besturen, en de bewegingspatronen weergeven op het 8X16 LED-dotmatrix.

De specifieke logica van de lijnvolgend slimme auto is weergegeven in de tabel:

|                        Ultrasone toets                        | Toetswaarde |                    Instructies van toetsen                    |
| :----------------------------------------------------------: | :-------: | :----------------------------------------------------------: |
| ![image-20230427094710725](media/image-20230427094710725.png) |  FF629D   | Vooruit rijden（stel PWM in op 200）<br />toon het patroon van vooruitrijden |
| ![image-20230427094716639](media/image-20230427094716639.png) |  FFA857   | Achteruit rijden（stel PWM in op 200）<br />toon het patroon van achteruitrijden |
| ![image-20230427094720417](media/image-20230427094720417.png) |  FF22DD   |           Links afslaan<br />toon het patroon "STOP"           |
| ![image-20230427094725151](media/image-20230427094725151.png) |  FFC23D   |     Rechts afslaan<br />toon het patroon van links afslaan      |
| ![image-20230427094729839](media/image-20230427094729839.png) |  FF02FD   |             Stoppen<br />toon het patroon "STOP"              |

**Begininstelling**: 8X16 LED-dotmatrix toont het patroon"![](media/wps20.jpg)".



#### **(2)Stroomschema:**

![](media/wps21.png)

#### **(3)Aansluitschema:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span>

GND, VCC, SDA en SCL van het 8x16 LED-paneel zijn verbonden met G（GND), V（VCC). SDA en SCL van het uitbreidingsbord.

Omdat het 8833-bord de IR-ontvanger integreert, hoeft u het niet aan te sluiten. De pinnen van de IR-ontvanger zijn G（GND), V（VCC) en D3.

#### (4)**Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook seriële communicatie gebruikt, en er mogelijk conflicten zijn met de Bluetooth seriële communicatie, wat kan leiden tot een mislukte upload.)

```C
/*
 Keyestudio Mini Tank Robot V3 (Popular Edition)
 lesson 15
 IRremote Control Tank
 http://www.keyestudio.com
*/
#include <IRremote.h>
IRrecv irrecv(3);  //
decode_results results;
long ir_rec;  // Gebruikt om de ontvangen infraroodwaarden op te slaan

// Array, gebruikt om gegevens van afbeeldingen op te slaan, kan zelf berekend worden of verkregen via modulustool
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  // Stel de klokpin in als A5
#define SDA_Pin  A4  // Stel de datapin in als A4

#define ML_Ctrl 4  // Definieer de richtingsbesturingspin van de linkermotor
#define ML_PWM 6   // Definieer de PWM-besturingspin van de linkermotor
#define MR_Ctrl 2  // Definieer de richtingsbesturingspin van de rechtermotor
#define MR_PWM 5    // Definieer de PWM-besturingspin van de rechtermotor

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  // Initialiseer de infrarood ontvanger bibliotheek

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // schermen wissen
  matrix_display(start01);  // toon de afbeelding om te starten
}

void loop() 
{
  if (irrecv.decode(&results))  // Ontvang infrarood afstandsbesturingswaarde
  {
    ir_rec = results.value;
    String type = "UNKNOWN";
    String typelist[14] = {"UNKNOWN", "NEC", "SONY", "RC5", "RC6", "DISH", "SHARP", "PANASONIC", "JVC", "SANYO", "MITSUBISHI", "SAMSUNG", "LG", "WHYNTER"};
    if (results.decode_type >= 1 && results.decode_type <= 13) 
    {
      type = typelist[results.decode_type];
    }
    Serial.print("IR TYPE:" + type + "  ");
    Serial.println(ir_rec, HEX);
    irrecv.resume();
  }

  switch (ir_rec) 
  {
    case 0xFF629D: Car_front();     break;   // het commando om vooruit te rijden
    case 0xFFA857: Car_back();      break;   // het commando om achteruit te rijden
    case 0xFF22DD: Car_T_left();    break;   // het commando om links af te slaan
    case 0xFFC23D: Car_T_right();   break;   // het commando om rechts af te slaan
    case 0xFF02FD: Car_Stop();      break;   // het commando om te stoppen
    case 0xFF30CF: Car_left();      break;   // het commando om naar links te draaien
    case 0xFF7A85: Car_right();     break;   // het commando om naar rechts te draaien
    default: break;
  }
}

/***************De functie om de motor aan te sturen***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  // Achteruit rijden
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(front);  // toon de afbeelding om vooruit te rijden
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  // toon de afbeelding om links af te slaan
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
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

void Car_T_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
  matrix_display(left);  // toon de afbeelding om links af te slaan
}

void Car_T_right() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 0);
  matrix_display(right);  // toon de afbeelding om rechts af te slaan
}

// Deze functie wordt gebruikt voor weergave op het dotmatrixscherm
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Functie om de startconditie voor gegevensoverdracht aan te roepen
  IIC_send(0xc0);  // Kies een adres
  for (int i = 0; i < 16; i++) // Patroongegevens hebben 16 bytes
  {
    IIC_send(matrix_value[i]); // patroongegevens overdragen
  }
  IIC_end();   // Einde patroongegevensoverdracht
  IIC_start();
  IIC_send(0x8A);  // weergavebesturing, selecteer pulsbreedte als 4/16
  IIC_end();
}

// Voorwaarden voor het starten van gegevensoverdracht
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
    digitalWrite(SCL_Pin, LOW); // Trek de klokpin SCL_Pin omlaag om signalen van SDA te wijzigen
  }
}
```

#### **(5)Testresultaat:**

Na het uploaden van de code, zet de aan/uit-schakelaar van het motoraandrijfschild aan. Plaats de robot op de vloer, raadpleeg de bovenstaande tabel en druk op verschillende knoppen; de robot beweegt in de bijbehorende vooraf ingestelde richting.

![](./media/img-20240117090114.png)