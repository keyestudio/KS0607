### Projekt 18: Ultraschall-Panzerroboter mit mehreren Funktionen

#### **(1)Beschreibung:**

Der Smartcar hat in jedem vorherigen Projekt eine einzelne Funktion ausgeführt.

Kann er mehrere Funktionen gleichzeitig anzeigen? Ja, das kann er.

In diesem abschließenden Großprojekt beabsichtigen wir, einen vollständigen Code zu verwenden, um den Smartcar zu steuern und alle in den vorherigen Projekten erwähnten Funktionen zu demonstrieren. Wir verwenden die Tasten der Bluetooth-APP, um automatisch zwischen verschiedenen Funktionen zu wechseln, was sehr einfach und bequem ist.

#### **(2)Ablaufdiagramm:**

![](media/wps122.png)

#### **(3)Anschlussdiagramm:**

![](media/e7ac834ba04aa2e8862995d2d33ce935.png)

1\. GND, VCC, SDA und SCL der 8x16-Platine sind mit G (GND), + (VCC), A4 und A5 der Erweiterungsplatine verbunden.

2\. VCC, Trig, Echo und Gnd des Ultraschallsensors sind mit 5V (V), 12 (S), 13 (S) und Gnd (G) verbunden.

3\. Das braune Kabel, das rote Kabel und das orangefarbene Kabel des Servos sind mit Gnd (G), 5v (V) und D10 verbunden.

4\. RXD, TXD, GND und VCC des BT-Moduls sind mit TX, RX, G (GND) und 5V (VCC) verbunden. STATE und BRK müssen nicht angeschlossen werden.

5\. Die Pins „G", „V" und S des linken Fotowiderstandsmoduls sind jeweils mit G (GND), V (VCC) und A1 verbunden; das rechte Fotowiderstandsmodul ist mit G (GND), V (VCC) und A2 verbunden.

6\. Die äußeren Ports des Spurverfolgungssensors sind 11, 7 und 8.

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-seriellen Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Sie können das Fahrzeug über die App nicht beschleunigen.

![](media/e3c4c6cf504b1b9ea6fbae63f5fd9077.png)

#### **(5)Testergebnis:**

Vor dem Hochladen des Programmcodes muss das Bluetooth-Modul entfernt werden, andernfalls schlägt der Code-Upload fehl.

Nachdem der Code erfolgreich hochgeladen wurde, aktivieren Sie die Standortdienste auf Ihrem Gerät und verbinden Sie dann das Bluetooth-Modul.

Sobald das Bluetooth-Modul eingesteckt und eingeschaltet ist und die mobile APP erfolgreich mit dem Bluetooth verbunden ist, können wir die mobile APP verwenden, um den Panzerroboter zu steuern.