### Progetto 1: LED Lampeggiante

#### (1)Descrizione：

![](./media/image-20250709122631704.png)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Per i principianti e gli appassionati, il LED lampeggiante è un programma fondamentale. LED, abbreviazione di diodi emettitori di luce, è composto da composti chimici Ga, As, P, N e così via. Il LED può lampeggiare in diversi colori modificando il tempo di ritardo nel codice di test. Durante il controllo, alimentare GND e VCC. Il LED si accende se il pin S è a livello alto; altrimenti si spegne.

#### **(2)Parametri:**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Interfaccia di controllo: porta digitale
- Tensione di lavoro: DC 3.3-5V
- Passo tra i pin: 2.54mm
- Colore del display LED: giallo

#### (3)Componenti Necessari:

![](./media/image-20250709122437613.png)

#### **(4)Scheda di Espansione Motor Driver 8833:**

La scheda di espansione motor driver Keyestudio 8833 è compatibile con la scheda di sviluppo Arduino UNO. È sufficiente inserirla sulla scheda di sviluppo durante l'utilizzo.

![](media/d8696e83ade31f2b7c56cc5911eacbd7.GIF)

#### **(5)Schema di Collegamento:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](./media/image-20250709122655936.png)

<span style="color: rgb(255, 76, 65);">**NOTA:**</span> Il LED è collegato alla porta D9. Ricordarsi di installare i cappucci jumper sullo shield.

#### **(6)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito.

![](media/cc43ba357acb68a4961adb7e5041b6fe.png)

![](media/26b69cd46ad24e1c900c4fb316430353.png)

![](media/21dc3c24da4271aa7ec2bfdac732eeb3.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/ba4723bab640078eccbe1811da138bc3.png)

#### **(7)Risultati del Test:**

Carica il programma: il LED lampeggia con un intervallo di 1s.

#### **(8)Pratica di Approfondimento:**

Abbiamo imparato come controllare il LED, ora modifichiamo la frequenza del LED.

Possiamo cambiare la frequenza del LED senza modificare il pin del LED. Modifichiamo il codice.

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito.

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/58c76be4c719a885afb500e8f3b80b85.png)

Il risultato del test mostra che il LED lampeggia più velocemente. Pertanto, possiamo concludere che i pin e il ritardo temporale influenzano la frequenza di lampeggio.