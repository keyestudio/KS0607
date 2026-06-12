### Progetto 19: Sensore di Fiamma

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Descrizione:**

Il sensore di fiamma utilizza un tubo ricevitore IR per rilevare le fiamme. Converte la luminosità della fiamma in segnali di livello alto e basso e li invia al processore centrale per la corrispondente elaborazione del programma. Il valore di tensione della porta analogica varia a seconda che ci sia una fiamma nelle vicinanze o nessuna fiamma.

Se non c'è fiamma, la porta analogica legge circa 0.3V; quando c'è una fiamma, la porta analogica legge circa 1.0V. Più la fiamma è vicina, più alto è il valore di tensione. Può essere utilizzato per rilevare una fonte di fuoco o per costruire un robot intelligente.

Si noti che la sonda del sensore di fiamma può resistere solo a temperature comprese tra -25℃ e 85℃.

Durante l'uso, assicurarsi di mantenere il sensore di fiamma a una distanza di sicurezza dal fuoco per evitare di danneggiarlo.

#### **(2)Parametri:**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Tensione di lavoro: 3.3V-5V (DC)

- Corrente: 100mA

- Potenza massima: 0.5W

- Temperatura di lavoro: da -10°C a +50 gradi Celsius

- Dimensioni del sensore: 31.6mmx23.7mm

- Interfaccia: interfaccia da 4pin a 3PIN

- Segnale di uscita: segnali analogici A0, A1

#### **(3)Schema di Collegamento:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

Il pin A dei due fotoresistori è collegato ad A1 e A2. Colleghiamo il sensore di fiamma ad A1 e A2. Sostituendo i due fotoresistori e il sensore a ultrasuoni con due sensori di fiamma e una ventola, si crea un'auto antincendio.

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Questo esperimento richiede l'uso di una fonte di fuoco. Si prega di tenerla lontana da materiali infiammabili per prevenire incendi. I bambini devono sperimentare sotto la supervisione di un adulto. Se non si è certi di essere al sicuro, si prega di abbandonare l'esperimento.
2）**Il sensore di fiamma non è ignifugo, si prega di non bruciarlo direttamente con la fiamma.**

#### **(4)Codice di Test:**

È possibile anche trascinare blocchi per modificare il codice, come mostrato di seguito

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/4bc6c8a4d6e964fd078a6aeb0dd51ff4.png)

#### **(5)Risultati del Test:**

Collegare i componenti, caricare il codice, aprire il monitor seriale e impostare il baud rate a 9600.

È possibile visualizzare il valore di simulazione del sensore di fiamma.

Più la fiamma è vicina, minore è il valore di simulazione.

Regolare il potenziometro sul modulo per mantenere il LED al punto critico. Quando il sensore non rileva fiamma, il LED sarà spento, ma se il sensore rileva fiamma, il LED si accenderà.

![](./media/img-20240117100139.png)

![](media/60d0ce2044a504135af3b1113a1a4c7d.png)

#### **(6)Pratica di Estensione:**

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Questo esperimento richiede l'uso di una fonte di fuoco. Si prega di tenerla lontana da materiali infiammabili per prevenire incendi. I bambini devono sperimentare sotto la supervisione di un adulto. Se non si è certi di essere al sicuro, si prega di abbandonare l'esperimento.
2）Il sensore di fiamma non è ignifugo, si prega di non bruciarlo direttamente con la fiamma.
Possiamo controllare un LED esterno con il sensore di fiamma. Il LED è ancora collegato a D9. Quando viene rilevato il fuoco, il LED si accenderà.

![](media/814c315d3bb44278b476a754d3681227.png)

È possibile trascinare blocchi per modificare il codice, come mostrato di seguito

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/9d2f5915e4a6991ed4549b39ec853fa5.png)

È possibile usare la fiamma di un accendino vicino al sensore di fiamma sinistro. Quando il sensore di fiamma rileva una fiamma, il modulo LED si accenderà come allarme.

![](./media/img-20240117100333.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Si prega di tenerla lontana da materiali infiammabili per prevenire incendi. I bambini devono sperimentare sotto la supervisione di un adulto. Se non si è certi di essere al sicuro, si prega di abbandonare l'esperimento. Il sensore di fiamma non è ignifugo, si prega di non bruciarlo direttamente con la fiamma.