### Project 21: Brandblussende Tank

#### **(1)Beschrijving:**

De lijnvolgfunctie van de slimme tank is uitgelegd in het vorige project. In dit project gebruiken we de vlamsensor om een brandblussende robot te maken.

Wanneer de auto vlammen tegenkomt, zal de motor van de ventilator draaien om het vuur te blussen. Natuurlijk moeten we eerst de ultrasone sensor en twee fotoweerstand vervangen door een ventilatormodule en vlamsensoren.

De specifieke logica van de slimme auto wordt weergegeven in de onderstaande tabel:

| Linker Vlamsensor | Rechter Vlamsensor | Status                                                        |
| :---------------: | :----------------: | :------------------------------------------------------------ |
|       ≤700        |        ≤700        | Auto stopt, ventilator begint te draaien om het vuur te blussen |
|       ≥700        |        ≥700        | Auto stopt, ventilator begint te draaien om het vuur te blussen |
|       ≥700        |        ≥700        | Auto stopt, ventilator begint te draaien om het vuur te blussen |
|       ＞700       |       ＞700        | Ventilator stopt, auto rijdt                                  |

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
1) Dit experiment vereist het gebruik van een vuurhaard. Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen moeten experimenteren onder toezicht van een volwassene. Als u niet zeker kunt zijn van uw veiligheid, laat het experiment dan achterwege.
2) De vlamsensor is niet vuurbestendig. Verbrand hem niet rechtstreeks met een vlam.
We kunnen een externe LED bedienen met de vlamsensor. De LED is nog steeds aangesloten op D9. Wanneer er vuur wordt gedetecteerd, gaat de LED aan.


#### **(2)Stroomdiagram:**

![](media/wps120.png)

#### **(3)Aansluitingsdiagram:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

<span style="color: rgb(255, 76, 65);">Opmerking:</span>

GND, VCC, SDA en SCL van het 8x16 LED-paneel zijn verbonden met G（GND), V（VCC), A4 en A5.

G, V en A van de twee vlamsensoren zijn verbonden met G（GND), V（VCC), A1 en A2 van het uitbreidingsbord.

#### **(4)Testcode:**


U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/2e3d4904d9605dfecb5736b4bf235ab2.png)

（4） ![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（5） ![](media/4b40151c7482ff9371570978b8ef9c77.png)

（6）![](media/c0365237fa7ec7de10e9fc465353fae1.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten ontstaan met de Bluetooth-seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/c07c09e5533a37838722b8c2b513646d.png)

#### **(5)Testresultaten:**

Nadat de testcode succesvol is geüpload, zet u de voeding aan en zet u de DIP-schakelaar op de ON-stand. De slimme auto zal het vuur blussen wanneer hij vlammen detecteert.

![](media/2de5f1d832d40c0fc94274f1d87443c6.jpeg)

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen moeten experimenteren onder toezicht van een volwassene. Als u niet zeker kunt zijn van uw veiligheid, laat het experiment dan achterwege. De vlamsensor is niet vuurbestendig. Verbrand hem niet rechtstreeks met een vlam.