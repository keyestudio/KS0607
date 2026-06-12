### Projekt 6: Ultraschallsensor

#### **(1)Beschreibung:**

![](media/0180b169a1c3b228394b43df704fac32.png)

Der HC-SR04 Ultraschallsensor verwendet Sonar, um die Entfernung zu einem Objekt zu bestimmen, ähnlich wie Fledermäuse es tun. Er bietet hervorragende berührungslose Entfernungsmessung mit hoher Genauigkeit und stabilen Messwerten in einem einfach zu verwendenden Gehäuse. Er wird komplett mit Ultraschall-Sende- und Empfangsmodulen geliefert.

Der HC-SR04 bzw. der Ultraschallsensor wird in einer Vielzahl von Elektronikprojekten zur Hinderniserkennung und Entfernungsmessung sowie für verschiedene andere Anwendungen eingesetzt. Hier haben wir die einfache Methode zur Entfernungsmessung mit Arduino und Ultraschallsensor vorgestellt und erklärt, wie man den Ultraschallsensor mit Arduino verwendet.

![](./media/image-20250709133626194.png)

#### **(2)Parameter:**

- Stromversorgung: +5V DC

- Ruhestrom: \<2mA

- Betriebsstrom: 15mA

- Effektiver Winkel: \<15°

- Messbereich: 2cm – 400 cm

- Auflösung: 0,3 cm

- Messwinkel: 30 Grad

- Triggereingangsimpulsbreite: 10uS

#### **(3)Das Funktionsprinzip des Ultraschallsensors:**

Wie im obigen Bild dargestellt, ähnelt er zwei Augen. Eines ist das Senderende, das andere ist das Empfangsende.

Das Ultraschallmodul sendet die Ultraschallwellen aus, nachdem ein Signal ausgelöst wurde. Wenn die Ultraschallwellen auf ein Objekt treffen und zurückreflektiert werden, gibt das Modul ein Echosignal aus, sodass die Entfernung des Objekts anhand der Zeitdifferenz zwischen dem Triggersignal und dem Echosignal bestimmt werden kann.

Hierbei ist t die Zeit von dem Moment, in dem das gesendete Signal auf das Hindernis trifft, bis zu seiner Rückkehr. Die Ausbreitungsgeschwindigkeit des Schalls in der Luft beträgt etwa 343 m/s, und Entfernung = Geschwindigkeit × Zeit. Da die Ultraschallwelle jedoch zum Hindernis und zurück läuft, repräsentiert die Zeit die doppelte Entfernung. Daher muss durch 2 geteilt werden. Die vom **Ultraschall gemessene Entfernung = (Geschwindigkeit × Zeit) / 2**.

1. Verwendungsmethode und Zeitdiagramm des Ultraschallmoduls:

2. Die Verzögerungszeit des Trig-Pins des SR04 auf mindestens 10 μs einstellen, um die Entfernungsmessung auszulösen.

3. Nach dem Auslösen sendet das Modul automatisch acht 40-kHz-Ultraschallimpulse und erkennt, ob ein Signal zurückkommt. Dieser Schritt wird automatisch vom Modul durchgeführt.

4. Wenn das Signal zurückkommt, gibt der Echo-Pin einen hohen Pegel aus, und die Dauer des hohen Pegels ist die Zeit von der Übertragung der Ultraschallwelle bis zur Rückkehr.

![](media/image-20230525110337646.png)

Schaltplan des Ultraschallsensors:

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4)Anschlussdiagramm:**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Verdrahtungshinweis:</span> Der VCC-Pin des Ultraschallsensor-Moduls ist mit dem 5V(V) der Keyestudio 8833 Motor-Ansteuerungserweiterungsplatine verbunden, der Trig-Pin ist mit dem digitalen Eingang D12 verbunden, der Echo-Pin ist mit dem digitalen Eingang D13 verbunden, und der Gnd-Pin ist mit Gnd(G) verbunden;

#### **(5)Testcode:**

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten dargestellt.

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/128e0b4ee7d3448410d72312175bc6da.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/a6df8829b69f7faed26a73d01da8d50d.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/eca0805413af12957d319c706d3e7cdb.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/569aff5ff2cbd2f3605f217ebb5ed50b.png)

#### **(6)Testergebnisse:**

Laden Sie den Testcode auf das Entwicklungsboard hoch, öffnen Sie den seriellen Monitor und stellen Sie die Baudrate auf 9600 ein. Die gemessene Entfernung wird in cm und Zoll angezeigt. Wenn Sie den Ultraschallsensor mit Ihrer Hand behindern, wird der angezeigte Entfernungswert kleiner.

![](media/4f77acbf5b226e20e3cdd70c0f90602e.png)

#### **(7)Erweiterungsübung:**

Wir haben gerade die vom Ultraschall angezeigte Entfernung gemessen. Wie wäre es damit, die LED mit der gemessenen Entfernung zu steuern? Versuchen wir es und schließen wir ein LED-Lichtmodul an den D9-Pin an.

![](media/291ac1db0f38418772d11bb1786b7314.png)


Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten dargestellt.

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/49d5523ae565e1d4dfc3504d1e1748d4.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/8d5fc923f5ded5305f36b1379c1ba38e.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/a6205e42e005084c33c247fe564bdcad.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/065eac0ad9cfa8f07aeb5e648698bdb5.png)

Laden Sie den Testcode auf das Entwicklungsboard hoch, bewegen Sie Ihre Hand in die Nähe des Ultraschallsensors und überprüfen Sie, ob die LED aufleuchtet.

![](./media/img-20240117092413.png)