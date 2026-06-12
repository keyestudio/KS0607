### Projekt 9: 8*16 LED-Punktmatrix für Gesichtsausdrücke

#### **(1)Beschreibung:**

Wäre es nicht toll, wenn dem Roboter ein Ausdrucks-Display hinzugefügt wird? Die Keyestudio 8*16 LED-Punktmatrix kann genau das leisten. Mit ihrer Hilfe können Sie selbst Gesichtsausdrücke, Bilder, Muster und andere Anzeigen gestalten.

Das 8*16 LED-Board verfügt über 128 LEDs. Die Daten des Mikroprozessors (Arduino) kommunizieren mit dem AiP1640 über eine Zwei-Draht-Busschnittstelle. Damit kann er das Ein- und Ausschalten von 128 LEDs auf dem Modul steuern, sodass die Punktmatrix auf dem Modul das gewünschte Muster anzeigt. Ein HX-2.54 4Pin-Kabel wird für Ihre Bequemlichkeit bei der Verkabelung mitgeliefert.

#### **(2)Parameter:**

-   Betriebsspannung: DC 3,3–5 V

-   Leistungsaufnahme: 400 mW

-   Schwingungsfrequenz: 450 KHz

-   Treiberstrom: 200 mA

-   Betriebstemperatur: -40\~80℃

-   Kommunikationsmodus: Zwei-Draht-Bus

#### **(3)Wissenswertes:**

**Schaltkreis der 8\*16 LED-Punktmatrix**

![](media/edf6c77d05904eebbaa89d557e9e9c1a.png)

**Funktionsprinzip der 8\*16 LED-Punktmatrix**

Wie steuert man jede LED der 8*16-Punktmatrix? Es ist bekannt, dass jedes Byte 8 Bits hat und jedes Bit 0 oder 1 ist. Wenn es 0 ist, ist die LED aus, wenn es 1 ist, ist die LED an. Ein Byte kann eine Spalte der LEDs steuern, und entsprechend können 16 Bytes 16 Spalten von LEDs steuern – das ist die 8*16-Punktmatrix.

**Pin-Beschreibung und Kommunikationsprotokoll**

Die Daten des Mikroprozessors (Arduino) kommunizieren mit dem AiP1640 über ein Zwei-Draht-Buskabel.

Das Kommunikationsprotokoll-Diagramm ist wie folgt: (SCLK) ist SCL, (DIN) ist SDA.

![](media/ea2bab37f23c09453c680590b84653d6.png)

①Die Startbedingung für die Dateneingabe: SCL ist High-Pegel und SDA wechselt von High zu Low.

②Für die Datenbefehls-Einstellung gibt es Methoden, wie in der folgenden Abbildung gezeigt.

In unserem Beispielprogramm wird die Methode **Adresse automatisch um 1 erhöhen** gewählt; der Binärwert ist 0100 0000 und der entsprechende Hexadezimalwert ist 0x40.

![](media/image-20230907161100692.png)

③Für die Adressbefehls-Einstellung kann die Adresse wie unten gezeigt ausgewählt werden.

Im Beispielprogramm wird die erste Adresse 00H ausgewählt, und die Binärzahl 1100 0000 entspricht dem Hexadezimalwert 0xc0.

![](media/image-20230907161152467.png)

④Die Anforderung für die Dateneingabe ist, dass bei High-Pegel von SCL während der Dateneingabe das Signal auf SDA unverändert bleiben muss. Nur wenn das Taktsignal auf SCL Low-Pegel hat, kann das Signal auf SDA geändert werden. Die Dateneingabe erfolgt zuerst mit dem niedrigsten Bit und zuletzt mit dem höchsten Bit.

⑤Die Bedingung für das Ende der Datenübertragung ist, dass wenn SCL auf Low-Pegel und SDA auf Low-Pegel ist und SCL auf High-Pegel wechselt, der Pegel von SDA auf High wechselt.

⑥Anzeigesteuerung: verschiedene Pulsbreiten einstellen; die Pulsbreite kann wie in der folgenden Abbildung gezeigt ausgewählt werden.

Im Beispiel beträgt die Pulsbreite 4/16, und das Hexadezimaläquivalent von 1000 1010 ist 0x8A.

![](media/image-20230907161220995.png)

**Anleitung zur Verwendung des Modulus-Tools**

Das Punktmatrix-Tool verwendet die Online-Version, der Link lautet: <http://dotmatrixtool.com/#>

①Rufen Sie den Link auf, und die Seite erscheint wie unten abgebildet.

![](media/354693b5679a2615c62e99b7025d6355.png)

②Die Punktmatrix ist 8\*16, passen Sie daher die Höhe auf 8 und die Breite auf 16 an, wie in der folgenden Abbildung gezeigt.

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③Hexadezimaldaten aus dem Muster generieren.

Wie in der folgenden Abbildung gezeigt: linke Maustaste drücken zum Auswählen, rechtsklicken zum Abbrechen; zeichnen Sie das gewünschte Muster, klicken Sie auf Generate, und die benötigten Hexadezimaldaten werden generiert.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4)Anschlussdiagramm:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

GND, VCC, SDA und SCL des 8x16 LED-Boards werden jeweils mit G(GND), V(VCC), A4 und A5 der Erweiterungsplatine für die serielle Zwei-Draht-Kommunikation verbunden.

(<span style="color: rgb(255, 76, 65);">Hinweis:</span> Obwohl es mit dem IIC-Pin des Arduino verbunden ist, ist dieses Modul nicht für die IIC-Kommunikation vorgesehen. Der IO-Port hier simuliert die I2C-Kommunikation und kann mit beliebigen zwei Pins verbunden werden.)

#### **(5)Testcode:**

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt.

![](media/e346413e7f38f5f6368dd8262f173514.png)

![](media/8ecfff600093779602b37d2202493057.png)

![](media/0f0df06e3ed2adbbe3ffaa20dd3fa0a5.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es möglicherweise zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

![](media/75e6f65c9a299868d37544ac42c54f66.png)

#### **(6)Testergebnisse:**

Nachdem der Testcode erfolgreich hochgeladen wurde, verkabeln Sie alles, drehen Sie den DIP-Schalter auf die ON-Seite und schalten Sie die Stromversorgung ein. Auf der Punktmatrix erscheint ein lächelndes Muster.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7)Erweiterungsübung:**

Wir verwenden das gerade erlernte Modulus-Tool, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), damit die Punktmatrix die Muster Start, Vorwärts fahren und Stopp anzeigt und dann das Muster löscht. Das Zeitintervall beträgt 2000 ms.

![](media/31ab1346c58438ca95c990e4ff963c0d.png)

Block zum Anzeigen eines lächelnden Gesichts![](media/1702a82ce685e3e7da7b136cbc51e718.png)

Code zum Anzeigen eines Ausdrucks![](media/bae6801afc8fbcc0e7a70c243559c266.png)

Block zum Anzeigen eines Herzens![](media/dcaa414f16d10068d2c3627959141da6.png)

Code für Vorwärtsfahren![](media/8fc218e6b35826aa31f5e00f61414651.png)

Block für Rückwärtsfahren![](media/043abae4540c578f93772ed9b6648e60.png)

Block für Linksdrehen![](media/7b3d80a76228ee5b23555af17269a02d.png)

Block für Rechtsdrehen![](media/5a84b3538a62367a8f35cc59071c0bda.png)

Block zum Stoppen![](media/733bd1f96e1c9d116033a317cb507fac.png)

Block zum Löschen![](media/06d37680acd61c9c5c4113c78c985eca.png)

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt.

（1）![](media/e346413e7f38f5f6368dd8262f173514.png)

（2）![](media/840217b5879f1fce9e36566dc76914a4.png)

（3）![](media/e72e75122897b0ef930196f762080623.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es möglicherweise zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

![](media/dee30ed46775feb634d4e8e4ec0a189a.png)

Laden Sie den Code auf das Entwicklungsboard hoch; das 8\*16-Board zeigt folgende Muster an.

![](./media/image-20250709134319784.png)

![](./media/image-20250709134332835.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)