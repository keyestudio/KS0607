### Project 12: Ultrasonic Hindernisvermijdende Tank

![](./media/image-20250709112200577.png)


#### **(1)Beschrijving:**

In het vorige project maakten we een ultrasone geluidvolgende slimme auto. In feite kunnen we met dezelfde componenten en dezelfde bedradingsmethode, door alleen de testcode te veranderen, er een ultrasone hindernisvermijdende slimme auto van maken. Deze slimme auto kan meebewegen met de beweging van de menselijke handen.

We gebruiken ultrasone sensoren om de afstand te meten tussen de slimme auto en het obstakel aan de voorkant, en besturen vervolgens de rotatie van de twee motoren op basis van deze gegevens om zo de bewegingen van de slimme auto te regelen.

|                          Detectie                            |        |
| :----------------------------------------------------------: | :----: |
| Afstand gemeten door de ultrasone sensor tussen de auto en het obstakel aan de voorkant <br />（stel de hoek van de servo in op 90°） | a(cm)  |
| Afstand gemeten door de ultrasone sensor tussen de auto en het obstakel aan de rechterkant <br />（stel de hoek van de servo in op 20°） | a2(cm) |
| Afstand gemeten door de ultrasone sensor tussen de auto en het obstakel aan de linkerkant <br />（stel de hoek van de servo in op 160°） | a1(cm) |
|   **Instelling:** stel de beginhoek van de servo in op 90°    |        |

|   Conditie 1   |        Conditie 2         | Conditie 3 | Beweging                                                     |
| :-------------: | :------------------------: | ----------- | ------------------------------------------------------------ |
|      a＜20      |                            |             | Stop gedurende 500ms；<br />stel de hoek van de servo in op 180°, lees a1, vertraging van 100ms；<br />stel de hoek van de servo in op 0°, lees a2, vertraging van 0.1s. |
|                 | a1＜50<br />of<br />a2＜50 |             | Vergelijk a1 met a2                                          |
|                 |                            | a1＞a2      | Stel de hoek van de servo in op 90°, draai links voor 700ms (stel PWM in op 255)<br />beweeg vooruit（stel PWM in op 200）. |
|                 |                            | a1＜a2      | Stel de hoek van de servo in op 90°, draai rechts voor 700ms (stel PWM in op 255) <br />beweeg vooruit（stel PWM in op 200）. |
| **Conditie 1** |      **Conditie 2**       |             | **Beweging**                                                 |
|      a＜20      | a1≥50<br />en<br />a2≥50  | Willekeurig      | stel de hoek van de servo in op 90°, draai links voor 500ms (stel PWM in op 255)<br />beweeg vooruit (stel PWM in op 200)<br /><br />stel de hoek van de servo in op 90°, draai rechts voor 500ms (stel PWM in op 255) <br />beweeg vooruit (stel PWM in op 200) |
|  **Conditie**  |                            |             | **Beweging**                                                 |
|      a≥20       |                            |             | beweeg vooruit (stel PWM in op 100)                                 |



#### **(2)Stroomdiagram:**

![](media/wps10.png)

#### **(3)Aansluitingsdiagram:**

![](media/72a10097d286bc5f9589df031b60484a.png)

(<span style="color: rgb(255, 76, 65);">Opmerking:</span> de bruine, rode en oranje draden van de servo zijn respectievelijk verbonden met G (GND), V（5V）en D10 van de uitbreidingskaart；en voor de ultrasone sensor is de VCC-pin verbonden met 5v (V), de Trig-pin met digitaal 12 (S), de Echo-pin met digitaal 13 (S), en de Gnd-pin met Gnd (G); hetzelfde als het vorige project.）

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er mogelijk conflicten kunnen optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 12
  Ultrasonic avoid tank
  http://www.keyestudio.com
*/
#define servoPin 10  //De pin van de servo
int a, a1, a2;
#define ML_Ctrl 4  //Definieer de richtingsbesturingspin van de linkermotor
#define ML_PWM 6   //Definieer de PWM-besturingspin van de linkermotor
#define MR_Ctrl 2  //Definieer de richtingsbesturingspin van de rechtermotor
#define MR_PWM 5   //Definieer de PWM-besturingspin van de rechtermotor
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  Serial.begin(9600);
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //Stel de hoek van de servo in op 90°
  delay(500); //vertraging van 500ms
}

void loop() 
{
  a = checkdistance();  //Wijs de door de ultrasone sensor gedetecteerde afstand aan de voorkant toe aan de variabele a

  if (a < 20) //Wanneer de afstand aan de voorkant kleiner is dan 20cm
  {
    Car_Stop();  //De robot stopt
    delay(500); //vertraging van 500ms
    procedure(180);  //Ultrasone pan-tilt draait naar links
    delay(500); //vertraging van 500ms
    a1 = checkdistance();  //Wijs de door de ultrasone sensor gedetecteerde afstand aan de linkerkant toe aan de variabele a1
    delay(100); //waarde lezen
    procedure(0); //Ultrasone pan-tilt draait naar rechts
    delay(500); //vertraging van 500ms
    a2 = checkdistance(); //Wijs de door de ultrasone sensor gedetecteerde afstand aan de rechterkant toe aan de variabele a2
    delay(100); //waarde lezen
    
    procedure(90);  //Terug naar 90°
    delay(500);
    if (a1 > a2) 
    { //Wanneer de afstand aan de linkerkant groter is dan aan de rechterkant
      Car_left();  //De robot draait naar links
      delay(700);  //700ms naar links draaien
    } 
    else 
    {
      Car_right(); //700ms naar links draaien
      delay(700);
    }
  } 
  else//Wanneer de afstand aan de voorkant >=20cm is, beweegt de robot vooruit
  {    
    Car_front(); //vooruit rijden
  }

}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
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

//De functie bestuurt servo's
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //Bereken de waarde van de pulsbreedte
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //De tijd in hoog niveau vertegenwoordigt de pulsbreedte
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //Omdat de cyclus 20ms is, is de resterende tijd op laag niveau
  }
}

//De functie bestuurt ultrasoon geluid
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //De 58.20 hier komt van 2*29.1=58.2
  delay(10);
  return distance;
}
```

#### **(5)Testresultaat:**

Na het succesvol uploaden van de testcode, de bedrading aansluiten, de DIP-schakelaar naar de ON-stand zetten en de stroom inschakelen, beweegt de slimme auto vooruit en vermijdt automatisch obstakels.

![](./media/img-20240117090420.png)