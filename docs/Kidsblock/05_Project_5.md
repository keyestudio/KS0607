### Progetto 5: Controllo del Servomotore

#### **(1)Descrizione:**

Un servomotore è un attuatore rotante per il controllo della posizione. È composto principalmente da un alloggiamento, una scheda circuito, un motore senza nucleo, un ingranaggio e un sensore di posizione. Il suo principio di funzionamento è che il servo riceve il segnale inviato dal MCU o dal ricevitore e produce un segnale di riferimento con un periodo di 20ms e una larghezza di 1,5ms. Confronta quindi la tensione di polarizzazione CC acquisita con la tensione del potenziometro e ottiene l'uscita della differenza di tensione.

Quando la velocità del motore è costante, il potenziometro viene azionato a ruotare attraverso l'ingranaggio di riduzione a cascata, il che porta la differenza di tensione a 0 e il motore si ferma. In generale, l'angolo di rotazione del servo è compreso tra 0° e 180°.

L'angolo di rotazione del servomotore è controllato regolando il ciclo di lavoro del segnale PWM (Pulse-Width Modulation). Il ciclo standard del segnale PWM è 20ms (50Hz). Teoricamente, la larghezza è distribuita tra 1ms-2ms, ma in realtà è tra 0,5ms-2,5ms. La larghezza corrisponde all'angolo di rotazione da 0° a 180°. Si noti che per motori di marchi diversi, lo stesso segnale può risultare in angoli di rotazione diversi.

![](media/69be958142b773acdae33eeef12afed7.png)

In generale, il servo ha tre fili: marrone, rosso e arancione. Il filo marrone è la massa, quello rosso è il polo positivo e quello arancione è il filo del segnale.

![](media/49467dfa70799401a5a5acc691014aee.png)

L'angolo del servo:

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Parametri:**

- Tensione di lavoro: DC 4,8V \~ 6V

- Intervallo angolo operativo: circa 180° (a 500 → 2500 μsec)

- Intervallo larghezza impulso: 500 → 2500 μsec

- Velocità a vuoto: 0,12 ± 0,01 sec / 60 (DC 4,8V) 0,1 ± 0,01 sec / 60 (DC 6V)

- Corrente a vuoto: 200 ± 20mA (DC 4,8V) 220 ± 20mA (DC 6V)

- Coppia di stallo: 1,3 ± 0,01kg · cm (DC 4,8V) 1,5 ± 0,1kg · cm (DC 6V)

- Corrente di stallo: ≦ 850mA (DC 4,8V) ≦ 1000mA (DC 6V)

- Corrente in standby: 3 ± 1mA (DC 4,8V) 4 ± 1mA (DC 6V)

#### **(3)Schema di Collegamento:**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span> I fili marrone, rosso e arancione del servo sono collegati rispettivamente a Gnd(G), 5v(V) e D10 dello shield. Ricordare di collegare un'alimentazione esterna a causa dell'elevata corrente del servo. In caso contrario, la scheda di sviluppo potrebbe bruciarsi.

#### **(4)Codice di Test:**

È possibile anche trascinare i blocchi per modificare il codice, come mostrato di seguito

![](media/5b04350e0310955ee2ecd48338f556a3.png)

![](media/7dd97d17b785de17e6c9362fa32e2a74.png)

![](media/69724a2063fa25e0f142e1eb48efd40f.png)

![](media/e149b45054fe94196dea220b319cb0bf.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/26e37037daf84d69320b76dd13346cd1.png)

#### **(6)Risultati del Test:**

Caricare il codice, collegare l'alimentazione e il servo si muove nell'intervallo tra 0° e 180°.

![](./media/img-20240117092225.png)