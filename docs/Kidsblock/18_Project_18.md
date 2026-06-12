### Progetto 18: Robot Carro Armato a Ultrasuoni - Funzioni Multiple

#### **(1)Descrizione:**

Il robot auto intelligente ha eseguito una singola funzione in ogni progetto precedente.

Può visualizzare più funzioni contemporaneamente? Sì, può farlo.

In questo ultimo grande progetto, intendiamo utilizzare un codice completo per controllare il robot auto intelligente e dimostrare tutte le funzioni menzionate nei progetti precedenti. Utilizziamo i tasti sull'APP Bluetooth per passare automaticamente tra le varie funzioni, il che è abbastanza semplice e conveniente.

#### **(2)Diagramma di Flusso:**

![](media/wps122.png)

#### **(3)Schema di Collegamento:**

![](media/e7ac834ba04aa2e8862995d2d33ce935.png)

1\. GND, VCC, SDA e SCL della scheda 8x16 sono collegati a G (GND), + (VCC), A4 e A5 della scheda di espansione.

2\. VCC, Trig, Echo e Gnd del sensore a ultrasuoni sono collegati a 5V (V), 12 (S), 13 (S) e Gnd (G).

3\. Il filo marrone, il filo rosso e il filo arancione del servo sono collegati a Gnd (G), 5v (V) e D10.

4\. RXD, TXD, GND e VCC del modulo BT sono collegati a TX, RX, G (GND) e 5V (VCC). STATE e BRK non devono essere collegati.

5\. I pin "G", "V" e S del modulo fotoresistore sinistro sono collegati rispettivamente a G (GND), V (VCC) e A1; Il modulo fotoresistore destro è collegato rispettivamente a G (GND), V (VCC) e A2.

6\. Le porte distali del sensore di rilevamento linea sono 11, 7 e 8.

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non è possibile accelerare il robot tramite l'App.

![](media/e3c4c6cf504b1b9ea6fbae63f5fd9077.png)

#### **(5)Risultato del Test:**

Prima di caricare il codice del programma, il modulo Bluetooth deve essere rimosso; altrimenti il caricamento del codice fallirà.

Dopo aver caricato il codice con successo, attivare i servizi di localizzazione sul dispositivo, quindi collegare il modulo Bluetooth.

Una volta che il modulo Bluetooth è inserito e alimentato, e l'APP mobile è connessa con successo al Bluetooth, possiamo utilizzare l'APP mobile per controllare il robot carro armato.