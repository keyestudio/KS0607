### Projekt 20: Flammensensor

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Beschreibung：**

Der Flammensensor verwendet eine IR-Empfangsdiode, um Flammen zu erkennen. Er wandelt die Helligkeit der Flamme in High- und Low-Pegel-Signale um und gibt diese an den Zentralprozessor zur entsprechenden Programmverarbeitung weiter. Der Spannungswert des Analogports variiert je nachdem, ob eine Flamme in der Nähe ist oder überhaupt keine Flamme vorhanden ist.

Wenn keine Flamme vorhanden ist, liest der Analogport etwa 0,3V; wenn eine Flamme vorhanden ist, liest der Analogport etwa 1,0V. Je näher die Flamme ist, desto höher ist der Spannungswert. Er kann verwendet werden, um eine Feuerquelle zu erkennen oder einen intelligenten Roboter zu bauen.

Beachten Sie, dass die Sonde des Flammensensors nur Temperaturen zwischen -25℃ und 85℃ standhalten kann.

Stellen Sie während des Betriebs sicher, dass der Flammensensor in einem sicheren Abstand zum Feuer gehalten wird, um Schäden daran zu vermeiden.

#### **(2)Parameter：**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Betriebsspannung: 3,3V-5V (DC)

- Strom: 100mA

- Maximale Leistung: 0,5W

- Betriebstemperatur: -10°C bis +50 Grad Celsius

- Sensorgröße: 31,6mm x 23,7mm

- Schnittstelle: 4pin zu 3PIN-Schnittstelle

- Ausgangssignal: Analogsignale A0, A1



#### **(3)Anschlussdiagramm:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

Flammensensoren sind an A1 und A2 angeschlossen.

Wenn wir Ultraschallsensoren und Fotowiderstände entfernen und dann Flammensensoren und Lüftermodule hinzufügen, entsteht der Feuerlöschroboter.

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
1）Dieses Experiment erfordert den Einsatz einer Feuerquelle. Bitte halten Sie sie von brennbaren Gegenständen fern, um Brände zu vermeiden. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie nicht sicher sein können, dass Sie sicher sind, verzichten Sie bitte auf das Experiment.
2）**Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.**


#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es möglicherweise zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, die dazu führen können, dass der Upload fehlschlägt.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.1

flame sensor

http://www.keyestudio.com

*/

int flame = A1; // Definiere den Flammen-Pin als analogen Pin A1
int val = 0; // Definiere digitale Variablen

void setup() 
{
	pinMode(flame, INPUT); // Definiere den Buzzer als Eingabequelle
    Serial.begin(9600); // Setze die Baudrate auf 9600
}

void loop() 
{
	val = analogRead(flame); // Lese den Analogwert des Flammensensors
	Serial.println(val); // Analogwert ausgeben und drucken
	delay(100); // Verzögerung von 100ms
}
```

#### **(5)Testergebnis：**

Verbinden Sie die Komponenten, laden Sie den Code hoch, öffnen Sie den seriellen Monitor und stellen Sie die Baudrate auf 9600.

Sie können den Simulationswert des Flammensensors anzeigen.

Je näher die Flamme ist, desto kleiner ist der Simulationswert.

Passen Sie das Potentiometer am Modul an, um D1 am kritischen Punkt zu halten. Wenn der Sensor keine Flamme erkennt, bleibt D1 aus, aber wenn der Sensor eine Flamme erkennt, leuchtet D1 auf.

![](./media/img-20240117085629.png)

![](media/05db06b3e205dfca63c2ba3aa7ff528e.png)

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
Bitte halten Sie ihn von brennbaren Gegenständen fern, um Brände zu vermeiden. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie nicht sicher sein können, dass Sie sicher sind, verzichten Sie bitte auf das Experiment. Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.

#### **(6)Erweiterungsübung:**

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
1）Dieses Experiment erfordert den Einsatz einer Feuerquelle. Bitte halten Sie sie von brennbaren Gegenständen fern, um Brände zu vermeiden. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie nicht sicher sein können, dass Sie sicher sind, verzichten Sie bitte auf das Experiment.
2）Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.

Als nächstes schließen Sie eine LED an Pin 9 an und wir können sie mit einem Flammensensor steuern, wie unten gezeigt:

![](media/814c315d3bb44278b476a754d3681227.png)

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es möglicherweise zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, die dazu führen können, dass der Upload fehlschlägt.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.2

flame sensor

http://www.keyestudio.com

*/

int flame = A1; // Definiere den Flammen-Pin als analogen Pin A1
int LED = 9; // Definiere die LED als digitalen Port 9
int val = 0; // Definiere digitale Variablen

void setup() 
{
    pinMode(flame, INPUT); // Definiere die Flamme als Eingabequelle
    pinMode(LED, OUTPUT); // Setze LED auf Ausgabemodus
    Serial.begin(9600); // Setze die Baudrate auf 9600
}

void loop() 
{
    val = analogRead(flame); // Lese den Analogwert des Flammensensors
    Serial.println(val); // Analogwert ausgeben und drucken
    if (val < 300)  // Wenn der Analogwert kleiner als 300 ist, leuchtet die LED
    {
    	digitalWrite(LED, HIGH); // LED leuchtet
    } 
    else 
    {
    	digitalWrite(LED, LOW); // LED ist aus
    }
    delay(50); // Verzögerung von 50ms
}
```

#### **(8)Testergebnisse：**

Sie können das Feuerzeug nahe am linken Flammensensor verwenden. Wenn der Flammensensor eine Flamme erkennt, leuchtet das LED-Modul als Alarm auf.

![](./media/img-20240117085131.png)

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span>
Bitte halten Sie ihn von brennbaren Gegenständen fern, um Brände zu vermeiden. Kinder sollten das Experiment unter Aufsicht von Erwachsenen durchführen. Wenn Sie nicht sicher sein können, dass Sie sicher sind, verzichten Sie bitte auf das Experiment. Der Flammensensor ist nicht feuerfest, bitte verbrennen Sie ihn nicht direkt mit einer Flamme.