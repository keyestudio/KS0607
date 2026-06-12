### Projekt 13: Panzer – Bewegung im begrenzten Raum


#### **(1) Beschreibung:**

Die Ultraschall-Verfolgungsfunktion und die Hindernisumfahrungsfunktion des Smart Cars wurden in vorherigen Projekten vorgestellt. Hier beabsichtigen wir, das Wissen aus den vorherigen Kursen zu kombinieren, um das Smart Car auf einen bestimmten Bereich zu beschränken. Im Experiment verwenden wir den Linienverfolgungssensor, um zu erkennen, ob sich eine schwarze Linie um das Smart Car befindet, und steuern dann die Drehung der beiden Motoren entsprechend der Erkennungsergebnisse, um das Smart Car innerhalb eines mit einer schwarzen Linie gezeichneten Kreises zu halten.

Die spezifische Logik des Smart Cars ist in der folgenden Tabelle dargestellt:

![](media/image-20230525114604923.png)

|                         Bedingung                         |                         Bewegung                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Wenn einer der drei Linienverfolgungssensoren schwarze Linien erkennt | Zurückfahren (PWM auf 150 setzen), dann links drehen (PWM auf 150 setzen) |
|             Keiner von ihnen erkennt schwarze Linien              |               Vorwärts fahren (PWM auf 100 setzen)                |

#### **(2) Flussdiagramm**

![](media/b3c30f92cb78d4c2a4a8bd746aef24e1.png)

#### **(3) Anschlussdiagramm:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4) Testcode:**

Sie können auch Blöcke per Drag-and-Drop verschieben, um Ihren Code zu bearbeiten, wie unten gezeigt

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/e48288f5b46e3e1c78489cb9d9b86333.png)

（3）![](media/801d176b32bc87904b8545ecf80874fc.png)

（4）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/b919eb2b47ee87ae36e21099e754e8a1.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass das Hochladen fehlschlägt.)

![](media/e656126c11bb8ebe7b6b0df8f22e7a79.png)

#### **(5) Testergebnisse:**

Nachdem der Testcode erfolgreich hochgeladen und das Gerät eingeschaltet wurde, bewegt sich das Smart Car innerhalb eines mit einer schwarzen Linie gezeichneten Kreises.

![](./media/img-20240117094034.png)