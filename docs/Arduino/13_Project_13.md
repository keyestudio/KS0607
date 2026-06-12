### Project 13: Tank die Beweegt in een Afgebakende Ruimte


#### **(1)Beschrijving:**

De ultrasone volgfunctie en obstakelvermijdingsfuncties van de slimme auto zijn in vorige projecten besproken. Hier willen we de kennis uit de vorige cursussen combineren om de slimme auto te beperken tot bewegen binnen een bepaalde ruimte.

In het experiment gebruiken we de lijnvolgsensor om te detecteren of er een zwarte lijn rondom de slimme auto aanwezig is, en vervolgens regelen we de rotatie van de twee motoren op basis van de detectieresultaten, zodat de slimme auto binnen een cirkel getrokken met een zwarte lijn blijft.

De specifieke logica van de lijnvolgende slimme auto wordt weergegeven in de onderstaande tabel:

![](./media/image-20250709112523897.png)

|                         Conditie                          |                         Beweging                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Als één van de drie lijnvolgsensoren zwarte lijnen detecteert | Achteruit rijden（PWM instellen op 150）Dan links afslaan（PWM instellen op 150） |
|             Geen van hen detecteert zwarte lijnen              |               Vooruit rijden（PWM instellen op 100）                |

#### **(2)Stroomdiagram:**

![](media/image-20230427092708208.png)

#### **(3)Aansluitingsschema:**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat de code wordt geüpload, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden mislukt.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 13
  draw a circle for tank
  http://www.keyestudio.com
*/

// De bedrading van de lijnvolgsensor
#define L_pin  11  // links
#define M_pin  7  // midden
#define R_pin  8  // rechts

#define ML_Ctrl 4  // Definieer de richtingsbesturingspin van de linkermotor
#define ML_PWM 6   // Definieer de PWM-besturingspin van de linkermotor
#define MR_Ctrl 2  // Definieer de richtingsbesturingspin van de rechtermotor
#define MR_PWM 5   // Definieer de PWM-besturingspin van de rechtermotor
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); // Stel de baudrate in op 9600
  pinMode(L_pin, INPUT); // Stel alle pinnen van de lijnvolgsensor in als invoermodus
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); // Lees de waarde van de linkersensor
  M_val = digitalRead(M_pin); // Lees de waarde van de middensensor
  R_val = digitalRead(R_pin); // Lees de waarde van de rechtersensor
  if ( L_val == 0 && M_val == 0 && R_val == 0 )  // wanneer er geen zwarte lijnen worden gedetecteerd, rijd vooruit
  {
    Car_front();
  }
  else  // zwarte lijnen gedetecteerd, rijd achteruit dan links afslaan
  {
    Car_back();
    delay(700);
    Car_left();
    delay(800);
  }
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Testresultaten:**

Nadat de testcode succesvol is geüpload en de stroom is ingeschakeld, beweegt de slimme auto binnen een afgebakende ruimte, de cirkel getrokken met een zwarte lijn.

![](./media/img-20240117090340.png)