### Progetto 17: Carro Armato Controllato via Bluetooth

#### **(1)Descrizione:**

Abbiamo imparato le conoscenze di base del Bluetooth nel progetto precedente. In questa lezione, utilizzeremo il Bluetooth per controllare il robot. Poiché riguarda il Bluetooth, sono necessari un trasmettitore e un ricevitore. Nel progetto, usiamo il telefono cellulare come trasmettitore (master), e il robot connesso con il modulo Bluetooth HM-10 (slave) come ricevitore.

Abbiamo imparato in precedenza che inviare un bit può controllare i LED. Il principio per controllare questo robot è lo stesso.

Per controllare meglio il robot carro armato intelligente, abbiamo creato appositamente un'APP. In questa lezione, leggeremo tutti i valori dei tasti su questa APP tramite codice, e poi presenteremo l'APP esclusiva del nostro robot carro armato.

#### **(2)Funzioni dei Tasti sull'APP:**

La tabella seguente illustra le funzioni dei tasti corrispondenti:

|                      Tasti                       |                                                |                          Funzioni                           |
| :---------------------------------------------: | :--------------------------------------------: | :----------------------------------------------------------: |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) |                                                | Associa e connette il modulo Bluetooth HM-10; clicca di nuovo per disconnettere |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) |                                                |                 seleziona il robot da controllare                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) |                                                |       controllare i movimenti del robot tramite pulsanti       |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) |                                                |      Controllare i movimenti del robot tramite joystick       |
| ![](media/3ab61154b4ae730a3757f40171846825.png) |                                                |       Controllare i movimenti del robot tramite gravità       |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) |   Invia "F" quando premuto e "S" quando rilasciato    | Il robot si muove in avanti quando premuto e si ferma quando rilasciato |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) |   Invia "L" quando premuto e "S" quando rilasciato    | Il robot gira a sinistra quando premuto e si ferma quando rilasciato |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) |   Invia "R" quando premuto e "S" quando rilasciato    | Il robot gira a destra quando premuto e si ferma quando rilasciato |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) |   Invia "B" quando premuto e "S" quando rilasciato    | Il robot va indietro quando premuto e si ferma quando rilasciato |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) |        Invia "u"+cifra+"\#" quando trascinato         |          Trascina per cambiare la velocità del motore sinistro          |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) |        Invia "v"+cifra+"\#" quando trascinato         |         Trascina per cambiare la velocità del motore destro          |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) |         Seleziona per entrare nella pagina Funzioni          |                                                              |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Invia "G" quando premuto e "S" quando premuto di nuovo | Entra in modalità evitamento ostacoli quando premuto ed esce quando premuto di nuovo |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Invia "h" quando premuto e "S" quando premuto di nuovo | Entra in modalità inseguimento quando premuto ed esce quando premuto di nuovo |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Invia "e" quando premuto e "S" quando premuto di nuovo | Entra in modalità segui-linea quando premuto ed esce quando premuto di nuovo |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Invia "f" quando premuto e "S" quando premuto di nuovo | Entra in modalità movimento-in-spazio-confinato quando premuto ed esce quando premuto di nuovo |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Invia "i" quando premuto e "S" quando premuto di nuovo | Entra in modalità inseguimento luce quando premuto ed esce quando premuto di nuovo |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Invia "j" quando premuto e "S" quando premuto di nuovo | Entra in modalità estinzione incendio quando premuto ed esce quando premuto di nuovo |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Seleziona per entrare nella modalità visualizzazione espressioni facciali |                                                              |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Invia "k" quando premuto e "z" quando premuto di nuovo | Mostra il pattern sorridente quando cliccato e cancella l'espressione quando cliccato di nuovo |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Invia "l" quando premuto e "z" quando premuto di nuovo | Mostra il pattern di disgusto quando cliccato e cancella l'espressione quando cliccato di nuovo |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Invia "m" quando premuto e "z" quando premuto di nuovo | Mostra la faccia felice quando cliccato e cancella l'espressione quando cliccato di nuovo |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Invia "n" quando premuto e "z" quando premuto di nuovo | Mostra il pattern triste quando cliccato e cancella l'espressione quando cliccato di nuovo |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Invia "o" quando premuto e "z" quando premuto di nuovo | Mostra il pattern sprezzante quando cliccato e cancella l'espressione quando cliccato di nuovo |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Invia "p" quando premuto e "z" quando premuto di nuovo | Mostra il pattern a forma di cuore quando cliccato e cancella l'espressione quando cliccato di nuovo |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) |                                                | Scegli per entrare nell'interfaccia delle funzioni personalizzate; ci sono sei tasti 1,2,3,4,5,6; con questi tasti puoi espandere alcune funzioni da solo |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) |               Clicca per inviare "w"                | Clicca per visualizzare il valore analogico rilevato dalla fotoresistenza sinistra |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) |                Clicca per inviare "y"                | Clicca per visualizzare il valore analogico rilevato dalla fotoresistenza destra |
| ![](media/a76df707b84409e57a1167889c3510d9.png) |                Clicca per inviare "x"                | Clicca per mostrare la distanza rilevata dal sensore a ultrasuoni (unità: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Clicca per inviare "c" <br />Clicca di nuovo per inviare "d"  |   Premi per accendere il ventilatore e premi di nuovo per spegnerlo    |

#### **(3)Diagramma di Flusso:**

![](./media/image-20250709135203165.png)

#### **(4)Schema di Collegamento:**

![](media/930a8024364e07505e845624a94c27bd.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

GND, VCC, SDA e SCL del pannello LED 8x16 sono collegati a G（GND), V（5V), A4 e A5 della scheda di espansione. STATE e BRK non devono essere collegati. Il modulo BT viene inserito nella scheda di espansione.

#### **(5)Codice di Test:**

Puoi trascinare i blocchi per modificare il codice

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/3b4fb768cbf7e0b80fa55cb15aa932b7.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6) ![](media/8a13abc40d27d0470902e528b40170c3.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non connettere il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anch'esso la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/341e0a01bd6a76edb53f9414ef641a75.png)

#### **(6)Risultato del Test:**

Dopo aver caricato il codice, connetti il robot al modulo Bluetooth e associa l'APP Bluetooth. Accendi l'interruttore di alimentazione dello shield per motori. Posiziona il robot sul pavimento, puoi usare questi pulsanti dell'app Bluetooth per controllare il robot.

![](media/352d5ec83c4246b980da10b5f99711c5.jpeg)

1. Le frecce su, giù, sinistra e destra controllano rispettivamente il robot per muoversi in avanti, indietro, a sinistra e a destra.

![](./media/img-20240117095015.png)

2. Clicca il pulsante joystick e trascina la direzione del punto nero nel cerchio bianco per controllare la direzione di movimento del robot.

![](./media/img-20240117095052.png)

3. Clicca il pulsante Gravità e inclina il telefono nelle direzioni avanti, indietro, sinistra e destra, e il robot si muoverà nella direzione in cui il telefono è inclinato.

![](./media/img-20240117095131.png)