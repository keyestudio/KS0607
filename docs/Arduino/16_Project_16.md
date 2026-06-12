### Projekt 16: Bluetooth-Fernsteuerung

![](./media/img-20240111140012.png)

#### **(1) Beschreibung:**

In den letzten Jahrzehnten ist Bluetooth zum beliebtesten drahtlosen Kommunikationsmodul geworden, da es einfach zu verwenden ist und breite Anwendung in den meisten batteriebetriebenen Geräten gefunden hat.

Um mit der Zeit, der Realität und den Bedürfnissen der Kunden Schritt zu halten, wurde Bluetooth mehrmals aktualisiert. In den letzten Jahren hat es viele Veränderungen hinsichtlich Datenübertragungsrate, Stromverbrauch von Wearables und IoT-Geräten sowie Sicherheitssystemen und anderem erfahren. Hier planen wir, das DX-BT24 mit dem Arduino-Board kennenzulernen.

#### **(2) Parameter:**

- Bluetooth-Protokoll: Bluetooth Specification V5.1 BLE

- Serielle Übertragung und Empfang ohne Byte-Begrenzung

- Kommunikationsreichweite: 40 m (offene Umgebung)

- Betriebsfrequenz: 2,4 GHz ISM-Band

- Modulationsverfahren: GFSK (Gaussian Frequency Shift Keying)

- Sicherheitsfunktionen: Authentifizierung und Verschlüsselung

- Unterstützte Dienste: Central und Peripheral UUIDs FFE0, FFE1, FFE2

- Stromverbrauch: automatischer Schlafmodus, Standby-Strom 400uA\~800uA, 8,5 mA während der Übertragung.

- Stromversorgung: 5 V

- Betriebstemperatur: –10 bis +65 Grad Celsius

#### **(3) Anschlussdiagramm:**

1. STATE ist der Statustestpin, der mit der internen Leuchtdiode verbunden ist, und bleibt normalerweise nicht angeschlossen.

2. RXD ist die serielle Schnittstellenstelle für den Empfangsanschluss.

3. TXD ist die serielle Schnittstellenstelle für den Sendeanschluss.

4. GND ist der Masseanschluss.

5. VCC ist der Pluspol.

6. EN/BRK: Das Trennen dieses Pins führt zur Trennung der Bluetooth-Verbindung und bleibt normalerweise nicht angeschlossen.

(Hinweis: Hier wird das Bluetooth direkt mit dem V2-Shield verbunden. **Bitte achten Sie auf die Richtung**.)

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)


#### **(4) App herunterladen und installieren:**

##### **Für iOS-System**

1\. Öffnen Sie den App Store.

2\. Suchen Sie <span style="color: rgb(61, 167, 66);">KeyesRobot</span> im Apple Store und klicken Sie auf Herunterladen.

![](./media/img-20240111141301.png)

3\. Nach der Installation der App sehen Sie folgendes Symbol auf Ihrem Telefon-Desktop.

![](./media/img-20240111141412.png)

**So verbinden Sie ein iOS-Gerät mit dem Bluetooth-Modul:**

1\. Aktivieren Sie Bluetooth und Ortungsdienste auf dem Telefon über die Einstellungen.

![](./media/img-20240111141943.png)

2\. Erlauben Sie der KeyesRobot-App den Zugriff auf Bluetooth über die Einstellungen.

![](./media/img-20240111142052.png)

3\. Klicken Sie zum Öffnen der KeyesRobot-App.

![](./media/img-20240111142140.png)

4\. Die KeyesRobot-App ist eine universelle App, die für mehrere Keyestudio-Roboter verwendet wird. Wenn auf der Benutzeroberfläche nicht „TANK ROBOT" angezeigt wird, können Sie auf die Schaltflächen links und rechts klicken, um „TANK ROBOT" zu finden.

5\. Klicken Sie auf die <span style="color: rgb(61, 167, 66);">Bluetooth</span>-Schaltfläche ![](./media/img-20240111142336.png) in der oberen rechten Ecke, um Bluetooth zu scannen.

![](./media/img-20240111142415.png)

6\. Sie sehen ein Bluetooth-Gerät namens <span style="color: rgb(0, 209, 0);">**BT24**</span>. Klicken Sie auf die Schaltfläche <span style="color: rgb(255, 169, 0);">Verbinden</span>.

![](./media/img-20240111142536.png)

7\. Wenn die integrierte LED am Bluetooth-Modul aufhört zu blinken und dauerhaft leuchtet, bedeutet dies, dass Ihr Telefon erfolgreich mit dem Bluetooth-Modul verbunden wurde.

![](./media/img-20240111142702.png)


##### **Für Android-System**

1\. Suchen Sie <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> in Google Play, oder öffnen Sie den folgenden Link, um die App herunterzuladen und zu installieren.

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Aktivieren Sie Bluetooth und Ortungsdienste des Mobiltelefons.

![](./media/img-20240111143354.png)

3\. Suchen Sie die KeyesRobot-Bluetooth-App in den Einstellungen, klicken Sie auf die Berechtigungsoptionen der App und aktivieren Sie Standort- und Berechtigungen für nahegelegene Geräte. (<span style="color: rgb(255, 76, 65);">Hinweis:</span> Einige Mobiltelefone verfügen nicht über die Funktion für Berechtigungen für nahegelegene Geräte.)

![](./media/img-20240111143451.png)

4\. Klicken Sie zum Öffnen der KeyesRobot-App.

![](./media/img-20240111143529.png)

5\. Die KeyesRobot-App ist eine universelle App, die für mehrere Keyestudio-Roboter verwendet wird. Wenn auf der Benutzeroberfläche nicht „TANK ROBOT" angezeigt wird, können Sie auf die Schaltflächen links und rechts klicken, um „TANK ROBOT" zu finden.

6\. Klicken Sie auf die <span style="color: rgb(61, 167, 66);">Bluetooth</span>-Schaltfläche ![](./media/img-20240111142336.png) in der oberen rechten Ecke, um Bluetooth zu scannen.

![](./media/img-20240111142415.png)

7\. Sie sehen ein Bluetooth-Gerät namens <span style="color: rgb(0, 209, 0);">**BT24**</span>. Klicken Sie auf die Schaltfläche <span style="color: rgb(255, 169, 0);">Verbinden</span>.

![](./media/img-20240111143910.png)

8\. Wenn Ihr Telefon erfolgreich mit dem Bluetooth-Modul verbunden wurde, hört die integrierte LED am Bluetooth-Modul auf zu blinken und leuchtet dauerhaft.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(5) Bluetooth-App testen:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was das Hochladen fehlschlagen lassen kann.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.1
Bluetooth
http://www.keyestudio.com
*/

char ble_val; // Zeichenvariable (zum Speichern des per Bluetooth empfangenen Wertes)

void setup() 
{
	Serial.begin(9600);
}

void loop() 
{
    if (Serial.available() > 0) // Bestimmen, ob Daten im seriellen Puffer vorhanden sind
    {
        ble_val = Serial.read(); // Daten aus dem seriellen Puffer lesen
        Serial.println(ble_val); // Ausgabe drucken
    }
}
```

Laden Sie den Code auf das Entwicklungsboard hoch, stecken Sie dann das Bluetooth-Modul ein und verbinden Sie anschließend das Mobiltelefon mit dem Bluetooth-Modul.

Nachdem das Mobiltelefon erfolgreich mit dem Bluetooth-Modul verbunden wurde, klicken Sie zum Öffnen der Bluetooth-App und klicken Sie auf die Schaltfläche <span style="color: rgb(0, 252, 255);">Auswählen</span> auf der <span style="color: rgb(0, 252, 255);">Startseite</span>.

![](./media/img-20240111144744.png)

Die Hauptoberfläche der Bluetooth-App ist in der folgenden Abbildung dargestellt.

![](./media/img-20240111144859.png)

Nachdem der obige Code erfolgreich hochgeladen wurde, öffnen Sie den seriellen Monitor der Arduino IDE und stellen Sie die Baudrate auf 9600 ein. Klicken Sie auf das Symbol auf der App-Oberfläche, und der serielle Monitor zeigt den per Schaltfläche gesendeten Befehl an.

![](media/805f8ee5c8998a5d6cb8bcef9da09186.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Hinweis: Die App-Verbindungsmethode ist wie unten beschrieben.**</span>
<br>
<b>

#### **(6) Code-Erklärung:**

**Serial.available()** gibt die Anzahl der aktuell im seriellen Puffer verbleibenden Zeichen an.

Diese Funktion wird im Allgemeinen verwendet, um zu bestimmen, ob Daten in diesem Bereich vorhanden sind. Wenn Serial.available()\>0, bedeutet dies, dass der serielle Port Daten empfangen hat und diese gelesen werden können.

**Serial.read()** bezieht sich auf das Entnehmen und Lesen eines Bytes an Daten aus dem seriellen Puffer. Wenn beispielsweise ein Gerät Daten über den seriellen Port an das Arduino sendet, können wir Serial.read() verwenden, um die gesendeten Daten zu lesen.

#### **(7) Erweiterungsprojekt:**

Hier verwenden wir den vom Mobiltelefon gesendeten Befehl, um eine LED-Leuchte ein- oder auszuschalten. Wie im Schaltplan zu sehen, ist eine LED am D9-Pin angeschlossen.

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">Hinweis: </span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Kommunikation des Bluetooth kommen kann, was das Hochladen des Codes fehlschlagen lassen kann.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.2
Bluetooth
http://www.keyestudio.com
*/

int LED = 9;
char ble_val; // Ganzzahlvariable zum Speichern des per Bluetooth empfangenen Wertes

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);
}

void loop() 
{

    if (Serial.available() > 0) // Bestimmen, ob Daten im seriellen Puffer vorhanden sind
    {
        ble_val = Serial.read(); // Daten aus dem seriellen Puffer lesen
        Serial.print("DATA RECEIVED:");
        Serial.println(ble_val);
        if (ble_val == 'a') 
        {
            digitalWrite(LED, HIGH);
            Serial.println("led on");
        }
        if (ble_val == 'b') 
        {
            digitalWrite(LED, LOW);
            Serial.println("led off");
        }
    }
}
```

![](media/3577f17c526b1dc55d4f587ef95f2d08.png)

Nachdem der obige Code erfolgreich hochgeladen wurde, öffnen Sie den seriellen Monitor der Arduino IDE und stellen Sie die Baudrate auf 9600 ein. Klicken Sie auf ![](media/3fd6c998c0f665fb607a5827794b9bfe.png), um die LED zu steuern. Beim Klicken wird ein Zeichen „a" gesendet, und die LED leuchtet auf. Wenn diese Schaltfläche erneut gedrückt wird, erlischt die LED.

![](./media/img-20240117094533.png)

![](media/b45c3c46391467218fe07003dbb2f3e3.png)

Sie müssen das BT-Modul entfernen, wenn Sie die Projekte abgeschlossen haben.