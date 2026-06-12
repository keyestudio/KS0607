### Project 5: Servo Besturing

#### **(1)Beschrijving:**

Een servomotor is een roterende actuator voor positieregeling. Het bestaat voornamelijk uit een behuizing, een printplaat, een kernloze motor, een tandwiel en een positiesensor. Het werkingsprincipe is dat de servo het signaal ontvangt dat door de MCU of ontvanger wordt verzonden en een referentiesignaal produceert met een periode van 20ms en een breedte van 1,5ms. Vervolgens vergelijkt het de verkregen DC-spanningsoffset met de spanning van de potentiometer en verkrijgt het de spanningsverschil-uitvoer.

Wanneer de motorsnelheid constant is, wordt de potentiometer via het trapsgewijs reductietandwiel aangedreven om te draaien, waardoor het spanningsverschil 0 wordt en de motor stopt met draaien. Over het algemeen is het hoekbereik van servorotatie 0° --180°.

De rotatiehoek van de servomotor wordt geregeld door de duty cycle van het PWM-signaal (Pulse-Width Modulation) aan te passen. De standaardcyclus van het PWM-signaal is 20ms (50Hz). Theoretisch is de breedte verdeeld tussen 1ms-2ms, maar in de praktijk is het tussen 0,5ms-2,5ms. De breedte correspondeert met de rotatiehoek van 0° tot 180°. Let op: voor verschillende merkmotoren kan hetzelfde signaal resulteren in verschillende rotatiehoeken.

![](media/69be958142b773acdae33eeef12afed7.png)

Over het algemeen heeft een servo drie draden in bruin, rood en oranje. De bruine draad is geaard, de rode is een positieve poolleiding en de oranje is een signaaldraad.

![](media/49467dfa70799401a5a5acc691014aee.png)

De hoek van de servo:

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Parameters:**

- Werkspanning: DC 4,8V \~ 6V

- Werkhoekbereik: ongeveer 180° (bij 500 → 2500 μsec)

- Pulsbreedte bereik: 500 → 2500 μsec

- Onbelaste snelheid: 0,12 ± 0,01 sec / 60 (DC 4,8V) 0,1 ± 0,01 sec / 60 (DC 6V)

- Onbelaste stroom: 200 ± 20mA (DC 4,8V) 220 ± 20mA (DC 6V)

- Stoppend koppel: 1,3 ± 0,01kg · cm (DC 4,8V) 1,5 ± 0,1kg · cm (DC 6V)

- Stoorstroom: ≦ 850mA (DC 4,8V) ≦ 1000mA (DC 6V)

- Standbystroom: 3 ± 1mA (DC 4,8V) 4 ± 1mA (DC 6V)

#### **(3)Aansluitschema:**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> De bruine, rode en oranje draden van de servo zijn respectievelijk aangesloten op Gnd(G), 5v(V) en D10 van het shield. Vergeet niet een externe voeding aan te sluiten vanwege de hoge stroom van de servo. Anders wordt het ontwikkelbord beschadigd.

#### **(4)Testcode:**

U kunt ook blokken slepen om uw code te bewerken, zoals hieronder weergegeven

![](media/5b04350e0310955ee2ecd48338f556a3.png)

![](media/7dd97d17b785de17e6c9362fa32e2a74.png)

![](media/69724a2063fa25e0f142e1eb48efd40f.png)

![](media/e149b45054fe94196dea220b319cb0bf.png)

**Volledige Testcode**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er kunnen conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden kan mislukken.)

![](media/26e37037daf84d69320b76dd13346cd1.png)

#### **(6)Testresultaten:**

Upload de code, sluit de voeding aan en de servo beweegt in het bereik van 0° en 180°.

![](./media/img-20240117092225.png)