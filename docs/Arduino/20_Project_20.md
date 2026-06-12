### Progetto 20: Sensore di Fiamma

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Descrizione：**

Il sensore di fiamma utilizza un tubo ricevitore IR per rilevare le fiamme. Converte la luminosità della fiamma in segnali di livello alto e basso e li invia al processore centrale per la corrispondente elaborazione del programma. Il valore di tensione della porta analogica varia a seconda che ci sia una fiamma nelle vicinanze o non ce ne sia affatto.

Se non c'è fiamma, la porta analogica legge circa 0,3V; quando c'è una fiamma, la porta analogica legge circa 1,0V. Più la fiamma è vicina, più alto è il valore di tensione. Può essere utilizzato per rilevare una fonte di fuoco o per costruire un robot intelligente.

Si noti che la sonda del sensore di fiamma può sopportare solo temperature comprese tra -25℃ e 85℃.

Durante l'uso, assicurarsi di mantenere il sensore di fiamma a una distanza di sicurezza dal fuoco per evitare di danneggiarlo.

#### **(2)Parametri：**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Tensione di funzionamento: 3,3V-5V (DC)

- Corrente: 100mA

- Potenza massima: 0,5W

- Temperatura di lavoro: da -10°C a +50 gradi Celsius

- Dimensioni del sensore: 31,6mm x 23,7mm

- Interfaccia: interfaccia da 4pin a 3PIN

- Segnale di uscita: segnali analogici A0, A1



#### **(3)Schema di Collegamento:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

I sensori di fiamma sono collegati ad A1 e A2.

Quando rimuoviamo i sensori a ultrasuoni e le fotoresistenze, quindi aggiungiamo i sensori di fiamma e i moduli ventola, si crea il robot antincendio.

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Questo esperimento richiede l'uso di una fonte di fuoco. Si prega di tenerla lontana da oggetti infiammabili per prevenire incendi. I bambini devono effettuare l'esperimento sotto la supervisione di un adulto. Se non si è in grado di confermare la propria sicurezza, si prega di abbandonare l'esperimento.
2）**Il sensore di fiamma non è ignifugo, non bruciarlo direttamente con una fiamma.**


#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.1

flame sensor

http://www.keyestudio.com

*/

int flame = A1; // Definisce il pin della fiamma come pin analogico A1
int val = 0; // Definisce le variabili digitali

void setup() 
{
	pinMode(flame, INPUT); // Definisce il buzzer come sorgente di input
    Serial.begin(9600); // Imposta la velocità di trasmissione a 9600
}

void loop() 
{
	val = analogRead(flame); // Legge il valore analogico del sensore di fiamma
	Serial.println(val); // Stampa e visualizza il valore analogico
	delay(100); // Ritardo di 100ms
}
```

#### **(5)Risultato del Test：**

Collegare i componenti, caricare il codice, aprire il monitor seriale e impostare la velocità di trasmissione a 9600.

È possibile visualizzare il valore di simulazione del sensore di fiamma.

Più la fiamma è vicina, minore è il valore di simulazione.

Regolare il potenziometro sul modulo per mantenere D1 al punto critico. Quando il sensore non rileva fiamma, D1 sarà spento, ma se il sensore rileva fiamma, D1 si accenderà.

![](./media/img-20240117085629.png)

![](media/05db06b3e205dfca63c2ba3aa7ff528e.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Si prega di tenerlo lontano da oggetti infiammabili per prevenire incendi. I bambini devono effettuare l'esperimento sotto la supervisione di un adulto. Se non si è in grado di confermare la propria sicurezza, si prega di abbandonare l'esperimento. Il sensore di fiamma non è ignifugo, non bruciarlo direttamente con una fiamma.

#### **(6)Pratica Estesa:**

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Questo esperimento richiede l'uso di una fonte di fuoco. Si prega di tenerla lontana da oggetti infiammabili per prevenire incendi. I bambini devono effettuare l'esperimento sotto la supervisione di un adulto. Se non si è in grado di confermare la propria sicurezza, si prega di abbandonare l'esperimento.
2）Il sensore di fiamma non è ignifugo, non bruciarlo direttamente con una fiamma.

Successivamente, collegare un LED al pin 9 e possiamo controllarlo tramite un sensore di fiamma, come mostrato di seguito;

![](media/814c315d3bb44278b476a754d3681227.png)

**Codice di Test**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.2

flame sensor

http://www.keyestudio.com

*/

int flame = A1; // Definisce il pin della fiamma come pin analogico A1
int LED = 9; // Definisce il LED come porta digitale 9
int val = 0; // Definisce le variabili digitali

void setup() 
{
    pinMode(flame, INPUT); // Definisce la fiamma come sorgente di input
    pinMode(LED, OUTPUT); // Imposta il LED in modalità output
    Serial.begin(9600); // Imposta la velocità di trasmissione a 9600
}

void loop() 
{
    val = analogRead(flame); // Legge il valore analogico del sensore di fiamma
    Serial.println(val); // Stampa e visualizza il valore analogico
    if (val < 300)  // Quando il valore analogico è inferiore a 300, il LED si accende
    {
    	digitalWrite(LED, HIGH); // Il LED si accende
    } 
    else 
    {
    	digitalWrite(LED, LOW); // Il LED si spegne
    }
    delay(50); // Ritardo di 50ms
}
```

#### **(8)Risultati del Test：**

È possibile avvicinare la fiamma di un accendino al sensore di fiamma sinistro. Quando il sensore di fiamma rileva una fiamma, il modulo LED si accenderà come allarme.

![](./media/img-20240117085131.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Si prega di tenerlo lontano da oggetti infiammabili per prevenire incendi. I bambini devono effettuare l'esperimento sotto la supervisione di un adulto. Se non si è in grado di confermare la propria sicurezza, si prega di abbandonare l'esperimento. Il sensore di fiamma non è ignifugo, non bruciarlo direttamente con una fiamma.