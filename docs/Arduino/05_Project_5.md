### Projekt 5: Servo-Steuerung

#### **(1)Beschreibung:**

Ein Servomotor ist ein positionsgesteuerter Drehantrieb. Er besteht hauptsächlich aus einem Gehäuse, einer Leiterplatte, einem kernlosen Motor, einem Getriebe und einem Positionssensor. Das Funktionsprinzip besteht darin, dass der Servo das vom Mikrocontroller oder Empfänger gesendete Signal empfängt und ein Referenzsignal mit einer Periode von 20 ms und einer Breite von 1,5 ms erzeugt. Anschließend wird die erfasste DC-Vorspannungsspannung mit der Spannung des Potentiometers verglichen und die Spannungsdifferenzausgabe ermittelt.

Wenn die Motorgeschwindigkeit konstant ist, wird das Potentiometer über das kaskadierende Untersetzungsgetriebe zum Drehen angetrieben, wodurch die Spannungsdifferenz 0 wird und der Motor aufhört zu drehen. Im Allgemeinen liegt der Drehwinkelbereich des Servos zwischen 0° und 180°.

Der Drehwinkel des Servomotors wird durch die Regelung des Tastverhältnisses des PWM-Signals (Pulsweitenmodulation) gesteuert. Der Standardzyklus des PWM-Signals beträgt 20 ms (50 Hz). Theoretisch liegt die Breite zwischen 1 ms und 2 ms, tatsächlich jedoch zwischen 0,5 ms und 2,5 ms. Die Breite entspricht dem Drehwinkel von 0° bis 180°. Beachten Sie, dass das gleiche Signal bei verschiedenen Motormarken zu unterschiedlichen Drehwinkeln führen kann.

![](media/69be958142b773acdae33eeef12afed7.png)

Im Allgemeinen hat ein Servo drei Leitungen in Braun, Rot und Orange. Die braune Leitung ist geerdet, die rote ist die Plusleitung und die orangefarbene ist die Signalleitung.

![](media/49467dfa70799401a5a5acc691014aee.png)

Der Winkel des Servos:

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Parameter:**

- Betriebsspannung: DC 4,8 V \~ 6 V

- Betriebswinkelbereich: ca. 180° (bei 500 → 2500 μsec)

- Pulsbreitenbereich: 500 → 2500 μsec

- Leerlaufdrehzahl: 0,12 ± 0,01 sec / 60 (DC 4,8 V) 0,1 ± 0,01 sec / 60 (DC 6 V)

- Leerlaufstrom: 200 ± 20 mA (DC 4,8 V) 220 ± 20 mA (DC 6 V)

- Haltemoment: 1,3 ± 0,01 kg · cm (DC 4,8 V) 1,5 ± 0,1 kg · cm (DC 6 V)

- Haltestrom: ≦ 850 mA (DC 4,8 V) ≦ 1000 mA (DC 6 V)

- Ruhestrom: 3 ± 1 mA (DC 4,8 V) 4 ± 1 mA (DC 6 V)

#### **(3)Anschlussdiagramm:**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span> Die braune, rote und orangefarbene Leitung des Servos werden jeweils mit Gnd(G), 5v(V) und 10 des Shields verbunden. Denken Sie daran, eine externe Stromversorgung anzuschließen, da der Servo einen hohen Strom benötigt. Andernfalls wird das Entwicklungsboard beschädigt.

#### **(4)Testcode 1:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.1
Servo
http://www.keyestudio.com
*/

#define servoPin 10 // Der Pin des Servos

int pos; // Die Variable des Servowinkels
int pulsewidth; // Die Variable der Pulsbreite des Servos

void setup() 
{
    pinMode(servoPin, OUTPUT); // Den Pin des Servos als Ausgang setzen
    procedure(0); // Den Winkel des Servos auf 0° setzen
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  // Von 1° bis 180°
    {
    	// in Schritten von 1 Grad	
        procedure(pos); // Zum Winkel 'pos' drehen
        delay(15); // Rotationsgeschwindigkeit steuern
    }
    for (pos = 180; pos >= 0; pos -= 1) // Von 180° bis 1°
    { 
        procedure(pos); // Zum Winkel 'pos' drehen
        delay(15);
    }
}
// Die Funktion steuert den Servo
void procedure(int myangle) 
{
    pulsewidth = myangle * 11 + 500; // Den Wert der Pulsbreite berechnen
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth); // Die Zeit im High-Pegel entspricht der Pulsbreite
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000)); // Da der Zyklus 20 ms beträgt, verbleibt die restliche Zeit im Low-Pegel
}
```

Nach dem Hochladen des Codes bewegt sich der Servo von 0° bis 180°. In den folgenden Kapiteln wird erläutert, wie ein Servo angesteuert wird. Darüber hinaus kann ein Servo mit einer Servo-Bibliothek von Arduino gesteuert werden.

<span style="color: rgb(255, 76, 65);">Hinweis:</span> Diese Servo-Bibliotheksdatei verwendet Timer 1, und die PWM-Ausgabe der IO-Ports 9 und 10 verwendet ebenfalls Timer 1. Daher kann diese Servo-Bibliothek nicht verwendet werden, wenn später die PWM-Ausgabe von D9 und D10 genutzt wird.

#### **(5)Testcode 2:**

(<span style="color: rgb(255, 76, 65);">Hinweis: </span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Kommunikation des Bluetooths kommen kann, was dazu führen kann, dass das Hochladen des Codes fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.2
Servo
<http://www.keyestudio.com>
*/

#include <Servo.h>

Servo myservo; // Servo erstellen
int pos = 0; // Die Variablen des Winkels speichern

void setup() 
{
	myservo.attach(10); // Den Servo mit dem digitalen Port 10 verbinden
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  // Von 0° bis 180°
    {
    	// Schrittlänge ist 1
        myservo.write(pos); // Zum Winkel 'pos' drehen
        delay(15); // 15 ms warten, um die Geschwindigkeit zu steuern
    }

    for (pos = 180; pos >= 0; pos -= 1)  // Von 180° bis 0°
    {
        myservo.write(pos); // Zum Winkel 'pos' drehen
        delay(15); // 15 ms warten, um die Geschwindigkeit zu steuern
    }
}
```

#### **(6)Testergebnisse:**

Code hochladen, Stromversorgung anschließen und der Servo bewegt sich im Bereich von 0° bis 180°.

![](./media/img-20240117090810.png)

#### **(7)Code-Erklärung:**

Arduino wird mit **\#include \<Servo.h\>** geliefert (Servo-Funktion und -Anweisungen)

Im Folgenden sind einige häufig verwendete Anweisungen der Servo-Funktion aufgeführt:

1\. **attach（Schnittstelle）**——Servo-Schnittstelle festlegen, Port 9 und 10 sind verfügbar

2\. **write（Winkel）**——Die Anweisung zum Festlegen des Drehwinkels des Servos, der Winkelbereich liegt zwischen 0° und 180°

3\. **read（）**——Die Anweisung zum Lesen des Winkels des Servos, liest den Befehlswert von „write()"

4\. **attached（）**——Überprüfen, ob der Parameter des Servos an seine Schnittstelle gesendet wurde

Hinweis: Das oben genannte Schreibformat lautet „Servo-Variablenname, spezifische Anweisung（）", zum Beispiel: myservo.attach(10)