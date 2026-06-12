### Project 17: Bluetooth Besturing Tank

#### **(1)Beschrijving:**

We hebben de basiskennis van Bluetooth geleerd in het vorige project. In deze les zullen we Bluetooth gebruiken om de slimme auto te besturen. Omdat het Bluetooth betreft, zijn een verzendend en een ontvangend einde nodig. In het project gebruiken we de mobiele telefoon als zender (master), en de slimme auto verbonden met de HM-10 Bluetooth module (slave) als ontvanger.

We hebben eerder geleerd dat het verzenden van een bit LED's kan besturen. En het principe van het besturen van deze robotauto is hetzelfde.

Om de intelligente tanktrobot beter te kunnen besturen, hebben we speciaal een APP gemaakt. In deze les lezen we alle toetswaarden op deze APP via code uit, en introduceren we vervolgens de exclusieve APP van onze tanktrobot.

#### **(2)Sleutelfuncties op de APP:**

De volgende tabel illustreert de functies van de bijbehorende toetsen:

|                      Toetsen                       |                                                |                          Functies                           |
| :---------------------------------------------: | :--------------------------------------------: | :----------------------------------------------------------: |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) |                                                | Koppel en verbind de HM-10 Bluetooth module; klik opnieuw om de verbinding te verbreken |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) |                                                |                 Selecteer de robot om te bedienen                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) |                                                |       Bestuur de bewegingen van de robot via knoppen       |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) |                                                |      Bestuur de bewegingen van de robot via joystick       |
| ![](media/3ab61154b4ae730a3757f40171846825.png) |                                                |       Bestuur de bewegingen van de robot via zwaartekracht       |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) |   Stuurt "F" bij indrukken en "S" bij loslaten    | De auto beweegt vooruit wanneer ingedrukt en stopt wanneer losgelaten |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) |   Stuurt "L" bij indrukken en "S" bij loslaten    | De auto draait links wanneer stevig ingedrukt en stopt wanneer losgelaten |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) |   Stuurt "R" bij indrukken en "S" bij loslaten    | De auto draait rechts wanneer stevig ingedrukt en stopt wanneer losgelaten |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) |   Stuurt "B" bij indrukken en "S" bij loslaten    | De auto rijdt achteruit wanneer stevig ingedrukt en stopt wanneer losgelaten |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) |        Stuurt "u"+cijfer+"\#" bij slepen         |          Sleep om de snelheid van de linkermotor te wijzigen          |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) |        Stuurt "v"+cijfer+"\#" bij slepen         |         Sleep om de snelheid van de rechtermotor te wijzigen          |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) |         Selecteer om de Functiepagina te openen          |                                                              |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Stuurt "G" bij indrukken en "S" bij opnieuw indrukken | Activeer obstakelvermijdingsmodus bij indrukken en deactiveer bij opnieuw indrukken |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Stuurt "h" bij indrukken en "S" bij opnieuw indrukken | Activeer volgmodus bij indrukken en deactiveer bij opnieuw indrukken |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Stuurt "e" bij indrukken en "S" bij opnieuw indrukken | Activeer lijnvolgmodus bij indrukken en deactiveer bij opnieuw indrukken |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Stuurt "f" bij indrukken en "S" bij opnieuw indrukken | Activeer rijden-in-beperkte-ruimte-modus bij indrukken en deactiveer bij opnieuw indrukken |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Stuurt "i" bij indrukken en "S" bij opnieuw indrukken | Activeer lichtvolgende modus bij indrukken en deactiveer bij opnieuw indrukken |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Stuurt "j" bij indrukken en "S" bij opnieuw indrukken | Activeer brandblussende modus bij indrukken en deactiveer bij opnieuw indrukken |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Selecteer om de weergavemodus voor gezichtsuitdrukkingen te openen |                                                              |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Stuurt "k" bij indrukken en "z" bij opnieuw indrukken | Toont lachend patroon bij klikken en wist de uitdrukking bij opnieuw klikken |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Stuurt "l" bij indrukken en "z" bij opnieuw indrukken | Toont walgend patroon bij klikken en wist de uitdrukking bij opnieuw klikken |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Stuurt "m" bij indrukken en "z" bij opnieuw indrukken | Toont blij gezicht bij klikken en wist de uitdrukking bij opnieuw klikken |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Stuurt "n" bij indrukken en "z" bij opnieuw indrukken | Toont verdrietig patroon bij klikken en wist de uitdrukking bij opnieuw klikken |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Stuurt "o" bij indrukken en "z" bij opnieuw indrukken | Toont minachtend patroon bij klikken en wist de uitdrukking bij opnieuw klikken |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Stuurt "p" bij indrukken en "z" bij opnieuw indrukken | Toont hartvormig patroon bij klikken en wist de uitdrukking bij opnieuw klikken |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) |                                                | Kies om de aangepaste functie-interface te openen; er zijn zes toetsen 1,2,3,4,5,6; met deze toetsen kunt u zelf enkele functies uitbreiden |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) |               Klik om "w" te versturen                | Klik om de analoge waarde weergeven die wordt gedetecteerd door de linker fotoweerstand |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) |                Klik om "y" te versturen                | Klik om de analoge waarde weer te geven die wordt gedetecteerd door de rechter fotoweerstand |
| ![](media/a76df707b84409e57a1167889c3510d9.png) |                Klik om "x" te versturen                | Klik om de afstand weer te geven die wordt gedetecteerd door de ultrasone sensor (eenheid: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Klik om "c" te versturen <br />Klik opnieuw om "d" te versturen  |   Druk om de ventilator aan te zetten en druk opnieuw om hem uit te zetten    |

#### **(3)Stroomdiagram:**

![](./media/image-20250709135203165.png)

#### **(4)Aansluitingsdiagram:**

![](media/930a8024364e07505e845624a94c27bd.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span>

GND, VCC, SDA en SCL van het 8x16 LED-paneel zijn verbonden met G（GND), V（5V), A4 en A5 van de uitbreidingskaart. STATE en BRK hoeven niet te worden aangesloten. De BT-module wordt in de uitbreidingskaart gestoken.

#### **(5)Testcode:**

U kunt blokken slepen om uw code te bewerken

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/3b4fb768cbf7e0b80fa55cb15aa932b7.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6) ![](media/8a13abc40d27d0470902e528b40170c3.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/341e0a01bd6a76edb53f9414ef641a75.png)

#### **(6)Testresultaat:**

Na het uploaden van de code, verbindt u de robot met de Bluetooth-module en koppelt u de Bluetooth APP. Zet de aan/uitschakelaar van het motoraandrijfschild aan. Plaats de robot op de vloer, u kunt de knoppen van de Bluetooth-app gebruiken om de robot te besturen.

![](media/352d5ec83c4246b980da10b5f99711c5.jpeg)

1. De pijlen omhoog, omlaag, links en rechts besturen de robot om respectievelijk vooruit, achteruit, naar links en naar rechts te bewegen.

![](./media/img-20240117095015.png)

2. Klik op de joystickknop en trek de richting van het zwarte punt in de witte cirkel om de bewegingsrichting van de robot te besturen.

![](./media/img-20240117095052.png)

3. Klik op de Zwaartekrachtknop en kantel de telefoon in de voorwaartse, achterwaartse, linker en rechter richtingen, en de robot zal bewegen in de richting waarin de telefoon wordt gekanteld.

![](./media/img-20240117095131.png)