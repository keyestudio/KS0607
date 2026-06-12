### Projekt 4: Linienverfolgungssensor

#### **(1) Beschreibung:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

Der Linienverfolgungssensor ist eigentlich ein Infrarotsensor. Das hier verwendete Bauteil ist die TCRT5000 Infrarotröhre.

Sein Funktionsprinzip beruht darauf, dass Infrarotlicht unterschiedlich stark von verschiedenen Farben reflektiert wird, und das reflektierte Signal wird in ein Stromsignal umgewandelt.

Während des Erkennungsvorgangs ist Schwarz bei HIGH-Pegel aktiv, während Weiß bei LOW-Pegel aktiv ist. Die Erkennungshöhe beträgt 0–3 cm.

Das Keyestudio 3-Kanal-Linienverfolgungsmodul hat 3 TCRT5000 Infrarotröhren auf einer einzigen Platine integriert, was die Verkabelung und Steuerung komfortabler macht.

Wenn der Linienverfolgungssensor nicht wie erwartet funktioniert, müssen Sie einen Schraubenzieher verwenden, um das Potentiometer anzupassen und ihn empfindlicher zu machen. Wenn Ihr Finger sich dem Sensor nähert, leuchtet die bordeigene LED auf, und wenn Ihr Finger sich entfernt, erlischt die bordeigene LED. Zu diesem Zeitpunkt ist die Empfindlichkeit relativ gut.

![](./media/img-20240117091947.png)

#### **(2) Parameter:**

- Betriebsspannung: 3,3–5 V (DC)
- Schnittstelle: 5PIN
- Ausgangssignal: Digitales Signal
- Erkennungshöhe: 0–3 cm

Besonderer Hinweis: Drehen Sie vor dem Test das Potentiometer am Sensor, um die Erkennungsempfindlichkeit einzustellen. Wenn die LED an der Schaltschwelle zwischen EIN und AUS eingestellt wird, ist die Empfindlichkeit am besten.

<span style="color: rgb(255, 76, 65);">Hinweis:</span> Der Linienverfolgungssensor ist unter dem Boden des Roboters montiert.

#### **(3) Anschlussdiagramm:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4) Testcode:**

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/700cb0ecc14cbccd6e367c5098360f08.png)

![](media/271423c55b5f147796beb344eed7e9cf.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/5298cdfb6fd7c71df155c969c80450cd.png)

#### **(5) Testergebnisse:**

Laden Sie den Code auf das Entwicklungsboard hoch, öffnen Sie den seriellen Monitor auf 9600 und überprüfen Sie die Linienverfolgungssensoren. Der angezeigte Wert ist 1 (HIGH-Pegel), wenn keine Signale empfangen werden. Der Wert wechselt zu 0, wenn der Sensor mit Papier abgedeckt wird.

![](media/5630032421adf9446d51b770f0e7f8af.png)

#### **(6) Erweiterungsübung:**

Wir können eine LED mit diesem Sensor steuern. Die LED ist mit D9 verbunden. Wenn wir ihn abdecken, leuchtet die LED auf.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/574854f4d96c40a85e1db549d85f14f4.png)

![](media/9077c0d059f7a4d3277f10ccb4e962fb.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

![](media/80e9c514357c63f4791c72220829b673.png)

![](media/b10e1897e99af2c1ade6c09da6c30dba.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/b5a4b5a04cdee9f79d6e18a5c48cbe48.png)

Wenn sich ein Objekt (wie Papier oder ein Finger) dem Linienverfolgungssensor nähert, erkennt der Sensor das von ihm selbst ausgesendete Rücksignal und das LED-Modul leuchtet auf. Wenn der Sensor kein Rücksignal erkennt, erlischt das LED-Modul.

![](./media/img-20240117092116.png)