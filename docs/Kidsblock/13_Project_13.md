### Progetto 13: Serbatoio di Movimento in Spazio Confinato


#### **(1)Descrizione:**

Le funzioni di inseguimento degli ultrasuoni e di evitamento degli ostacoli dell'auto intelligente sono state introdotte nei progetti precedenti. Qui, intendiamo combinare le conoscenze dei corsi precedenti per confinare l'auto intelligente a muoversi all'interno di un determinato spazio. Nell'esperimento, utilizziamo il sensore di rilevamento della linea per rilevare se c'è una linea nera intorno all'auto intelligente, e poi controlliamo la rotazione dei due motori in base ai risultati del rilevamento, in modo da bloccare l'auto intelligente all'interno di un cerchio disegnato con una linea nera.

La logica specifica dell'auto intelligente è mostrata nella tabella seguente:

![](media/image-20230525114604923.png)

|                         Condizione                         |                         Movimento                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Se uno dei tre sensori di rilevamento della linea rileva linee nere | Vai indietro（imposta PWM a 150）Poi gira a sinistra（imposta PWM a 150） |
|             Nessuno di essi rileva linee nere              |               Vai avanti（imposta PWM a 100）                |

#### **(2)Diagramma di flusso**

![](media/b3c30f92cb78d4c2a4a8bd746aef24e1.png)

#### **(3)Schema di collegamento:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/e48288f5b46e3e1c78489cb9d9b86333.png)

（3）![](media/801d176b32bc87904b8545ecf80874fc.png)

（4）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/b919eb2b47ee87ae36e21099e754e8a1.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/e656126c11bb8ebe7b6b0df8f22e7a79.png)

#### **(5)Risultati del Test:**

Dopo aver caricato con successo il codice di test e aver alimentato il dispositivo, l'auto intelligente si muove all'interno di un cerchio disegnato con una linea nera.

![](./media/img-20240117094034.png)