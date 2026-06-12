### Progetto 9: Matrice LED per Espressioni Facciali 8*16

![](./media/image-20250709110751263.png)

#### **(1)Descrizione:**

Non sarebbe divertente aggiungere un pannello per le espressioni al robot? La matrice LED 8*16 di Keyestudio può fare al caso nostro. Con il suo aiuto, puoi progettare espressioni facciali, immagini, pattern e altri display da solo.

La scheda LED 8*16 è dotata di 128 LED. I dati del microprocessore (Arduino) comunicano con l'AiP1640 attraverso un'interfaccia bus a due fili. Pertanto, può controllare l'accensione e lo spegnimento dei 128 LED sul modulo, in modo da far visualizzare alla matrice di punti sul modulo il pattern desiderato. È fornito un cavo HX-2.54 4Pin per la comodità del collegamento.

#### **(2)Parametri:**

- Tensione di lavoro: DC 3.3-5V
- Dissipazione di potenza: 400mW
- Frequenza di oscillazione: 450KHz
- Corrente di pilotaggio: 200mA
- Temperatura di lavoro: -40\~80℃
- Modalità di comunicazione: bus a due fili

#### **(3)Nozioni:**

**Principio della matrice LED 8\*16**

Come controllare ogni LED della matrice di punti 8\*16? È noto che ogni byte ha 8 bit e ogni bit è 0 o 1. Quando è 0, il LED è spento, mentre quando è 1 il LED è acceso. Un byte può controllare una colonna del LED, e naturalmente 16 byte possono controllare 16 colonne di LED, questa è la matrice di punti 8\*16.

![](media/image-20230427082712905.png)

**Descrizione dei pin e protocollo di comunicazione**

I dati del microprocessore (Arduino) comunicano con l'AiP1640 attraverso un cavo bus a due fili.

Il diagramma del protocollo di comunicazione è il seguente: (SCLK) è SCL, (DIN) è SDA

![](media/ea2bab37f23c09453c680590b84653d6.png)

①La condizione iniziale per l'ingresso dei dati: SCL è ad alto livello e SDA passa da alto a basso.

②Per l'impostazione del comando dati, esistono i metodi mostrati nella figura seguente

Nel nostro programma di esempio, seleziona il metodo per **aggiungere automaticamente 1 all'indirizzo**, il valore binario è 0100 0000 e il corrispondente valore esadecimale è 0x40

![](media/image-20230427083500152.png)

③Per l'impostazione del comando di indirizzo, l'indirizzo può essere selezionato come mostrato di seguito.

Nel nostro programma di esempio viene selezionato il primo 00H, e il numero binario 1100 0000 corrisponde all'esadecimale 0xc0

![](media/image-20230427083716284.png)


④Il requisito per l'ingresso dei dati è che quando SCL è ad alto livello durante l'ingresso dei dati, il segnale su SDA deve rimanere invariato. Solo quando il segnale di clock su SCL è a basso livello, il segnale su SDA può essere modificato. L'ingresso dei dati avviene prima con il bit meno significativo e poi con il bit più significativo.

⑤La condizione per la fine della trasmissione dei dati è che quando SCL è a basso livello, SDA a basso livello e SCL ad alto livello, il livello di SDA diventa alto.

⑥Controllo del display, impostare diverse larghezze di impulso; la larghezza di impulso può essere selezionata come mostrato nella figura seguente. Nell'esempio, la larghezza di impulso è 4/16, e l'esadecimale corrispondente a 1000 1010 è 0x8A

![](media/image-20230427084941994.png)



**Istruzioni per l'uso dello strumento di modulazione**

Lo strumento per la matrice di punti utilizza la versione online, e il link è: [http://dotmatrixtool.com/#]( http://dotmatrixtool.com/#)

①Inserisci il link e la pagina appare come mostrato di seguito

![](media/354693b5679a2615c62e99b7025d6355.png)

②La matrice di punti è 8\*16, quindi regola l'altezza a 8 e la larghezza a 16, come mostrato nella figura seguente

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③Genera dati esadecimali dal pattern

Come mostrato nella figura seguente, premi il tasto sinistro del mouse per selezionare, fai clic destro per annullare; disegna il pattern che desideri, fai clic su Generate, e verranno generati i dati esadecimali necessari.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4)Schema di Collegamento:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

GND, VCC, SDA e SCL della scheda LED 8x16 sono collegati rispettivamente alla scheda di espansione sensori keyestudio -(GND), +(VCC), A4, A5 per la comunicazione seriale a due fili.

(<span style="color: rgb(255, 76, 65);">Nota:</span> sebbene sia collegato al pin IIC di Arduino, questo modulo non è per la comunicazione IIC. La porta IO qui serve per simulare la comunicazione I2C e può essere collegata a qualsiasi due pin)

#### **(5)Codice di Test:**

Il codice per mostrare la faccina sorridente

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.1
  Matrix face
  http://www.keyestudio.com
*/
// ottieni i dati dell'immagine sorridente da uno strumento di modulazione
unsigned char smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};

#define SCL_Pin  A5  // imposta il pin del clock su A5
#define SDA_Pin  A4  // imposta il pin dei dati su A4

void setup() {
  // imposta il pin su OUTPUT
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // pulisci lo schermo
  //matrix_display(clear);
}
void loop() {
  matrix_display(smile);  // visualizza l'immagine sorridente
}
// questa funzione è utilizzata per il display della matrice di punti
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // usa la funzione per iniziare la trasmissione dei dati
  IIC_send(0xc0);  // seleziona un indirizzo

  for (int i = 0; i < 16; i++) // i dati dell'immagine hanno 16 caratteri
  {
    IIC_send(matrix_value[i]); // dati per trasmettere le immagini
  }

  IIC_end();   // termina la trasmissione dei dati delle immagini

  IIC_start();
  IIC_send(0x8A);  // mostra il controllo e seleziona la larghezza di impulso 4/16
  IIC_end();
}

// la condizione che i dati inizino a trasmettere
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// il segnale che la trasmissione dei dati è terminata
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

// trasmetti i dati
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // ogni carattere ha 8 cifre, che vengono rilevate una per una
  {
    if (send_data & mask) { // imposta livelli alti o bassi in base a ogni bit (0 o 1)
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // alza il pin del clock SCL_Pin per terminare la trasmissione dei dati
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // abbassa il pin del clock SCL_Pin per cambiare i segnali di SDA
  }
}
```

#### **(6)Risultati del Test:**

Dopo aver caricato con successo il codice di test, collegato secondo il diagramma di cablaggio, posizionato il selettore DIP verso destra e alimentato il dispositivo, sulla matrice di punti appare un pattern a forma di faccina sorridente.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7)Progetto di Espansione:**

Utilizziamo lo strumento di modulazione appena appreso, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), per far visualizzare alla matrice di punti i pattern di avvio, avanzamento e arresto, e poi pulire il pattern. L'intervallo di tempo è di 2000 ms.

![](media/9866c73416df7466b5fe8be3712e6eb3.png)

![](media/1c7ab4b08636c2fe61deaf6c784da7d8.png)

![](media/b0a961f27eb5f0b66603abe23d6bb56a.png)


**Codice ottenuto dallo strumento di modulazione：**

**Codice per il pattern di avvio:**

0x01,0x02,0x04,0x08,0x10,0x20,0x40,0x80,0x80,0x40,0x20,0x10,0x08,0x04,0x02,0x01

**Codice per il pattern di avanzamento:**

0x00,0x00,0x00,0x00,0x00,0x24,0x12,0x09,0x12,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**Codice per il pattern di retromarcia:**

0x00,0x00,0x00,0x00,0x00,0x24,0x48,0x90,0x48,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**Codice per il pattern di svolta a sinistra：**

0x00,0x00,0x00,0x00,0x00,0x00,0x44,0x28,0x10,0x44,0x28,0x10,0x44,0x28,0x10,0x00

**Codice per il pattern di svolta a destra：**

0x00,0x10,0x28,0x44,0x10,0x28,0x44,0x10,0x28,0x44,0x00,0x00,0x00,0x00,0x00,0x00

**Codice per il pattern di arresto：**

0x2E,0x2A,0x3A,0x00,0x02,0x3E,0x02,0x00,0x3E,0x22,0x3E,0x00,0x3E,0x0A,0x0E,0x00

**Codice per pulire lo schermo：**

0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00

**Codice di Test**


(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
  keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.2
  Matrix face
  http://www.keyestudio.com
*/

// Array, utilizzato per salvare i dati delle immagini, può essere calcolato manualmente o ottenuto dallo strumento di modulazione
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  // imposta il pin del clock su A5
#define SDA_Pin  A4  // imposta il pin dei dati su A4

void setup() {
  // imposta il pin su OUTPUT
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // pulisci lo schermo
  matrix_display(clear);
}
void loop() {
  matrix_display(start01);  // mostra l'immagine "Start"
  delay(2000);
  matrix_display(front);    // mostra l'immagine "front"
  delay(2000);
  matrix_display(STOP01);   // mostra l'immagine "STOP01"
  delay(2000);
  matrix_display(clear);    // mostra l'immagine "clear"
  delay(2000);
}
// questa funzione è utilizzata per il display della matrice di punti
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // usa la funzione per iniziare la trasmissione dei dati
  IIC_send(0xc0);  // seleziona un indirizzo

  for (int i = 0; i < 16; i++) // i dati dell'immagine hanno 16 caratteri
  {
    IIC_send(matrix_value[i]); // dati per trasmettere le immagini
  }

  IIC_end();   // termina la trasmissione dei dati delle immagini

  IIC_start();
  IIC_send(0x8A);  // mostra il controllo e seleziona la larghezza di impulso 4/16
  IIC_end();
}

// la condizione che i dati inizino a trasmettere
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// il segnale che la trasmissione dei dati è terminata
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

// trasmetti i dati
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // ogni carattere ha 8 cifre, che vengono rilevate una per una
  {
    if (send_data & mask) { // imposta livelli alti o bassi in base a ogni bit (0 o 1)
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // alza il pin del clock SCL_Pin per terminare la trasmissione dei dati
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // abbassa il pin del clock SCL_Pin per cambiare i segnali di SDA
  }
}
```

Dopo aver caricato il codice di test, il pannello per le espressioni facciali mostra questi pattern in ordine e ripete questa sequenza.

![](media/e7ba47508826acc25d348182a0530c05.png)

![](media/831b7e0e07250cbc7bdc4fa509c5a0a3.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)