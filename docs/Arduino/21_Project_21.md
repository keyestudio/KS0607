### Projekt 21: Lüfter

#### **(1) Beschreibung：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Dieses Lüftermodul verwendet einen HR1124S Motorsteuerungs-Chip, einen einspurigen H-Brücken-Treiber-Chip, der einen PMOS- und NMOS-Leistungstransistor mit niedrigem Leitwiderstand enthält. Der niedrige Leitwiderstand kann den Energieverbrauch verringern und dazu beitragen, dass der Chip länger sicher arbeitet.

Darüber hinaus macht ihn sein niedriger Standby-Strom und niedriger statischer Arbeitsstrom für Spielzeug geeignet. Wir können die Drehrichtung und Geschwindigkeit des Lüfters durch Ausgabe von IN+ und IN- Signalen sowie PWM-Signalen steuern.

#### **(2) Spezifikation:**

Betriebsspannung: 5V

Strom: 200MA

Maximale Leistung: 2W

Betriebstemperatur: -10 Grad Celsius bis +50 Grad Celsius

Größe: 47,6MM \*23,8MM

#### **(3) Anschlussdiagramm:**

Das Lüftermodul benötigt einen hohen Strom zum Antrieb; daher installieren wir einen Batteriehalter.

![](media/2bd9aa5cc21e274458328958561f1915.png)

Die Pins GND, VCC, IN+ und IN- des Lüftermoduls sind mit den Pins G, V, D12 und D13 des Shields verbunden.

#### **(4) Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.1
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;

void setup()
{
    pinMode(INA, OUTPUT);// Digitalen Port INA als Ausgang setzen
    pinMode(INB, OUTPUT);// Digitalen Port INB als Ausgang setzen
}

void loop() 
{
    // Lüfter für 3s gegen den Uhrzeigersinn drehen lassen
    digitalWrite(INA, LOW);
    digitalWrite(INB, HIGH);
    delay(3000);
    // Lüfter für 1s anhalten
    digitalWrite(INA, LOW);
    digitalWrite(INB, LOW);
    delay(1000);
    // Lüfter für 3s im Uhrzeigersinn drehen lassen
    digitalWrite(INA, HIGH);
    digitalWrite(INB, LOW);
    delay(3000);
}
```

#### **(5) Testergebnisse：**

Code hochladen, Komponenten verdrahten und Strom anschließen. Der kleine Lüfter dreht sich 3000ms lang gegen den Uhrzeigersinn, hält 1000ms an und dreht sich dann 300ms im Uhrzeigersinn.

![](./media/img-20240117085032.png)

#### **(6) Erweiterte Übung:**

Wir haben das Funktionsprinzip des Flammensensors verstanden. Als Nächstes schließen wir einen Flammensensor in den Schaltkreis an, wie unten gezeigt. Dann steuern wir den Lüfter so, dass er ein Feuer mit dem Flammensensor ausbläst.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.2
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;
int flame = A1; // Flammensensor-Pin als analogen Pin A1 definieren
int val = 0; // Digitale Variable definieren

void setup() 
{
    pinMode(INA, OUTPUT);// Digitalen Port INA als Ausgang setzen
    pinMode(INB, OUTPUT);// Digitalen Port INB als Ausgang setzen
    pinMode(flame, INPUT); // Flamme als Eingangsquelle definieren
}

void loop() 
{
    val = analogRead(flame); // Analogen Wert des Flammensensors lesen
    if (val <= 700)  // Wenn analoger Wert ≤ 700, Lüfter einschalten
    {
        // Lüfter einschalten, wenn Flamme erkannt wird
        digitalWrite(INA, LOW);
        digitalWrite(INB, HIGH);
    } 
    else 
    {
        // Andernfalls stoppt er den Betrieb
        digitalWrite(INA, LOW);
        digitalWrite(INB, LOW);
    }
}
```

Nachdem der Code hochgeladen wurde, schalten Sie den Netzschalter des Motorantriebs-Shields ein. Sie können den Lüfter einschalten, wenn eine Flamme vom linken Flammensensor des Roboters erkannt wird.

![](./media/image-20250709115926832.png)