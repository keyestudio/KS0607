### Progetto 8: Controllo e Velocità del Motore

#### **(1)Descrizione:**

Esistono molti modi per pilotare i motori. La nostra auto intelligente utilizza la soluzione più comune chiamata L298P. L298P, prodotto da STMicroelectronics, è un eccellente chip di pilotaggio appositamente progettato per guidare motori ad alta potenza. Può pilotare direttamente motori DC, motori a due e quattro fasi con una corrente di pilotaggio fino a 2A. Il terminale di uscita del motore adotta 8 diodi Schottky ad alta velocità come protezione. Abbiamo progettato una scheda di espansione basata sul circuito L298P, il cui design a impilamento può essere collegato direttamente alla scheda UNO R3 riducendo le difficoltà tecniche per gli utenti nell'uso e nel pilotaggio del motore.

Impila la scheda di espansione sulla scheda, alimenta la BAT, porta il selettore DIP sull'estremità ON e alimenta contemporaneamente la scheda di espansione e la scheda UNO R3 tramite alimentazione esterna. Per facilitare il cablaggio, la scheda di espansione è dotata di un'interfaccia anti-inversione (PH2.0 -2P -3P -4P -5P) e quindi può essere collegata direttamente con motori, alimentatori e sensori/moduli. L'interfaccia Bluetooth della scheda di espansione del driver è completamente compatibile con il modulo Bluetooth Keyestudio HM-10. Pertanto, dobbiamo solo inserire il modulo Bluetooth HM-10 nell'interfaccia corrispondente durante la connessione. Allo stesso tempo, la scheda di espansione del driver utilizza anche header pin da 2,54 mm per estendere alcune porte digitali e analogiche disponibili, così da poter continuare ad aggiungere altri sensori ed effettuare esperimenti di espansione.

La scheda di espansione può essere collegata a 4 motori DC. Nella modalità di connessione con jumper cap predefinita, i motori delle interfacce A e A1, B e B1 sono collegati in parallelo e il loro schema di movimento è lo stesso. 8 jumper cap possono essere utilizzati per controllare il senso di rotazione delle 4 interfacce motore. Ad esempio, quando i due jumper cap davanti all'interfaccia del motore A vengono cambiati da una connessione orizzontale a una connessione verticale, il senso di rotazione del motore A diventa opposto a quello originale.

![](media/6c3731f639e113c8f32fe1829f239898.png)

![](media/62ee9578858ecc8e27b824af65fb22bb.png)

#### **(2)Parametri:**

-   Tensione di ingresso della parte logica: DC 5V

-   Tensione di ingresso della parte di pilotaggio: DC 7-12V

-   Corrente di funzionamento della parte logica: ≤36mA

-   Corrente di funzionamento della parte di pilotaggio: ≤ 2A

-   Potenza massima di dissipazione: 25W (T=75℃)

-   Livello del segnale di controllo in ingresso:

    Livello alto: 2.3V ≤ Vin ≤ 5V

    Livello basso: 0V ≤ Vin ≤ 1.5V

-   Temperatura di funzionamento: -25℃～＋130℃

#### **(3)Guida il robot a muoversi:**

Il pin di direzione del motore A è D2, il pin di controllo della velocità è D5; il pin di direzione del motore B è D4 e il pin di controllo della velocità è D6.

In base alla tabella seguente, possiamo sapere come controllare il movimento del robot controllando la rotazione di due motori tramite le porte digitali e le porte PWM. Il valore PWM è compreso nell'intervallo 0-255. Maggiore è il valore, più velocemente ruota il motore.

|   Funzione   |  D4  | D6（PWM） | Motore (sinistra) B |  D2  | D5（PWM） | Motore (destra) A |
| :----------: | :--: | :-------: | :-----------------: | :--: | :-------: | :---------------: |
| Avanza | HIGH |     0     |   Ruota a sinistra   | HIGH |     0     |   Ruota a sinistra   |
|   Indietreggia    | LOW  |    255    |  Ruota a destra   | LOW  |    255    |  Ruota a destra   |
| Gira a sinistra  | LOW  |    255    |  Ruota a destra   | HIGH |    100    |   Ruota a sinistra   |
| Gira a destra | HIGH |    100    |   Ruota a sinistra   | LOW  |    255    |  Ruota a destra   |
|     Stop     | LOW  |     0     |      Stop       | LOW  |     0     |      Stop       |

#### **(4)Schema di collegamento:**

![](./media/image-20250709134029403.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

Il connettore a 4 pin è contrassegnato con A, A1, B1 e B. Il motore posteriore destro è collegato a B della scheda 8833 e quello anteriore sinistro è collegato alla porta A.

#### **(5)Codice di Test:**

Puoi anche trascinare i blocchi per modificare il tuo codice, come mostrato di seguito.

（1）![](media/7cbc4d14c2e2dac956f2e9f145f01f31.png)

（2）![](media/0067d367772d4e3005bfc097ba3b59b0.png)

（3）![](media/f0c505e8268454c7996b755f97c6322b.png)

（4）![](media/b7215c8a4997a188947e80fdee1a8cd9.png)

**Codice di Test Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

![](media/332229f3dc01a38de898367f52531b28.png)


#### **(6)Risultati del Test:**

Dopo aver cablato secondo lo schema, caricato il codice di test e alimentato il tutto.

![](./media/img-20240117092625.png)

l'auto intelligente avanza per 2s, indietreggia per 2s, gira a sinistra per 2s, gira a destra per 2s e si ferma per 2s.