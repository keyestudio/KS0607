### Projekt 17: Bluetooth-gesteuerter Panzer


#### **(1) Beschreibung:**

Im vorherigen Projekt haben wir die Grundkenntnisse über Bluetooth erlernt. In dieser Lektion werden wir Bluetooth verwenden, um das Smart Car zu steuern. Da es Bluetooth betrifft, werden ein Sender und ein Empfänger benötigt. In diesem Projekt verwenden wir das Mobiltelefon als Sender (Master) und das Smart Car mit dem angeschlossenen HM-10 Bluetooth-Modul (Slave) als Empfänger.

Wir haben früher gelernt, dass das Senden eines Bits LEDs steuern kann. Das Prinzip der Steuerung dieses Roboterfahrzeugs ist dasselbe.

Wir verstehen zunächst die Funktion jeder Schaltfläche in der APP und verwenden dann die Schaltflächen der APP, um den Panzer zu steuern.

#### **(2) Hauptfunktionen der APP**

Die folgende Tabelle veranschaulicht die Funktionen der entsprechenden Tasten:

|                      TASTEN                       | FUNKTIONEN                                                    |
| :---------------------------------------------: | ------------------------------------------------------------ |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) | HM-10 Bluetooth-Modul koppeln und verbinden; erneut klicken zum Trennen |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) | Auswahl des zu bedienenden Roboters                                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) | Steuerung der Roboterbewegungen über Schaltflächen             |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) | Steuerung der Roboterbewegungen über Joystick            |
| ![](media/3ab61154b4ae730a3757f40171846825.png) | Steuerung der Roboterbewegungen über Schwerkraft             |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) | Sendet „F" beim Drücken und „S" beim Loslassen<br />Das Auto fährt vorwärts beim Drücken und hält beim Loslassen an |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) | Sendet „L" beim Drücken und „S" beim Loslassen <br />Das Auto dreht links beim Drücken und hält beim Loslassen an |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) | Sendet „R" beim Drücken und „S" beim Loslassen<br />Das Auto dreht rechts beim Drücken und hält beim Loslassen an |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) | Sendet „B" beim Drücken und „S" beim Loslassen<br />Das Auto fährt rückwärts beim Drücken und hält beim Loslassen an |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) | Sendet „u"+Ziffer+„\#" beim Ziehen<br />Ziehen zum Ändern der Geschwindigkeit des linken Motors |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) | Sendet „v"+Ziffer+„\#" beim Ziehen<br />Ziehen zum Ändern der Geschwindigkeit des rechten Motors |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) | Auswahl zum Öffnen der Funktionsseite                                |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Sendet „G" beim Drücken und „S" beim erneuten Drücken<br />Hindernisumfahrungsmodus beim Drücken aktivieren, beim erneuten Drücken beenden |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Sendet „h" beim Drücken und „S" beim erneuten Drücken<br />Folgemodus beim Drücken aktivieren, beim erneuten Drücken beenden |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Sendet „e" beim Drücken und „S" beim erneuten Drücken<br />Linienfolgemodus beim Drücken aktivieren, beim erneuten Drücken beenden |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Sendet „f" beim Drücken und „S" beim erneuten Drücken<br />Modus „Bewegung im begrenzten Raum" beim Drücken aktivieren, beim erneuten Drücken beenden |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Sendet „i" beim Drücken und „S" beim erneuten Drücken<br />Lichtfolgemodus beim Drücken aktivieren, beim erneuten Drücken beenden |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Sendet „j" beim Drücken und „S" beim erneuten Drücken<br />Feuerlöschmodus beim Drücken aktivieren, beim erneuten Drücken beenden |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Auswahl zum Öffnen des Gesichtsausdrucks-Anzeigemodus               |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Sendet „k" beim Drücken und „z" beim erneuten Drücken<br />Lächelndes Muster beim Klicken anzeigen, Ausdruck beim erneuten Klicken löschen |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Sendet „l" beim Drücken und „z" beim erneuten Drücken<br />Ekeliges Muster beim Klicken anzeigen, Ausdruck beim erneuten Klicken löschen |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Sendet „m" beim Drücken und „z" beim erneuten Drücken<br />Fröhliches Gesicht beim Klicken anzeigen, Ausdruck beim erneuten Klicken löschen |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Sendet „n" beim Drücken und „z" beim erneuten Drücken<br />Trauriges Muster beim Klicken anzeigen, Ausdruck beim erneuten Klicken löschen |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Sendet „o" beim Drücken und „z" beim erneuten Drücken<br />Verachtendes Muster beim Klicken anzeigen, Ausdruck beim erneuten Klicken löschen |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Sendet „p" beim Drücken und „z" beim erneuten Drücken<br />Herzförmiges Muster beim Klicken anzeigen, Ausdruck beim erneuten Klicken löschen |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) | Auswahl zum Öffnen der benutzerdefinierten Funktionsoberfläche; es gibt sechs Tasten 1,2,3,4,5,6; mit diesen Tasten können Sie selbst einige Funktionen erweitern |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) | Klicken zum Senden von „w"<br />Klicken zur Anzeige des analogen Wertes des linken Fotowiderstands |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) | Klicken zum Senden von „y"<br />Klicken zur Anzeige des analogen Wertes des rechten Fotowiderstands |
| ![](media/a76df707b84409e57a1167889c3510d9.png) | Klicken zum Senden von „x" <br />Klicken zur Anzeige der vom Ultraschallsensor erkannten Entfernung (Einheit: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Klicken zum Senden von „c", erneut klicken zum Senden von „d"<br />Drücken zum Einschalten des Lüfters, erneut drücken zum Ausschalten |

#### **(3) Flussdiagramm:**

![](media/image-20230427101759352.png)

#### **(4) Schaltplan:**

![](media/930a8024364e07505e845624a94c27bd.png)

GND, VCC, SDA und SCL der 8x16 LED-Punktmatrix sind jeweils mit -(GND), +(VCC), SDA, SCL der Erweiterungsplatine verbunden;

Die STATE- und BRK-Pins des Bluetooth-Moduls müssen nicht angeschlossen werden.

#### **(5) Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Beim Hochladen des Codes muss das Bluetooth-Modul getrennt sein. Bluetooth kann nach dem Hochladevorgang wieder verbunden werden. Andernfalls kann der Code möglicherweise nicht erfolgreich hochgeladen werden.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 17.
  bluetooth Control tank
  http://www.keyestudio.com
*/

// Array, zum Speichern von Bilddaten, kann selbst berechnet oder mit einem Modulwerkzeug ermittelt werden
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
#define MR_PWM 5   // PWM-Steuerungspin des rechten Motors definieren
char ble_val;      // Zum Speichern des über Bluetooth empfangenen Wertes

void setup() 
{
  Serial.begin(9600);

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
  if (Serial.available())
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
  }
  switch (ble_val)
  {
    case 'F':  // Befehl zum Vorwärtsfahren
      Car_front();
      break;
    case 'B':  // Befehl zum Rückwärtsfahren
      Car_back();
      break;
    case 'L':  // Befehl zum Linksdrehen
      Car_left();
      break;
    case 'R':  // Befehl zum Rechtsdrehen
      Car_right();
      break;
    case 'S':  // Befehl zum Anhalten
      Car_Stop();
      break;
  }
}

/***************Funktion zum Betrieb des Motors***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  // Rückwärtsfahren
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
  matrix_display(left);  // Bild für Linksdrehen anzeigen
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  // Bild für Rechtsdrehen anzeigen
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // Bild für Anhalten anzeigen
}

// Diese Funktion wird zur Anzeige auf der Punktmatrixanzeige verwendet
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Funktion zum Aufrufen der Startbedingung der Datenübertragung
  IIC_send(0xc0);  // Adresse auswählen
  for (int i = 0; i < 16; i++) // Musterdaten haben 16 Bytes
  {
    IIC_send(matrix_value[i]); // Musterdaten übertragen
  }
  IIC_end();   // Musterdatenübertragung beenden
  IIC_start();
  IIC_send(0x8A);  // Anzeigesteuerung, Impulsbreite als 4/16 auswählen
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
    digitalWrite(SCL_Pin, HIGH); // Taktpin SCL_Pin hochziehen, um Datenübertragung zu stoppen
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // Taktpin SCL_Pin herunterziehen, um SDA-Signale zu ändern
  }
}
```

#### **(6) Testergebnis:**

Nach dem Hochladen des Codes verbinden Sie den Roboter mit dem Bluetooth-Modul und koppeln Sie die Bluetooth-APP. Schalten Sie den Netzschalter des Motorantriebsschields ein. Stellen Sie den Roboter auf den Boden und Sie können diese Schaltflächen der Bluetooth-App verwenden, um den Roboter zu steuern.

![](media/4655aeffe0d2081fa2b9fd254113c392.jpeg)

1. Die Pfeile nach oben, unten, links und rechts steuern den Roboter, um ihn vorwärts, rückwärts, links und rechts zu bewegen.


![](./media/img-20240117095345.png)

2. Klicken Sie auf die Joystick-Schaltfläche und ziehen Sie die Richtung des schwarzen Punktes im weißen Kreis, um die Bewegungsrichtung des Roboters zu steuern.

![](./media/img-20240117095401.png)

3. Klicken Sie auf die Schwerkraft-Schaltfläche und neigen Sie das Telefon in die Vorwärts-, Rückwärts-, Links- und Rechtsrichtungen. Der Roboter bewegt sich in die Richtung, in die das Telefon geneigt ist.

![](./media/img-20240117095419.png)