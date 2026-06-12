### Progetto 2: Regolare la Luminosità del LED

#### **(1)Descrizione:**

Nella lezione precedente, abbiamo controllato l'accensione e lo spegnimento del LED facendolo lampeggiare.

In questo progetto, controlleremo la luminosità del LED tramite PWM simulando un effetto di respirazione. Allo stesso modo, è possibile modificare la lunghezza del passo e il tempo di ritardo nel codice per ottenere diversi effetti di respirazione.

Il PWM è un mezzo per controllare l'uscita analogica tramite metodi digitali. Il controllo digitale viene utilizzato per generare onde quadre con diversi cicli di lavoro (un segnale che passa costantemente tra livelli alti e bassi) per controllare l'uscita analogica.

In generale, le tensioni di ingresso delle porte sono 0V e 5V. Cosa succede se sono richiesti 3V? O una commutazione tra 1V, 3V e 3.5V? Non possiamo cambiare continuamente i resistori. Per questo motivo, ricorriamo al PWM.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Per le uscite di tensione delle porte digitali di Arduino, esistono solo livelli BASSO e ALTO, che corrispondono rispettivamente alle uscite di tensione di 0V e 5V. È possibile definire BASSO come "0" e ALTO come "1", e lasciare che Arduino emetta cinquecento "0" o "1" in 1 secondo. Se vengono emessi cinquecento "1", corrisponde a 5V; se tutti sono "0", corrisponde a 0V; se viene emesso il pattern 250 01, corrisponde a 2.5V.

Questo processo può essere paragonato alla visione di un film. I film che guardiamo non sono completamente continui. In realtà, vengono generate 25 immagini al secondo, che l'occhio umano non riesce a distinguere. Pertanto, lo interpretiamo come un processo continuo. Il PWM funziona allo stesso modo. Per emettere tensioni diverse, è necessario controllare il rapporto tra 0 e 1. Più "0" o "1" vengono emessi per unità di tempo, più il controllo è preciso.

#### **(2)Parametri:**

![](./media/image-20250709104949184.png)

Interfaccia di controllo: Porta digitale 3

Tensione di lavoro: DC 3.3-5V

Passo tra i pin: 2.54mm

Colore del display LED: giallo

#### **(3)Schema di Collegamento:**

I pin PWM di Arduino sono collegati a 3, 5, 6, 9, 10 e 11. Mantenere invariato il pin 9

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.1

pwm

http://www.keyestudio.com

*/

int LED = 9; // Definisce il pin del LED come 9

void setup () 
{
	pinMode(LED, OUTPUT); // Imposta il pin del LED su OUTPUT
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED acceso
		delay(5); // ritardo di 5ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // il LED si affievolisce
		delay(5); // ritardo di 5ms
	}
}
```

#### **(5)Risultati del Test:**

Dopo aver caricato correttamente il codice di test, il LED cambia gradualmente da luminoso a scuro, come il respiro umano, anziché accendersi e spegnersi immediatamente.

#### **(6)Spiegazione del Codice:**

Per ripetere alcune istruzioni specifiche, possiamo usare l'istruzione FOR. Il formato dell'istruzione FOR è mostrato di seguito:

![图1(1)](media/65da124bdd0ea488291c71c6b879fe95.jpeg)

Sequenza ciclica FOR:

Turno 1：1 → 2 → 3 → 4

Turno 2：2 → 3 → 4

…

Finché il numero 2 non è più verificato, il ciclo "for" termina.

Dopo aver compreso questo ordine, torniamo al codice:

**for (int value = 0; value \< 255; value=value+1){**

**...}**

**for (int value = 255; value \>0; value=value-1){**

**...}**

Le due istruzioni "for" fanno aumentare il valore da 0 a 255, poi diminuire da 255 a 0, poi aumentare di nuovo a 255,... in ciclo infinito.

Nel codice è presente una nuova funzione ----- analogWrite()

Sappiamo che la porta digitale ha solo due stati, 0 e 1. Come si invia quindi un valore analogico a un valore digitale? Qui è necessaria questa funzione. Osserviamo la scheda Arduino e troviamo 6 pin contrassegnati con "\~" che possono emettere segnali PWM.

Il formato della funzione è il seguente:

**analogWrite(pin,value)**

analogWrite() viene utilizzata per scrivere un valore analogico da 0 a 255 per la porta PWM, quindi il valore è nell'intervallo 0\~255. Attenzione: è possibile scrivere solo sui pin digitali con funzione PWM, come il pin 3, 5, 6, 9, 10, 11.

Il PWM è una tecnologia per ottenere quantità analogiche tramite metodi digitali. Il controllo digitale forma un'onda quadra, e il segnale dell'onda quadra ha solo due stati di accensione e spegnimento (ovvero livelli alti o bassi). Controllando il rapporto tra la durata dell'accensione e dello spegnimento, è possibile simulare una tensione variabile da 0 a 5V. Il tempo di accensione (accademicamente denominato livello alto) è chiamato larghezza di impulso, quindi il PWM è chiamato anche modulazione della larghezza di impulso.

Attraverso le seguenti cinque onde quadre, approfondiamo la conoscenza del PWM.

![](media/553f3d1b6ca04e1aa0479841dd075fa2.png)

Nella figura sopra, la linea verde rappresenta un periodo, e il valore di analogWrite() corrisponde a una percentuale chiamata anche Ciclo di Lavoro (Duty Cycle).

Il ciclo di lavoro indica che la durata del livello alto è divisa per la durata del livello basso in un ciclo. Dall'alto verso il basso, il ciclo di lavoro della prima onda quadra è 0% e il suo valore corrispondente è 0. La luminosità del LED è minima, ovvero spento. Più a lungo dura il livello alto, più il LED è luminoso. Pertanto, l'ultimo ciclo di lavoro è 100%, che corrisponde a 255, e il LED è al massimo della luminosità. E il 25% significa più scuro.

Il PWM viene utilizzato principalmente per regolare la luminosità del LED o la velocità di rotazione dei motori.

Svolge un ruolo fondamentale nel controllo dei robot car intelligenti. Sono sicuro che non vedete l'ora di passare al prossimo progetto.

#### **(7)Esercitazione Avanzata:**

Modifichiamo il valore del ritardo mantenendo invariato il pin, quindi osserviamo come cambia il LED.

**Codice di Test**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.2

pwm-slow

http://www.keyestudio.com

*/

int LED = 9; // Definisce il pin del LED come 9

void setup() 
{
	pinMode(LED, OUTPUT); // Imposta il pin del LED su OUTPUT
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED acceso
		delay(30); // ritardo di 30ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // il LED si affievolisce
		delay (30); // ritardo di 30ms
	}
}
```

Dopo aver caricato il codice sulla scheda di sviluppo, il LED lampeggia più lentamente.