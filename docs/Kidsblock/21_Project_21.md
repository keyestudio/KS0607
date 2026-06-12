### Progetto 21: Carro Armato Antincendio

#### **(1)Descrizione:**

La funzione di rilevamento della linea del carro armato intelligente è stata spiegata nel progetto precedente. In questo progetto utilizziamo il sensore di fiamma per realizzare un robot antincendio.

Quando il veicolo incontra delle fiamme, il motore della ventola ruoterà per spegnere il fuoco. Ovviamente, dobbiamo prima sostituire il sensore a ultrasuoni e le due fotoresistenze con un modulo ventola e sensori di fiamma.

La logica specifica del veicolo intelligente è mostrata nella tabella seguente:

| Sensore Fiamma Sinistro | Sensore Fiamma Destro | Stato                                                        |
| :---------------------: | :-------------------: | :----------------------------------------------------------- |
|          ≤700           |         ≤700          | Il veicolo si ferma, la ventola inizia a ruotare per spegnere la fiamma |
|          ≥700           |         ≥700          | Il veicolo si ferma, la ventola inizia a ruotare per spegnere la fiamma |
|          ≥700           |         ≥700          | Il veicolo si ferma, la ventola inizia a ruotare per spegnere la fiamma |
|          ＞700          |         ＞700         | La ventola si ferma, il veicolo si muove                    |

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Questo esperimento richiede l'uso di una fonte di fuoco. Tenerla lontana da materiali infiammabili per prevenire incendi. I bambini devono sperimentare sotto la supervisione di un adulto. Se non si è in grado di confermare la propria sicurezza, abbandonare l'esperimento.
2）Il sensore di fiamma non è ignifugo, si prega di non bruciarlo direttamente con la fiamma.
Possiamo controllare un LED esterno con il sensore di fiamma. Il LED è ancora collegato a D9. Quando viene rilevato il fuoco, il LED si accenderà.


#### **(2)Diagramma di flusso:**

![](media/wps120.png)

#### **(3)Schema di collegamento:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

GND, VCC, SDA e SCL del pannello LED 8x16 sono collegati a G（GND), V（VCC), A4 e A5.

G, V e A dei due sensori di fiamma sono interfacciati con G（GND), V（VCC), A1 e A2 della scheda di espansione.

#### **(4)Codice di Test:**


Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/2e3d4904d9605dfecb5736b4bf235ab2.png)

（4） ![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（5） ![](media/4b40151c7482ff9371570978b8ef9c77.png)

（6）![](media/c0365237fa7ec7de10e9fc465353fae1.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/c07c09e5533a37838722b8c2b513646d.png)

#### **(5)Risultati del Test:**

Dopo aver caricato con successo il codice di test, alimentare il dispositivo e portare il selettore DIP sulla posizione ON. Il veicolo intelligente spegnerà il fuoco quando rileva una fiamma.

![](media/2de5f1d832d40c0fc94274f1d87443c6.jpeg)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Tenerlo lontano da materiali infiammabili per prevenire incendi. I bambini devono sperimentare sotto la supervisione di un adulto. Se non si è in grado di confermare la propria sicurezza, abbandonare l'esperimento. Il sensore di fiamma non è ignifugo, si prega di non bruciarlo direttamente con la fiamma.