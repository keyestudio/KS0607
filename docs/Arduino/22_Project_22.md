### Progetto 22: Carro Armato Antincendio


#### **(1)Descrizione:**

La funzione di inseguimento della linea del carro armato intelligente è stata spiegata nel progetto precedente. In questo progetto utilizziamo il sensore di fiamma per realizzare un robot antincendio.

Quando il veicolo incontra delle fiamme, il motore della ventola ruoterà per spegnere il fuoco. Naturalmente, dobbiamo prima sostituire il sensore a ultrasuoni e i due fotoresistori con un modulo ventola e sensori di fiamma.

La logica specifica del carro armato intelligente per il tracciamento della linea è mostrata nella tabella seguente:

| Sensore Fiamma Sinistro | Sensore Fiamma Destro | Stato                                                       |
| :---------------------: | :-------------------: | :---------------------------------------------------------- |
|          ≤700           |         ≤700          | Il carro si ferma, la ventola inizia a ruotare per spegnere la fiamma |
|          ≥700           |         ≥700          | Il carro si ferma, la ventola inizia a ruotare per spegnere la fiamma |
|          ≥700           |         ≥700          | Il carro si ferma, la ventola inizia a ruotare per spegnere la fiamma |
|          ＞700          |         ＞700         | La ventola si ferma, il carro si muove                      |

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Questo esperimento richiede l'uso di una fonte di fuoco. Si prega di tenerla lontana da materiali infiammabili per prevenire incendi. I bambini devono sperimentare sotto la supervisione di un adulto. Se non si è sicuri della propria sicurezza, si prega di abbandonare l'esperimento.
2）Il sensore di fiamma non è ignifugo, si prega di non bruciarlo direttamente con la fiamma.
Possiamo controllare un LED esterno con il sensore di fiamma. Il LED è ancora collegato a D9. Quando viene rilevato il fuoco, il LED si accenderà.

#### **(2)Diagramma di flusso:**

![](media/wps12.png)

#### **(3)Schema di collegamento:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, poiché il caricamento del codice utilizza anch'esso la comunicazione seriale e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 22
  Fire extinguishing tank
  http://www.keyestudio.com
*/

int flame_L = A1; //Definisce l'interfaccia della fiamma a sinistra come pin analogico A1
int flame_R = A2; //Definisce l'interfaccia della fiamma a destra come pin analogico A2
//Il cablaggio del sensore di tracciamento della linea
#define L_pin  11  //sinistra
#define M_pin  7  //centro
#define R_pin  8  //destra
//Il pin del servo 130
int INA = 12;
int INB = 13;
#define ML_Ctrl 4  //Definisce il pin di controllo della direzione del motore sinistro
#define ML_PWM 6   //Definisce il pin di controllo PWM del motore sinistro
#define MR_Ctrl 2  //Definisce il pin di controllo della direzione del motore destro
#define MR_PWM 5   //Definisce il pin di controllo PWM del motore destro
int L_val, M_val, R_val, flame_valL, flame_valR;

void setup()
{
  Serial.begin(9600);
  //Imposta tutti i pin del sensore di tracciamento della linea in modalità input
  pinMode(L_pin, INPUT);
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  //Definisce la fiamma come INPUT
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
  //Definisce il motore come OUTPUT
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  pinMode(INA, OUTPUT);//Imposta la porta digitale INA come OUTPUT
  pinMode(INB, OUTPUT);//Imposta la porta digitale INB come OUTPUT
}

void loop () 
{
  //Legge il valore analogico dei sensori di fiamma
  flame_valL = analogRead(flame_L);
  flame_valR = analogRead(flame_R);
  Serial.print(flame_valL);
  Serial.print("  ");
  Serial.print(flame_valR);
  Serial.println("  ");
//  delay(500);
  if (flame_valL <= 700 || flame_valR <= 700) 
  {
    Car_Stop();
    fan_begin();
  } 
  else 
  {
    fan_stop();
    L_val = digitalRead(L_pin); //Legge il valore del sensore sinistro
    M_val = digitalRead(M_pin); //Legge il valore del sensore centrale
    R_val = digitalRead(R_pin); //Legge il valore del sensore destro
    
    if (M_val == 1)  //il sensore centrale rileva le linee nere
    {
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
    else  //Il sensore centrale non rileva linee nere
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
}

void fan_stop() 
{
  //smetti di ruotare
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

void fan_begin() 
{
  //la ventola ruota
  digitalWrite(INA, LOW);
  digitalWrite(INB, HIGH);
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 150);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 150);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
  
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Risultato del Test:**

Dopo aver caricato con successo il codice di test e alimentato il dispositivo, il carro armato intelligente spegne il fuoco quando rileva una fiamma e continua a muoversi lungo la linea nera.

![](media/694677ab33053846ec588667dc40ecfa.jpeg)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Si prega di tenerlo lontano da materiali infiammabili per prevenire incendi. I bambini devono sperimentare sotto la supervisione di un adulto. Se non si è sicuri della propria sicurezza, si prega di abbandonare l'esperimento. Il sensore di fiamma non è ignifugo, si prega di non bruciarlo direttamente con la fiamma.