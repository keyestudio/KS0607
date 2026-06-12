### Projekt 14: Linienverfolgungs-Panzer


#### **(1)Beschreibung:**

Das vorherige Projekt hat erklärt, wie man das Smart Car dazu bringt, sich in einem bestimmten Bereich zu bewegen. In diesem Projekt können wir das zuvor erlernte Wissen nutzen, um ein linienverfolgendes Smart Car zu bauen. Im Experiment verwenden wir den Linienverfolgungssensor, um zu erkennen, ob sich eine schwarze Linie in der Nähe des Smart Cars befindet, und steuern dann die Drehung der beiden Motoren entsprechend den Erkennungsergebnissen, damit das Smart Car entlang der schwarzen Linie fährt.

Die spezifische Logik des linienverfolgungs-Smart Cars ist in der folgenden Tabelle dargestellt:

|               Sensor               |                          Erkennung                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Linienverfolgungssensor in der Mitte | Schwarze Linie erkannt: High-Pegel<br />Weiße Linie erkannt: Low-Pegel |
|  Linienverfolgungssensor links  | Schwarze Linie erkannt: High-Pegel<br />Weiße Linie erkannt: Low-Pegel |
| Linienverfolgungssensor rechts  | Schwarze Linie erkannt: High-Pegel<br />Weiße Linie erkannt: Low-Pegel |

|                         Bedingung 1                          |                         Bedingung 2                          |             Bewegung             |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :------------------------------: |
| Linienverfolgungssensor in der Mitte <br />erkennt die schwarze Linie | Linienverfolgungssensor links erkennt die schwarze Linie <br />und <br />der rechte erkennt weiße Linie | Links drehen<br />PWM auf 200 setzen  |
| Linienverfolgungssensor in der Mitte <br />erkennt die schwarze Linie | Linienverfolgungssensor links erkennt weiße Linie <br />und <br />der rechte erkennt die schwarze Linie | Rechts drehen<br />PWM auf 200 setzen |
| Linienverfolgungssensor in der Mitte <br />erkennt die schwarze Linie | Beide Linienverfolgungssensoren (links und rechts) erkennen weiße Linie<br />oder<br />Beide (links und rechts) erkennen die schwarze Linie |           Vorwärts fahren           |
| Linienverfolgungssensor in der Mitte <br />erkennt weiße Linie  | Linienverfolgungssensor links erkennt die schwarze Linie <br />und <br />der rechte erkennt weiße Linie | Links drehen<br />PWM auf 200 setzen  |
| Linienverfolgungssensor in der Mitte <br />erkennt weiße Linie  | Linienverfolgungssensor links erkennt weiße Linie<br />und <br />der rechte erkennt die schwarze Linie | Rechts drehen<br />PWM auf 200 setzen |
| Linienverfolgungssensor in der Mitte <br />erkennt weiße Linie  | Beide Linienverfolgungssensoren (links und rechts) erkennen weiße Linie<br />oder<br />Beide Linienverfolgungssensoren (links und rechts) erkennen die schwarze Linie |               Stopp               |

#### **(2)Flussdiagramm:**

![](media/wps11.png)

#### **(3)Schaltplan:**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, die das Hochladen zum Scheitern bringen können.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 14
  Line track tank
  http://www.keyestudio.com
*/

// Verdrahtung des Linienverfolgungssensors
#define L_pin  11  // links
#define M_pin  7  // Mitte
#define R_pin  8  // rechts
#define ML_Ctrl 4  // Richtungssteuerungspin des linken Motors definieren
#define ML_PWM 6   // PWM-Steuerungspin des linken Motors definieren
#define MR_Ctrl 2  // Richtungssteuerungspin des rechten Motors definieren
#define MR_PWM 5   // PWM-Steuerungspin des rechten Motors definieren
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); // Baudrate auf 9600 setzen
  pinMode(L_pin, INPUT); // Alle Pins des Linienverfolgungssensors als Eingangsmodus setzen
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); // Wert des linken Sensors lesen
  M_val = digitalRead(M_pin); // Wert des mittleren Sensors lesen
  R_val = digitalRead(R_pin); // Wert des rechten Sensors lesen
  if (M_val == 1) { // Der mittlere erkennt schwarze Linien
    if (L_val == 1 && R_val == 0)  // Wenn links eine schwarze Linie erkannt wird, aber nicht rechts, nach links drehen
    {
      Car_left();
    }
    else if (L_val == 0 && R_val == 1)  // Wenn rechts eine schwarze Linie erkannt wird, aber nicht links, nach rechts drehen
    {
      Car_right();
    }
    else  // andernfalls vorwärts fahren
    {
      Car_front();
    }
  }
  else  // Der mittlere erkennt keine schwarzen Linien
  {
    if (L_val == 1 && R_val == 0)  // Wenn links eine schwarze Linie erkannt wird, aber nicht rechts, nach links drehen
    {
      Car_left();
    }
    else if (L_val == 0 && R_val == 1)  // Wenn rechts eine schwarze Linie erkannt wird, aber nicht links, nach rechts drehen
    {
      Car_right();
    }
    else  // andernfalls stoppen
    {
      Car_Stop();
    }
  }
}

// vorwärts fahren
void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

// rückwärts fahren
void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

// nach links drehen
void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

// nach rechts drehen
void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

// stoppen
void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Testergebnis:**

Nachdem der Testcode erfolgreich hochgeladen und das Gerät eingeschaltet wurde, fährt das Smart Car entlang der schwarzen Linie.

![](./media/img-20240117085916.png)