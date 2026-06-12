### Progetto 3: Fotoresistore

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Descrizione:**

Il resistore fotosensibile è un resistore speciale realizzato con un materiale semiconduttore come un solfuro o il selenio, e viene applicata anche una resina impermeabile all'umidità con effetto fotoconduttivo. Il resistore fotosensibile è molto sensibile alla luce ambientale; con diverse intensità di illuminazione, la resistenza del resistore fotosensibile cambia. Utilizziamo il resistore fotosensibile per progettare il modulo del resistore fotosensibile.

Il segnale del modulo è collegato alla porta analogica del microcontrollore. Quando l'intensità della luce è maggiore, la tensione della porta analogica è più alta, ovvero anche il valore di simulazione del microcontrollore è più grande; al contrario, quando l'intensità della luce è minore, la tensione della porta analogica è più bassa, ovvero anche il valore di simulazione del microcontrollore è più piccolo.

In questo modo, possiamo leggere il valore analogico corrispondente utilizzando il modulo del resistore fotosensibile e rilevare l'intensità della luce nell'ambiente.

![](./media/image-20250709122809574.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Parametri:**

- Valore di resistenza del resistore fotosensibile: 5K Ω - 0.5M

- Tipo di interfaccia: porta di simulazione A0, A1

- Tensione di lavoro: 3.3V-5V

- Spaziatura dei pin: 2.54mm

#### **(3)Schema di collegamento:**

Quello che testeremo di seguito è il modulo fotoresistore sul lato sinistro del robot.

![](./media/img-20240117091730.png)

Il fotoresistore sinistro è collegato ad A1/P3 dello shield di controllo motore.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)


#### **(4)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il codice, come mostrato di seguito.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/f29c7da2238bcc2bc70cb4b2c773b50d.png)

#### **(5)Risultati del Test:**

Carica il codice sulla scheda di sviluppo. Clicca su ![](media/9011f20d83897d7a5936793c4ae142fc.png) per impostare il baud rate a 9600. Quando lo si copre con la mano, il valore diminuisce; se non lo si copre, il valore aumenta.

![](media/53e2fc37ee5bb2c6ec187c309c431c47.png)



#### **(6)Pratica di Approfondimento:**

Il codice sopra si limita a leggere il valore del fotoresistore. Possiamo combinare il fotoresistore con un LED per modificare il comportamento del LED. Che ne dici di controllare la luminosità del LED tramite di esso?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

Il PWM può cambiare la luminosità del LED, ovvero il LED deve essere collegato al PWM della scheda di sviluppo.

Collega il LED a D9 e lascia invariati gli altri pin, poi modifichiamo il codice.

Puoi anche trascinare i blocchi per modificare il codice, come mostrato di seguito.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/b94c3789429c5fed4fd38467cb9792dd.png)

![](media/9ecdfd77e2a69dea5a8df04e7d56a13a.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/b23bcae806e8e27382b162909d30f3c0.png)

Carica il codice sulla scheda di sviluppo, premiamo sul fotoresistore per vedere se la luminosità del LED è cambiata.

![](./media/img-20240117091759.png)