### Projekt 7: IR-Empfang

#### **(1) Beschreibung:**

![](media/8969111328604c5358f7c915ac94e474.png)

Zweifellos ist die Infrarot-Fernbedienung im täglichen Leben allgegenwärtig. Sie wird zur Steuerung verschiedener Haushaltsgeräte verwendet, wie z. B. Fernseher, Stereoanlagen, Videorekorder und Satellitenreceiver. Die Infrarot-Fernbedienung besteht aus einem Infrarot-Sende- und einem Infrarot-Empfangssystem, also einer Infrarot-Fernbedienung, einem Infrarot-Empfangsmodul und einem Mikrocontroller, der zur Dekodierung fähig ist.

Das vom Fernbedienungsgerät ausgesendete 38K-Infrarot-Trägersignal wird vom Kodierchip im Fernbedienungsgerät kodiert. Es besteht aus einem Pilotcode-Abschnitt, einem Benutzercode, einem invertierten Benutzercode, einem Datencode und einem invertierten Datencode. Das Zeitintervall des Impulses wird verwendet, um zu unterscheiden, ob es sich um ein 0- oder 1-Signal handelt, und die Kodierung setzt sich aus diesen 0- und 1-Signalen zusammen.

Der Benutzercode derselben Fernbedienung bleibt unverändert, während der Datencode die Taste unterscheidet.

Wenn die Taste der Fernbedienung gedrückt wird, sendet die Fernbedienung ein Infrarot-Trägersignal aus. Wenn der IR-Empfänger das Signal empfängt, dekodiert das Programm das Trägersignal und stellt fest, welche Taste gedrückt wurde. Der Mikrocontroller dekodiert das empfangene 01-Signal und bestimmt damit, welche Taste der Fernbedienung gedrückt wurde.

![](media/image-20230426172824683.png)

Der Infrarot-Empfänger ist auf der Motorsteuerungsplatine eingelötet. Er integriert Empfang, Verstärkung und Demodulation, wobei der interne IC bereits so eingestellt ist, dass er Infrarotempfang und -ausgabe ermöglicht und mit TTL-Signalen kompatibel ist. Er gibt digitale Signale aus und eignet sich für Infrarot-Fernbedienung und Infrarot-Datenübertragung. Dieses Modul verfügt über nur drei Pins, darunter Signal, VCC und GND, sodass es sehr einfach zu verbinden und mit Mikrocontrollern wie Arduino zu kommunizieren ist.

#### **(2) Parameter:**

Betriebsspannung: 3,3–5 V (DC)

Schnittstelle: 3PIN

Ausgangssignal: Digitalsignal

Empfangswinkel: 90 Grad

Frequenz: 38 kHz

Empfangsreichweite: 10 m

Auf der Motorsteuerungsplatine integrierter Infrarot-Empfänger:

![](./media/img-20240117082433.png)




#### **(3) Testcode:**

Sie müssen zunächst die IR-Bibliothek importieren.

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 7.1

IRremote

http://www.keyestudio.com

*/

#include <IRremote.h> // IRremote-Bibliotheksdeklaration

int RECV_PIN = 3; // Pin des IR-Empfängers als 3 definieren
IRrecv irrecv(RECV_PIN);
decode_results results; // Dekodierungsergebnisse werden im "result" von "decode results" gespeichert

void setup() 
{
    Serial.begin(9600);
    irrecv.enableIRIn(); // Empfänger aktivieren
}

void loop() 
{
    if (irrecv.decode(&results)) // Erfolgreich dekodiert, eine Reihe von Infrarotsignalen empfangen
    {
        Serial.println(results.value, HEX); // Zeile in 16er HEX ausgeben und empfangenen Code ausgeben
        irrecv.resume(); // Nächsten Wert empfangen
    }
    delay(100);
}
```

#### **(4) Testergebnisse:**

Laden Sie den Testcode hoch, öffnen Sie den seriellen Monitor und stellen Sie die Baudrate auf 9600 ein, und richten Sie die Fernbedienung auf den IR-Empfänger. Dann wird der entsprechende Wert angezeigt. Wenn Tasten längere Zeit gedrückt gehalten werden, erscheinen Fehlercodes.

![](media/a484b81d031c8d6e8addb169136fd45c.png)

Im Folgenden haben wir den Tastenwert der Keyestudio-Fernbedienung aufgelistet. Sie können ihn als Referenz aufbewahren.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

Der IR-Empfänger ist an D3 angeschlossen, daher ist keine Verkabelung erforderlich.

#### **(5) Code-Erklärung:**

**irrecv.enableIRIn():** Nach dem Aktivieren der IR-Dekodierung werden die IR-Signale empfangen, dann prüft die Funktion „decode()" kontinuierlich, ob die Dekodierung erfolgreich war.

**irrecv.decode(&results):** Nach erfolgreicher Dekodierung gibt diese Funktion „true" zurück und speichert das Ergebnis in „results". Nach dem Dekodieren eines IR-Signals wird die Funktion resume() ausgeführt und das nächste Signal empfangen.

#### **(6) Erweiterungsübung:**

Wir haben den Tastenwert der IR-Fernbedienung dekodiert. Wie wäre es, die LED durch den gemessenen Wert zu steuern? Wir könnten ein Experiment entwerfen.

Schließen Sie eine LED an D9 an und drücken Sie dann die Tasten der Fernbedienung, um die LED ein- und auszuschalten.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 7.2
IRremote
http://www.keyestudio.com
*/

#include <IRremote.h> // IRremote-Deklaration

int RECV_PIN = 3; // Pin der LED als Pin 3 definieren
int LED = 9;
bool flag = 0;
IRrecv irrecv(RECV_PIN);
decode_results results; // Dekodierungsergebnisse werden im "result" von "decode results" gespeichert

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT); // LED als Ausgang festlegen
    irrecv.enableIRIn(); // Empfänger aktivieren
}

void loop() 
{
    if (irrecv.decode(&results)) 
    {
        if (results.value == 0xFF02FD & flag == 0) // Der obige Tastencode, wir verwenden die OK-Taste der Fernbedienung, wenn die OK-Taste gedrückt wird
        {
            digitalWrite(LED, HIGH); // LED ein
            flag = 1;
        }

        else if (results.value == 0xFF02FD & flag == 1) // Erneut drücken
        {
            digitalWrite(LED, LOW); // LED aus
            flag = 0;
        }
        irrecv.resume(); // Nächsten Wert empfangen
    }
}
```

Laden Sie den Code auf die Entwicklungsplatine hoch und drücken Sie die „OK"-Taste auf der Fernbedienung, um die LED ein- und auszuschalten.

![](./media/img-20240117090645.png)