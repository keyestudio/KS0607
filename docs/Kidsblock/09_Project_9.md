### Progetto 9: Matrice LED Facciale 8*16

#### **(1)Descrizione:**

Non sarebbe divertente aggiungere un pannello espressivo al robot? La matrice LED 8*16 di Keyestudio può fare al caso tuo. Con il suo aiuto, potresti progettare espressioni facciali, immagini, pattern e altri display da solo.

Il pannello LED 8*16 è dotato di 128 LED. I dati del microprocessore (Arduino) comunicano con l'AiP1640 attraverso un'interfaccia bus a due fili. Pertanto, può controllare l'accensione e lo spegnimento di 128 LED sul modulo, in modo da far visualizzare alla matrice di punti sul modulo il pattern desiderato. Un cavo HX-2.54 4Pin è fornito per comodità di cablaggio.

#### **(2)Parametri:**

-   Tensione di lavoro: DC 3.3-5V

-   Dissipazione di potenza: 400mW

-   Frequenza di oscillazione: 450KHz

-   Corrente di pilotaggio: 200mA

-   Temperatura di lavoro: -40\~80℃

-   Modalità di comunicazione: bus a due fili

#### **(3)Conoscenze:**

**Circuito della matrice LED 8\*16**

![](media/edf6c77d05904eebbaa89d557e9e9c1a.png)

**Principio della matrice LED 8\*16**

Come controllare ogni LED della matrice di punti 8\*16? È noto che ogni byte ha 8 bit e ogni bit è 0 o 1. Quando è 0, il LED è spento, mentre quando è 1 il LED è acceso. Un byte può controllare una colonna di LED, e naturalmente 16 byte possono controllare 16 colonne di LED, questa è la matrice di punti 8\*16.

**Descrizione dei pin e protocollo di comunicazione**

I dati del microprocessore (Arduino) comunicano con l'AiP1640 attraverso un cavo bus a due fili.

Il diagramma del protocollo di comunicazione è il seguente: (SCLK) è SCL, (DIN) è SDA.

![](media/ea2bab37f23c09453c680590b84653d6.png)

①La condizione di partenza per l'ingresso dati: SCL è a livello alto e SDA cambia da alto a basso.

②Per l'impostazione del comando dati, ci sono metodi come mostrato nella figura sottostante.

Nel nostro programma di esempio, selezionare il metodo per **aggiungere 1 all'indirizzo automaticamente**, il valore binario è 0100 0000 e il corrispondente valore esadecimale è 0x40.

![](media/image-20230907161100692.png)

③Per l'impostazione del comando indirizzo, l'indirizzo può essere selezionato come mostrato di seguito.

Il primo 00H è selezionato nel nostro programma di esempio, e il numero binario 1100 0000 corrisponde all'esadecimale 0xc0.

![](media/image-20230907161152467.png)

④Il requisito per l'ingresso dati è che quando SCL è a livello alto durante l'inserimento dei dati, il segnale su SDA deve rimanere invariato. Solo quando il segnale di clock su SCL è a livello basso, il segnale su SDA può essere modificato. L'inserimento dei dati avviene prima con il bit meno significativo e poi con il bit più significativo.

⑤La condizione per la fine della trasmissione dati è che quando SCL è a livello basso, SDA a livello basso e SCL a livello alto, il livello di SDA diventa alto.

⑥Controllo del display, impostare diverse larghezze di impulso; la larghezza di impulso può essere selezionata come mostrato nella figura sottostante.

Nell'esempio, la larghezza di impulso è 4/16, e l'esadecimale corrispondente a 1000 1010 è 0x8A.

![](media/image-20230907161220995.png)

**Istruzioni per l'uso dello strumento modulus**

Lo strumento per la matrice di punti utilizza la versione online, e il link è: <http://dotmatrixtool.com/#>

①Inserire il link e la pagina appare come mostrato di seguito

![](media/354693b5679a2615c62e99b7025d6355.png)

②La matrice di punti è 8\*16, quindi regolare l'altezza a 8 e la larghezza a 16, come mostrato nella figura sottostante.

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③Generare dati esadecimali dal pattern.

Come mostrato nella figura sottostante, premere il tasto sinistro del mouse per selezionare, fare clic con il tasto destro per annullare; disegnare il pattern desiderato, fare clic su Generate, e i dati esadecimali di cui abbiamo bisogno verranno generati.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4)Schema di Collegamento:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

GND, VCC, SDA e SCL del pannello LED 8x16 sono collegati rispettivamente a G(GND), V (VCC), A4 e A5 della scheda di espansione per la comunicazione seriale a due fili.

(<span style="color: rgb(255, 76, 65);">Nota:</span> sebbene sia collegato al pin IIC di Arduino, questo modulo non è per la comunicazione IIC. La porta IO qui serve per simulare la comunicazione I2C e può essere collegata a qualsiasi due pin)

#### **(5)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito

![](media/e346413e7f38f5f6368dd8262f173514.png)

![](media/8ecfff600093779602b37d2202493057.png)

![](media/0f0df06e3ed2adbbe3ffaa20dd3fa0a5.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, il che può causare il fallimento del caricamento.)

![](media/75e6f65c9a299868d37544ac42c54f66.png)

#### **(6)Risultati del Test:**

Dopo aver caricato con successo il codice di test, collegare i cavi, portare l'interruttore DIP sull'estremità ON e alimentare il dispositivo; sulla matrice di punti appare un pattern a forma di sorriso.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7)Pratica di Estensione:**

Utilizziamo lo strumento modulus appena imparato, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), per far visualizzare alla matrice di punti il pattern di avvio, andare avanti, fermarsi e poi cancellare il pattern. L'intervallo di tempo è di 2000 ms.

![](media/31ab1346c58438ca95c990e4ff963c0d.png)

Blocco per mostrare la faccina sorridente![](media/1702a82ce685e3e7da7b136cbc51e718.png)

Codice per mostrare l'espressione![](media/bae6801afc8fbcc0e7a70c243559c266.png)

Blocco per mostrare il cuore![](media/dcaa414f16d10068d2c3627959141da6.png)

Codice per andare avanti![](media/8fc218e6b35826aa31f5e00f61414651.png)

Blocco per andare indietro![](media/043abae4540c578f93772ed9b6648e60.png)

Blocco per girare a sinistra![](media/7b3d80a76228ee5b23555af17269a02d.png)

Blocco per girare a destra![](media/5a84b3538a62367a8f35cc59071c0bda.png)

Blocco per fermarsi![](media/733bd1f96e1c9d116033a317cb507fac.png)

Blocco per cancellare![](media/06d37680acd61c9c5c4113c78c985eca.png)

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito.

（1）![](media/e346413e7f38f5f6368dd8262f173514.png)

（2）![](media/840217b5879f1fce9e36566dc76914a4.png)

（3）![](media/e72e75122897b0ef930196f762080623.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, il che può causare il fallimento del caricamento.)

![](media/dee30ed46775feb634d4e8e4ec0a189a.png)

Caricare il codice sulla scheda di sviluppo, il pannello 8\*16 mostrerà i seguenti pattern.

![](./media/image-20250709134319784.png)

![](./media/image-20250709134332835.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)