### Progetto 22: Robot Antincendio con Funzioni Multiple

#### **(1)Descrizione:**

Il veicolo intelligente ha eseguito una singola funzione in ogni progetto precedente.

Può mostrare più funzioni contemporaneamente? Sì, può farlo.

In questo ultimo grande progetto, intendiamo utilizzare un codice completo per controllare il veicolo intelligente e dimostrare tutte le funzioni menzionate nei progetti precedenti. Utilizziamo i tasti dell'APP Bluetooth per passare automaticamente da una funzione all'altra, il che è abbastanza semplice e conveniente.

#### **(2)Diagramma di Flusso:**

<span style="color: rgb(255, 76, 65);">**Fare riferimento al Progetto 16 per installare e configurare l'APP Bluetooth**</span>

![](media/wps122.png)

#### **(3)Schema di Collegamento:**

![](media/e7ac834ba04aa2e8862995d2d33ce935.png)

1\. GND, VCC, SDA e SCL della scheda 8x16 sono collegati a G (GND), + (VCC), A4 e A5 della scheda di espansione.

2\. VCC, IN+, IN- e Gnd del modulo ventola sono collegati a 5V (V), 12 (S), 13 (S) e Gnd (G).

3\. Il filo marrone, il filo rosso e il filo arancione del servo sono collegati a Gnd (G), 5v (V) e D10.

4\. RXD, TXD, GND e VCC del modulo BT sono collegati a TX, RX, G (GND) e 5V (VCC). STATE e BRK non devono essere collegati.

5\. I pin "G", "V" e A del sensore di fiamma sinistro sono collegati rispettivamente a G (GND), V (VCC) e A1; il sensore di fiamma destro è collegato a G (GND), V (VCC) e A2, rispettivamente.

6\. Le porte distali del sensore di rilevamento linea sono 11, 7 e 8.

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando un fallimento del caricamento.)
<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non è possibile accelerare il veicolo tramite l'App.

![](media/b1527b806741e28e8f2af5107db505fe.png)


#### **(5)Risultato del Test:**

Prima di caricare il codice del programma, il modulo Bluetooth deve essere rimosso; altrimenti, il caricamento del codice fallirà.

Dopo aver caricato il codice con successo, attivare i servizi di localizzazione sul dispositivo, quindi collegare il modulo Bluetooth.

Una volta che il modulo Bluetooth è inserito e alimentato, e l'APP mobile è collegata con successo al Bluetooth, possiamo utilizzare l'APP mobile per controllare il robot cingolato.

![](media/13656cfee75dc5acbeba18a90a084e159.jpg)