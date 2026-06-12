### Projekt 11: Ultraschall-Folge-Panzer


#### **(1)Beschreibung:**

In der vorherigen Lektion haben wir den lichtfolgenden Smart-Car kennengelernt. In dieser Lektion können wir das Wissen kombinieren, um ein ultraschallgesteuertes Folgeauto zu bauen.

In diesem Projekt verwenden wir Ultraschallsensoren, um den Abstand zwischen dem Auto und dem Hindernis davor zu erkennen, und steuern dann die Drehung der beiden Motoren basierend auf diesen Daten, um so die Bewegungen des Smart-Cars zu kontrollieren.

Die spezifische Logik des ultraschallgesteuerten Folge-Smart-Cars ist in der folgenden Tabelle dargestellt:

|                        Erkennung                        |              Einstellung              |
| :-----------------------------------------------------: | :-----------------------------------: |
| Der Abstand (cm) zwischen dem Auto und dem Hindernis vorne | Servowinkel auf 90° einstellen |
|                      **Bedingung**                      |           **Bewegung**            |
|               Abstand≥20 und Abstand≤50               |             Vorwärts fahren              |
|            10＜Abstand＜20<br/>Abstand＞50            |               Stopp                |
|                       Abstand≤10                       |              Rückwärts fahren              |

#### **(2)Flussdiagramm:**

![](media/wps9.png)

#### **(3)Anschlussdiagramm:**

![](media/72a10097d286bc5f9589df031b60484a.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 11
  Ultrasonic follow tank
  http://www.keyestudio.com
*/
#define servoPin 10  //Der Pin des Servos

#define ML_Ctrl 4  //Richtungssteuerungspin des linken Motors definieren
#define ML_PWM 6   //PWM-Steuerungspin des linken Motors definieren
#define MR_Ctrl 2  //Richtungssteuerungspin des rechten Motors definieren
#define MR_PWM 5   //PWM-Steuerungspin des rechten Motors definieren
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //Servowinkel auf 90° einstellen
  delay(500); //Verzögerung von 500ms
}

void loop() 
{
  distance = checkdistance();  //Den vom Ultraschall gemessenen Abstand der Variablen distance zuweisen
  if (distance >= 20 && distance <= 50) //vorwärts fahren
  {
    Car_front();
  }
  else if (distance > 10 && distance < 20)  //stopp
  {
    Car_Stop();
  }
  else if (distance <= 10)  //rückwärts fahren
  {
    Car_back();
  }
  else  //In anderen Fällen stoppt es
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

//Die Funktion zur Steuerung von Servos
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //Den Wert der Impulsbreite berechnen    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //Die Zeit im High-Pegel entspricht der Impulsbreite
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //Da der Zyklus 20ms beträgt, verbleibt die restliche Zeit im Low-Pegel
  }
}
//Die Funktion zur Steuerung des Ultraschalls
float checkdistance() 
{
  static float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //Die 58.20 ergibt sich aus 2*29.1=58.2
  delay(10);
  return distance;
}
```

#### **(5)Testergebnisse:**

Nach erfolgreichem Hochladen des Testcodes, Verkabelung, Umlegen des DIP-Schalters auf die rechte Seite, Einschalten der Stromversorgung und Einstellen des Servos auf 90° folgt das Smart-Car dem Hindernis in seiner Bewegung.

![](./media/img-20240117090457.png)