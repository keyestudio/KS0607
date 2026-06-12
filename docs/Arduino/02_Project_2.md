### Projekt 2: LED-Helligkeit einstellen

#### **(1) Beschreibung:**

In der vorherigen Lektion haben wir die LED ein- und ausgeschaltet und zum Blinken gebracht.

In diesem Projekt steuern wir die Helligkeit der LED über PWM, um einen Atemeffekt zu simulieren. Ebenso können Sie die Schrittlänge und die Verzögerungszeit im Code ändern, um verschiedene Atemeffekte darzustellen.

PWM ist eine Methode zur Steuerung des analogen Ausgangs über digitale Mittel. Die digitale Steuerung wird verwendet, um Rechteckwellen mit unterschiedlichen Tastverhältnissen (ein Signal, das ständig zwischen hohen und niedrigen Pegeln wechselt) zu erzeugen, um den analogen Ausgang zu steuern.

Im Allgemeinen betragen die Eingangsspannungen der Ports 0V und 5V. Was ist, wenn 3V benötigt werden? Oder ein Wechsel zwischen 1V, 3V und 3,5V? Wir können nicht ständig Widerstände wechseln. Aus diesem Grund greifen wir auf PWM zurück.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Bei den digitalen Port-Spannungsausgaben des Arduino gibt es nur LOW- und HIGH-Pegel, die den Spannungsausgaben von 0V bzw. 5V entsprechen. Sie können LOW als „0" und HIGH als „1" definieren und den Arduino innerhalb von 1 Sekunde fünfhundert „0" oder „1" ausgeben lassen. Wenn fünfhundert „1" ausgegeben werden, entspricht das 5V; wenn alles „0" ist, entspricht das 0V; wenn 250 01-Muster ausgegeben werden, entspricht das 2,5V.

Dieser Prozess lässt sich mit dem Abspielen eines Films vergleichen. Die Filme, die wir sehen, sind nicht vollständig kontinuierlich. Tatsächlich werden 25 Bilder pro Sekunde erzeugt, was vom menschlichen Auge nicht wahrgenommen werden kann. Daher halten wir es für einen kontinuierlichen Prozess. PWM funktioniert auf die gleiche Weise. Um verschiedene Spannungen auszugeben, müssen wir das Verhältnis von 0 und 1 steuern. Je mehr „0" oder „1" pro Zeiteinheit ausgegeben werden, desto genauer ist die Steuerung.

#### **(2) Parameter:**

![](./media/image-20250709104949184.png)

Steuerungsschnittstelle: Digitaler Port 3

Betriebsspannung: DC 3,3–5V

Pin-Abstand: 2,54mm

LED-Anzeigefarbe: Gelb

#### **(3) Anschlussdiagramm:**

Die PWM-Pins des Arduino sind mit den Pins 3, 5, 6, 9, 10 und 11 verbunden. Pin 9 bleibt unverändert.

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4) Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.1

pwm

http://www.keyestudio.com

*/

int LED = 9; // Den Pin der LED als 9 definieren

void setup () 
{
	pinMode(LED, OUTPUT); // Den Pin der LED als OUTPUT setzen
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED AN
		delay(5); // Verzögerung von 5ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // LED wird dunkler
		delay(5); // Verzögerung von 5ms
	}
}
```

#### **(5) Testergebnisse:**

Nachdem der Testcode erfolgreich hochgeladen wurde, ändert sich die LED allmählich von hell nach dunkel, wie der Atem eines Menschen, anstatt sofort ein- und auszuschalten.

#### **(6) Code-Erklärung:**

Um bestimmte Anweisungen zu wiederholen, können wir die FOR-Anweisung verwenden. Das Format der FOR-Anweisung ist unten dargestellt:

![图1(1)](media/65da124bdd0ea488291c71c6b879fe95.jpeg)

FOR-Schleifenreihenfolge:

Runde 1: 1 → 2 → 3 → 4

Runde 2: 2 → 3 → 4

…

Bis Bedingung 2 nicht mehr erfüllt ist, ist die „for"-Schleife beendet.

Nachdem Sie diese Reihenfolge kennen, kehren wir zum Code zurück:

**for (int value = 0; value \< 255; value=value+1){**

**...}**

**for (int value = 255; value \>0; value=value-1){**

**...}**

Die beiden „for"-Anweisungen lassen den Wert von 0 auf 255 ansteigen, dann von 255 auf 0 sinken, dann wieder auf 255 ansteigen, ... unendliche Schleife.

Im Folgenden gibt es eine neue Funktion ----- analogWrite()

Wir wissen, dass der digitale Port nur zwei Zustände hat: 0 und 1. Wie sendet man also einen analogen Wert an einen digitalen Ausgang? Dafür wird diese Funktion benötigt. Schauen wir uns die Arduino-Platine an und finden Sie 6 mit „\~" markierte Pins, die PWM-Signale ausgeben können.

Funktionsformat wie folgt:

**analogWrite(pin,value)**

analogWrite() wird verwendet, um einen analogen Wert von 0\~255 für den PWM-Port zu schreiben, sodass der Wert im Bereich von 0\~255 liegt. Beachten Sie, dass Sie nur die digitalen Pins mit PWM-Funktion beschreiben können, wie Pin 3, 5, 6, 9, 10, 11.

PWM ist eine Technologie, um analoge Größen durch digitale Methoden zu erhalten. Die digitale Steuerung bildet eine Rechteckwelle, und das Rechteckwellensignal hat nur zwei Zustände: Ein und Aus (d. h. hohe oder niedrige Pegel). Durch die Steuerung des Verhältnisses der Ein- und Ausschaltdauer kann eine Spannung von 0 bis 5V simuliert werden. Die Einschaltzeit (akademisch als hoher Pegel bezeichnet) wird als Impulsbreite bezeichnet, daher wird PWM auch als Pulsweitenmodulation bezeichnet.

Anhand der folgenden fünf Rechteckwellen wollen wir mehr über PWM erfahren.

![](media/553f3d1b6ca04e1aa0479841dd075fa2.png)

In der obigen Abbildung stellt die grüne Linie eine Periode dar, und der Wert von analogWrite() entspricht einem Prozentsatz, der auch als Tastverhältnis bezeichnet wird.

Das Tastverhältnis gibt an, dass die Dauer des hohen Pegels durch die Dauer des niedrigen Pegels in einem Zyklus geteilt wird. Von oben nach unten beträgt das Tastverhältnis der ersten Rechteckwelle 0% und der entsprechende Wert ist 0. Die LED-Helligkeit ist am niedrigsten, d. h. sie ist ausgeschaltet. Je länger der hohe Pegel andauert, desto heller leuchtet die LED. Daher beträgt das letzte Tastverhältnis 100%, was 255 entspricht, und die LED ist am hellsten. Und 25% bedeutet dunkler.

PWM wird hauptsächlich zur Einstellung der Helligkeit von LEDs oder der Drehzahl von Motoren verwendet.

Es spielt eine entscheidende Rolle bei der Steuerung intelligenter Roboterfahrzeuge. Ich glaube, Sie können es kaum erwarten, das nächste Projekt zu lernen.

#### **(7) Erweiterungsübung:**

Ändern wir den Verzögerungswert und lassen den Pin unverändert, dann beobachten wir, wie sich die LED verändert.

**Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.2

pwm-slow

http://www.keyestudio.com

*/

int LED = 9; // Den Pin der LED als 9 definieren

void setup() 
{
	pinMode(LED, OUTPUT); // Den Pin der LED als OUTPUT setzen
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED AN
		delay(30); // Verzögerung von 30ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // LED wird dunkler
		delay (30); // Verzögerung von 30ms
	}
}
```

Laden Sie den Code auf die Entwicklungsplatine hoch; die LED blinkt langsamer.