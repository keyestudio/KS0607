### Project 17: Bluetooth Control Tank


#### **(1)Beschrijving:**

We hebben de basiskennis van Bluetooth geleerd in het vorige project. In deze les gebruiken we Bluetooth om de slimme auto te besturen. Omdat het Bluetooth betreft, zijn een zender en een ontvanger nodig. In het project gebruiken we de mobiele telefoon als zender (master), en de slimme auto verbonden met de HM-10 Bluetooth-module (slave) als ontvanger.

We hebben eerder geleerd dat het verzenden van een bit LED's kan besturen. Het principe van het besturen van deze robotauto is hetzelfde.

We begrijpen eerst de functie van elke knop op de APP, en gebruiken dan de knop op de APP om de tank te besturen.

#### **(2)Hoofdfuncties op de APP**

De volgende tabel illustreert de functies van de bijbehorende knoppen:

|                      KNOPPEN                       | FUNCTIES                                                    |
| :---------------------------------------------: | ------------------------------------------------------------ |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) | Koppelen en verbinden met HM-10 Bluetooth-module; klik nogmaals om te verbreken |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) | Selecteer de robot om te bedienen                                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) | Om de bewegingen van de robot te besturen via knoppen             |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) | Om de bewegingen van de robot te besturen via joystick            |
| ![](media/3ab61154b4ae730a3757f40171846825.png) | Om de bewegingen van de robot te besturen via zwaartekracht             |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) | Stuurt "F" wanneer ingedrukt en "S" wanneer losgelaten<br />De auto beweegt vooruit wanneer ingedrukt en stopt wanneer losgelaten |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) | Stuurt "L" wanneer ingedrukt en "S" wanneer losgelaten <br />De auto draait links wanneer stevig ingedrukt en stopt wanneer losgelaten |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) | Stuurt "R" wanneer ingedrukt en "S" wanneer losgelaten<br />De auto draait rechts wanneer stevig ingedrukt en stopt wanneer losgelaten |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) | Stuurt "B" wanneer ingedrukt en "S" wanneer losgelaten<br />De auto rijdt achteruit wanneer stevig ingedrukt en stopt wanneer losgelaten |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) | Stuurt "u"+cijfer+"\#" wanneer gesleept<br />Sleep om de snelheid van de linkermotor te wijzigen |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) | Stuurt "v"+cijfer+"\#" wanneer gesleept<br />Sleep om de snelheid van de rechtermotor te wijzigen |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) | Selecteer om de Functiepagina te openen                                |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Stuurt "G" wanneer ingedrukt en "S" wanneer nogmaals ingedrukt<br />Activeer obstakelontwijkingsmodus wanneer ingedrukt en verlaat wanneer nogmaals ingedrukt |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Stuurt "h" wanneer ingedrukt en "S" wanneer nogmaals ingedrukt<br />Activeer volgmodus wanneer ingedrukt en verlaat wanneer nogmaals ingedrukt |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Stuurt "e" wanneer ingedrukt en "S" wanneer nogmaals ingedrukt<br />Activeer lijnvolgmodus wanneer ingedrukt en verlaat wanneer nogmaals ingedrukt |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Stuurt "f" wanneer ingedrukt en "S" wanneer nogmaals ingedrukt<br />Activeer modus bewegen-in-afgesloten-ruimte wanneer ingedrukt en verlaat wanneer nogmaals ingedrukt |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Stuurt "i" wanneer ingedrukt en "S" wanneer nogmaals ingedrukt<br />Activeer lichtvolgmodus wanneer ingedrukt en verlaat wanneer nogmaals ingedrukt |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Stuurt "j" wanneer ingedrukt en "S" wanneer nogmaals ingedrukt<br />Activeer brandblusmodus wanneer ingedrukt en verlaat wanneer nogmaals ingedrukt |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Selecteer om de weergavemodus voor gezichtsuitdrukkingen te openen               |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Stuurt "k" wanneer ingedrukt en "z" wanneer nogmaals ingedrukt<br />Toont lachend patroon wanneer geklikt en wist uitdrukking wanneer nogmaals geklikt |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Stuurt "l" wanneer ingedrukt en "z" wanneer nogmaals ingedrukt<br />Toont walgend patroon wanneer geklikt en wist uitdrukking wanneer nogmaals geklikt |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Stuurt "m" wanneer ingedrukt en "z" wanneer nogmaals ingedrukt<br />Toont blij gezicht wanneer geklikt en wist uitdrukking wanneer nogmaals geklikt |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Stuurt "n" wanneer ingedrukt en "z" wanneer nogmaals ingedrukt<br />Toont verdrietig patroon wanneer geklikt en wist uitdrukking wanneer nogmaals geklikt |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Stuurt "o" wanneer ingedrukt en "z" wanneer nogmaals ingedrukt<br />Toont misprijzend patroon wanneer geklikt en wist uitdrukking wanneer nogmaals geklikt |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Stuurt "p" wanneer ingedrukt en "z" wanneer nogmaals ingedrukt<br />Toont hartvormig patroon wanneer geklikt en wist uitdrukking wanneer nogmaals geklikt |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) | Kies om de aangepaste functie-interface te openen; er zijn zes knoppen 1,2,3,4,5,6; met deze knoppen kun je zelf enkele functies uitbreiden |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) | Klik om "w" te sturen<br />Klik om de analoge waarde weer te geven die door de linker fotoweerstand is gedetecteerd |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) | Klik om "y" te sturen<br />Klik om de analoge waarde weer te geven die door de rechter fotoweerstand is gedetecteerd |
| ![](media/a76df707b84409e57a1167889c3510d9.png) | Klik om "x" te sturen <br />Klik om de afstand weer te geven die door de ultrasone sensor is gedetecteerd (eenheid: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Klik om "c" te sturen, klik nogmaals om "d" te sturen<br />Druk om de ventilator aan te zetten en druk nogmaals om hem uit te zetten |

#### **(3)Stroomschema:**

![](media/image-20230427101759352.png)

#### **(4)Aansluitdiagram:**

![](media/930a8024364e07505e845624a94c27bd.png)

De GND, VCC, SDA en SCL van de 8x16 LED-dotmatrix zijn respectievelijk verbonden met -(GND), +(VCC), SDA, SCL van de uitbreidingskaart;

De STATE en BRK pinnen van de Bluetooth-module hoeven niet verbonden te worden.

#### **(5)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Wanneer de code wordt geüpload, moet de Bluetooth-module losgekoppeld zijn, en Bluetooth kan opnieuw worden verbonden na het uploadproces. Anders kan de code mogelijk niet succesvol worden geüpload.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 17.
  bluetooth Control tank
  http://www.keyestudio.com
*/

//Array, used to save data of images, can be calculated by yourself or gotten from modulus tool
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  // Stel de klokpin in als A5
#define SDA_Pin  A4  // Stel de datapen in als A4

#define ML_Ctrl 4  // Definieer de richtingsstuurpin van de linkermotor
#define ML_PWM 6   // Definieer de PWM-stuurpin van de linkermotor
#define MR_Ctrl 2  // Definieer de richtingsstuurpin van de rechtermotor
#define MR_PWM 5   // Definieer de PWM-stuurpin van de rechtermotor
char ble_val;      // Gebruikt om de waarde op te slaan die via Bluetooth is verkregen

void setup() 
{
  Serial.begin(9600);

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // Scherm wissen
  matrix_display(start01);  // Toon de afbeelding om te starten
}

void loop() 
{
  if (Serial.available())
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
  }
  switch (ble_val)
  {
    case 'F':  // Het commando om vooruit te gaan
      Car_front();
      break;
    case 'B':  // Het commando om achteruit te gaan
      Car_back();
      break;
    case 'L':  // Het commando om links af te slaan
      Car_left();
      break;
    case 'R':  // Het commando om rechts af te slaan
      Car_right();
      break;
    case 'S':  // Het commando om te stoppen
      Car_Stop();
      break;
  }
}

/***************De functie om de motor te laten draaien***************/
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
  matrix_display(front);  // Toon de afbeelding om vooruit te gaan
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  // Toon de afbeelding om links af te slaan
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  // Toon de afbeelding om rechts af te slaan
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // Toon de afbeelding om te stoppen
}

// Deze functie wordt gebruikt voor de weergave op het dotmatrixscherm
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Functie om de startconditie van gegevensoverdracht aan te roepen
  IIC_send(0xc0);  // Kies een adres
  for (int i = 0; i < 16; i++) // Patroondata heeft 16 bytes
  {
    IIC_send(matrix_value[i]); // Patroondata overdragen
  }
  IIC_end();   // Einde patroondata overdracht
  IIC_start();
  IIC_send(0x8A);  // Weergavebesturing, selecteer pulsbreedte als 4/16
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

// Het teken van het beëindigen van gegevensoverdracht
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

// Gegevens overdragen
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // Elk teken heeft 8 cijfers, die één voor één worden gedetecteerd
  {
    if (send_data & mask)  // Stel hoge of lage niveaus in op basis van elk bit (0 of 1)
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
    digitalWrite(SCL_Pin, LOW); // Trek de klokpin SCL_Pin laag om signalen van SDA te wijzigen
  }
}
```

#### **(6)Testresultaat:**

Na het uploaden van de code, verbind de robot met de Bluetooth-module en koppel de Bluetooth APP. Schakel de aan/uit-schakelaar van het motoraandrijfschild in. Plaats de robot op de vloer, je kunt deze knoppen van de Bluetooth-app gebruiken om de robot te besturen.

![](media/4655aeffe0d2081fa2b9fd254113c392.jpeg)

1. De pijlen omhoog, omlaag, links en rechts besturen de robot om respectievelijk vooruit, achteruit, links en rechts te bewegen.


![](./media/img-20240117095345.png)

2. Klik op de joystickknop en trek de richting van het zwarte punt in de witte cirkel om de bewegingsrichting van de robot te besturen.

![](./media/img-20240117095401.png)

3. Klik op de Zwaartekrachtknop en kantel de telefoon in de voorwaartse, achterwaartse, linker en rechter richting, en de robot beweegt in de richting waarin de telefoon wordt gekanteld.

![](./media/img-20240117095419.png)