### Projekt 17: Bluetooth-gesteuerter Panzer

#### **(1) Beschreibung:**

Im vorherigen Projekt haben wir die Grundlagen von Bluetooth kennengelernt. In dieser Lektion werden wir Bluetooth verwenden, um das Smart Car zu steuern. Da Bluetooth involviert ist, werden ein Sender und ein Empfänger benötigt. In diesem Projekt verwenden wir das Mobiltelefon als Sender (Master) und das Smart Car mit dem angeschlossenen HM-10 Bluetooth-Modul (Slave) als Empfänger.

Wir haben früher gelernt, dass das Senden eines Bits LEDs steuern kann. Das Prinzip der Steuerung dieses Roboter-Autos ist dasselbe.

Um den intelligenten Panzerroboter besser steuern zu können, haben wir speziell eine APP entwickelt. In dieser Lektion lesen wir alle Tastenwerte dieser APP durch Code aus und stellen anschließend die exklusive APP unseres Panzerroboters vor.

#### **(2) Tastenfunktionen der APP:**

Die folgende Tabelle zeigt die Funktionen der entsprechenden Tasten:

|                      Tasten                      |                                                |                          Funktionen                           |
| :---------------------------------------------: | :--------------------------------------------: | :----------------------------------------------------------: |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) |                                                | HM-10 Bluetooth-Modul koppeln und verbinden; erneut klicken zum Trennen |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) |                                                |                 Roboter zur Steuerung auswählen                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) |                                                |       Roboterbewegungen mit Tasten steuern       |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) |                                                |      Roboterbewegungen mit Joystick steuern       |
| ![](media/3ab61154b4ae730a3757f40171846825.png) |                                                |       Roboterbewegungen durch Neigung steuern       |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) |   Sendet "F" beim Drücken und "S" beim Loslassen    | Das Auto fährt vorwärts, wenn gedrückt, und stoppt beim Loslassen |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) |   Sendet "L" beim Drücken und "S" beim Loslassen    | Das Auto dreht links, wenn gedrückt, und stoppt beim Loslassen |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) |   Sendet "R" beim Drücken und "S" beim Loslassen    | Das Auto dreht rechts, wenn gedrückt, und stoppt beim Loslassen |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) |   Sendet "B" beim Drücken und "S" beim Loslassen    | Das Auto fährt rückwärts, wenn gedrückt, und stoppt beim Loslassen |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) |        Sendet "u"+Zahl+"\#" beim Ziehen         |          Ziehen zum Ändern der Geschwindigkeit des linken Motors          |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) |        Sendet "v"+Zahl+"\#" beim Ziehen         |         Ziehen zum Ändern der Geschwindigkeit des rechten Motors          |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) |         Auswählen zum Öffnen der Funktionsseite          |                                                              |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Sendet "G" beim Drücken und "S" beim erneuten Drücken | Beim Drücken wird der Hindernisumfahrmodus aktiviert und beim erneuten Drücken deaktiviert |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Sendet "h" beim Drücken und "S" beim erneuten Drücken | Beim Drücken wird der Folgemodus aktiviert und beim erneuten Drücken deaktiviert |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Sendet "e" beim Drücken und "S" beim erneuten Drücken | Beim Drücken wird der Linienverfolgungsmodus aktiviert und beim erneuten Drücken deaktiviert |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Sendet "f" beim Drücken und "S" beim erneuten Drücken | Beim Drücken wird der Modus „Bewegung im begrenzten Raum" aktiviert und beim erneuten Drücken deaktiviert |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Sendet "i" beim Drücken und "S" beim erneuten Drücken | Beim Drücken wird der Lichtfolgemodus aktiviert und beim erneuten Drücken deaktiviert |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Sendet "j" beim Drücken und "S" beim erneuten Drücken | Beim Drücken wird der Feuerlöschmodus aktiviert und beim erneuten Drücken deaktiviert |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Auswählen zum Öffnen des Gesichtsausdrucks-Anzeigemodus |                                                              |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Sendet "k" beim Drücken und "z" beim erneuten Drücken | Zeigt ein lächelndes Muster beim Klicken und löscht den Ausdruck beim erneuten Klicken |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Sendet "l" beim Drücken und "z" beim erneuten Drücken | Zeigt ein angewidertes Muster beim Klicken und löscht den Ausdruck beim erneuten Klicken |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Sendet "m" beim Drücken und "z" beim erneuten Drücken | Zeigt ein fröhliches Gesicht beim Klicken und löscht den Ausdruck beim erneuten Klicken |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Sendet "n" beim Drücken und "z" beim erneuten Drücken | Zeigt ein trauriges Muster beim Klicken und löscht den Ausdruck beim erneuten Klicken |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Sendet "o" beim Drücken und "z" beim erneuten Drücken | Zeigt ein verachtendes Muster beim Klicken und löscht den Ausdruck beim erneuten Klicken |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Sendet "p" beim Drücken und "z" beim erneuten Drücken | Zeigt ein herzförmiges Muster beim Klicken und löscht den Ausdruck beim erneuten Klicken |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) |                                                | Auswählen zum Öffnen der benutzerdefinierten Funktionsoberfläche; es gibt sechs Tasten 1, 2, 3, 4, 5, 6; mit diesen Tasten können Sie selbst einige Funktionen erweitern |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) |               Klicken zum Senden von "w"                | Klicken zum Anzeigen des Analogwerts des linken Fotowiderstands |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) |                Klicken zum Senden von "y"                | Klicken zum Anzeigen des Analogwerts des rechten Fotowiderstands |
| ![](media/a76df707b84409e57a1167889c3510d9.png) |                Klicken zum Senden von "x"                | Klicken zum Anzeigen der vom Ultraschallsensor gemessenen Entfernung (Einheit: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Klicken zum Senden von "c" <br />Erneut klicken zum Senden von "d"  |   Drücken zum Einschalten des Lüfters und erneut drücken zum Ausschalten   |

#### **(3) Ablaufdiagramm:**

![](./media/image-20250709135203165.png)

#### **(4) Anschlussdiagramm:**

![](media/930a8024364e07505e845624a94c27bd.png)

<span style="color: rgb(255, 76, 65);">Hinweis:</span>

GND, VCC, SDA und SCL des 8x16 LED-Panels sind mit G（GND), V（5V), A4 und A5 der Erweiterungsplatine verbunden. STATE und BRK müssen nicht angeschlossen werden. Das BT-Modul wird in die Erweiterungsplatine eingesteckt.

#### **(5) Testcode:**

Sie können Blöcke ziehen, um Ihren Code zu bearbeiten

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/3b4fb768cbf7e0b80fa55cb15aa932b7.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6) ![](media/8a13abc40d27d0470902e528b40170c3.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Vollständiger Testcode**

(<span style="color: rgb(255, 76, 65);">**Hinweis:**</span> Verbinden Sie das Bluetooth-Modul nicht, bevor Sie den Code hochladen, da das Hochladen ebenfalls die serielle Kommunikation verwendet und es zu Konflikten mit der seriellen Bluetooth-Kommunikation kommen kann, was dazu führen kann, dass der Upload fehlschlägt.)

![](media/341e0a01bd6a76edb53f9414ef641a75.png)

#### **(6) Testergebnis:**

Nach dem Hochladen des Codes verbinden Sie den Roboter mit dem Bluetooth-Modul und koppeln Sie die Bluetooth-APP. Schalten Sie den Netzschalter des Motorantriebsschields ein. Stellen Sie den Roboter auf den Boden. Sie können die Tasten der Bluetooth-APP verwenden, um den Roboter zu steuern.

![](media/352d5ec83c4246b980da10b5f99711c5.jpeg)

1. Die Pfeile oben, unten, links und rechts steuern den Roboter, um ihn vorwärts, rückwärts, nach links und nach rechts zu bewegen.

![](./media/img-20240117095015.png)

2. Klicken Sie auf die Joystick-Taste und ziehen Sie die Richtung des schwarzen Punktes im weißen Kreis, um die Bewegungsrichtung des Roboters zu steuern.

![](./media/img-20240117095052.png)

3. Klicken Sie auf die Neigungstaste und neigen Sie das Telefon in die vorwärts, rückwärts, links und rechts Richtungen, und der Roboter bewegt sich in die Richtung, in die das Telefon geneigt wird.

![](./media/img-20240117095131.png)