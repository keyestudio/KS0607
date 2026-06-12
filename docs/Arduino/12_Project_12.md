### Progetto 12: Tank con Evitamento Ostacoli a Ultrasuoni

![](./media/image-20250709112200577.png)


#### **(1)Descrizione:**

Nel progetto precedente, abbiamo realizzato un'auto intelligente che segue i movimenti utilizzando ultrasuoni. In realtà, utilizzando gli stessi componenti e lo stesso schema di collegamento, è sufficiente modificare il codice di test per trasformarla in un'auto intelligente che evita gli ostacoli con ultrasuoni. Questa auto intelligente può muoversi seguendo il movimento delle mani umane.

Utilizziamo i sensori a ultrasuoni per rilevare la distanza tra l'auto intelligente e l'ostacolo di fronte, e quindi controlliamo la rotazione dei due motori in base a questi dati per controllare i movimenti dell'auto intelligente.

|                          Rilevamento                         |        |
| :----------------------------------------------------------: | :----: |
| Distanza misurata dal sensore a ultrasuoni tra l'auto e l'ostacolo di fronte <br />（impostare l'angolo del servo a 90°） | a(cm)  |
| Distanza misurata dal sensore a ultrasuoni tra l'auto e l'ostacolo a destra <br />（impostare l'angolo del servo a 20°） | a2(cm) |
| Distanza misurata dal sensore a ultrasuoni tra l'auto e l'ostacolo a sinistra <br />（impostare l'angolo del servo a 160°） | a1(cm) |
|   **Impostazione:** impostare l'angolo iniziale del servo a 90°    |        |

|   Condizione 1   |        Condizione 2         | Condizione 3 | Movimento                                                     |
| :-------------: | :------------------------: | ----------- | ------------------------------------------------------------ |
|      a＜20      |                            |             | Stop per 500ms；<br />impostare l'angolo del servo a 180°, leggere a1, ritardo di 100ms；<br />impostare l'angolo del servo a 0°, leggere a2, ritardo di 0,1s. |
|                 | a1＜50<br />o<br />a2＜50 |             | Confrontare a1 con a2                                           |
|                 |                            | a1＞a2      | Impostare l'angolo del servo a 90°, ruotare a sinistra per 700ms (impostare PWM a 255)<br />avanzare（impostare PWM a 200）. |
|                 |                            | a1＜a2      | Impostare l'angolo del servo a 90°, ruotare a destra per 700ms (impostare PWM a 255) <br />avanzare（impostare PWM a 200）. |
| **Condizione 1** |      **Condizione 2**       |             | **Movimento**                                                 |
|      a＜20      | a1≥50<br />e<br />a2≥50  | Casuale      | impostare l'angolo del servo a 90°, ruotare a sinistra per 500ms (impostare PWM a 255)<br />avanzare (impostare PWM a 200)<br /><br />impostare l'angolo del servo a 90°, ruotare a destra per 500ms (impostare PWM a 255) <br />avanzare (impostare PWM a 200) |
|  **Condizione**  |                            |             | **Movimento**                                                 |
|      a≥20       |                            |             | avanzare (impostare PWM a 100)                                 |



#### **(2)Diagramma di flusso:**

![](media/wps10.png)

#### **(3)Schema di collegamento:**

![](media/72a10097d286bc5f9589df031b60484a.png)

(<span style="color: rgb(255, 76, 65);">Nota:</span> i fili marrone, rosso e arancione del servo sono collegati rispettivamente a G (GND), V（5V）e D10 della scheda di espansione；e per il sensore a ultrasuoni, il pin VCC è collegato a 5v (V), il pin Trig al digitale 12 (S), il pin Echo al digitale 13 (S), e il pin Gnd a Gnd (G); come nel progetto precedente.）

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 12
  Ultrasonic avoid tank
  http://www.keyestudio.com
*/
#define servoPin 10  //Il pin del servo
int a, a1, a2;
#define ML_Ctrl 4  //Definisce il pin di controllo della direzione del motore sinistro
#define ML_PWM 6   //Definisce il pin di controllo PWM del motore sinistro
#define MR_Ctrl 2  //Definisce il pin di controllo della direzione del motore destro
#define MR_PWM 5   //Definisce il pin di controllo PWM del motore destro
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  Serial.begin(9600);
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //Imposta l'angolo del servo a 90°
  delay(500); //ritardo di 500ms
}

void loop() 
{
  a = checkdistance();  //Assegna la distanza frontale rilevata dal sensore a ultrasuoni alla variabile a

  if (a < 20) //Quando la distanza frontale è inferiore a 20cm
  {
    Car_Stop();  //Il robot si ferma
    delay(500); //ritardo di 500ms
    procedure(180);  //Il supporto pan-tilt a ultrasuoni gira a sinistra
    delay(500); //ritardo di 500ms
    a1 = checkdistance();  //Assegna la distanza a sinistra rilevata dal sensore a ultrasuoni alla variabile a1
    delay(100); //leggi il valore
    procedure(0); //Il supporto pan-tilt a ultrasuoni gira a destra
    delay(500); //ritardo di 500ms
    a2 = checkdistance(); //Assegna la distanza a destra rilevata dal sensore a ultrasuoni alla variabile a2
    delay(100); //leggi il valore
    
    procedure(90);  //Torna a 90°
    delay(500);
    if (a1 > a2) 
    { //Quando la distanza a sinistra è maggiore di quella a destra
      Car_left();  //Il robot gira a sinistra
      delay(700);  //gira a sinistra per 700ms
    } 
    else 
    {
      Car_right(); //Gira a destra per 700ms
      delay(700);
    }
  } 
  else//Quando la distanza frontale è >=20cm，il robot avanza
  {    
    Car_front(); //vai avanti
  }

}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}

//La funzione controlla i servo
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //Calcola il valore della larghezza dell'impulso
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //Il tempo in livello alto rappresenta la larghezza dell'impulso
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //Poiché il ciclo è di 20ms, il tempo rimanente è in livello basso
  }
}

//La funzione controlla gli ultrasuoni
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //Il 58.20 deriva da 2*29.1=58.2
  delay(10);
  return distance;
}
```

#### **(5)Risultato del Test:**

Dopo aver caricato con successo il codice di test, collegato i cavi, spostato il selettore DIP sull'estremità ON e alimentato il sistema, l'auto intelligente avanza e schiva automaticamente gli ostacoli.

![](./media/img-20240117090420.png)