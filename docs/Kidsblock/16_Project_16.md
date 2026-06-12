### Projekt 16: Bluetooth-Fernsteuerung

![](./media/image-20250709134858245.png)

#### **(1)Beschreibung:**

In den letzten Jahrzehnten hat sich Bluetooth zum beliebtesten drahtlosen Kommunikationsmodul entwickelt, da es einfach zu bedienen ist und in den meisten batteriebetriebenen Geräten weit verbreitet eingesetzt wird.

Um sich an die Zeit, die Realität und die Bedürfnisse der Kunden anzupassen, wurde Bluetooth mehrfach aktualisiert. In den letzten Jahren hat es viele Veränderungen hinsichtlich Datenübertragungsrate, Stromverbrauch von Wearables und IoT-Geräten sowie Sicherheitssystemen und anderem erfahren. Hier planen wir, das DX-BT24 mit dem Arduino-Board kennenzulernen.

#### **(2)Parameter:**

- Bluetooth-Protokoll: Bluetooth Specification V5.1 BLE
- Betriebsreichweite: In einer offenen Umgebung bis zu 40 m Ultralangstrecke
- Betriebsfrequenz für die Kommunikation: 2,4 GHz ISM-Band
- Kommunikationsschnittstelle: UART
- Bluetooth-Zertifizierung: Entspricht den FCC CE ROHS REACH-Zertifizierungsstandards
- Serielle Schnittstellenparameter: 9600, 8 Datenbits, 1 Stoppbit, kein ungültiges Bit, keine Flusssteuerung
- Stromversorgung: 5V DC
- Betriebstemperatur: –10 bis +65 Grad Celsius


#### **(3)Anwendung:**

Das DX-BT24-Modul unterstützt auch das BT5.1 BLE-Protokoll, das direkt mit iOS-Geräten mit BLE-Bluetooth-Funktion verbunden werden kann und das dauerhafte Ausführen von Hintergrundprogrammen unterstützt. Wird hauptsächlich im Bereich der drahtlosen Kurzstrecken-Datenübertragung eingesetzt. Vermeidet umständliche Kabelverbindungen und kann Serienkabel direkt ersetzen. Erfolgreiche Anwendungsbereiche von BT24-Modulen:

※ Drahtlose Bluetooth-Datenübertragung;

※ Mobiltelefone, Computerperipheriegeräte;

※ Tragbare POS-Geräte;

※ Drahtlose Datenübertragung medizinischer Geräte;

※ Smart-Home-Steuerung;

※ Bluetooth-Drucker;

※ Bluetooth-Fernsteuerungsspielzeug;

※ Leihfahrräder;

#### **(4)Pin-Beschreibung:**

![](media/cd97cf79ff5cdd5bbd78f4cc960d38e5.png)

①STATE：Statuspin

②RX：Empfangspin

③TX：Sendepin

④GND：Masse

⑤VCC：Stromversorgungspin

⑥EN：Aktivierungspin

Bluetooth mit dem Entwicklungsboard verbinden

| Uno  | BT24 |
| :--: | :--: |
|  TX  |  RX  |
|  RX  |  TX  |
| VCC  |  5V  |
| GND  | GND  |

#### **(5)Schaltungsdiagramm:**

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)

#### **(6)APP herunterladen:**

##### **Für iOS-System**

1\. App Store öffnen.

2\. Suchen Sie nach <span style="color: rgb(61, 167, 66);">KeyesRobot</span> im Apple Store und klicken Sie auf Herunterladen.

![](./media/img-20240111141301.png)

3\. Nach der Installation der App sehen Sie das folgende Symbol auf dem Startbildschirm Ihres Telefons.

![](./media/img-20240111141412.png)

**So verbinden Sie das iOS-Telefon mit dem Bluetooth-Modul:**

1\. Aktivieren Sie Bluetooth und Ortungsdienste auf dem Telefon über die Einstellungen.

![](./media/img-20240111141943.png)

2\. Erlauben Sie der KeyesRobot APP, über die Einstellungen auf Bluetooth zuzugreifen.

![](./media/img-20240111142052.png)

3\. Klicken Sie zum Öffnen der KeyesRobot App.

![](./media/img-20240111142140.png)

4\. KeyesRobot App ist eine universelle APP, die für mehrere Keyestudio-Roboter verwendet wird. Wenn die Oberfläche nicht „TANK ROBOT" anzeigt, können Sie auf die linken und rechten Schaltflächen klicken, um „TANK ROBOT" zu finden.

5\. Klicken Sie auf die <span style="color: rgb(61, 167, 66);">Bluetooth-Schaltfläche</span>![](./media/img-20240111142336.png) in der oberen rechten Ecke, um Bluetooth zu scannen.

![](./media/img-20240111142415.png)

6\. Sie sehen ein Bluetooth-Gerät mit dem Namen <span style="color: rgb(0, 209, 0);">**BT24**</span>, klicken Sie auf die Schaltfläche <span style="color: rgb(255, 169, 0);">Verbinden</span>.

![](./media/img-20240111142536.png)

7\. Wenn die integrierte LED am Bluetooth-Modul aufhört zu blinken und dauerhaft leuchtet, bedeutet dies, dass Ihr Telefon erfolgreich mit dem Bluetooth-Modul verbunden wurde.

![](./media/img-20240111142702.png)


##### **Für Android-System**

1\. Suchen Sie nach <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> in Google Play, oder öffnen Sie den folgenden Link, um die App herunterzuladen und zu installieren.

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Schalten Sie Bluetooth und die Ortungsdienste des Mobiltelefons ein.

![](./media/img-20240111143354.png)

3\. Suchen Sie die KeyesRobot Bluetooth-App in den Einstellungen, klicken Sie auf die Berechtigungsoptionen der App und aktivieren Sie die Berechtigungen für Standort und Geräte in der Nähe. (<span style="color: rgb(255, 76, 65);">Hinweis:</span> Einige Mobiltelefone verfügen nicht über die Funktion für Berechtigungen für Geräte in der Nähe.)

![](./media/img-20240111143451.png)

4\. Klicken Sie zum Öffnen der KeyesRobot App.

![](./media/img-20240111143529.png)

5\. KeyesRobot App ist eine universelle APP, die für mehrere Keyestudio-Roboter verwendet wird. Wenn die Oberfläche nicht „TANK ROBOT" anzeigt, können Sie auf die linken und rechten Schaltflächen klicken, um „TANK ROBOT" zu finden.

6\. Klicken Sie auf die <span style="color: rgb(61, 167, 66);">Bluetooth-Schaltfläche</span>![](./media/img-20240111142336.png) in der oberen rechten Ecke, um Bluetooth zu scannen.

![](./media/img-20240111142415.png)

7\. Sie sehen ein Bluetooth-Gerät mit dem Namen <span style="color: rgb(0, 209, 0);">**BT24**</span>, klicken Sie auf die Schaltfläche <span style="color: rgb(255, 169, 0);">Verbinden</span>.![](./media/img-20240111143910.png)

8\. Wenn Ihr Telefon erfolgreich mit dem Bluetooth-Modul verbunden ist, hört die integrierte LED am Bluetooth-Modul auf zu blinken und bleibt dauerhaft an.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(7)BT-Testcode:**

Sie können auch Blöcke per Drag-and-Drop ziehen, um Ihren Code zu bearbeiten, wie unten gezeigt.

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/19a90ffb7565966f7d40462abed876a7.png)

（5）![](media/c8228c5040a43ae322612b312c995ac3.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es möglicherweise zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, die zum Fehlschlagen des Uploads führen können.)

![](media/4766ada3bf48bb35522f292d9352bb78.png)


Laden Sie den Code auf das Entwicklungsboard hoch, stecken Sie dann das Bluetooth-Modul ein und verbinden Sie anschließend das Mobiltelefon mit dem Bluetooth-Modul.

Nachdem das Mobiltelefon erfolgreich mit dem Bluetooth-Modul verbunden wurde, klicken Sie auf die Bluetooth-APP, um sie zu öffnen, und klicken Sie auf der <span style="color: rgb(0, 252, 255);">Startseite</span> auf die Schaltfläche <span style="color: rgb(0, 252, 255);">Auswählen</span>.

![](./media/img-20240111144744.png)

Die Hauptoberfläche der Bluetooth-App ist in der folgenden Abbildung dargestellt.

![](./media/img-20240111144859.png)

Klicken Sie auf ![Img](./media/img-20240111171312.png) und stellen Sie die Baudrate auf 9600 ein. Klicken Sie auf das Symbol in der APP-Oberfläche und der serielle Monitor zeigt den per Schaltfläche gesendeten Befehl an.

![](media/f5004f5334fb4885ac0096f99e4133f9.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Hinweis: Die APP-Verbindungsmethode ist dieselbe wie unten beschrieben.**</span>
<br>
<br>


#### **(8)Erweiterungsübung:**

Im obigen Projekt empfängt Bluetooth das vom Mobiltelefon gesendete Signal und zeigt es auf dem seriellen Port des Entwicklungsboards an. Hier verwenden wir den vom Mobiltelefon gesendeten Befehl, um eine LED ein- oder auszuschalten. Wie im Schaltungsdiagramm zu sehen ist, ist eine LED am Pin D9 angeschlossen.

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)


Sie können auch Blöcke per Drag-and-Drop ziehen, um Ihren Code zu bearbeiten, wie unten gezeigt.

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/aa78663af261ff1d9bc8ffa6ad7a65bc.png)

(5）![](media/c8228c5040a43ae322612b312c995ac3.png)

（6）![](media/4164bcf66d3d2415f43a0efcd1ce4243.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Schließen Sie das Bluetooth-Modul nicht an, bevor Sie den Code hochladen, da das Hochladen des Codes ebenfalls die serielle Kommunikation verwendet und es möglicherweise zu Konflikten mit der Bluetooth-Serielkommunikation kommen kann, die zum Fehlschlagen des Uploads führen können.)

![](media/91fd9d6f85e291fe90a63e5095ed7f44.png)

Nachdem der obige Code erfolgreich hochgeladen wurde, klicken Sie auf ![](media/d5e59839bafc63f8b35c78c60573d1fc.png), um die LED zu steuern.

![](./media/img-20240117094418.png)


Nachdem Sie das BT-Projekt abgeschlossen haben, entfernen Sie es.