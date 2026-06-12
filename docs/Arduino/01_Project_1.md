### Projekt 1: LED blinkt

#### **(1)Beschreibung:**

![](media/64b0b431d58473408ac46b39d2dc2ad0.jpeg)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Für Einsteiger und Enthusiasten ist das LED-Blinken ein grundlegendes Programm. LED, die Abkürzung für Leuchtdioden, besteht aus chemischen Verbindungen wie Ga, As, P, N und so weiter. Die LED kann in verschiedenen Farben aufleuchten, indem die Verzögerungszeit im Testcode geändert wird. Bei der Steuerung werden GND und VCC mit Strom versorgt. Die LED leuchtet, wenn der S-Anschluss auf hohem Pegel ist; andernfalls geht sie aus.

#### **(2)Parameter:**

![](./media/image-20250709104606457.png)

- Steuerungsschnittstelle: digitaler Port
- Betriebsspannung: DC 3,3–5 V
- Pin-Abstand: 2,54 mm
- LED-Anzeigefarbe: gelb

#### **(3)Benötigte Komponenten:**

![](media/img-20240117081416.png)


#### **(4)8833 Motor-Treiber-Erweiterungsplatine:**

Die Keyestudio 8833 Motor-Treiber-Erweiterungsplatine ist kompatibel mit dem Arduino UNO Entwicklungsboard. Beim Verwenden einfach auf das Entwicklungsboard aufstecken.

![](./media/image-20250709104749140.png)

#### **(5)Anschlussdiagramm:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](media/d68e6475a7c9ed55bb057b75d1b11689.png)

<span style="color: rgb(255, 76, 65);">**HINWEIS:**</span> Die LED ist mit dem D9-Port verbunden. Denken Sie daran, Jumper-Kappen auf dem Shield zu installieren.

#### **(6)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, die das Hochladen fehlschlagen lassen.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.1

Blink

http://www.keyestudio.com

*/

int LED = 9; // Definiere den Pin der LED, der mit dem digitalen Port 9 verbunden ist

void setup()
{
	pinMode(LED, OUTPUT); // Initialisiere den LED-Pin als Ausgang
}

void loop() // Endlosschleife
{
	digitalWrite(LED, HIGH); // Hohen Pegel ausgeben und LED einschalten
	delay(1000); // 1s warten
	digitalWrite(LED, LOW); // Niedrigen Pegel ausgeben und LED ausschalten
	delay(1000); // 1s warten
}
```

#### **(7)Testergebnisse:**

Nach dem Hochladen des Programms blinkt die LED im Abstand von 1 s.

#### **(8)Code-Erklärung:**

**pinMode(LED，OUTPUT) -** Diese Funktion kann angeben, ob der Pin INPUT oder OUTPUT ist

**digitalWrite(LED，HIGH) -** Wenn der Pin OUTPUT ist, kann er auf HIGH (5 V ausgeben) oder LOW (0 V ausgeben) gesetzt werden

#### **(9)Erweiterungsübung:**

Wir haben die LED erfolgreich zum Blinken gebracht. Als Nächstes beobachten wir, was mit der LED passiert, wenn wir Pins und Verzögerungszeit ändern.

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, die das Hochladen fehlschlagen lassen.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.2

Blink

http://www.keyestudio.com

*/

int LED = 9; // Definiere den Pin der LED als 9

void setup()
{
	pinMode(LED, OUTPUT); // Setze den Pin der LED auf OUTPUT
}

void loop() // Endlosschleife
{
    digitalWrite(LED, HIGH); // Hohe Pegel ausgeben, LED einschalten
	delay(100); // 0,1s warten
	digitalWrite(LED, LOW); // LED gibt niedrige Pegel aus, LED ausschalten
	delay(100); // 0,1s warten

}
```

Das Testergebnis zeigt, dass die LED schneller blinkt. Daher können wir schlussfolgern, dass Pins und Verzögerungszeit die Blinkfrequenz beeinflussen.