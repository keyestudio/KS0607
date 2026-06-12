### Progetto 2: Regolare la Luminosità del LED

#### **(1)Descrizione:**

Nella lezione precedente, abbiamo controllato l'accensione e lo spegnimento del LED facendolo lampeggiare.

In questo progetto, controlleremo la luminosità del LED tramite PWM simulando un effetto di respirazione. Allo stesso modo, è possibile modificare la lunghezza del passo e il tempo di ritardo nel codice per ottenere diversi effetti di respirazione.

Il PWM è un mezzo per controllare l'uscita analogica tramite mezzi digitali. Il controllo digitale viene utilizzato per generare onde quadre con diversi cicli di lavoro (un segnale che cambia costantemente tra livelli alti e bassi) per controllare l'uscita analogica.

In generale, le tensioni di ingresso delle porte sono 0V e 5V. Cosa succede se è necessario il 3V? O un cambio tra 1V, 3V e 3.5V? Non possiamo cambiare le resistenze continuamente. Per questo motivo, ricorriamo al PWM.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Per le uscite di tensione delle porte digitali di Arduino, ci sono solo livelli LOW e HIGH, che corrispondono rispettivamente alle uscite di tensione di 0V e 5V. Puoi definire LOW come "0" e HIGH come "1", e lasciare che Arduino emetta cinquecento "0" o "1" in 1 secondo. Se vengono emessi cinquecento "1", equivale a 5V; se tutti sono "0", equivale a 0V; se viene emesso uno schema di 250 "01", equivale a 2.5V.

Questo processo può essere paragonato alla visione di un film. I film che guardiamo non sono completamente continui. In realtà, vengono generate 25 immagini al secondo, il che non può essere percepito dall'occhio umano. Pertanto, lo percepiamo come un processo continuo. Il PWM funziona allo stesso modo. Per produrre tensioni diverse, dobbiamo controllare il rapporto tra 0 e 1. Più "0" o "1" vengono emessi per unità di tempo, più preciso è il controllo.

#### **(2)Parametri:**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Interfaccia di controllo: Porta digitale 3

- Tensione di lavoro: DC 3.3-5V

- Passo dei pin: 2.54mm

- Colore del display LED: giallo

#### **(3)Schema di Collegamento**

I pin PWM di Arduino sono collegati a 3, 5, 6, 9, 10 e 11. Mantenere il pin9 invariato.

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito

![](media/de8ccd3cb6621f0eb89a8514a9fd8452.png)

![](media/659b8a45b8e8d271226d9a25034aedfd.png)

![](media/3157917e305c01f1920cf4d06aff4ff9.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/aaab53a06684ab078936ee61f9abcbb3.png)


#### **(5)Risultati del Test**

Dopo aver caricato il codice di test con successo, il LED cambia gradualmente da luminoso a scuro, come il respiro umano, anziché accendersi e spegnersi immediatamente.

#### **(6)Pratica di Estensione:**

Modifichiamo il valore del ritardo mantenendo il pin invariato, quindi osserviamo come cambia il LED.

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/2ff0d71c2688d39695b760a1d0f76965.png)

Carica il codice sulla scheda di sviluppo, il LED lampeggia più lentamente.