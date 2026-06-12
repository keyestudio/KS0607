### Projekt 13: Panzer bewegt sich in einem begrenzten Bereich


#### **(1)Beschreibung:**

Die Funktionen zur Ultraschall-Verfolgung und zur Hindernisumgehung des Smart Cars wurden in früheren Projekten vorgestellt. Hier beabsichtigen wir, das Wissen aus den vorherigen Kursen zu kombinieren, um das Smart Car auf einen bestimmten Bereich zu beschränken.

Im Experiment verwenden wir den Linienverfolgungssensor, um zu erkennen, ob sich eine schwarze Linie in der Nähe des Smart Cars befindet, und steuern dann die Drehung der beiden Motoren entsprechend den Erkennungsergebnissen, um das Smart Car innerhalb eines mit schwarzer Linie gezeichneten Kreises zu halten.

Die spezifische Logik des linienverfolgenden Smart Cars ist in der folgenden Tabelle dargestellt:

![](./media/image-20250709112523897.png)

|                         Bedingung                         |                         Bewegung                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Wenn einer der drei Linienverfolgungssensoren schwarze Linien erkennt | Rückwärtsfahren（PWM auf 150 setzen）Dann links abbiegen（PWM auf 150 setzen） |
|             Keiner von ihnen erkennt schwarze Linien              |               Vorwärts fahren（PWM auf 100 setzen）                |

#### **(2)Flussdiagramm:**

![](media/image-20230427092708208.png)

#### **(3)Anschlussdiagramm:**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-Serialkommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 13
  draw a circle for tank
  http://www.keyestudio.com
*/

//Verdrahtung des Linienverfolgungssensors
#define L_pin  11  //links
#define M_pin  7  //mitte
#define R_pin  8  //rechts

#define ML_Ctrl 4  //Definiere den Richtungssteuerungspin des linken Motors
#define ML_PWM 6   //Definiere den PWM-Steuerungspin des linken Motors
#define MR_Ctrl 2  //Definiere den Richtungssteuerungspin des rechten Motors
#define MR_PWM 5   //Definiere den PWM-Steuerungspin des rechten Motors
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); //Baudrate auf 9600 setzen
  pinMode(L_pin, INPUT); //Alle Pins des Linienverfolgungssensors als Eingang setzen
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); //Wert des linken Sensors lesen
  M_val = digitalRead(M_pin); //Wert des mittleren Sensors lesen
  R_val = digitalRead(R_pin); //Wert des rechten Sensors lesen
  if ( L_val == 0 && M_val == 0 && R_val == 0 )  //wenn keine schwarzen Linien erkannt werden, vorwärts fahren
  {
    Car_front();
  }
  else  //schwarze Linien erkannt, rückwärts fahren dann links abbiegen
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

#### **(5)Testergebnisse:**

Nachdem der Testcode erfolgreich hochgeladen und das Gerät eingeschaltet wurde, bewegt sich das Smart Car in einem begrenzten Bereich, dem mit schwarzer Linie gezeichneten Kreis.

![](./media/img-20240117090340.png)