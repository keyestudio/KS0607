### Progetto 8: Guida e Controllo della Velocità del Motore

#### **(1)Descrizione:**

Esistono molti modi per pilotare i motori. La nostra auto intelligente utilizza la soluzione più comune chiamata L298P. L298P, prodotto da STMicroelectronics, è un eccellente chip di pilotaggio appositamente progettato per pilotare motori ad alta potenza.

Può pilotare direttamente motori DC, motori a due fasi e a quattro fasi con una corrente di pilotaggio che raggiunge i 2A. Il terminale di uscita del motore adotta 8 diodi Schottky ad alta velocità come protezione.

Abbiamo progettato una scheda di espansione basata sul circuito L298P il cui design a impilamento può essere inserito direttamente nella scheda UNO R3 per l'uso, riducendo le difficoltà tecniche per gli utenti nell'utilizzo e nel pilotaggio del motore.

Impilare la scheda di espansione sulla scheda, alimentare la BAT, girare l'interruttore DIP sull'estremità ON e alimentare la scheda di espansione e la scheda UNO R3 contemporaneamente tramite alimentazione esterna.

Per facilitare il cablaggio, la scheda di espansione è dotata di interfaccia anti-inversione (PH2.0 -2P -3P -4P -5P) e quindi può essere collegata direttamente con motori, alimentatori e sensori/moduli.

L'interfaccia Bluetooth della scheda di espansione per il pilotaggio è completamente compatibile con il modulo Bluetooth Keyestudio HM-10. Pertanto, dobbiamo solo inserire il modulo Bluetooth HM-10 nell'interfaccia corrispondente durante il collegamento.

Allo stesso tempo, la scheda di espansione utilizza anche pin header da 2,54 mm per estendere alcune porte digitali e analogiche disponibili, in modo da poter continuare ad aggiungere altri sensori e svolgere esperimenti di espansione.

La scheda di espansione può essere collegata a 4 motori DC. Nella modalità di connessione predefinita con il cappuccio jumper, i motori delle interfacce A e A1, B e B1 sono collegati in parallelo e il loro schema di movimento è lo stesso. 8 cappucci jumper possono essere utilizzati per controllare la direzione di rotazione delle 4 interfacce motore.

Ad esempio, quando i due cappucci jumper davanti all'interfaccia del motore A vengono cambiati da una connessione orizzontale a una connessione verticale, la direzione di rotazione del motore A è ora opposta alla direzione di rotazione originale.

![](media/image-20230427081635216.png)

![](media/5381c98d3be6da099ce43e841b8f736b.png)

#### **(2)Parametri：**

- Tensione di ingresso della parte logica: DC 5V

- Tensione di ingresso della parte di pilotaggio: DC 7-12V

- Corrente di lavoro della parte logica: ≤36mA

- Corrente di lavoro della parte di pilotaggio: ≤ 2A

- Potenza massima dissipata: 25W (T=75℃)

- Livello del segnale di controllo in ingresso:
  
  ​	Livello alto: 2,3V ≤ Vin ≤ 5V
  
  ​	Livello basso: 0V ≤ Vin ≤ 1,5V

- Temperatura di lavoro: -25℃～＋130℃

#### **(3)Pilotare il robot in movimento**

Il pin di direzione del motore A è D2, il pin di controllo della velocità è D5; il pin di direzione del motore B è D4 e il pin di controllo della velocità è D6.

Secondo la tabella seguente, possiamo sapere come controllare il movimento del robot controllando la rotazione di due motori attraverso le porte digitali e le porte PWM. Il range del valore PWM è 0-255. Maggiore è il valore, più veloce ruota il motore.

|   Funzione    |  D4  | D6（PWM） | Motore（sinistra）B |  D2  | D5（PWM） | Motore（destra）A |
| :-----------: | :--: | :-------: | :-----------------: | :--: | :-------: | :---------------: |
| Avanti        | HIGH |  255-200  |   Ruota Sinistra    | HIGH |  255-200  |  Ruota Sinistra   |
| Indietro      | LOW  |    200    |   Ruota Destra      | LOW  |    200    |   Ruota Destra    |
| Gira Sinistra | LOW  |    200    |   Ruota Destra      | HIGH |  255-200  |  Ruota Sinistra   |
| Gira Destra   | HIGH |  255-200  |   Ruota Sinistra    | LOW  |    200    |   Ruota Destra    |
| Stop          | LOW  |     0     |        Stop         | LOW  |     0     |       Stop        |




#### **(4)Schema di Collegamento:**

![](media/3e53cf19ea5f85a931b955453b86304b.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

Il connettore a 4 pin è contrassegnato con A, A1, B1 e B. Il motore posteriore destro è collegato a B della scheda 8833 e quello anteriore sinistro è collegato alla porta A.

#### **(5)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.1
motor driver
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // Definire il pin di controllo della direzione del motore sinistro
#define ML_PWM 6 // Definire il pin di controllo PWM del motore sinistro
#define MR_Ctrl 2 // Definire il pin di controllo della direzione del motore destro
#define MR_PWM 5 // Definire il pin di controllo PWM del motore destro

void setup()
{
    pinMode(ML_Ctrl, OUTPUT);// Definire il pin di controllo della direzione del motore sinistro come OUTPUT
    pinMode(ML_PWM, OUTPUT);// Definire il pin di controllo PWM del motore sinistro come OUTPUT
    pinMode(MR_Ctrl, OUTPUT);// Definire il pin di controllo della direzione del motore destro come OUTPUT
    pinMode(MR_PWM, OUTPUT);// Definire il pin di controllo PWM del motore destro come OUTPUT
}

void loop()
{
    // avanti
    digitalWrite(ML_Ctrl, HIGH); // Impostare la velocità di controllo della direzione del motore sinistro su HIGH
    analogWrite(ML_PWM, 55); // La velocità di controllo PWM del motore sinistro è 55
    digitalWrite(MR_Ctrl, HIGH); // Impostare la velocità di controllo della direzione del motore destro su HIGH
    analogWrite(MR_PWM, 55); // La velocità di controllo PWM del motore destro è 55
    delay(2000);// ritardo di 2s

    // indietro
    digitalWrite(ML_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore sinistro su LOW
    analogWrite(ML_PWM, 200); // La velocità di controllo PWM del motore sinistro è 200
    digitalWrite(MR_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore destro su LOW
    analogWrite(MR_PWM, 200); // La velocità di controllo PWM del motore destro è 200
    delay(2000);// ritardo di 2s

    // gira sinistra
    digitalWrite(ML_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore sinistro su LOW
    analogWrite(ML_PWM, 200); // La velocità di controllo PWM del motore sinistro è 200
    digitalWrite(MR_Ctrl, HIGH); // Impostare la velocità di controllo della direzione del motore destro su HIGH
    analogWrite(MR_PWM, 55); // La velocità di controllo PWM del motore destro è 55
    delay(2000);// ritardo di 2s

    // gira destra
    digitalWrite(ML_Ctrl, HIGH); // Impostare la velocità di controllo della direzione del motore sinistro su HIGH
    analogWrite(ML_PWM, 55); // La velocità di controllo PWM del motore sinistro è 55
    digitalWrite(MR_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore destro su LOW
    analogWrite(MR_PWM, 200); // La velocità di controllo PWM del motore destro è 200
    delay(2000);// ritardo di 2s

    // stop
    digitalWrite(ML_Ctrl, LOW);
    analogWrite(ML_PWM, 0); // La velocità di controllo PWM del motore sinistro è 0
    digitalWrite(MR_Ctrl, LOW);
    analogWrite(MR_PWM, 0); // La velocità di controllo PWM del motore destro è 0
    delay(2000);// ritardo di 2s
}
```

#### **(6)Risultati del Test:**

Dopo aver effettuato il cablaggio secondo lo schema, caricato il codice di test e acceso l'alimentazione.

![](./media/img-20240117082646.png)

l'auto intelligente si muove in avanti per 2s, indietro per 2s, gira a sinistra per 2s, gira a destra per 2s e si ferma per 2s, ripetendo questa sequenza.

#### **(7)Spiegazione del Codice:**

**digitalWrite(ML_Ctrl,LOW);**

Il cambiamento tra livelli alto e basso può far ruotare i motori in senso orario o antiorario. I pin digitali generali possono essere utilizzati per controllare questi movimenti.

**analogWrite(ML_PWM,200);**

La regolazione della velocità del motore è realizzata tramite PWM, e il pin che controlla la velocità del motore deve essere il pin PWM di Arduino.

#### **(8)Progetto di Espansione:**

Regoliamo la velocità dei motori controllando il PWM e il cablaggio rimane invariato.

**Codice di Test**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.2
motor driver pwm
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // Definire il pin di controllo della direzione del motore sinistro
#define ML_PWM 6 // Definire il pin di controllo PWM del motore sinistro
#define MR_Ctrl 2 // Definire il pin di controllo della direzione del motore destro
#define MR_PWM 5 // Definire il pin di controllo PWM del motore destro

void setup() 
{
    pinMode(ML_Ctrl, OUTPUT);// Definire il pin di controllo della direzione del motore sinistro come OUTPUT
    pinMode(ML_PWM, OUTPUT);// Definire il pin di controllo PWM del motore sinistro come OUTPUT
    pinMode(MR_Ctrl, OUTPUT);// Definire il pin di controllo della direzione del motore destro come OUTPUT
    pinMode(MR_PWM, OUTPUT);// Definire il pin di controllo PWM del motore destro come OUTPUT
}

void loop() 
{
    // avanti
    digitalWrite(ML_Ctrl, HIGH); // Impostare la velocità di controllo della direzione del motore sinistro su HIGH
    analogWrite(ML_PWM, 155); // La velocità di controllo PWM del motore sinistro è 155
    digitalWrite(MR_Ctrl, HIGH); // Impostare la velocità di controllo della direzione del motore destro su HIGH
    analogWrite(MR_PWM, 155); // La velocità di controllo PWM del motore destro è 155
    delay(2000);// ritardo di 2s

    // indietro
    digitalWrite(ML_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore sinistro su LOW
    analogWrite(ML_PWM, 100); // La velocità di controllo PWM del motore sinistro è 100
    digitalWrite(MR_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore destro su LOW
    analogWrite(MR_PWM, 100); // La velocità di controllo PWM del motore destro è 100
    delay(2000);// ritardo di 2s

    // sinistra
    digitalWrite(ML_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore sinistro su LOW
    analogWrite(ML_PWM, 100); // La velocità di controllo PWM del motore sinistro è 100
    digitalWrite(MR_Ctrl, HIGH); // Impostare la velocità di controllo della direzione del motore destro su HIGH
    analogWrite(MR_PWM, 155); // La velocità di controllo PWM del motore destro è 155
    delay(2000);// ritardo di 2s

    // destra
    digitalWrite(ML_Ctrl, HIGH); // Impostare la velocità di controllo della direzione del motore sinistro su HIGH
    analogWrite(ML_PWM, 155); // La velocità di controllo PWM del motore sinistro è 155
    digitalWrite(MR_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore destro su LOW
    analogWrite(MR_PWM, 100); // La velocità di controllo PWM del motore destro è 100
    delay(2000);// ritardo di 2s

    // stop
    digitalWrite(ML_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore sinistro su LOW
    analogWrite(ML_PWM, 0); // La velocità di controllo PWM del motore sinistro è 0
    digitalWrite(MR_Ctrl, LOW); // Impostare la velocità di controllo della direzione del motore destro su LOW
    analogWrite(MR_PWM, 0); // La velocità di controllo PWM del motore destro è 0
    delay(2000);// ritardo di 2s
}
```

Caricare il codice, la velocità del motore è più lenta.

Una corrente bassa farà ruotare il motore lentamente.