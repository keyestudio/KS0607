### Project 10: Lichtvolgende Tank


#### **(1)Beschrijving:**

In de vorige projecten hebben we het gebruik van diverse sensoren, modules en uitbreidingskaarten op de slimme auto in detail besproken. Nu gaan we over naar de projecten van de slimme auto. De lichtvolgende slimme auto, zoals de naam al aangeeft, is een slimme auto die het licht kan volgen.

We kunnen de kennis uit de projecten over de lichtgevoelige weerstand en de motoraansturing combineren om een lichtzoekende slimme auto te maken. In dit project gebruiken we twee fotoweerststandmodules om de lichtintensiteit aan de linker- en rechterkant van de slimme auto te detecteren, de bijbehorende analoge waarden uit te lezen, en vervolgens de rotatie van de twee motoren op basis van deze twee gegevens te sturen om zo de bewegingen van de slimme auto te regelen.

De specifieke logica van de lichtvolgende slimme auto wordt hieronder weergegeven.

![](./media/image-20250709111733042.png)

#### **(2)Stroomdiagram:**

![](media/wps8.png)

#### **(3)Aansluitschema:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Let op:</span> De pin "G", "V" en S van de linker fotoweerststandmodule zijn verbonden met respectievelijk G (GND), V (VCC) en A1;

De pin "G", "V" en S van de rechter fotoweerststandmodule zijn verbonden met respectievelijk G (GND), V (VCC) en A2.

De 4-pins kabel is gemarkeerd met A, A1, B1 en B. De rechter achtermotor is verbonden met poort B van de 8833 motordriver-uitbreidingskaart en de linker voormotor is verbonden met poort A van de 8833 motordriver-uitbreidingskaart.

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Let op:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 10
  light follow tank
  http://www.keyestudio.com
*/
#define light_L_Pin A1   // Definieer de pin van de lichtgevoelige sensor aan de linkerkant
#define light_R_Pin A2   // Definieer de pin van de lichtgevoelige sensor aan de rechterkant
#define ML_Ctrl 4  // Definieer de richtingsbesturingspin van de linkermotor
#define ML_PWM 6   // Definieer de PWM-besturingspin van de linkermotor
#define MR_Ctrl 2  // Definieer de richtingsbesturingspin van de rechtermotor
#define MR_PWM 5   // Definieer de PWM-besturingspin van de rechtermotor
int left_light;
int right_light;
void setup() 
{
  Serial.begin(9600);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop() 
{
  left_light = analogRead(light_L_Pin);
  right_light = analogRead(light_R_Pin);
  Serial.print("left_light_value = ");
  Serial.println(left_light);
  Serial.print("right_light_value = ");
  Serial.println(right_light);
  if (left_light > 650 && right_light > 650) // rijd vooruit
  {
    Car_front();
  }
  else if (left_light > 650 && right_light <= 650)  // draai naar links
  {
    Car_left();
  }
  else if (left_light <= 650 && right_light > 650) // draai naar rechts
  {
    Car_right();
  }
  else  // anders, stop
  {
    Car_Stop();
  }
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Testresultaat**

Nadat de testcode succesvol is geüpload, de bedrading is aangesloten volgens het aansluitschema, de DIP-schakelaar naar de rechterkant is omgezet en de stroom is ingeschakeld, volgt de slimme auto het licht om te bewegen.

![Img](./media/img-20240117090537.png)