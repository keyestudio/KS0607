### Project 8: Motor Aansturing en Snelheidsregeling

#### **(1)Beschrijving:**

Er zijn veel manieren om motoren aan te sturen. Onze slimme auto gebruikt de meest gangbare oplossing genaamd L298P. L298P, geproduceerd door STMicroelectronics, is een uitstekende aandrijfchip die speciaal is ontworpen voor het aansturen van hoogvermogen motoren. Het kan DC-motoren, twee-fase en vier-fase motoren rechtstreeks aansturen met een aandrijfstroom tot 2A. En de uitgangsaansluiting van de motor maakt gebruik van 8 snelle Schottky-diodes als beveiliging. We hebben een uitbreidingskaart ontworpen op basis van het L298P-circuit waarvan het gestapelde ontwerp rechtstreeks in het UNO R3-board kan worden gestoken, waardoor de technische moeilijkheden voor gebruikers bij het gebruik en aansturen van de motor worden verminderd.

Stapel de uitbreidingskaart op het board, geef stroom aan de BAT, zet de DIP-schakelaar naar de ON-kant, en geef de uitbreidingskaart en het UNO R3-board tegelijkertijd stroom via externe voeding. Om het bedraden te vergemakkelijken, is de uitbreidingskaart uitgerust met anti-omkeers interfaces (PH2.0 -2P -3P -4P -5P) en kan daardoor rechtstreeks worden aangesloten op motoren, voeding en sensoren/modules. De Bluetooth-interface van de aandrijfuitbreidingskaart is volledig compatibel met de Keyestudio HM-10 Bluetooth-module. Daarom hoeven we de HM-10 Bluetooth-module alleen maar in de bijbehorende interface te steken bij het aansluiten. Tegelijkertijd gebruikt de aandrijfuitbreidingskaart ook 2.54 pin-headers om enkele beschikbare digitale poorten en analoge poorten uit te breiden, zodat u andere sensoren kunt blijven toevoegen en uitbreidingsexperimenten kunt uitvoeren.

De uitbreidingskaart kan worden aangesloten op 4 DC-motoren. In de standaard jumper-cap verbindingsmodus zijn de A en A1, B en B1 interface-motoren parallel geschakeld, en hun bewegingspatroon is hetzelfde. 8 jumper-caps kunnen worden gebruikt om de rotatierichting van de 4 motor-interfaces te regelen. Als de twee jumper-caps voor de motor A-interface bijvoorbeeld worden gewijzigd van een horizontale verbinding naar een verticale verbinding, is de rotatierichting van motor A nu tegengesteld aan de oorspronkelijke rotatierichting.

![](media/6c3731f639e113c8f32fe1829f239898.png)

![](media/62ee9578858ecc8e27b824af65fb22bb.png)

#### **(2)Parameters:**

-   Logisch deel ingangsspanning: DC 5V

-   Aandrijvingsdeel ingangsspanning: DC 7-12V

-   Logisch deel werkstroom: ≤36mA

-   Aandrijvingsdeel werkstroom: ≤ 2A

-   Maximaal dissipatieverogen: 25W (T=75℃)

-   Ingangsniveau stuursignaal:

    Hoog niveau: 2.3V ≤ Vin ≤ 5V

    Laag niveau: 0V ≤ Vin ≤ 1.5V

-   Werktemperatuur: -25℃～＋130℃

#### **(3)De robot laten bewegen:**

De richtingspin van motor A is D2, de snelheidsregelingspin is D5; de richtingspin van motor B is D4 en de snelheidsregelingspin is D6.

Aan de hand van de onderstaande tabel kunnen we zien hoe we de beweging van de robot kunnen regelen door de rotatie van twee motoren te besturen via de digitale poorten en PWM-poorten. Hierbij is het bereik van de PWM-waarde 0-255. Hoe groter de waarde, hoe sneller de motor draait.

|    Functie    |  D4  | D6（PWM） | Motor（links）B |  D2  | D5（PWM） | Motor（rechts）A |
| :-----------: | :--: | :-------: | :-------------: | :--: | :-------: | :--------------: |
| Vooruit rijden | HIGH |     0     |  Draait links   | HIGH |     0     |  Draait links    |
|  Achteruit rijden  | LOW  |    255    |  Draait rechts  | LOW  |    255    |  Draait rechts   |
|  Links draaien  | LOW  |    255    |  Draait rechts  | HIGH |    100    |  Draait links    |
| Rechts draaien  | HIGH |    100    |  Draait links   | LOW  |    255    |  Draait rechts   |
|    Stoppen     | LOW  |     0     |     Stopt       | LOW  |     0     |     Stopt        |

#### **(4)Aansluitingsdiagram:**

![](./media/image-20250709134029403.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span>

De 4-pins connector is gemarkeerd met A, A1, B1 en B. De rechter achtermotor is aangesloten op B van het 8833-board en de linker voormotor is aangesloten op de A-poort.

#### **(5)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.

（1）![](media/7cbc4d14c2e2dac956f2e9f145f01f31.png)

（2）![](media/0067d367772d4e3005bfc097ba3b59b0.png)

（3）![](media/f0c505e8268454c7996b755f97c6322b.png)

（4）![](media/b7215c8a4997a188947e80fdee1a8cd9.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/332229f3dc01a38de898367f52531b28.png)


#### **(6)Testresultaten:**

Na het bedraden volgens het diagram, het uploaden van de testcode en het inschakelen van de stroom.

![](./media/img-20240117092625.png)

rijdt de slimme auto 2s vooruit, rijdt 2s achteruit, draait 2s naar links, draait 2s naar rechts en stopt 2s.