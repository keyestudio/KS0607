### Progetto 1: LED Lampeggiante

#### **(1)Descrizione:**

![](media/64b0b431d58473408ac46b39d2dc2ad0.jpeg)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Per i principianti e gli appassionati, il LED Lampeggiante è un programma fondamentale. Il LED, abbreviazione di diodi emettitori di luce, è composto da composti chimici Ga, As, P, N e altri. Il LED può lampeggiare in diversi colori modificando il tempo di ritardo nel codice di test. Quando è in funzione, alimentare GND e VCC. Il LED si accenderà se il terminale S è a livello alto; in caso contrario, si spegnerà.

#### **(2)Parametri:**

![](./media/image-20250709104606457.png)

- Interfaccia di controllo: porta digitale
- Tensione di lavoro: DC 3.3-5V
- Passo pin: 2.54mm
- Colore display LED: giallo

#### **(3)Componenti Necessari:**

![](media/img-20240117081416.png)


#### **(4)Scheda di espansione driver motore 8833:**

La scheda di espansione driver motore Keyestudio 8833 è compatibile con la scheda di sviluppo Arduino UNO. Basta installarla sulla scheda di sviluppo durante l'utilizzo.

![](./media/image-20250709104749140.png)

#### **(5)Schema di Collegamento:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](media/d68e6475a7c9ed55bb057b75d1b11689.png)

<span style="color: rgb(255, 76, 65);">**NOTA:**</span> Il LED è collegato alla porta D9. Ricordarsi di installare i cappucci jumper sullo shield.

#### **(6)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.1

Blink

http://www.keyestudio.com

*/

int LED = 9; // Definisce il pin del LED da collegare alla porta digitale 9

void setup()
{
	pinMode(LED, OUTPUT); // Inizializza il pin del LED in modalità output
}

void loop() // ciclo infinito
{
	digitalWrite(LED, HIGH); // Emette livello alto e accende il LED
	delay(1000); // Attendi 1s
	digitalWrite(LED, LOW); // Emette livello basso e spegne il LED
	delay(1000); // Attendi 1s
}
```

#### **(7)Risultati del Test:**

Carica il programma, il LED lampeggia con un intervallo di 1s.

#### **(8)Spiegazione del Codice:**

**pinMode(LED，OUTPUT) -** Questa funzione può indicare che il pin è INPUT o OUTPUT

**digitalWrite(LED，HIGH) -** Quando il pin è OUTPUT, possiamo impostarlo su HIGH (output 5V) o LOW (output 0V)

#### **(9)Pratica di Estensione:**

Abbiamo fatto lampeggiare il LED con successo. Ora, osserviamo cosa succederà al LED se modifichiamo i pin e il tempo di ritardo.

**Codice di Test**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.2

Blink

http://www.keyestudio.com

*/

int LED = 9; // Definisce il pin del LED come 9

void setup()
{
	pinMode(LED, OUTPUT); // Imposta il pin del LED su OUTPUT
}

void loop() // Ciclo infinito
{
    digitalWrite(LED, HIGH); // emette livelli alti, accende il LED
	delay(100); // Attendi 0.1s
	digitalWrite(LED, LOW); // LED emette livelli bassi, spegne il LED
	delay(100); // Attendi 0.1s

}
```

Il risultato del test mostra che il LED lampeggia più velocemente. Pertanto, possiamo concludere che i pin e il tempo di ritardo influenzano la frequenza di lampeggio.