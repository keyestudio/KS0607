### Progetto 7: Ricezione IR

#### **(1)Descrizione:**

![](media/8969111328604c5358f7c915ac94e474.png)

Non c'è dubbio che il telecomando a infrarossi sia onnipresente nella vita quotidiana. Viene utilizzato per controllare vari elettrodomestici, come televisori, stereo, videoregistratori e ricevitori di segnale satellitare. Il telecomando a infrarossi è composto da sistemi di trasmissione e ricezione a infrarossi, ovvero un telecomando a infrarossi, un modulo ricevitore a infrarossi e un microcontrollore in grado di decodificare.

Il segnale portante a infrarossi da 38K emesso dal telecomando viene codificato dal chip di codifica nel telecomando. È composto da una sezione di codice pilota, codice utente, codice utente inverso, codice dati e codice dati inverso. L'intervallo di tempo degli impulsi viene utilizzato per distinguere se si tratta di un segnale 0 o 1, e la codifica è composta da questi segnali 0 e 1.

Il codice utente dello stesso telecomando rimane invariato mentre il codice dati può distinguere il tasto premuto.

Quando viene premuto il tasto del telecomando, il telecomando invia un segnale portante a infrarossi. Quando il ricevitore IR riceve il segnale, il programma decodifica il segnale portante e determina quale tasto è stato premuto. Il MCU decodifica il segnale 01 ricevuto, determinando così quale tasto è stato premuto sul telecomando.

![](media/image-20230426172824683.png)

Il ricevitore a infrarossi è saldato sulla scheda di controllo motore. Integra ricezione, amplificazione e demodulazione, il cui IC interno è già regolato per eseguire la ricezione a infrarossi e l'uscita, ed è compatibile con segnali TTL. Produce segnali digitali ed è adatto per il telecomando a infrarossi e la trasmissione dati a infrarossi. Questo modulo dispone di soli tre pin, tra cui segnale, VCC e GND, quindi è molto conveniente da collegare e comunicare con microcontrollori come Arduino.

#### **(2)Parametri:**

Tensione di funzionamento: 3.3-5V（DC）

Interfaccia: 3PIN

Segnale di uscita: Segnale digitale

Angolo di ricezione: 90 gradi

Frequenza: 38khz

Distanza di ricezione: 10m

Ricevitore a infrarossi integrato sulla scheda di controllo motore：

![](./media/img-20240117082433.png)




#### **(3)Codice di Test:**

È necessario importare prima la libreria IR.

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 7.1

IRremote

http://www.keyestudio.com

*/

#include <IRremote.h> // dichiarazione della libreria IRremote

int RECV_PIN = 3; //definisci i pin del ricevitore IR come 3
IRrecv irrecv(RECV_PIN);
decode_results results; //i risultati della decodifica esistono nel "result" di "decode results"

void setup() 
{
    Serial.begin(9600);
    irrecv.enableIRIn(); //Abilita il ricevitore
}

void loop() 
{
    if (irrecv.decode(&results))//decodifica riuscita, ricevuto un insieme di segnali infrarossi
    {
        Serial.println(results.value, HEX);//Stampa in formato HEX a 16 bit il codice ricevuto
        irrecv.resume(); //Ricevi il valore successivo
    }
    delay(100);
}
```

#### **(4)Risultati del Test:**

Carica il codice di test, apri il monitor seriale e imposta il baud rate a 9600, punta il telecomando verso il ricevitore IR. Verrà visualizzato il valore corrispondente. Se si tiene premuto un tasto per un po', appariranno codici di errore.

![](media/a484b81d031c8d6e8addb169136fd45c.png)

Di seguito abbiamo elencato il valore di ogni pulsante del telecomando Keyestudio. Puoi tenerlo come riferimento.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

Il ricevitore IR è collegato a D3, quindi non è necessario effettuare alcun collegamento

#### **(5)Spiegazione del Codice:**

**irrecv.enableIRIn():** dopo aver abilitato la decodifica IR, i segnali IR verranno ricevuti, quindi la funzione "decode()" verificherà continuamente se la decodifica è avvenuta con successo.

**irrecv.decode(&results):** dopo una decodifica riuscita, questa funzione restituirà "true" e manterrà il risultato in "results". Dopo aver decodificato un segnale IR, esegui la funzione resume() e ricevi il segnale successivo.

#### **(6)Pratica Estesa:**

Abbiamo decodificato il valore dei tasti del telecomando IR. Che ne dici di controllare un LED con il valore misurato? Potremmo progettare un esperimento.

Collega un LED a D9, poi premi i tasti del telecomando per accendere e spegnere il LED.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)

**Codice di Test**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 7.2
IRremote
http://www.keyestudio.com
*/

#include <IRremote.h> //dichiarazione IRremote

int RECV_PIN = 3; //definisci il pin del LED come pin 3
int LED = 9;
bool flag = 0;
IRrecv irrecv(RECV_PIN);
decode_results results; //i risultati della decodifica esistono nel "result" di "decode results"

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);//imposta LED come uscita
    irrecv.enableIRIn(); //Abilita il ricevitore
}

void loop() 
{
    if (irrecv.decode(&results)) 
    {
        if (results.value == 0xFF02FD & flag == 0) //Il codice del tasto sopra, usiamo il tasto OK del telecomando, se premi il tasto OK
        {
            digitalWrite(LED, HIGH); //LED acceso
            flag = 1;
        }

        else if (results.value == 0xFF02FD & flag == 1) //premi di nuovo
        {
            digitalWrite(LED, LOW); //LED spento
            flag = 0;
        }
        irrecv.resume(); // Ricevi il valore successivo
    }
}
```

Carica il codice sulla scheda di sviluppo e premi il tasto "OK" sul telecomando per accendere e spegnere il LED.

![](./media/img-20240117090645.png)