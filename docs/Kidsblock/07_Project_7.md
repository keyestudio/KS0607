### Progetto 7: Ricezione IR

#### **(1)Descrizione:**

![](./media/image-20250709133757050.png)

Non c'è dubbio che il telecomando a infrarossi sia onnipresente nella vita quotidiana. Viene utilizzato per controllare vari elettrodomestici, come televisori, stereo, videoregistratori e ricevitori di segnale satellitare. Il controllo remoto a infrarossi è composto da un sistema di trasmissione e da un sistema di ricezione a infrarossi, ovvero un telecomando a infrarossi, un modulo ricevitore a infrarossi e un microcontrollore in grado di decodificare il segnale.

Il segnale portante a infrarossi da 38K emesso dal telecomando viene codificato dal chip di codifica presente nel telecomando stesso. È composto da un codice pilota, un codice utente, il codice utente inverso, il codice dati e il codice dati inverso. L'intervallo di tempo degli impulsi viene utilizzato per distinguere se si tratta di un segnale 0 o 1, e la codifica è composta da questi segnali 0 e 1.

Il codice utente dello stesso telecomando rimane invariato, mentre il codice dati consente di distinguere il tasto premuto.

Quando viene premuto un tasto del telecomando, quest'ultimo invia un segnale portante a infrarossi. Quando il ricevitore IR riceve il segnale, il programma decodifica il segnale portante e determina quale tasto è stato premuto. Il microcontrollore decodifica il segnale 01 ricevuto, determinando così quale tasto è stato premuto sul telecomando.

![](media/5ad0f889b39646ecb13664511479efc8.png)

Il ricevitore a infrarossi che utilizziamo è un modulo ricevitore IR. È composto principalmente da una testa ricevitrice a infrarossi, che è un dispositivo che integra ricezione, amplificazione e demodulazione. Il suo IC interno ha completato la demodulazione e può realizzare la ricezione a infrarossi fino all'uscita, risultando compatibile con i segnali TTL. Inoltre, è adatto per il controllo remoto a infrarossi e la trasmissione di dati a infrarossi. Il modulo di ricezione a infrarossi realizzato con questo ricevitore ha solo tre pin: linea del segnale, VCC e GND. È molto comodo da collegare con Arduino e altri microcontrollori.

#### **(2)Parametri:**

- Tensione di funzionamento: 3.3-5V（DC）
- Interfaccia: 3PIN
- Segnale di uscita: Segnale digitale
- Angolo di ricezione: 90 gradi
- Frequenza: 38khz
- Distanza di ricezione: 10m

Ricevitore a infrarossi integrato nella scheda di controllo motori:

![](./media/image-20250709133832650.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span> Poiché il ricevitore IR è integrato nella scheda di espansione Keyestudio 8833 motor drive, non è necessario effettuare ulteriori collegamenti. I pin del ricevitore IR sulla scheda di espansione Keyestudio 8833 motor drive sono G (GND), V (VCC) e D3.

#### **(4)Codice di Test:**

È possibile anche trascinare i blocchi per modificare il codice, come mostrato di seguito

![](media/cfe0841bcc9404c29519ed623195ca6a.png)

![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

![](media/5a48421831518ea8e0c00be83cf4edf4.png)

![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/90978855cddd94c161f9ed02f85b0674.png)

#### **(5)Risultati del Test:**

Carica il codice sulla scheda di sviluppo e imposta il baud rate a 9600. Prendi il telecomando, puntalo verso il sensore ricevitore a infrarossi e premi un tasto per inviare il segnale. Vedrai il valore del tasto corrispondente. Se il tasto viene tenuto premuto troppo a lungo, potrebbe facilmente apparire un carattere illeggibile "FFFFFFFF".

![](media/5c01c594a5a11511cf52466eb5f27e45.png)

Di seguito abbiamo elencato il valore di ciascun tasto del telecomando Keyestudio, che puoi conservare come riferimento.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

#### **(6)Pratica di Approfondimento:**

Abbiamo appena decodificato i valori dei tasti del telecomando IR. Ora utilizziamolo per controllare l'accensione e lo spegnimento di un LED. È necessario collegare un modulo LED al pin D9, mentre la posizione del pin del ricevitore a infrarossi rimane invariata. Quando viene premuto il tasto OK sul telecomando, il LED collegato a D9 si accenderà, e quando il tasto OK viene premuto di nuovo, il LED si spegnerà.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)


È possibile anche trascinare i blocchi per modificare il codice, come mostrato di seguito

（1）![](media/cfe0841bcc9404c29519ed623195ca6a.png)

（2）![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

（3）![](media/ba67c48d67b1c9753fca82964c9dddc7.png)

(4) ![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

（5）![](media/f8b75df8ccea3efe1cd3ea383b0f88f2.png)

（6）![](media/7406d60c93cdba0b13ded27cba718ec7.png)

（7）![](media/d7be3fa06a1456d46472fffd61823c73.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/57149c79243ff22aa00ff2c54dd4f70b.png)

Carica il codice sulla scheda di sviluppo e premi il tasto "OK" sul telecomando per accendere e spegnere il LED.

![](./media/img-20240117092532.png)