### Projekt 15: IR-Ferngesteuerter Panzer

![](./media/image-20250709113214889.png)


#### **(1) Beschreibung:**

Infrarot-Fernsteuerung ist eine der häufigsten Fernsteuerungsanwendungen in Elektromotoren, Ventilatoren und vielen anderen Haushaltsgeräten. In diesem Projekt nutzen wir das zuvor erlernte Wissen, um ein infrarotgesteuertes Smart-Car zu bauen.

In der 9. Lektion haben wir den entsprechenden Tastenwert jeder Taste der Infrarot-Fernbedienung getestet. In diesem Projekt können wir den Code (Tastenwert) so festlegen, dass die entsprechende Taste die Bewegungen des Smart-Cars steuert und die Bewegungsmuster auf der 8×16 LED-Punktmatrix angezeigt werden.

Die genaue Logik des linienführenden Smart-Cars ist in der folgenden Tabelle dargestellt:

|                        Ultraschall-Taste                     | Tastenwert |                    Anweisungen der Tasten                    |
| :----------------------------------------------------------: | :--------: | :----------------------------------------------------------: |
| ![image-20230427094710725](media/image-20230427094710725.png) |  FF629D    | Vorwärts fahren（PWM auf 200 setzen）<br />Muster „Vorwärts" anzeigen |
| ![image-20230427094716639](media/image-20230427094716639.png) |  FFA857    | Rückwärts fahren（PWM auf 200 setzen）<br />Muster „Rückwärts" anzeigen |
| ![image-20230427094720417](media/image-20230427094720417.png) |  FF22DD    |           Links abbiegen<br />Muster „STOP" anzeigen         |
| ![image-20230427094725151](media/image-20230427094725151.png) |  FFC23D    |     Rechts abbiegen<br />Muster „Links abbiegen" anzeigen    |
| ![image-20230427094729839](media/image-20230427094729839.png) |  FF02FD    |             Anhalten<br />Muster „STOP" anzeigen             |

**Anfangseinstellung**: Das 8×16 LED-Punktmatrix-Display zeigt das Muster „![](media/wps20.jpg)".



#### **(2) Ablaufdiagramm:**

![](media/wps21.png)

#### **(3) Schaltplan:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span>

GND, VCC, SDA und SCL des 8×16 LED-Panels sind mit G（GND), V（VCC), SDA und SCL der Erweiterungsplatine verbunden.

Da die 8833-Platine den IR-Empfänger integriert, muss dieser nicht separat verdrahtet werden. Die Pins des IR-Empfängers sind G（GND), V（VCC) und D3.

#### (4) **Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

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
long ir_rec;  // Wird verwendet, um empfangene Infrarotwerte zu speichern

// Array, um Bilddaten zu speichern, kann selbst berechnet oder mit einem Modultool ermittelt werden
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  // Taktpin als A5 festlegen
#define SDA_Pin  A4  // Datenpin als A4 festlegen

#define ML_Ctrl 4  // Richtungssteuerungspin des linken Motors definieren
#define ML_PWM 6   // PWM-Steuerungspin des linken Motors definieren
#define MR_Ctrl 2  // Richtungssteuerungspin des rechten Motors definieren
#define MR_PWM 5    // PWM-Steuerungspin des rechten Motors definieren

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  // Infrarot-Empfänger-Bibliothek initialisieren

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // Bildschirm löschen
  matrix_display(start01);  // Startbild anzeigen
}

void loop() 
{
  if (irrecv.decode(&results))  // Infrarot-Fernsteuerwert empfangen
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
    case 0xFF629D: Car_front();     break;   // Befehl zum Vorwärtsfahren
    case 0xFFA857: Car_back();      break;   // Befehl zum Rückwärtsfahren
    case 0xFF22DD: Car_T_left();    break;   // Befehl zum Linksabbiegen
    case 0xFFC23D: Car_T_right();   break;   // Befehl zum Rechtsabbiegen
    case 0xFF02FD: Car_Stop();      break;   // Befehl zum Anhalten
    case 0xFF30CF: Car_left();      break;   // Befehl zum Drehen nach links
    case 0xFF7A85: Car_right();     break;   // Befehl zum Drehen nach rechts
    default: break;
  }
}

/***************Funktion zum Antreiben der Motoren***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  // Rückwärts fahren
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(front);  // Bild für Vorwärtsfahren anzeigen
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  // Bild für Linksabbiegen anzeigen
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  // Bild für Rechtsabbiegen anzeigen
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // Bild für Anhalten anzeigen
}

void Car_T_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
  matrix_display(left);  // Bild für Linksabbiegen anzeigen
}

void Car_T_right() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 0);
  matrix_display(right);  // Bild für Rechtsabbiegen anzeigen
}

// Diese Funktion wird für die Anzeige auf der Punktmatrix verwendet
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Funktion zum Aufrufen der Startbedingung für die Datenübertragung
  IIC_send(0xc0);  // Adresse auswählen
  for (int i = 0; i < 16; i++) // Musterdaten haben 16 Bytes
  {
    IIC_send(matrix_value[i]); // Musterdaten übertragen
  }
  IIC_end();   // Musterdatenübertragung beenden
  IIC_start();
  IIC_send(0x8A);  // Anzeigesteuerung, Pulsbreite als 4/16 auswählen
  IIC_end();
}

// Bedingungen für den Start der Datenübertragung
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// Zeichen für das Ende der Datenübertragung
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

// Daten übertragen
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // Jedes Zeichen hat 8 Stellen, die einzeln geprüft werden
  {
    if (send_data & mask)  // Hohe oder niedrige Pegel entsprechend jedem Bit (0 oder 1) setzen
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Taktpin SCL_Pin auf HIGH ziehen, um die Datenübertragung zu stoppen
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // Taktpin SCL_Pin auf LOW ziehen, um SDA-Signale zu ändern
  }
}
```

#### **(5) Testergebnis:**

Nach dem Hochladen des Codes schalten Sie den Netzschalter des Motorantriebsmoduls ein. Stellen Sie den Roboter auf den Boden, beziehen Sie sich auf die obige Tabelle und drücken Sie verschiedene Tasten – der Roboter bewegt sich in die entsprechende voreingestellte Richtung.

![](./media/img-20240117090114.png)