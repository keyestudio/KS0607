### Project 9: 8*16 Gezichtsuitdrukking LED Dot Matrix

#### **(1)Beschrijving:**

Zou het niet leuk zijn als er een uitdrukkingsbord aan de robot wordt toegevoegd? En de Keyestudio 8*16 LED dot matrix kan dit voor elkaar krijgen. Met behulp hiervan kunt u zelf gezichtsuitdrukkingen, afbeeldingen, patronen en andere weergaven ontwerpen.

Het 8*16 LED-bord heeft 128 LED's. De gegevens van de microprocessor (Arduino) communiceren met de AiP1640 via een tweedraads businterface. Daardoor kan het de aan- en uitschakeling van 128 LED's op de module besturen, zodat de dot matrix op de module het gewenste patroon kan weergeven. Er wordt een HX-2.54 4Pin-kabel meegeleverd voor uw gemak bij de bedrading.

#### **(2)Parameters:**

-   Werkspanning: DC 3.3-5V

-   Vermogensverlies: 400mW

-   Oscillatiefrequentie: 450KHz

-   Rijstroom: 200mA

-   Werktemperatuur: -40\~80℃

-   Communicatiemodus: tweedraads bus

#### **(3)Kennis:**

**Schakeling van de 8\*16 LED dot matrix**

![](media/edf6c77d05904eebbaa89d557e9e9c1a.png)

**Principe van de 8\*16 LED dot matrix**

Hoe beheert u elke LED van de 8\*16 dot matrix? Het is bekend dat elke byte 8 bits heeft en elke bit 0 of 1 is. Wanneer het 0 is, is de LED uit, terwijl wanneer het 1 is, de LED aan is. Één byte kan één kolom van de LED's besturen, en natuurlijk kunnen 16 bytes 16 kolommen van LED's besturen, dat is de 8\*16 dot matrix.

**Pinbeschrijving en communicatieprotocol**

De gegevens van de microprocessor (Arduino) communiceren met de AiP1640 via een tweedraadse buskabel.

Het communicatieprotocoldiagram is als volgt: (SCLK) is SCL, (DIN) is SDA.

![](media/ea2bab37f23c09453c680590b84653d6.png)

①De startconditie voor gegevensinvoer: SCL is hoog niveau en SDA verandert van hoog naar laag.

②Voor het instellen van gegevensopdrachten zijn er methoden zoals weergegeven in de onderstaande figuur.

In ons voorbeeldprogramma selecteren we de manier om **het adres automatisch met 1 te verhogen**, de binaire waarde is 0100 0000 en de overeenkomstige hexadecimale waarde is 0x40.

![](media/image-20230907161100692.png)

③Voor het instellen van adresopdrachten kan het adres worden geselecteerd zoals hieronder weergegeven.

Het eerste 00H is geselecteerd in ons voorbeeldprogramma, en het binaire getal 1100 0000 komt overeen met het hexadecimale getal 0xc0.

![](media/image-20230907161152467.png)

④De vereiste voor gegevensinvoer is dat wanneer SCL op hoog niveau is bij het invoeren van gegevens, het signaal op SDA onveranderd moet blijven. Alleen wanneer het kloksignaal op SCL op laag niveau is, kan het signaal op SDA worden gewijzigd. De invoer van gegevens gebeurt eerst het laagste bit en daarna het hoogste bit.

⑤De conditie voor het einde van gegevensoverdracht is dat wanneer SCL op laag niveau is, SDA op laag niveau en SCL op hoog niveau, het niveau van SDA hoog wordt.

⑥Weergavebesturing, stel verschillende pulsbreedte in; de pulsbreedte kan worden geselecteerd zoals weergegeven in de onderstaande figuur.

In het voorbeeld is de pulsbreedte 4/16, en het hexadecimale getal dat overeenkomt met 1000 1010 is 0x8A.

![](media/image-20230907161220995.png)

**Instructies voor het gebruik van het modulustool**

Het dot matrix-tool gebruikt de online versie, en de link is: <http://dotmatrixtool.com/#>

①Voer de link in en de pagina verschijnt zoals hieronder weergegeven

![](media/354693b5679a2615c62e99b7025d6355.png)

②De dot matrix is 8\*16, dus pas de hoogte aan naar 8 en de breedte naar 16, zoals weergegeven in de onderstaande figuur.

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③Genereer hexadecimale gegevens uit het patroon.

Zoals weergegeven in de onderstaande figuur, druk op de linkermuisknop om te selecteren, klik met de rechtermuisknop om te annuleren; teken het gewenste patroon, klik op Generate, en de hexadecimale gegevens die we nodig hebben worden gegenereerd.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4)Aansluitdiagram:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

De GND, VCC, SDA en SCL van het 8x16 LED-lichtbord zijn respectievelijk verbonden met de G(GND), V (VCC), A4 en A5 van de uitbreidingskaart voor tweedraadse seriële communicatie.

(<span style="color: rgb(255, 76, 65);">Opmerking:</span> hoewel het is verbonden met de IIC-pin van Arduino, is deze module niet voor IIC-communicatie. En de IO-poort hier is om I2C-communicatie te simuleren en kan worden verbonden met twee willekeurige pinnen)

#### **(5)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

![](media/e346413e7f38f5f6368dd8262f173514.png)

![](media/8ecfff600093779602b37d2202493057.png)

![](media/0f0df06e3ed2adbbe3ffaa20dd3fa0a5.png)

**Volledige testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/75e6f65c9a299868d37544ac42c54f66.png)

#### **(6)Testresultaten:**

Na het succesvol uploaden van de testcode, de bedrading aansluiten, de DIP-schakelaar naar de ON-stand zetten en inschakelen, verschijnt er een patroon in de vorm van een smiley op de dot matrix.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7)Uitbreidingspraktijk:**

We gebruiken het modulustool dat we zojuist hebben geleerd, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), om de dot matrix het patroon start, vooruit gaan en stop te laten weergeven en vervolgens het patroon te wissen. Het tijdsinterval is 2000 ms.

![](media/31ab1346c58438ca95c990e4ff963c0d.png)

Blok om smiley te tonen![](media/1702a82ce685e3e7da7b136cbc51e718.png)

Code om uitdrukking te tonen![](media/bae6801afc8fbcc0e7a70c243559c266.png)

Blok om hart te tonen![](media/dcaa414f16d10068d2c3627959141da6.png)

Code voor vooruit rijden![](media/8fc218e6b35826aa31f5e00f61414651.png)

Blok voor achteruit rijden![](media/043abae4540c578f93772ed9b6648e60.png)

Blok voor links afslaan![](media/7b3d80a76228ee5b23555af17269a02d.png)

Blok voor rechts afslaan![](media/5a84b3538a62367a8f35cc59071c0bda.png)

Blok voor stoppen![](media/733bd1f96e1c9d116033a317cb507fac.png)

Blok voor wissen![](media/06d37680acd61c9c5c4113c78c985eca.png)

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.

（1）![](media/e346413e7f38f5f6368dd8262f173514.png)

（2）![](media/840217b5879f1fce9e36566dc76914a4.png)

（3）![](media/e72e75122897b0ef930196f762080623.png)

**Volledige testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/dee30ed46775feb634d4e8e4ec0a189a.png)

Upload de code naar de ontwikkelkaart; het 8\*16-bord toont de volgende patronen.

![](./media/image-20250709134319784.png)

![](./media/image-20250709134332835.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)