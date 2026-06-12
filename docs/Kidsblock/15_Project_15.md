### Progetto 15: Tank con Telecomando IR

![](./media/image-20250709134800790.png)

#### **(1)Descrizione:**

Il telecomando a infrarossi è una delle applicazioni di controllo remoto più comuni, presente in motori elettrici, ventilatori elettrici e molti altri elettrodomestici. In questo progetto, utilizziamo le conoscenze apprese in precedenza per realizzare una macchina intelligente con telecomando a infrarossi.

Nella 9ª lezione, abbiamo testato il valore corrispondente di ogni tasto del telecomando a infrarossi. In questo progetto, possiamo impostare il codice (valore del tasto) per far sì che il pulsante corrispondente controlli i movimenti della macchina intelligente, e visualizzare i pattern di movimento sulla matrice LED 8X16.

La logica specifica della macchina intelligente è mostrata nella tabella seguente:

|                 Tasto ultrasonico                  | Valore tasto | Istruzioni dai tasti                                         |
| :------------------------------------------------: | :----------: | ------------------------------------------------------------ |
| ![](media/b11dc5ffa6cccebc6088e5d557d76daf.png)   |   FF629D     | Muovi avanti（imposta PWM a 200）<br />visualizza il pattern di avanzamento |
| ![](media/ae8110034aacb083151cfd882ee599ba.png)   |   FFA857     | Vai indietro（imposta PWM a 200）<br />visualizza il pattern di retromarcia |
| ![](media/bce9cba2c6d2465fbcce570ad4210eba.png)   |   FF22DD     | Gira a sinistra<br />visualizza il pattern"STOP"             |
| ![](media/ad907a618af86f30d52986bbbd57ba76.png)   |   FFC23D     | Gira a destra<br />visualizza il pattern di svolta a sinistra |
| ![](media/9716a4ed61a4064d2f47a7b73eccaf87.png)   |   FF02FD     | Fermati<br />visualizza il pattern"STOP"                     |

**Impostazione iniziale: la matrice LED 8X16 mostra il pattern"![](media/dc59c5fcb4fcf6af4d4a5ebb14b7a919.png)"**



#### **(2)Diagramma di flusso:**

![](media/wps121.png)

#### **(3)Schema di collegamento:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

GND, VCC, SDA e SCL del pannello LED 8x16 sono collegati a G（GND), V（VCC). A4 e A5 della scheda di espansione.

Poiché la scheda 8833 integra il ricevitore IR, non è necessario collegarlo. I pin del ricevitore IR sono G（GND), V（VCC) e D3.

#### **(4)Codice di test:**

Puoi modificare i blocchi per costruire il tuo codice

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/a9042e77ebe3009fbb7653bef3429b66.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6）![](media/51e30aa2aca3a7da67ee4f0f81c7dad1.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/7ab62148fa2a23259b8039475978d8fc.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Codice di test completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/fae6c22640ced038daca9cb6721ab95e.png)

#### **(5)Risultati del test:**

Dopo aver caricato con successo il codice di test e aver fornito alimentazione, la macchina intelligente può essere controllata nel movimento tramite il telecomando IR e la matrice 8\*16 mostra i pattern corrispondenti ai suoi movimenti.

![](./media/img-20240117094223.png)