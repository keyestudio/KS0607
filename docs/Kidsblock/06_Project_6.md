### Progetto 6: Sensore a Ultrasuoni

#### **(1)Descrizione:**

![](media/0180b169a1c3b228394b43df704fac32.png)

Il sensore a ultrasuoni HC-SR04 utilizza il sonar per determinare la distanza da un oggetto, come fanno i pipistrelli. Offre un'eccellente rilevazione della distanza senza contatto, con alta precisione e letture stabili in un pacchetto facile da usare. È completo di moduli trasmettitore e ricevitore a ultrasuoni.

L'HC-SR04 o il sensore a ultrasuoni viene utilizzato in una vasta gamma di progetti elettronici per creare applicazioni di rilevamento degli ostacoli e misurazione della distanza, nonché varie altre applicazioni. Qui abbiamo proposto il metodo semplice per misurare la distanza con Arduino e il sensore a ultrasuoni e come utilizzare il sensore a ultrasuoni con Arduino.

![](./media/image-20250709133626194.png)

#### **(2)Parametri:**

- Alimentazione: +5V DC

- Corrente a riposo: \<2mA

- Corrente di funzionamento: 15mA

- Angolo efficace: \<15°

- Distanza di rilevamento: 2cm – 400 cm

- Risoluzione: 0.3 cm

- Angolo di misurazione: 30 gradi

- Larghezza del impulso di trigger in ingresso: 10uS

#### **(3)Il principio del sensore a ultrasuoni:**

Come mostrato nell'immagine sopra, è come due occhi. Uno è il terminale di trasmissione, l'altro è il terminale di ricezione.

Il modulo a ultrasuoni emetterà le onde ultrasoniche dopo aver ricevuto un segnale di attivazione. Quando le onde ultrasoniche incontrano l'oggetto e vengono riflesse indietro, il modulo produce un segnale eco, quindi può determinare la distanza dell'oggetto dalla differenza di tempo tra il segnale di trigger e il segnale eco.

Qui, t è il tempo da quando il segnale emesso incontra l'ostacolo a quando ritorna. La velocità di propagazione del suono nell'aria è di circa 343m/s, e distanza = velocità * tempo. Tuttavia, poiché l'onda ultrasonica percorre la distanza fino all'ostacolo e ritorna, il tempo rappresenta il doppio della distanza. Pertanto, è necessario dividere per 2. La distanza misurata dall'**onda ultrasonica = (velocità * tempo) / 2**.

1. Metodo di utilizzo e diagramma temporale del modulo a ultrasuoni:

2. Impostare il ritardo del pin Trig dell'SR04 ad almeno 10μs, il che può attivarlo per rilevare la distanza.

3. Dopo l'attivazione, il modulo invierà automaticamente otto impulsi ultrasonici a 40KHz e rileverà se c'è un segnale di ritorno. Questo passaggio verrà completato automaticamente dal modulo.

4. Se il segnale ritorna, il pin Echo produrrà un livello alto, e la durata del livello alto è il tempo dalla trasmissione dell'onda ultrasonica al ritorno.

![](media/image-20230525110337646.png)

Schema del circuito del sensore a ultrasuoni:

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4)Schema di collegamento:**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Nota sul cablaggio:</span> Il pin VCC del modulo sensore a ultrasuoni è collegato al 5v(V) della scheda di espansione del motore Keyestudio 8833, il pin Trig è collegato al digitale D12, il pin Echo è collegato al digitale D13, e il pin Gnd è collegato a Gnd(G);

#### **(5)Codice di test:**

Puoi anche trascinare blocchi per modificare il tuo codice, come mostrato di seguito.

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/128e0b4ee7d3448410d72312175bc6da.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/a6df8829b69f7faed26a73d01da8d50d.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/eca0805413af12957d319c706d3e7cdb.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Codice di test completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, il che può causare il fallimento del caricamento.)

![](media/569aff5ff2cbd2f3605f217ebb5ed50b.png)

#### **(6)Risultati del test:**

Carica il codice di test sulla scheda di sviluppo, apri il monitor seriale e imposta la velocità di trasmissione a 9600. La distanza rilevata verrà visualizzata in cm e pollici. Quando ostacoli il sensore a ultrasuoni con la tua mano, il valore della distanza visualizzato si ridurrà.

![](media/4f77acbf5b226e20e3cdd70c0f90602e.png)

#### **(7)Pratica di estensione:**

Abbiamo appena misurato la distanza visualizzata dagli ultrasuoni. Che ne dici di controllare il LED con la distanza misurata? Proviamoci e colleghiamo un modulo LED al pin D9.

![](media/291ac1db0f38418772d11bb1786b7314.png)


Puoi anche trascinare blocchi per modificare il tuo codice, come mostrato di seguito

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/49d5523ae565e1d4dfc3504d1e1748d4.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/8d5fc923f5ded5305f36b1379c1ba38e.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/a6205e42e005084c33c247fe564bdcad.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Codice di test completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, il che può causare il fallimento del caricamento.)

![](media/065eac0ad9cfa8f07aeb5e648698bdb5.png)

Carica il codice di test sulla scheda di sviluppo, avvicina la mano al sensore a ultrasuoni e verifica se il LED si accende.

![](./media/img-20240117092413.png)