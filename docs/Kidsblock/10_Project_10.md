### Progetto 10: Tank Insegui-Luce


#### **(1)Descrizione:**

Nei progetti precedenti, abbiamo introdotto in dettaglio l'uso di vari sensori, moduli e schede di espansione sul robot smart car. Ora passiamo ai progetti del robot smart car. I robot smart car insegui-luce, come suggerisce il nome, sono robot smart car in grado di seguire la luce.

Possiamo combinare le conoscenze dei progetti sul fotoresistore e sul driver motore per realizzare un robot smart car che cerca la luce. Nel progetto, utilizziamo due moduli fotoresistore per rilevare l'intensità luminosa sul lato sinistro e destro del robot smart car, leggiamo i valori analogici corrispondenti e quindi controlliamo la rotazione dei due motori in base a questi due dati in modo da controllare i movimenti del robot smart car.

La logica specifica del robot smart car insegui-luce è mostrata di seguito.

![image-20230525113331422](media/image-20230525113331422.png)

#### **(2)Diagramma di flusso:**

![](media/wps117.png)

#### **(3)Schema di collegamento:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Nota: </span>I pin "G", "V" e S del modulo fotoresistore sinistro sono collegati rispettivamente a G (GND), V (VCC), A1;

I pin "G", "V" e S del modulo fotoresistore destro sono collegati rispettivamente a G (GND), V (VCC) e A2.

Il cavo a 4 pin è contrassegnato con A, A1, B1 e B. Il motore posteriore destro è collegato alla porta B della scheda di espansione driver motore 8833 e il motore anteriore sinistro è collegato alla porta A della scheda di espansione driver motore 8833.

#### **(4)Codice di Test:**


Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito.

（1）![](media/9352e6447f9648efddc7d5a748618332.png)

（2）![](media/1d99d71f5fe52dd2145cb11d75cabb21.png)

（3）![](media/5004e509325dffb32c05afe25abedfc9.png)

（4）![](media/6c6f0492f657c4c78a0497bb86519561.png)

（5）![](media/b8fc70fa8b3f335dcdf0c8ad9ed998c6.png)

（6）![](media/9eb0e93fbd43aa24f2ce656191f7cd79.png)

(7) ![](media/9f023e6f571e597e661a8d71a7f803cb.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">Nota:</span> La soglia 650 nel codice può essere regolata opportunamente in base all'intensità luminosa specifica.

Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anch'esso la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale del Bluetooth, causando il fallimento del caricamento del codice.)

![](media/6300174b85f63c05dbdcb3b77188f9dc.png)


#### **(5)Risultati del Test:**

Dopo aver caricato con successo il codice di test, effettuare i collegamenti, portare il selettore DIP sull'estremità ON e accendere il dispositivo: il robot smart car seguirà la luce per muoversi.

![](./media/img-20240117093758.png)