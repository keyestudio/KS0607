### Progetto 14: Robot Cingolato Segui-Linea


#### **(1)Descrizione:**

Il progetto precedente ha illustrato come confinare l'auto intelligente in modo che si muova all'interno di un determinato spazio. In questo progetto, utilizzeremo le conoscenze apprese in precedenza per trasformarlo in un'auto intelligente segui-linea. Nell'esperimento, utilizziamo il sensore di rilevamento della linea per rilevare se c'è una linea nera intorno all'auto intelligente, e poi controlliamo la rotazione dei due motori in base ai risultati del rilevamento, in modo da far muovere l'auto intelligente lungo la linea nera.

La logica specifica dell'auto intelligente è mostrata nella tabella seguente:

|               Sensore               |                          Rilevamento                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Sensore di rilevamento linea al centro | Linea nera rilevata: livello alto<br />Linea bianca rilevata: livello basso |
|  Sensore di rilevamento linea a sinistra  | Linea nera rilevata: livello alto<br />Linea bianca rilevata: livello basso |
| Sensore di rilevamento linea a destra  | Linea nera rilevata: livello alto<br />Linea bianca rilevata: livello basso |

|                         Condizione 1                          |                         Condizione 2                          |   Movimento   |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------: |
| Il sensore di rilevamento linea <br />al centro <br />rileva la linea nera | Il sensore di rilevamento linea a sinistra rileva la linea nera<br />quello a destra rileva linee bianche | Ruota a sinistra  |
| Il sensore di rilevamento linea <br />al centro <br />rileva la linea nera | Il sensore di rilevamento linea a sinistra rileva linee bianche<br />quello a destra rileva la linea nera | Ruota a destra |
| Il sensore di rilevamento linea <br />al centro <br />rileva la linea nera | Entrambi i sensori sinistro e destro rilevano linee bianche<br />Entrambi i sensori sinistro e destro rilevano la linea nera | Avanza |
| Il sensore di rilevamento linea<br />al centro <br />rileva linee bianche | Il sensore di rilevamento linea a sinistra rileva la linea nera<br />quello a destra rileva linee bianche | Ruota a sinistra  |
| Il sensore di rilevamento linea<br />al centro <br />rileva linee bianche | Il sensore di rilevamento linea a sinistra rileva linee bianche<br />quello a destra rileva la linea nera | Ruota a destra |
| Il sensore di rilevamento linea<br />al centro <br />rileva linee bianche | Entrambi i sensori sinistro e destro rilevano linee bianche<br />Entrambi i sensori sinistro e destro rilevano la linea nera |     Stop     |

#### **(2)Diagramma di flusso:**

![](media/wps11.png)

#### **(3)Schema di collegamento:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

（7）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（8）![](media/fec93c7b8b089de709fd50575931519c.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/294ae4c01072e34b58a334912c90083a.png)


#### **(5)Risultati del Test:**

Dopo aver caricato con successo il codice di test e aver alimentato il dispositivo, l'auto intelligente si muove lungo la linea nera.

![](./media/img-20240117094129.png)