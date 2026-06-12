### Project 7: IR-ontvangst

#### **(1)Beschrijving:**

![](./media/image-20250709133757050.png)

Het staat buiten kijf dat infrarood afstandsbediening alomtegenwoordig is in het dagelijks leven. Het wordt gebruikt om verschillende huishoudelijke apparaten te bedienen, zoals televisies, stereo-installaties, videorecorders en satellietsignaalontvangers. Infrarood afstandsbediening bestaat uit een infrarood zend- en ontvangstysteem, dat wil zeggen een infrarood afstandsbediening en een infrarood ontvangstmodule en een enkelvoudige-chip microcomputer die in staat is tot decodering.

Het 38K infrarood draaggolfsignaal dat door de afstandsbediening wordt uitgezonden, wordt gecodeerd door de coderingschip in de afstandsbediening. Het bestaat uit een stuk pilootcode, gebruikerscode, inverse gebruikerscode, datacode en inverse datacode. Het tijdsinterval van de puls wordt gebruikt om te onderscheiden of het een 0- of 1-signaal is, en de codering bestaat uit deze 0- en 1-signalen.

De gebruikerscode van dezelfde afstandsbediening blijft ongewijzigd, terwijl de datacode de toets kan onderscheiden.

Wanneer de knop op de afstandsbediening wordt ingedrukt, verzendt de afstandsbediening een infrarood draaggolfsignaal. Wanneer de IR-ontvanger het signaal ontvangt, zal het programma het draaggolfsignaal decoderen en bepalen welke toets is ingedrukt. De MCU decodeert het ontvangen 01-signaal en bepaalt daarmee welke toets op de afstandsbediening is ingedrukt.

![](media/5ad0f889b39646ecb13664511479efc8.png)

De infrarood ontvanger die we gebruiken is een infrarood ontvangstmodule. Deze bestaat voornamelijk uit een infrarood ontvangerhoofd, wat een apparaat is dat ontvangst, versterking en demodulatie integreert. De interne IC heeft de demodulatie voltooid en kan infraroodontvangst tot uitvoer verwezenlijken en is compatibel met TTL-signalen. Bovendien is het geschikt voor infrarood afstandsbediening en infraroodgegevensoverdracht. De infrarood ontvangstmodule die door de ontvanger is gemaakt, heeft slechts drie pinnen: signaallijn, VCC en GND. Het is zeer eenvoudig om te communiceren met Arduino en andere microcontrollers.

#### **(2)Parameters:**

- Werkspanning: 3,3-5V (DC)
- Interface: 3PIN
- Uitgangssignaal: Digitaal signaal
- Ontvangsthoek: 90 graden
- Frequentie: 38khz
- Ontvangstafstand: 10m

Infrarood ontvanger geïntegreerd op de motoraansturingskaart:

![](./media/image-20250709133832650.png)

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Aangezien de IR-ontvanger is geïntegreerd in de Keyestudio 8833 motoraansturing uitbreidingskaart, is geen extra bedrading vereist. De pinnen van de IR-ontvanger op de Keyestudio 8833 motoraansturing uitbreidingskaart zijn G (GND), V (VCC) en D3.

#### **(4)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

![](media/cfe0841bcc9404c29519ed623195ca6a.png)

![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

![](media/5a48421831518ea8e0c00be83cf4edf4.png)

![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

**Volledige testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/90978855cddd94c161f9ed02f85b0674.png)

#### **(5)Testresultaten:**

Upload de code naar de ontwikkelkaart en stel de baudrate in op 9600. Pak de afstandsbediening erbij, richt hem op de infrarood ontvangersensor en druk op een knop om het signaal te verzenden. U zult de overeenkomstige toetswaarde zien. Als de toets te lang wordt ingedrukt, kan er gemakkelijk een onleesbaar "FFFFFFFF" verschijnen.

![](media/5c01c594a5a11511cf52466eb5f27e45.png)

Hieronder hebben we elke toetswaarde van de Keyestudio afstandsbediening vermeld. U kunt dit als referentie bewaren.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

#### **(6)Uitbreidingsoefening:**

We hebben zojuist de toetswaarden van de IR-afstandsbediening gedecodeerd. Laten we die nu gebruiken om een LED-lamp aan en uit te zetten. We moeten een LED-lichtmodule aansluiten op pin D9, terwijl de pinpositie van de infrarood ontvanger ongewijzigd blijft. Wanneer de OK-knop op de afstandsbediening wordt ingedrukt, gaat de LED aangesloten op D9 aan, en wanneer de OK-knop opnieuw wordt ingedrukt, gaat de LED uit.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)


U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

（1）![](media/cfe0841bcc9404c29519ed623195ca6a.png)

（2）![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

（3）![](media/ba67c48d67b1c9753fca82964c9dddc7.png)

(4) ![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

（5）![](media/f8b75df8ccea3efe1cd3ea383b0f88f2.png)

（6）![](media/7406d60c93cdba0b13ded27cba718ec7.png)

（7）![](media/d7be3fa06a1456d46472fffd61823c73.png)

**Volledige testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/57149c79243ff22aa00ff2c54dd4f70b.png)

Upload de code naar de ontwikkelkaart en druk op de "OK"-toets op de afstandsbediening om de LED aan en uit te zetten.

![](./media/img-20240117092532.png)