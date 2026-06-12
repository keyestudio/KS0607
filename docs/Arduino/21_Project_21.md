### Progetto 21: Ventilatore

#### **(1)Descrizione：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Questo modulo ventilatore utilizza un chip di controllo motore HR1124S, un chip driver H-bridge a canale singolo contenente transistor di potenza PMOS e NMOS a bassa resistenza di conduzione. La bassa resistenza di conduzione può ridurre il consumo energetico, contribuendo al funzionamento sicuro del chip per un tempo più lungo.

Inoltre, la sua bassa corrente di standby e la bassa corrente di lavoro statica lo rendono adatto ai giocattoli. Possiamo controllare la direzione di rotazione e la velocità del ventilatore inviando segnali IN+ e IN- e segnali PWM.

#### **(2)Specifiche:**

Tensione di lavoro: 5V

Corrente: 200MA

Potenza massima: 2W

Temperatura di funzionamento: da -10 gradi Celsius a +50 gradi Celsius

Dimensioni: 47.6MM \*23.8MM

#### **(3)Schema di collegamento:**

Il modulo ventilatore necessita di essere alimentato con corrente elevata; pertanto, installiamo un portabatterie.

![](media/2bd9aa5cc21e274458328958561f1915.png)

I pin GND, VCC, IN+ e IN- del modulo ventilatore sono collegati ai pin G, V, D12 e D13 dello shield.

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.1
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;

void setup()
{
    pinMode(INA, OUTPUT);//Imposta la porta digitale INA come uscita
    pinMode(INB, OUTPUT);//Imposta la porta digitale INB come uscita
}

void loop() 
{
    //Imposta il ventilatore per ruotare in senso antiorario per 3s
    digitalWrite(INA, LOW);
    digitalWrite(INB, HIGH);
    delay(3000);
    //Imposta il ventilatore per fermarsi per 1s
    digitalWrite(INA, LOW);
    digitalWrite(INB, LOW);
    delay(1000);
    //Imposta il ventilatore per ruotare in senso orario per 3s
    digitalWrite(INA, HIGH);
    digitalWrite(INB, LOW);
    delay(3000);
}
```

#### **(5)Risultati del Test：**

Carica il codice, collega i componenti e inserisci l'alimentazione. Il piccolo ventilatore girerà in senso antiorario per 3000ms, si fermerà per 1000ms e girerà in senso orario per 3000ms.

![](./media/img-20240117085032.png)

#### **(6)Pratica Avanzata:**

Abbiamo compreso il principio di funzionamento del sensore di fiamma. Ora, collegare un sensore di fiamma nel circuito, come mostrato di seguito. Quindi controllare il ventilatore per spegnere il fuoco con il sensore di fiamma.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.2
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;
int flame = A1; //Definisci il pin della fiamma come pin analogico A1
int val = 0; //Definisci variabili digitali

void setup() 
{
    pinMode(INA, OUTPUT);//Imposta la porta digitale INA come uscita
    pinMode(INB, OUTPUT);//Imposta la porta digitale INB come uscita
    pinMode(flame, INPUT); //Definisci la fiamma come sorgente di ingresso
}

void loop() 
{
    val = analogRead(flame); //Leggi il valore analogico del sensore di fiamma
    if (val <= 700)  //Quando il valore analogico≤700, il ventilatore è acceso
    {
        //Accendi il ventilatore quando viene rilevata una fiamma
        digitalWrite(INA, LOW);
        digitalWrite(INB, HIGH);
    } 
    else 
    {
        //Altrimenti si ferma
        digitalWrite(INA, LOW);
        digitalWrite(INB, LOW);
    }
}
```

Dopo aver caricato il codice, accendi l'interruttore di alimentazione dello shield del driver motore; potrai accendere il ventilatore quando viene rilevata una fiamma dal sensore di fiamma sinistro del robot.

![](./media/image-20250709115926832.png)