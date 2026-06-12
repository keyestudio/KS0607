### Progetto 13: Carro Armato in Movimento in uno Spazio Limitato


#### **(1)Descrizione:**

Le funzioni di inseguimento tramite ultrasuoni e di evitamento degli ostacoli del robot smart car sono state introdotte nei progetti precedenti. Qui intendiamo combinare le conoscenze dei corsi precedenti per confinare il robot smart car in modo che si muova in un determinato spazio.

Nell'esperimento, utilizziamo il sensore di rilevamento della linea per rilevare se c'è una linea nera intorno al robot smart car, e poi controlliamo la rotazione dei due motori in base ai risultati del rilevamento, in modo da bloccare il robot smart car all'interno di un cerchio tracciato con una linea nera.

La logica specifica del robot smart car con rilevamento della linea è mostrata nella tabella seguente:

![](./media/image-20250709112523897.png)

|                         Condizione                         |                         Movimento                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Se uno dei tre sensori di rilevamento della linea rileva linee nere | Vai indietro（imposta PWM a 150）Poi gira a sinistra（imposta PWM a 150） |
|             Nessuno di essi rileva linee nere              |               Vai avanti（imposta PWM a 100）                |

#### **(2)Diagramma di flusso:**

![](media/image-20230427092708208.png)

#### **(3)Schema di collegamento:**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 13
  draw a circle for tank
  http://www.keyestudio.com
*/

//Collegamento del sensore di rilevamento della linea
#define L_pin  11  //sinistra
#define M_pin  7  //centro
#define R_pin  8  //destra

#define ML_Ctrl 4  //Definisce il pin di controllo della direzione del motore sinistro
#define ML_PWM 6   //Definisce il pin di controllo PWM del motore sinistro
#define MR_Ctrl 2  //Definisce il pin di controllo della direzione del motore destro
#define MR_PWM 5   //Definisce il pin di controllo PWM del motore destro
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); //Imposta il baud rate a 9600
  pinMode(L_pin, INPUT); //Imposta tutti i pin del sensore di rilevamento della linea come modalità input
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); //Leggi il valore del sensore sinistro
  M_val = digitalRead(M_pin); //Leggi il valore del sensore centrale
  R_val = digitalRead(R_pin); //Leggi il valore del sensore destro
  if ( L_val == 0 && M_val == 0 && R_val == 0 )  //quando le linee nere non vengono rilevate, vai avanti
  {
    Car_front();
  }
  else  //le linee nere vengono rilevate, vai indietro poi gira a sinistra
  {
    Car_back();
    delay(700);
    Car_left();
    delay(800);
  }
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Risultati del Test:**

Dopo aver caricato con successo il codice di test e averlo alimentato, il robot smart car si muove in uno spazio confinato, all'interno del cerchio tracciato con la linea nera.

![](./media/img-20240117090340.png)