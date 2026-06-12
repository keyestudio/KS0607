### Projekt 4: Linienverfolgungssensor

#### **(1)Beschreibung:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

Der Linienverfolgungssensor ist eigentlich ein Infrarotsensor. Das hier verwendete Bauteil ist die TCRT5000 Infrarotröhre.

Sein Funktionsprinzip beruht darauf, die unterschiedliche Reflektivität von Infrarotlicht auf verschiedene Farben zu nutzen und dann die Stärke des reflektierten Signals in ein Stromsignal umzuwandeln.

Während des Erkennungsvorgangs ist Schwarz bei HIGH-Pegel aktiv, während Weiß bei LOW-Pegel aktiv ist. Die Erkennungshöhe beträgt 0-3 cm.

Das Keyestudio 3-Kanal-Linienverfolgungsmodul integriert 3 TCRT5000 Infrarotröhren auf einer einzelnen Platine, was die Verkabelung und Steuerung komfortabler macht.

Wenn der Linienverfolgungssensor nicht wie erwartet funktioniert, müssen Sie einen Schraubenzieher verwenden, um seinen Potentiometer einzustellen und ihn empfindlicher zu machen. Wenn Ihr Finger nahe am Sensor ist, leuchtet die bordeigene LED-Leuchte auf, und wenn Ihr Finger sich entfernt, erlischt die bordeigene LED-Leuchte. In diesem Fall ist seine Empfindlichkeit relativ gut.

![](./media/img-20240117090858.png)

#### **(2)Parameter:**

- Betriebsspannung: 3,3-5V (DC)

- Schnittstelle: 5PIN

- Ausgangssignal: Digitales Signal

- Erkennungshöhe: 0-3 cm


Besonderer Hinweis: Drehen Sie vor dem Testen das Potentiometer am Sensor, um die Erkennungsempfindlichkeit einzustellen. Wenn die LED an der Schwelle zwischen EIN und AUS eingestellt wird, ist die Empfindlichkeit am besten.

<span style="color: rgb(255, 76, 65);">Hinweis:</span> Der Linienverfolgungssensor ist unter dem Boden des Roboters installiert.

#### **(3)Anschlussdiagramm:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.1

Line Track sensor

http://www.keyestudio.com

*/

// Verkabelung der Linienverfolgungssensoren

#define L_pin 11 // links

#define M_pin 7 // mitte

#define R_pin 8 // rechts

void setup()
{
    Serial.begin(9600); // Baudrate auf 9600 setzen
    pinMode(L_pin, INPUT); // Alle Pins der Linienverfolgungssensoren auf Eingabemodus setzen
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); // Den Wert des linken Sensors lesen
    int M_val = digitalRead(M_pin); // Den Wert des mittleren Sensors lesen
    int R_val = digitalRead(R_pin); // Den Wert des rechten Sensors lesen

    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); // Verzögerung von 100ms
}
```

#### **(5)Testergebnisse:**

Laden Sie den Code auf das Entwicklungsboard hoch und öffnen Sie den seriellen Monitor, um die Linienverfolgungssensoren zu überprüfen. Der angezeigte Wert ist 1 (HIGH-Pegel), wenn keine Signale empfangen werden. Der Wert wechselt zu 0, wenn der Sensor mit Papier abgedeckt wird.

![](./media/img-20240117090920.png)


![](media/b9319753c148f66aabc9bf648ed93da1.png)

#### **(6)Code-Erklärung:**

**Serial.begin(9600)** - Seriellen Port initialisieren, Baudrate auf 9600 setzen

**pinMode-** Den Pin als Eingangs- oder Ausgangsmodus definieren

**digitalRead-** Den Zustand des Pins lesen, der in der Regel HIGH- und LOW-Pegel ist

#### **(7)Erweiterungsübung:**

Nachdem Sie das Funktionsprinzip kennen, können Sie eine LED an D9 anschließen, um die LED über den Linienverfolgungssensor zu steuern.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.2

Line Track sensor

http://www.keyestudio.com

*/

// LED-Pin

#define LED 9
// Verkabelung der Linienverfolgungssensoren
#define L_pin 11 // links
#define M_pin 7 // mitte
#define R_pin 8 // rechts

void setup()
{
    Serial.begin(9600); // Baudrate auf 9600 setzen
    pinMode(LED, OUTPUT); // LED auf Ausgabemodus setzen
    pinMode(L_pin, INPUT); // Alle Pins der Linienverfolgungssensoren auf Eingabemodus setzen
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); // Den Wert des linken Sensors lesen
    int M_val = digitalRead(M_pin); // Den Wert des mittleren Sensors lesen
    int R_val = digitalRead(R_pin); // Den Wert des rechten Sensors lesen
    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); // Verzögerung

    if (L_val == 0 || M_val == 0 || R_val == 0) 
    {
    	digitalWrite(LED, HIGH);
    }
    else 
    {
    	digitalWrite(LED, LOW);
    }
}
```