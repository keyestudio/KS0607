### Progetto 12: Tank con Elusione degli Ostacoli a Ultrasuoni

#### **(1)Descrizione:**

Nel progetto precedente, abbiamo realizzato un'auto intelligente che segue il suono a ultrasuoni. In realtà, utilizzando gli stessi componenti e lo stesso metodo di cablaggio, dobbiamo solo modificare il codice di test per trasformarla in un'auto intelligente per l'elusione degli ostacoli a ultrasuoni. Questa auto intelligente può muoversi con il movimento delle mani umane.

Utilizziamo sensori a ultrasuoni per rilevare la distanza tra l'auto intelligente e l'ostacolo di fronte, e poi controlliamo la rotazione dei due motori in base a questi dati per controllare i movimenti dell'auto intelligente.

|                          Rilevamento                          |         |
| :----------------------------------------------------------: | :-----: |
| Distanza misurata dal sensore a ultrasuoni tra l'auto e l'ostacolo di fronte <br />（impostare l'angolo del servo a 90°） | a (cm)  |
| Distanza misurata dal sensore a ultrasuoni tra l'auto e l'ostacolo a destra <br />（impostare l'angolo del servo a 0°） | a2 (cm) |
| Distanza misurata dal sensore a ultrasuoni tra l'auto e l'ostacolo a sinistra <br />（impostare l'angolo del servo a 180°） | a1 (cm) |

**Impostazione: impostare l'angolo iniziale del servo a 90°**

| Condizione 1 |        Condizione 2         |      Condizione 3       | Movimento                                                     |
| :---------: | :------------------------: | :--------------------: | :----------------------------------------------------------- |
|    a＜20    |                            |                        | Fermarsi per 500ms；impostare l'angolo del servo a 180°，leggere a1，ritardo di 100ms；impostare l'angolo del servo a 0°，leggere a2，ritardo di 0.1s. |
|             | a1＜50<br />o<br />a2＜50 | **Confrontare a1 con a2** |                                                              |
|             |                            |         a1＞a2         | Impostare l'angolo del servo a 90°，ruotare a sinistra per 700ms（impostare PWM a 255），e muoversi in avanti（impostare PWM a 200）. |
|             |                            |         a1＜a2         | Impostare l'angolo del servo a 90°，ruotare a destra per 700ms（impostare PWM a 255），e muoversi in avanti（impostare PWM a 200）. |
|             | a1≥50<br />e<br />a2≥50  |         Casuale         | Impostare l'angolo del servo a 90°，ruotare a sinistra per 500ms（impostare PWM a 255），e muoversi in avanti（impostare PWM a 200）.<br /><br />Impostare l'angolo del servo a 90°，ruotare a destra per 500ms（impostare PWM a 255），e muoversi in avanti（impostare PWM a 200）. |
|    a≥20     |                            |                        | muoversi in avanti（impostare PWM a 100）                               |

#### **(2)Diagramma di flusso:**

![](media/wps119.png)

#### **(3)Schema di collegamento:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

(<span style="color: rgb(255, 76, 65);">Nota:</span> i fili marrone, rosso e arancione del servo sono collegati rispettivamente a G (GND), V（5V）e D10 della scheda di espansione；e per il sensore a ultrasuoni, il pin VCC è collegato al 5v (V), il pin Trig al digitale 12 (S), il pin Echo al digitale 13 (S), e il pin Gnd a Gnd (G); come nel progetto precedente.）

#### **(4)Codice di Test:**


Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito.![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/5dcbd405806b8e341505d7316246dbdd.png)

（3）![](media/996c8d4e5dd9620757dfb097329e7d5d.png)

（4）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

（10）![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

（11）![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/4360f9642a8c6b2488767c079d481482.png)

#### **(5)Risultati del Test:**

Dopo aver caricato con successo il codice di test, effettuare il cablaggio, portare il selettore DIP sull'estremità ON e alimentare il dispositivo. L'auto intelligente si muoverà in avanti ed eviterà automaticamente gli ostacoli.

![](./media/img-20240117093950.png)