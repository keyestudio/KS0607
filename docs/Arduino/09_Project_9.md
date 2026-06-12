### Projekt 9: 8\*16 Gesichtsausdruck LED-Punktmatrix

![](./media/image-20250709110751263.png)

#### **(1) Beschreibung:**

Wäre es nicht toll, wenn dem Roboter ein Ausdrucks-Display hinzugefügt würde? Und die Keyestudio 8\*16 LED-Punktmatrix kann genau das. Mit ihrer Hilfe können Sie selbst Gesichtsausdrücke, Bilder, Muster und andere Anzeigen gestalten.

Das 8\*16 LED-Board verfügt über 128 LEDs. Der Mikrocontroller (Arduino) kommuniziert mit dem AiP1640 über eine Zwei-Draht-Bus-Schnittstelle. Dadurch kann er das Ein- und Ausschalten der 128 LEDs auf dem Modul steuern und so die Punktmatrix des Moduls das gewünschte Muster anzeigen lassen. Ein HX-2.54 4Pin-Kabel wird zur einfacheren Verkabelung mitgeliefert.

#### **(2) Parameter:**

- Betriebsspannung: DC 3,3–5 V
- Leistungsaufnahme: 400 mW
- Schwingfrequenz: 450 KHz
- Treiberstrom: 200 mA
- Betriebstemperatur: -40\~80 ℃
- Kommunikationsmodus: Zwei-Draht-Bus

#### **(3) Wissen:**

**Funktionsprinzip der 8\*16 LED-Punktmatrix**

Wie steuert man jede LED der 8\*16-Punktmatrix? Es ist bekannt, dass jedes Byte 8 Bits hat und jedes Bit 0 oder 1 ist. Wenn es 0 ist, ist die LED aus; wenn es 1 ist, ist die LED an. Ein Byte kann eine Spalte der LED steuern, und entsprechend können 16 Bytes 16 Spalten von LEDs steuern – das ist die 8\*16-Punktmatrix.

![](media/image-20230427082712905.png)

**Pin-Beschreibung und Kommunikationsprotokoll**

Der Mikrocontroller (Arduino) kommuniziert mit dem AiP1640 über ein Zwei-Draht-Bus-Kabel.

Das Kommunikationsprotokoll-Diagramm ist wie folgt dargestellt: (SCLK) ist SCL, (DIN) ist SDA

![](media/ea2bab37f23c09453c680590b84653d6.png)

① Die Startbedingung für die Dateneingabe: SCL ist auf hohem Pegel und SDA wechselt von hoch nach niedrig.

② Für die Einstellung des Datenbefehls gibt es Methoden, wie in der folgenden Abbildung dargestellt.

In unserem Beispielprogramm wird die Methode **Adresse automatisch um 1 erhöhen** gewählt; der Binärwert ist 0100 0000 und der entsprechende Hexadezimalwert ist 0x40.

![](media/image-20230427083500152.png)

③ Für die Einstellung des Adressbefehls kann die Adresse wie unten dargestellt gewählt werden.

Im Beispielprogramm wird die erste Adresse 00H gewählt; die Binärzahl 1100 0000 entspricht dem Hexadezimalwert 0xc0.

![](media/image-20230427083716284.png)

④ Die Anforderung für die Dateneingabe besteht darin, dass das Signal an SDA unverändert bleiben muss, wenn SCL auf hohem Pegel ist und Daten eingegeben werden. Nur wenn das Taktsignal an SCL auf niedrigem Pegel ist, kann das Signal an SDA geändert werden. Die Dateneingabe erfolgt zuerst mit dem niedrigstwertigen Bit und dann mit dem höchstwertigen Bit.

⑤ Die Bedingung für das Ende der Datenübertragung ist, dass wenn SCL auf niedrigem Pegel und SDA auf niedrigem Pegel ist und SCL dann auf hohen Pegel geht, der Pegel von SDA auf hoch wechselt.

⑥ Anzeigesteuerung: Verschiedene Pulsbreiten einstellen; die Pulsbreite kann wie in der folgenden Abbildung dargestellt gewählt werden. Im Beispiel beträgt die Pulsbreite 4/16, und der Hexadezimalwert für 1000 1010 ist 0x8A.

![](media/image-20230427084941994.png)

**Anleitung zur Verwendung des Modulus-Tools**

Das Punktmatrix-Tool wird in der Online-Version verwendet; der Link lautet: [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#)

① Öffnen Sie den Link, und die Seite erscheint wie unten dargestellt.

![](media/354693b5679a2615c62e99b7025d6355.png)

② Die Punktmatrix ist 8\*16, also passen Sie die Höhe auf 8 und die Breite auf 16 an, wie in der folgenden Abbildung dargestellt.

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③ Hexadezimaldaten aus dem Muster generieren

Wie in der folgenden Abbildung dargestellt: Drücken Sie die linke Maustaste zum Auswählen, klicken Sie mit der rechten Maustaste zum Abbrechen; zeichnen Sie das gewünschte Muster, klicken Sie auf „Generate", und die benötigten Hexadezimaldaten werden generiert.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4) Anschlussplan:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

GND, VCC, SDA und SCL der 8x16 LED-Leuchttafel werden jeweils mit der Keyestudio Sensor-Erweiterungsplatine – (GND), + (VCC), A4, A5 für die serielle Zwei-Draht-Kommunikation verbunden.

(<span style="color: rgb(255, 76, 65);">Hinweis:</span> Obwohl es mit dem IIC-Pin von Arduino verbunden ist, ist dieses Modul nicht für IIC-Kommunikation vorgesehen. Der IO-Port hier simuliert I2C-Kommunikation und kann mit beliebigen zwei Pins verbunden werden.)

#### **(5) Testcode:**

Der Code zur Anzeige des Lächelgesichts

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls die serielle Kommunikation nutzt und es zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, was das Hochladen zum Scheitern bringen kann.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.1
  Matrix face
  http://www.keyestudio.com
*/
// Daten des Lächelbildes aus einem Modulus-Tool abrufen
unsigned char smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};

#define SCL_Pin  A5  // Takt-Pin auf A5 setzen
#define SDA_Pin  A4  // Daten-Pin auf A4 setzen

void setup() {
  // Pin als Ausgang setzen
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // Bildschirm löschen
  //matrix_display(clear);
}
void loop() {
  matrix_display(smile);  // Lächelbild anzeigen
}
// Diese Funktion wird für die Anzeige der Punktmatrix verwendet
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Funktion zum Starten der Datenübertragung aufrufen
  IIC_send(0xc0);  // Adresse auswählen

  for (int i = 0; i < 16; i++) // Bilddaten bestehen aus 16 Zeichen
  {
    IIC_send(matrix_value[i]); // Daten zum Übertragen von Bildern
  }

  IIC_end();   // Datenübertragung des Bildes beenden

  IIC_start();
  IIC_send(0x8A);  // Anzeigesteuerung und Pulsbreite 4/16 auswählen
  IIC_end();
}

// Bedingung, unter der die Datenübertragung beginnt
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
  for (byte mask = 0x01; mask != 0; mask <<= 1) // Jedes Zeichen hat 8 Stellen, die einzeln erkannt werden
  {
    if (send_data & mask) { // Hohe oder niedrige Pegel entsprechend jedem Bit (0 oder 1) setzen
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Takt-Pin SCL_Pin hochziehen, um die Datenübertragung zu beenden
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // Takt-Pin SCL_Pin herunterziehen, um SDA-Signale zu ändern
  }
}
```

#### **(6) Testergebnisse:**

Nach dem erfolgreichen Hochladen des Testcodes, dem Anschließen gemäß dem Schaltplan, dem Umlegen des DIP-Schalters nach rechts und dem Einschalten zeigt die Punktmatrix ein lächelndes Muster.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7) Erweiterungsprojekt:**

Wir verwenden das gerade erlernte Modulus-Tool, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), um auf der Punktmatrix die Muster Start, Vorwärtsfahren und Stopp nacheinander anzuzeigen und das Muster anschließend zu löschen. Das Zeitintervall beträgt 2000 ms.

![](media/9866c73416df7466b5fe8be3712e6eb3.png)

![](media/1c7ab4b08636c2fe61deaf6c784da7d8.png)

![](media/b0a961f27eb5f0b66603abe23d6bb56a.png)

**Vom Moduls-Tool erhaltener Code:**

**Code für das Muster Start:**

0x01,0x02,0x04,0x08,0x10,0x20,0x40,0x80,0x80,0x40,0x20,0x10,0x08,0x04,0x02,0x01

**Code für das Muster Vorwärtsfahren:**

0x00,0x00,0x00,0x00,0x00,0x24,0x12,0x09,0x12,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**Code für das Muster Rückwärtsfahren:**

0x00,0x00,0x00,0x00,0x00,0x24,0x48,0x90,0x48,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**Code für das Muster Linkskurve:**

0x00,0x00,0x00,0x00,0x00,0x00,0x44,0x28,0x10,0x44,0x28,0x10,0x44,0x28,0x10,0x00

**Code für das Muster Rechtskurve:**

0x00,0x10,0x28,0x44,0x10,0x28,0x44,0x10,0x28,0x44,0x00,0x00,0x00,0x00,0x00,0x00

**Code für das Muster Stopp:**

0x2E,0x2A,0x3A,0x00,0x02,0x3E,0x02,0x00,0x3E,0x22,0x3E,0x00,0x3E,0x0A,0x0E,0x00

**Code zum Bildschirm löschen:**

0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls die serielle Kommunikation nutzt und es zu Konflikten mit der Bluetooth-Seriellkommunikation kommen kann, was das Hochladen zum Scheitern bringen kann.)

```C
/*
  keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.2
  Matrix face
  http://www.keyestudio.com
*/

// Array zum Speichern von Bilddaten; kann selbst berechnet oder aus dem Modulus-Tool entnommen werden
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  // Takt-Pin auf A5 setzen
#define SDA_Pin  A4  // Daten-Pin auf A4 setzen

void setup() {
  // Pin als Ausgang setzen
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // Bildschirm löschen
  matrix_display(clear);
}
void loop() {
  matrix_display(start01);  // "Start"-Bild anzeigen
  delay(2000);
  matrix_display(front);    // "Vorwärts"-Bild anzeigen
  delay(2000);
  matrix_display(STOP01);   // "STOP01"-Bild anzeigen
  delay(2000);
  matrix_display(clear);    // "Löschen"-Bild anzeigen
  delay(2000);
}
// Diese Funktion wird für die Anzeige der Punktmatrix verwendet
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Funktion zum Starten der Datenübertragung aufrufen
  IIC_send(0xc0);  // Adresse auswählen

  for (int i = 0; i < 16; i++) // Bilddaten bestehen aus 16 Zeichen
  {
    IIC_send(matrix_value[i]); // Daten zum Übertragen von Bildern
  }

  IIC_end();   // Datenübertragung des Bildes beenden

  IIC_start();
  IIC_send(0x8A);  // Anzeigesteuerung und Pulsbreite 4/16 auswählen
  IIC_end();
}

// Bedingung, unter der die Datenübertragung beginnt
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
  for (byte mask = 0x01; mask != 0; mask <<= 1) // Jedes Zeichen hat 8 Stellen, die einzeln erkannt werden
  {
    if (send_data & mask) { // Hohe oder niedrige Pegel entsprechend jedem Bit (0 oder 1) setzen
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Takt-Pin SCL_Pin hochziehen, um die Datenübertragung zu beenden
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // Takt-Pin SCL_Pin herunterziehen, um SDA-Signale zu ändern
  }
}
```

Nach dem Hochladen des Testcodes zeigt das Gesichtsausdrucks-Display diese Muster der Reihe nach und wiederholt diese Sequenz.

![](media/e7ba47508826acc25d348182a0530c05.png)

![](media/831b7e0e07250cbc7bdc4fa509c5a0a3.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)