### Project 20: Ventilator

#### **(1)Beschrijving：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Deze ventilatormodule gebruikt een HR1124S motorbesturingschip, een enkelvoudig H-brug stuurprogrammachip dat een laag-geleidingsweerstand PMOS en NMOS vermogenstransistoren bevat. De lage geleidingsweerstand kan het stroomverbruik verminderen, wat bijdraagt aan het veilig werken van de chip voor een langere tijd.

Bovendien maken zijn lage stand-bystroomverbruik en lage statische werkstroom het geschikt voor speelgoed. We kunnen de rotatierichting en snelheid van de ventilator regelen door IN+ en IN- signalen en PWM-signalen uit te sturen.

#### **(2)Parameters:**

- Werkspanning: 5V

- Stroom: 200mA

- Maximaal vermogen: 2W

- Werktemperatuur: -10°C tot +50 graden Celsius

- Afmeting: 47,6mm \* 23,8mm

#### **(3)Aansluitschema:**

De ventilatormodule heeft aandrijving door een grote stroom nodig; daarom installeren we een batterijhouder.

![](media/2bd9aa5cc21e274458328958561f1915.png)

De pinnen GND, VCC, IN+ en IN- van de ventilatormodule zijn verbonden met de pinnen G, V, 12 en 13 van het shield.

#### **(4)Testcode:**

Je kunt ook blokken slepen om je code te bewerken, zoals hieronder weergegeven

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/1360090880c1cd9b20671c17604f4108.png)

![](media/4e9354e674060efe6cf540a3e1b87813.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voor het uploaden van de code, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/cbb8f153dd0d114bdd350577af7a1f02.png)

#### **(5)Testresultaten:**

Upload de code, verbind de componenten, zet de stroom aan en zet de DIP-schakelaar op ON. De kleine ventilator draait 2s met de klok mee, stopt 2s en draait 2s tegen de klok in.

![](./media/img-20240117100504.png)

#### **(6)Uitbreidingsoefening:**

We hebben het werkingsprincipe van de vlamsensor begrepen. Vervolgens sluiten we een vlamsensor aan in het circuit, zoals hieronder weergegeven. Vervolgens regelen we de ventilator om het vuur uit te blazen met de vlamsensor.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)


Je kunt blokken slepen om je code te bewerken, zoals hieronder weergegeven

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voor het uploaden van de code, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/74ddb07daf4063f0640c31f4243a0864.png)


Na het uploaden van de code, zet de aan/uit-schakelaar van het motoraandrijvingsshield aan. De ventilator kan worden ingeschakeld wanneer er vlammen worden gedetecteerd door de linker vlamsensor van de robot.

![](./media/img-20240117102303.png)