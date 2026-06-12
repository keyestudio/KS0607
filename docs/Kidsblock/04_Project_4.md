### Progetto 4: Sensore di Inseguimento Linea

#### **(1)Descrizione:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

Il sensore di tracciamento è in realtà un sensore a infrarossi. Il componente utilizzato qui è il tubo a infrarossi TCRT5000.

Il suo principio di funzionamento consiste nell'utilizzare la diversa riflettività della luce infrarossa ai colori, per poi convertire l'intensità del segnale riflesso in un segnale di corrente.

Durante il processo di rilevamento, il nero è attivo al livello ALTO mentre il bianco è attivo al livello BASSO. L'altezza di rilevamento è 0-3 cm.

Il modulo di tracciamento linea a 3 canali Keyestudio ha integrato 3 set di tubi a infrarossi TCRT5000 su una singola scheda, il che è più conveniente per il cablaggio e il controllo.

Se il Sensore di Inseguimento Linea non funziona come previsto, sarà necessario utilizzare un cacciavite per regolare il suo potenziometro per renderlo più sensibile. Quando il dito si avvicina al sensore, il suo LED integrato si accende, e quando il dito si allontana, il suo LED integrato si spegne. In questo momento, la sua sensibilità è relativamente buona.

![](./media/img-20240117091947.png)

#### **(2)Parametri:**

- Tensione di funzionamento: 3.3-5V (DC)
- Interfaccia: 5PIN
- Segnale di uscita: Segnale digitale
- Altezza di rilevamento: 0-3 cm

Nota speciale: prima del test, ruotare il potenziometro sul sensore per regolare la sensibilità di rilevamento. Quando si regola il LED alla soglia tra ON e OFF, la sensibilità è la migliore.

<span style="color: rgb(255, 76, 65);">Nota:</span> il sensore di inseguimento linea è installato sotto il fondo del robot.

#### **(3)Schema di Collegamento:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4)Codice di Test:**

È anche possibile trascinare i blocchi per modificare il codice, come mostrato di seguito.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/700cb0ecc14cbccd6e367c5098360f08.png)

![](media/271423c55b5f147796beb344eed7e9cf.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/5298cdfb6fd7c71df155c969c80450cd.png)

#### **(5)Risultati del Test:**

Caricare il codice sulla scheda di sviluppo, aprire il monitor seriale a 9600 e verificare i sensori di inseguimento linea. Il valore visualizzato è 1 (livello alto) quando non vengono ricevuti segnali. Il valore passa a 0 quando il sensore viene coperto con della carta.

![](media/5630032421adf9446d51b770f0e7f8af.png)

#### **(6)Pratica di Estensione:**

Possiamo controllare un LED con questo sensore. Il LED è collegato a D9. Se lo copriamo, il LED si accenderà.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

È anche possibile trascinare i blocchi per modificare il codice, come mostrato di seguito.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/574854f4d96c40a85e1db549d85f14f4.png)

![](media/9077c0d059f7a4d3277f10ccb4e962fb.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

![](media/80e9c514357c63f4791c72220829b673.png)

![](media/b10e1897e99af2c1ade6c09da6c30dba.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/b5a4b5a04cdee9f79d6e18a5c48cbe48.png)

Quando un oggetto (come carta o un dito) si avvicina al sensore di inseguimento linea, il sensore rileva il segnale di ritorno emesso da se stesso, e il modulo LED si accende. Quando il sensore non rileva alcun segnale di ritorno, il modulo LED si spegne.

![](./media/img-20240117092116.png)