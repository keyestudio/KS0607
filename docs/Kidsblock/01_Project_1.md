### Projekt 1: LED blinkt

#### (1) Beschreibung：

![](./media/image-20250709122631704.png)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Für Einsteiger und Enthusiasten ist das LED-Blinken ein grundlegendes Programm. LED ist die Abkürzung für Leuchtdioden und besteht aus chemischen Verbindungen wie Ga, As, P, N usw. Die LED kann in verschiedenen Farben blinken, indem die Verzögerungszeit im Testcode geändert wird. Bei der Steuerung wird GND und VCC mit Strom versorgt. Die LED leuchtet, wenn der S-Anschluss auf einem hohen Pegel liegt; andernfalls erlischt sie.

#### **(2) Parameter:**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Steuerschnittstelle: Digitalport
- Betriebsspannung: DC 3,3–5 V
- Pin-Abstand: 2,54 mm
- LED-Anzeigefarbe: Gelb

#### (3) Benötigte Komponenten:

![](./media/image-20250709122437613.png)

#### **(4) 8833 Motor-Treiber-Erweiterungsplatine:**

Die Keyestudio 8833 Motor-Treiber-Erweiterungsplatine ist mit dem Arduino UNO-Entwicklungsboard kompatibel. Stecken Sie sie einfach auf das Entwicklungsboard, wenn Sie sie verwenden.

![](media/d8696e83ade31f2b7c56cc5911eacbd7.GIF)

#### **(5) Anschlussdiagramm:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](./media/image-20250709122655936.png)

<span style="color: rgb(255, 76, 65);">**HINWEIS:**</span> Die LED ist mit dem D9-Port verbunden. Denken Sie daran, Jumper-Kappen auf dem Shield zu installieren.

#### **(6) Testcode:**

Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt.

![](media/cc43ba357acb68a4961adb7e5041b6fe.png)

![](media/26b69cd46ad24e1c900c4fb316430353.png)

![](media/21dc3c24da4271aa7ec2bfdac732eeb3.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/ba4723bab640078eccbe1811da138bc3.png)

#### **(7) Testergebnisse:**

Laden Sie das Programm hoch, die LED blinkt im Abstand von 1 s.

#### **(8) Erweiterungsübung:**

Wir wissen nun, wie man die LED steuert. Dann wollen wir die Blinkfrequenz der LED ändern.

Wir können die Frequenz der LED ändern, ohne den Pin der LED zu wechseln. Lassen Sie uns den Code anpassen.

Sie können auch Blöcke per Drag-and-Drop bearbeiten, wie unten gezeigt.

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen ebenfalls serielle Kommunikation verwendet und es zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/58c76be4c719a885afb500e8f3b80b85.png)

Das Testergebnis zeigt, dass die LED schneller blinkt. Daher können wir schlussfolgern, dass Pins und Zeitverzögerung die Blinkfrequenz beeinflussen.