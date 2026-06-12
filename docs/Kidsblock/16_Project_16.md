### Progetto 16: Controllo Remoto Bluetooth

![](./media/image-20250709134858245.png)

#### **(1)Descrizione:**

Negli ultimi decenni, il Bluetooth è diventato il modulo di comunicazione wireless più popolare perché è facile da usare e ha trovato ampie applicazioni nella maggior parte dei dispositivi alimentati a batteria.

Per adattarsi ai tempi, alla realtà e alle esigenze dei clienti, il Bluetooth è stato aggiornato più volte. Negli ultimi anni, ha subito molte trasformazioni in termini di velocità di trasferimento dati, consumo energetico dei dispositivi indossabili e dispositivi IoT, sistemi di sicurezza e altro ancora. Qui, abbiamo intenzione di apprendere l'uso del DX-BT24 con la scheda Arduino.

#### **(2)Parametri:**

- Protocollo Bluetooth: Bluetooth Specification V5.1 BLE
- Distanza di funzionamento: In un ambiente aperto, raggiunge una distanza ultra-lunga di 40m
- Frequenza operativa di comunicazione: Banda ISM 2.4GHz
- Interfaccia di comunicazione: UART
- Certificazione Bluetooth: conforme agli standard di certificazione FCC CE ROHS REACH
- Parametri della porta seriale: 9600, 8 bit di dati, 1 bit di stop, bit non valido, nessun controllo di flusso
- Alimentazione: 5V DC
- Temperatura operativa: da –10 a +65 gradi Celsius


#### **(3)Applicazioni:**

Il modulo DX-BT24 supporta anche il protocollo BT5.1 BLE, che può essere connesso direttamente a dispositivi iOS con funzione Bluetooth BLE, e supporta l'esecuzione in background dei programmi. Principalmente utilizzato nel campo della trasmissione dati wireless a corta distanza. Evita ingombranti connessioni via cavo e può sostituire direttamente i cavi seriali. Aree di applicazione di successo dei moduli BT24:

※ Trasmissione dati wireless Bluetooth;

※ Telefoni cellulari, periferiche per computer;

※ Dispositivi POS portatili;

※ Trasmissione dati wireless di apparecchiature mediche;

※ Controllo smart home;

※ Stampanti Bluetooth;

※ Giocattoli con telecomando Bluetooth;

※ Biciclette condivise;

#### **(4)Descrizione dei pin:**

![](media/cd97cf79ff5cdd5bbd78f4cc960d38e5.png)

①STATE：pin di stato

②RX：pin di ricezione

③TX：pin di trasmissione

④GND：messa a terra

⑤VCC：pin di alimentazione

⑥EN：pin di abilitazione

Collegare il Bluetooth alla scheda di sviluppo

| Uno  | BT24 |
| :--: | :--: |
|  TX  |  RX  |
|  RX  |  TX  |
| VCC  |  5V  |
| GND  | GND  |

#### **(5)Schema di Collegamento:**

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)

#### **(6)Scarica l'APP:**

##### **Per sistema iOS**

1\. Apri App Store.

2\. Cerca <span style="color: rgb(61, 167, 66);">KeyesRobot</span> nell'Apple Store e clicca su scarica.

![](./media/img-20240111141301.png)

3\. Dopo aver installato l'app, vedrai la seguente icona sul desktop del tuo telefono.

![](./media/img-20240111141412.png)

**Come connettere il telefono iOS al modulo Bluetooth:**

1\. Attiva il Bluetooth e i servizi di localizzazione sul telefono tramite le impostazioni.

![](./media/img-20240111141943.png)

2\. Consenti all'APP KeyesRobot di accedere al Bluetooth tramite le impostazioni.

![](./media/img-20240111142052.png)

3\. Clicca per aprire l'app KeyesRobot.

![](./media/img-20240111142140.png)

4\. KeyesRobot App è un'APP universale, applicata a più robot keyestudio. Se l'interfaccia non mostra "TANK ROBOT", puoi cliccare i pulsanti sinistra e destra per trovare "TANK ROBOT".

5\. Clicca il <span style="color: rgb(61, 167, 66);">pulsante Bluetooth</span>![](./media/img-20240111142336.png) nell'angolo in alto a destra per scansionare il bluetooth

![](./media/img-20240111142415.png)

6\. Vedrai un Bluetooth di nome <span style="color: rgb(0, 209, 0);">**BT24**</span>, clicca il pulsante <span style="color: rgb(255, 169, 0);">Connect</span>.

![](./media/img-20240111142536.png)

7\. Se il LED integrato sul modulo Bluetooth smette di lampeggiare e rimane acceso, significa che il tuo telefono è connesso con successo al modulo Bluetooth.

![](./media/img-20240111142702.png)


##### **Per sistema Android**

1\. Cerca <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> in Google Play, o apri il seguente link per scaricare e installare l'app.

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Attiva il Bluetooth e i servizi di localizzazione del telefono cellulare

![](./media/img-20240111143354.png)

3\. Trova l'app Bluetooth KeyesRobot dalle impostazioni, clicca sulle opzioni di autorizzazione dell'app e abilita i permessi per la Posizione e i dispositivi nelle vicinanze. (<span style="color: rgb(255, 76, 65);">Nota:</span> Alcuni telefoni cellulari non hanno la funzione dei permessi per i dispositivi nelle vicinanze.)

![](./media/img-20240111143451.png)

4\. Clicca per aprire l'app KeyesRobot.

![](./media/img-20240111143529.png)

5\. KeyesRobot App è un'APP universale, applicata a più robot keyestudio. Se l'interfaccia non mostra "TANK ROBOT", puoi cliccare i pulsanti sinistra e destra per trovare "TANK ROBOT".

6\. Clicca il <span style="color: rgb(61, 167, 66);">pulsante Bluetooth</span>![](./media/img-20240111142336.png) nell'angolo in alto a destra per scansionare il bluetooth

![](./media/img-20240111142415.png)

7\. Vedrai un Bluetooth di nome <span style="color: rgb(0, 209, 0);">**BT24**</span>, clicca il pulsante <span style="color: rgb(255, 169, 0);">Connect</span>.![](./media/img-20240111143910.png)

8\. Quando il tuo telefono è connesso con successo al modulo Bluetooth, il LED integrato sul modulo Bluetooth smetterà di lampeggiare e rimarrà acceso.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(7)Codice di Test BT:**

Puoi anche trascinare blocchi per modificare il tuo codice, come mostrato di seguito

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/19a90ffb7565966f7d40462abed876a7.png)

（5）![](media/c8228c5040a43ae322612b312c995ac3.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/4766ada3bf48bb35522f292d9352bb78.png)


Carica il codice sulla scheda di sviluppo, poi collega il modulo Bluetooth, e quindi connetti il telefono cellulare al modulo Bluetooth.

Dopo che il telefono cellulare è stato connesso con successo al modulo Bluetooth, clicca per aprire l'APP Bluetooth e clicca il pulsante <span style="color: rgb(0, 252, 255);">Select</span> sulla <span style="color: rgb(0, 252, 255);">homepage</span>.

![](./media/img-20240111144744.png)

L'interfaccia principale dell'app Bluetooth è mostrata nella figura seguente.

![](./media/img-20240111144859.png)

Clicca ![Img](./media/img-20240111171312.png) e imposta il baud rate a 9600. Clicca l'icona sull'interfaccia dell'APP e il monitor seriale mostrerà il comando inviato dal pulsante.

![](media/f5004f5334fb4885ac0096f99e4133f9.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Nota: Il metodo di connessione dell'APP è lo stesso di seguito.**</span>
<br>
<br>


#### **(8)Pratica Estensiva:**

Nel progetto precedente, il Bluetooth riceve il segnale inviato dal telefono cellulare e lo visualizza sulla porta seriale della scheda di sviluppo. Qui utilizziamo il comando inviato dal telefono cellulare per accendere o spegnere un LED. Osservando il diagramma di cablaggio, un LED è collegato al pin D9,

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)


Puoi anche trascinare blocchi per modificare il tuo codice, come mostrato di seguito

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/aa78663af261ff1d9bc8ffa6ad7a65bc.png)

(5）![](media/c8228c5040a43ae322612b312c995ac3.png)

（6）![](media/4164bcf66d3d2415f43a0efcd1ce4243.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/91fd9d6f85e291fe90a63e5095ed7f44.png)

Dopo che il codice precedente è stato caricato con successo. Clicca ![](media/d5e59839bafc63f8b35c78c60573d1fc.png) per controllare il LED.

![](./media/img-20240117094418.png)


Dopo aver completato il progetto BT, rimuoverlo.