### Progetto 14: Tank Seguiriga


#### **(1)Descrizione:**

Il progetto precedente ha illustrato come confinare l'auto intelligente a muoversi in uno spazio determinato. In questo progetto, potremmo utilizzare le conoscenze apprese in precedenza per trasformarla in un'auto intelligente seguiriga. Nell'esperimento, utilizziamo il sensore di rilevamento della linea per rilevare se c'è una linea nera intorno all'auto intelligente, quindi controlliamo la rotazione dei due motori in base ai risultati del rilevamento, in modo da far muovere l'auto intelligente lungo la linea nera.

La logica specifica dell'auto intelligente seguiriga è mostrata nella tabella seguente:

|               Sensore               |                          Rilevamento                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Sensore di rilevamento linea al centro | Linea nera rilevata: livello alto<br />Linea bianca rilevata: livello basso |
|  Sensore di rilevamento linea a sinistra  | Linea nera rilevata: livello alto<br />Linea bianca rilevata: livello basso |
| Sensore di rilevamento linea a destra  | Linea nera rilevata: livello alto<br />Linea bianca rilevata: livello basso |

|                         Condizione 1                          |                         Condizione 2                          |             Movimento             |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :------------------------------: |
| Il sensore di rilevamento linea al centro <br />rileva la linea nera | Il sensore di rilevamento linea a sinistra rileva la linea nera <br />e <br />quello a destra rileva la linea bianca | Ruota a sinistra<br />imposta PWM a 200  |
| Il sensore di rilevamento linea al centro <br />rileva la linea nera | Il sensore di rilevamento linea a sinistra rileva la linea bianca <br />e <br />quello a destra rileva la linea nera | Ruota a destra<br />imposta PWM a 200 |
| Il sensore di rilevamento linea al centro <br />rileva la linea nera | Entrambi i sensori sinistro e destro rilevano la linea bianca<br />o<br />Entrambi i sensori sinistro e destro rilevano la linea nera |           Avanza           |
| Il sensore di rilevamento linea al centro <br />rileva la linea bianca  | Il sensore di rilevamento linea a sinistra rileva la linea nera <br />e <br />quello a destra rileva la linea bianca | Ruota a sinistra<br />imposta PWM a 200  |
| Il sensore di rilevamento linea al centro <br />rileva la linea bianca  | Il sensore di rilevamento linea a sinistra rileva la linea bianca<br />e <br />quello a destra rileva la linea nera | Ruota a destra<br />imposta PWM a 200 |
| Il sensore di rilevamento linea al centro <br />rileva la linea bianca  | Entrambi i sensori sinistro e destro rilevano la linea bianca<br />o<br />Entrambi i sensori sinistro e destro rilevano la linea nera |               Ferma               |

#### **(2)Diagramma di flusso:**

![](media/wps11.png)

#### **(3)Schema di collegamento:**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)Codice di test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 14
  Line track tank
  http://www.keyestudio.com
*/

//Il collegamento del sensore di rilevamento linea
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
  Serial.begin(9600); //Imposta la velocità di trasmissione a 9600
  pinMode(L_pin, INPUT); //Imposta tutti i pin del sensore di rilevamento linea come modalità input
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); //Legge il valore del sensore sinistro
  M_val = digitalRead(M_pin); //Legge il valore del sensore centrale
  R_val = digitalRead(R_pin); //Legge il valore del sensore destro
  if (M_val == 1) { //quello centrale rileva linee nere
    if (L_val == 1 && R_val == 0)  //Se viene rilevata una linea nera a sinistra, ma non a destra, gira a sinistra
    {
      Car_left();
    }
    else if (L_val == 0 && R_val == 1)  //Se viene rilevata una linea nera a destra, non a sinistra, gira a destra
    {
      Car_right();
    }
    else  //altrimenti, vai avanti
    {
      Car_front();
    }
  }
  else  //quello centrale non rileva linee nere
  {
    if (L_val == 1 && R_val == 0)  //Se viene rilevata una linea nera a sinistra, ma non a destra, gira a sinistra
    {
      Car_left();
    }
    else if (L_val == 0 && R_val == 1)  //Se viene rilevata una linea nera a destra, non a sinistra, gira a destra
    {
      Car_right();
    }
    else  //altrimenti, fermati
    {
      Car_Stop();
    }
  }
}

//vai avanti
void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

//vai indietro
void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

//gira a sinistra
void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

//gira a destra
void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

//fermati
void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Risultato del test:**

Dopo aver caricato con successo il codice di test e aver alimentato il dispositivo, l'auto intelligente si muove lungo la linea nera.

![](./media/img-20240117085916.png)