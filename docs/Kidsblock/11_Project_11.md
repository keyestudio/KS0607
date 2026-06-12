### Progetto 11: Tank che Segue il Suono a Ultrasuoni


#### **(1)Descrizione:**

Nella lezione precedente, abbiamo imparato a conoscere l'auto intelligente che segue la luce. In questa lezione, possiamo combinare le conoscenze acquisite per realizzare un'auto che segue il suono a ultrasuoni. Nel progetto, utilizziamo sensori a ultrasuoni per rilevare la distanza tra l'auto e l'ostacolo davanti, e poi controlliamo la rotazione dei due motori in base a questi dati in modo da controllare i movimenti dell'auto intelligente.

La logica specifica dell'auto intelligente che segue il suono a ultrasuoni è mostrata nella tabella seguente:

|                        Rilevamento                        |              Impostazione              |
| :-----------------------------------------------------: | :-------------------------------: |
| La distanza (cm) tra l'auto e l'ostacolo frontale | Imposta l'angolo del servo a 90° |
|                      **Condizione**                      |           **Movimento**            |
|               distanza≥20 e distanza≤50               |             Vai avanti              |
|            10＜distanza＜20<br/>distanza＞50            |               Stop                |
|                       distanza≤10                       |              Vai indietro              |

#### **(2)Diagramma di Flusso:**

![](media/wps118.png)

#### **(3)Schema di Collegamento:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

<span style="color: rgb(255, 76, 65);">Nota:</span> Il collegamento del sensore a ultrasuoni, del servo e del motore è lo stesso dell'esperimento del progetto precedente. GND, VCC, SDA e SCL del pannello LED 8x16 sono collegati rispettivamente a G (GND), V (VCC), A4 e A5 sulla scheda di espansione.

#### **(4)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito.

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/f6fb93211f786d023eb77eb210eae454.png)

（3）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

(7) ![](media/4b40151c7482ff9371570978b8ef9c77.png)

(8) ![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

(9) ![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

(10) ![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

![](media/b895ca60e3249e09d4c15c356c60099a.png)


#### **(5)Risultato del Test:**

Carica il codice, alimenta il dispositivo e porta l'interruttore DIP su ON. Il servo ruoterà di 90°, il pannello LED 8X16 mostrerà ![](media/fdd4ae50b3372cc9c4ef27f6bddda387.png), e l'auto seguirà l'ostacolo durante il movimento.

![](./media/img-20240117093900.png)