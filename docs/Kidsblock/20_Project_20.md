### Progetto 20: Ventilatore

#### **(1)Descrizione：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Questo modulo ventilatore utilizza un chip di controllo motore HR1124S, un chip driver H-bridge a canale singolo contenente transistor di potenza PMOS e NMOS a bassa resistenza di conduzione. La bassa resistenza di conduzione può ridurre il consumo energetico, contribuendo al funzionamento sicuro del chip per un tempo più lungo.

Inoltre, la sua bassa corrente in standby e la bassa corrente di lavoro statica lo rendono adatto ai giocattoli. Possiamo controllare la direzione di rotazione e la velocità del ventilatore inviando segnali IN+ e IN- e segnali PWM.

#### **(2)Parametri:**

- Tensione di lavoro: 5V

- Corrente: 200mA

- Potenza massima: 2W

- Temperatura di lavoro: da -10°C a +50 gradi Celsius

- Dimensioni: 47,6mm \* 23,8mm

#### **(3)Schema di collegamento:**

Il modulo ventilatore necessita di essere alimentato con corrente elevata; pertanto, installiamo un portabatterie.

![](media/2bd9aa5cc21e274458328958561f1915.png)

I pin GND, VCC, IN+ e IN- del modulo ventilatore sono collegati ai pin G, V, 12 e 13 dello shield.

#### **(4)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/1360090880c1cd9b20671c17604f4108.png)

![](media/4e9354e674060efe6cf540a3e1b87813.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/cbb8f153dd0d114bdd350577af7a1f02.png)

#### **(5)Risultati del Test:**

Carica il codice, collega i componenti, accendi e porta l'interruttore DIP su ON. Il piccolo ventilatore girerà in senso orario per 2s, si fermerà per 2s e girerà in senso antiorario per 2s

![](./media/img-20240117100504.png)

#### **(6)Pratica di Estensione:**

Abbiamo compreso il principio di funzionamento del sensore di fiamma. Successivamente, collega un sensore di fiamma nel circuito, come mostrato di seguito. Quindi controlla il ventilatore per spegnere le fiamme con il sensore di fiamma.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)


Puoi trascinare i blocchi per modificare il tuo codice, come mostrato di seguito

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/74ddb07daf4063f0640c31f4243a0864.png)


Dopo aver caricato il codice, accendi l'interruttore di alimentazione dello shield di controllo motore; potrai accendere il ventilatore quando viene rilevata una fiamma dal sensore di fiamma sinistro del robot.

![](./media/img-20240117102303.png)