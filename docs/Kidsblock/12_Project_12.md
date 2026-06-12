### Project 12: Ultrasonic Hindernisontwijkende Tank

#### **(1)Beschrijving:**

In het vorige project hebben we een ultrasonische geluid-volgende slimme auto gemaakt. In feite kunnen we met dezelfde componenten en dezelfde bedradingsmethode, door alleen de testcode te wijzigen, er een ultrasonische hindernisontwijkende slimme auto van maken. Deze slimme auto kan bewegen met de beweging van de menselijke handen.

We gebruiken ultrasonische sensoren om de afstand tussen de slimme auto en het obstakel aan de voorkant te meten, en vervolgens de rotatie van de twee motoren op basis van deze gegevens te regelen om zo de bewegingen van de slimme auto te besturen.

|                          Detectie                            |         |
| :----------------------------------------------------------: | :-----: |
| Afstand gemeten door de ultrasonische sensor tussen de auto en het obstakel aan de voorkant <br />（stel de hoek van de servo in op 90°） | a (cm)  |
| Afstand gemeten door de ultrasonische sensor tussen de auto en het obstakel aan de rechterkant <br />（stel de hoek van de servo in op 0°） | a2 (cm) |
| Afstand gemeten door de ultrasonische sensor tussen de auto en het obstakel aan de linkerkant <br />（stel de hoek van de servo in op 180°） | a1 (cm) |

**Instelling: stel de beginhoek van de servo in op 90°**

| Voorwaarde 1 |        Voorwaarde 2         |      Voorwaarde 3       | Beweging                                                     |
| :---------: | :------------------------: | :--------------------: | :----------------------------------------------------------- |
|    a＜20    |                            |                        | Stop gedurende 500ms；stel de hoek van de servo in op 180°，lees a1，vertraging van 100ms；stel de hoek van de servo in op 0°，lees a2，vertraging van 0.1s. |
|             | a1＜50<br />of<br />a2＜50 | **Vergelijk a1 met a2** |                                                              |
|             |                            |         a1＞a2         | Stel de hoek van de servo in op 90°，draai links gedurende 700ms（stel PWM in op 255），en beweeg naar voren（stel PWM in op 200）. |
|             |                            |         a1＜a2         | Stel de hoek van de servo in op 90°，draai rechts gedurende 700ms（stel PWM in op 255），en beweeg naar voren（stel PWM in op 200）. |
|             | a1≥50<br />en<br />a2≥50  |         Willekeurig         | Stel de hoek van de servo in op 90°，draai links gedurende 500ms（stel PWM in op 255），en beweeg naar voren（stel PWM in op 200）.<br /><br />Stel de hoek van de servo in op 90°，draai rechts gedurende 500ms（stel PWM in op 255），en beweeg naar voren（stel PWM in op 200）. |
|    a≥20     |                            |                        | Beweeg naar voren（stel PWM in op 100）                               |

#### **(2)Stroomdiagram:**

![](media/wps119.png)

#### **(3)Aansluitingsdiagram:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

(<span style="color: rgb(255, 76, 65);">Opmerking:</span> de bruine, rode en oranje draden van de servo zijn respectievelijk verbonden met G (GND), V（5V）en D10 van het uitbreidingsbord；en voor de ultrasonische sensor is de VCC-pin verbonden met 5v (V), de Trig-pin met digitaal 12 (S), de Echo-pin met digitaal 13 (S), en de Gnd-pin met Gnd (G); hetzelfde als het vorige project.）

#### **(4)Testcode:**


U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven.![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/5dcbd405806b8e341505d7316246dbdd.png)

（3）![](media/996c8d4e5dd9620757dfb097329e7d5d.png)

（4）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

（10）![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

（11）![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er mogelijk conflicten ontstaan met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/4360f9642a8c6b2488767c079d481482.png)

#### **(5)Testresultaten:**

Na het succesvol uploaden van de testcode, de bedrading aansluiten, de DIP-schakelaar naar de ON-stand zetten en de stroom inschakelen. De slimme auto zal naar voren bewegen en automatisch obstakels ontwijken.

![](./media/img-20240117093950.png)