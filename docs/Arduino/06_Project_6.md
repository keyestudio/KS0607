### Projekt 6: Ultraschallsensor

#### **(1) Beschreibung:**

![](media/0180b169a1c3b228394b43df704fac32.png)

Der HC-SR04 Ultraschallsensor verwendet Sonar zur Entfernungsmessung zu einem Objekt, ähnlich wie Fledermäuse es tun. Er bietet eine hervorragende berührungslose Entfernungserkennung mit hoher Genauigkeit und stabilen Messwerten in einem einfach zu verwendenden Gehäuse. Er wird komplett mit Ultraschall-Sender- und Empfängermodulen geliefert.

Der HC-SR04 bzw. der Ultraschallsensor wird in einer Vielzahl von Elektronikprojekten zur Erstellung von Hinderniserkennung und Entfernungsmessanwendungen sowie verschiedenen anderen Anwendungen eingesetzt. Hier haben wir die einfache Methode zur Entfernungsmessung mit Arduino und Ultraschallsensor vorgestellt und erläutert, wie man den Ultraschallsensor mit Arduino verwendet.

![](./media/image-20250709105712919.png)

#### **(2) Parameter:**

- Stromversorgung: +5V DC

- Ruhestrom: \<2mA

- Betriebsstrom: 15mA

- Effektiver Winkel: \<15°

- Messbereich: 2cm – 400 cm

- Auflösung: 0,3 cm

- Messwinkel: 30 Grad

- Trigger-Eingangsimpulsbreite: 10uS


#### **(3) Das Prinzip des Ultraschallsensors:**

Wie im obigen Bild gezeigt, sieht es aus wie zwei Augen. Eines ist das Senderende, das andere ist das Empfangsende.

Das Ultraschallmodul sendet nach dem Auslösen eines Signals Ultraschallwellen aus. Wenn die Ultraschallwellen auf ein Objekt treffen und reflektiert werden, gibt das Modul ein Echosignal aus, sodass es den Abstand des Objekts anhand der Zeitdifferenz zwischen dem Triggersignal und dem Echosignal bestimmen kann.

Die Zeit t ist die Zeit, die das ausgesendete Signal benötigt, um auf ein Hindernis zu treffen und zurückzukehren. Die Ausbreitungsgeschwindigkeit des Schalls in der Luft beträgt etwa 343m/s, und Entfernung = Geschwindigkeit × Zeit. Da die Ultraschallwelle jedoch ausgesendet wird und zurückkommt, entspricht dies dem 2-fachen der Entfernung. Daher muss durch 2 dividiert werden: die mit **Ultraschall gemessene Entfernung = (Geschwindigkeit × Zeit)/2**

1. Verwendungsmethode und Zeitdiagramm des Ultraschallmoduls:

2. Die Verzögerungszeit des Trig-Pins des SR04 auf mindestens 10μs einstellen, um die Entfernungsmessung auszulösen.

3. Nach dem Auslösen sendet das Modul automatisch acht 40KHz-Ultraschallimpulse aus und erkennt, ob ein Signal zurückkommt. Dieser Schritt wird automatisch vom Modul ausgeführt.

4. Wenn das Signal zurückkommt, gibt der Echo-Pin einen hohen Pegel aus, und die Dauer des hohen Pegels ist die Zeit von der Aussendung der Ultraschallwelle bis zur Rückkehr.

![](media/image-20230426172540424.png)

Schaltplan des Ultraschallsensors:

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4) Anschlussdiagramm:**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span> Die Pins VCC, Trig, Echo und Gnd des Ultraschallsensors sind jeweils mit 5v(V), 12(S), 13(S) und Gnd(G) des Shields verbunden.

#### **(5) Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-Seriellkommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.1
Ultrasonic sensor
http://www.keyestudio.com
*/

int trigPin = 12; // Pin Trig ist an 12 angeschlossen
int echoPin = 13; // Pin Echo ist an 13 angeschlossen
long duration, cm, inches;

void setup() 
{
    // Serielle Schnittstelle starten
    Serial.begin(9600);// Baudrate auf 9600 setzen
    // Ein- und Ausgabe definieren
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
}

void loop() 
{
    // Kurzen niedrigen Impuls vorab geben, um einen sauberen hohen Impuls sicherzustellen
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// Mindestens 10us hohen Pegel als Trigger geben
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // Die Zeit im hohen Pegel entspricht der Zeitdifferenz zwischen Aussendung und Rückkehr des Ultraschalls
    duration = pulseIn(echoPin, HIGH);
    // In Entfernung umrechnen
    cm = (duration / 2) / 29.1; // In Zentimeter umrechnen
    inches = (duration / 2) / 74; // In Zoll umrechnen
    // Serielle Schnittstelle gibt aus
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    delay(50);
}
```

#### **(6) Testergebnisse:**

Laden Sie den Testcode auf das Entwicklungsboard hoch, öffnen Sie den seriellen Monitor und stellen Sie die Baudrate auf 9600 ein. Die gemessene Entfernung wird in cm und Zoll angezeigt. Wenn Sie den Ultraschallsensor mit Ihrer Hand blockieren, wird der angezeigte Entfernungswert kleiner.

![](media/2ff018e5d9d631a32fce99eb9b4778be.png)

#### **(7) Code-Erklärung:**

**int trigPin = 12;** Dieser Pin ist zum Senden von Ultraschallwellen definiert, im Allgemeinen Ausgang.

**int echoPin = 13;** Dies ist als Empfangspin definiert, im Allgemeinen Eingang.

**cm = (duration/2) / 29.1; inches = (duration/2) / 74; durch 0.0135**

Wir können die Entfernung mit folgender Formel berechnen:

Entfernung = (Laufzeit/2) × Schallgeschwindigkeit

Die Schallgeschwindigkeit beträgt: 343m/s = 0,0343 cm/uS = 1/29,1 cm/uS

Oder in Zoll: 13503,9in/s = 0,0135in/uS = 1/74in/uS

Wir müssen die Laufzeit durch 2 dividieren, da wir berücksichtigen müssen, dass die Welle ausgesendet wurde, auf das Objekt traf und dann zum Sensor zurückgekehrt ist.

#### **(8) Erweiterungsübung:**

Wir haben gerade die vom Ultraschall angezeigte Entfernung gemessen. Wie wäre es, eine LED mit der gemessenen Entfernung zu steuern? Probieren wir es aus und schließen wir ein LED-Lichtmodul an den D9-Pin an.

![](media/291ac1db0f38418772d11bb1786b7314.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-Seriellkommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.2
Ultrasonic LED
http://www.keyestudio.com
*/

int trigPin = 12; // Trig ist an 12 angeschlossen
int echoPin = 13; // Echo ist an 13 angeschlossen
int LED = 9;
long duration, cm, inches;

void setup() 
{
    // Serielle Schnittstelle starten
    Serial.begin (9600);// Baudrate auf 9600 setzen
    // Ein- und Ausgabe definieren
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(LED, OUTPUT);
}

void loop() 
{
    // Kurzen niedrigen Impuls vorab geben, um einen sauberen hohen Impuls sicherzustellen
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// Mindestens 10us hohen Pegel als Trigger geben
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // Die Dauer des hohen Pegels ist die Zeit von der Aussendung bis zur Rückkehr der Ultraschallwelle
    duration = pulseIn(echoPin, HIGH);
    // In Entfernung umrechnen
    cm = (duration / 2) / 29.1; // In Zentimeter umrechnen
    inches = (duration / 2) / 74; // In Zoll umrechnen
    // Serielle Schnittstelle gibt aus
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    if (cm >= 2 && cm <= 10) 
    {
    	digitalWrite(LED, HIGH);// LED einschalten
    } 
    else 
    {
    	digitalWrite(LED, LOW); // LED ausschalten
    }
    delay(50);
}
```

Laden Sie den Testcode auf das Entwicklungsboard hoch und blockieren Sie den Ultraschallsensor mit der Hand, dann überprüfen Sie, ob die LED leuchtet.

![](./media/img-20240117090734.png)