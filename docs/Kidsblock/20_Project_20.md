### Projekt 20: Lüfter

#### **(1)Beschreibung：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Dieses Lüftermodul verwendet einen HR1124S Motor-Steuerchip, einen einkanal H-Brücken-Treiber-Chip, der einen PMOS- und NMOS-Leistungstransistor mit niedrigem Leitwiderstand enthält. Der niedrige Leitwiderstand kann den Stromverbrauch verringern und dazu beitragen, dass der Chip länger sicher arbeitet.

Darüber hinaus macht sein niedriger Standby-Strom und niedriger statischer Arbeitsstrom ihn für den Einsatz in Spielzeug geeignet. Wir können die Drehrichtung und Geschwindigkeit des Lüfters steuern, indem wir IN+- und IN--Signale sowie PWM-Signale ausgeben.

#### **(2)Parameter:**

- Betriebsspannung: 5V

- Strom: 200mA

- Maximale Leistung: 2W

- Arbeitstemperatur: -10 °C bis +50 Grad Celsius

- Größe: 47,6mm \* 23,8mm

#### **(3)Anschlussdiagramm:**

Das Lüftermodul benötigt einen hohen Antriebsstrom; daher installieren wir einen Batteriehalter.

![](media/2bd9aa5cc21e274458328958561f1915.png)

Die Pins GND, VCC, IN+ und IN- des Lüftermoduls sind mit den Pins G, V, 12 und 13 des Shields verbunden.

#### **(4)Testcode:**

Sie können auch Blöcke ziehen, um Ihren Code zu bearbeiten, wie unten gezeigt

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/1360090880c1cd9b20671c17604f4108.png)

![](media/4e9354e674060efe6cf540a3e1b87813.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/cbb8f153dd0d114bdd350577af7a1f02.png)

#### **(5)Testergebnisse:**

Code hochladen, Komponenten verdrahten, einschalten und den DIP-Schalter auf ON stellen. Der kleine Lüfter dreht sich 2s lang im Uhrzeigersinn, hält 2s lang an und dreht sich dann 2s lang gegen den Uhrzeigersinn.

![](./media/img-20240117100504.png)

#### **(6)Erweiterungsübung:**

Wir haben das Funktionsprinzip des Flammensensors verstanden. Als nächstes schließen wir einen Flammensensor in die Schaltung an, wie unten gezeigt. Dann steuern wir den Lüfter so, dass er das Feuer mit dem Flammensensor ausbläst.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)


Sie können Blöcke ziehen, um Ihren Code zu bearbeiten, wie unten gezeigt

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/74ddb07daf4063f0640c31f4243a0864.png)


Nach dem Hochladen des Codes schalten Sie den Netzschalter des Motor-Drive-Shields ein. Der Lüfter kann eingeschaltet werden, wenn eine Flamme vom linken Flammensensor des Roboters erkannt wird.

![](./media/img-20240117102303.png)