### Progetto 4: Sensore di Rilevamento Linea

#### **(1) Descrizione:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

Il sensore di tracciamento è in realtà un sensore a infrarossi. Il componente utilizzato qui è il tubo a infrarossi TCRT5000.

Il suo principio di funzionamento è quello di utilizzare la diversa riflettività della luce infrarossa sui colori, convertendo poi l'intensità del segnale riflesso in un segnale di corrente.

Durante il processo di rilevamento, il nero è attivo al livello ALTO mentre il bianco è attivo al livello BASSO. L'altezza di rilevamento è 0-3 cm.

Il modulo di tracciamento linea a 3 canali Keyestudio ha integrato 3 set di tubi a infrarossi TCRT5000 su un singolo scheda, il che rende il cablaggio e il controllo più comodi.

Se il Sensore di Rilevamento Linea non funziona come previsto, sarà necessario utilizzare un cacciavite per regolare il suo potenziometro per renderlo più sensibile. Quando il dito si avvicina al sensore, il LED integrato si accende, e quando il dito si allontana, il LED integrato si spegne. In questo momento, la sensibilità è relativamente buona.

![](./media/img-20240117090858.png)

#### **(2) Parametri:**

- Tensione di funzionamento: 3.3-5V (DC)

- Interfaccia: 5PIN

- Segnale di uscita: Segnale digitale

- Altezza di rilevamento: 0-3 cm


Nota speciale: prima del test, ruotare il potenziometro sul sensore per regolare la sensibilità di rilevamento. Quando si regola il LED alla soglia tra ON e OFF, la sensibilità è la migliore.

<span style="color: rgb(255, 76, 65);">Nota:</span> il sensore di tracciamento linea è installato sotto il fondo del robot.

#### **(3) Schema di Collegamento:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4) Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.1

Line Track sensor

http://www.keyestudio.com

*/

//Il cablaggio dei sensori di tracciamento linea

#define L_pin 11 //sinistra

#define M_pin 7 //centro

#define R_pin 8 //destra

void setup()
{
    Serial.begin(9600); //Imposta il baud rate a 9600
    pinMode(L_pin, INPUT); //Imposta tutti i pin dei sensori di tracciamento linea in modalità input
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); //Leggi il valore del sensore sinistro
    int M_val = digitalRead(M_pin); //Leggi il valore del sensore centrale
    int R_val = digitalRead(R_pin); //Leggi il valore del sensore destro

    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); //ritardo di 100ms
}
```

#### **(5) Risultati del Test:**

Carica il codice sulla scheda di sviluppo, apri il monitor seriale per verificare i sensori di tracciamento linea. Il valore visualizzato è 1 (livello alto) quando non vengono ricevuti segnali. Il valore passa a 0 quando il sensore è coperto con della carta.

![](./media/img-20240117090920.png)


![](media/b9319753c148f66aabc9bf648ed93da1.png)

#### **(6) Spiegazione del Codice:**

**Serial.begin(9600)** - Inizializza la porta seriale, imposta il baud rate a 9600

**pinMode** - Definisce il pin come modalità input o output

**digitalRead** - Legge lo stato del pin, che sono generalmente livello ALTO e BASSO

#### **(7) Pratica di Estensione:**

Dopo aver compreso il suo principio di funzionamento, puoi collegare un LED a D9, in modo da controllare il LED tramite il sensore di tracciamento linea.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

**Codice di Test**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.2

Line Track sensor

http://www.keyestudio.com

*/

//Pin LED

#define LED 9
//Il cablaggio dei sensori di tracciamento linea
#define L_pin 11 //sinistra
#define M_pin 7 //centro
#define R_pin 8 //destra

void setup()
{
    Serial.begin(9600); //Imposta il baud rate a 9600
    pinMode(LED, OUTPUT); //Imposta LED in modalità output
    pinMode(L_pin, INPUT); //Imposta tutti i pin dei sensori di tracciamento linea in modalità input
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); //Leggi il valore del sensore sinistro
    int M_val = digitalRead(M_pin); //Leggi il valore del sensore centrale
    int R_val = digitalRead(R_pin); //Leggi il valore del sensore destro
    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); //Ritardo di

    if (L_val == 0 || M_val == 0 || R_val == 0) 
    {
    	digitalWrite(LED, HIGH);
    }
    else 
    {
    	digitalWrite(LED, LOW);
    }
}
```