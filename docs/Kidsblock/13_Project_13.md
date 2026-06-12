### Project 13: Beweeg-in-Beperkte-Ruimte Tank


#### **(1)Beschrijving:**

De ultrasone volgfunctie en obstakelvermijdingsfuncties van de slimme auto zijn in eerdere projecten besproken. Hier willen we de kennis uit de vorige cursussen combineren om de slimme auto te beperken tot bewegen binnen een bepaalde ruimte. In het experiment gebruiken we de lijnvolgsensor om te detecteren of er een zwarte lijn rondom de slimme auto is, en vervolgens de rotatie van de twee motoren te besturen op basis van de detectieresultaten, zodat de slimme auto binnen een cirkel getekend met een zwarte lijn blijft.

De specifieke logica van de slimme auto wordt weergegeven in de onderstaande tabel:

![](media/image-20230525114604923.png)

|                         Voorwaarde                         |                         Beweging                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Als één van de drie lijnvolgsensoren zwarte lijnen detecteert | Ga achteruit（stel PWM in op 150）Dan draai links（stel PWM in op 150） |
|             Geen van hen detecteert zwarte lijnen              |               Ga vooruit（stel PWM in op 100）                |

#### **(2)Stroomdiagram**

![](media/b3c30f92cb78d4c2a4a8bd746aef24e1.png)

#### **(3)Aansluitingsdiagram:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/e48288f5b46e3e1c78489cb9d9b86333.png)

（3）![](media/801d176b32bc87904b8545ecf80874fc.png)

（4）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/b919eb2b47ee87ae36e21099e754e8a1.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/e656126c11bb8ebe7b6b0df8f22e7a79.png)

#### **(5)Testresultaten:**

Na het succesvol uploaden van de testcode en het inschakelen van de voeding, beweegt de slimme auto binnen een cirkel getekend met een zwarte lijn.

![](./media/img-20240117094034.png)