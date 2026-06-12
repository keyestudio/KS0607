### Project 22: Brandblussende Robot Meerdere Functies

#### **(1)Beschrijving:**

De slimme auto heeft in elk vorig project één enkele functie uitgevoerd.

Kan hij meerdere functies tegelijk weergeven? Ja, dat kan.

In dit laatste grote project willen we een volledige code gebruiken om de slimme auto alle functies die in de vorige projecten zijn besproken te laten demonstreren. We gebruiken de toetsen op de Bluetooth APP om automatisch te schakelen tussen verschillende functies, wat heel eenvoudig en handig is.

#### **(2)Stroomdiagram:**

<span style="color: rgb(255, 76, 65);">**Raadpleeg Project 16 voor het installeren en configureren van de Bluetooth APP**</span>

![](media/wps122.png)

#### **(3)Aansluitingsdiagram:**

![](media/e7ac834ba04aa2e8862995d2d33ce935.png)

1\. GND, VCC, SDA en SCL van het 8x16-bord zijn verbonden met G (GND), + (VCC), A4 en A5 van het uitbreidingsbord.

2\. VCC, IN+, IN- en Gnd van de ventilatormodule zijn verbonden met 5V (V), 12 (S), 13 (S) en Gnd (G).

3\. De bruine draad, rode draad en oranje draad van de servo zijn verbonden met Gnd (G), 5v (V) en D10.

4\. RXD, TXD, GND en VCC van de BT-module zijn verbonden met TX, RX, G (GND) en 5V (VCC). STATE en BRK hoeven niet te worden aangesloten.

5\. De pinnen "G", "V" en A van de linker vlamsensor zijn respectievelijk verbonden met G (GND), V (VCC) en A1; De rechter vlamsensor is verbonden met G (GND), V (VCC) en A2.

6\. De distale poorten van de lijnvolgsensor zijn 11, 7 en 8.

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)
<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> U kunt de auto niet versnellen via de App.

![](media/b1527b806741e28e8f2af5107db505fe.png)


#### **(5)Testresultaat:**

Voordat u de programmacode uploadt, moet de Bluetooth-module worden verwijderd; anders mislukt het uploaden van de code.

Nadat de code succesvol is geüpload, schakelt u de locatieservices op uw apparaat in en verbindt u vervolgens de Bluetooth-module.

Zodra de Bluetooth-module is ingeplugd en ingeschakeld, en de mobiele APP succesvol is verbonden met de Bluetooth, kunnen we de mobiele APP gebruiken om de tankrobot te besturen.

![](media/13656cfee75dc5acbeba18a90a084e159.jpg)