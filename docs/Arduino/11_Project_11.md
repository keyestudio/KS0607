### Progetto 11: Tank con Inseguimento a Ultrasuoni


#### **(1)Descrizione:**

Nella lezione precedente, abbiamo appreso del robot auto intelligente che segue la luce. In questa lezione, possiamo combinare le conoscenze acquisite per realizzare un'auto che segue il suono a ultrasuoni. 

Nel progetto, utilizziamo sensori a ultrasuoni per rilevare la distanza tra l'auto e l'ostacolo davanti, e poi controlliamo la rotazione dei due motori in base a questi dati per controllare i movimenti del robot auto intelligente.

La logica specifica del robot auto intelligente che segue il suono a ultrasuoni è mostrata nella tabella seguente:

|                        Rilevamento                        |              Impostazione              |
| :-------------------------------------------------------: | :------------------------------------: |
| La distanza(cm) tra l'auto e l'ostacolo frontale | Impostare l'angolo del servo a 90° |
|                      **Condizione**                      |           **Movimento**            |
|               distanza≥20 e distanza≤50               |             Avanti              |
|            10＜distanza＜20<br/>distanza＞50            |               Ferma                |
|                       distanza≤10                       |              Indietro              |

#### **(2)Diagramma di flusso:**

![](media/wps9.png)

#### **(3)Schema di collegamento:**

![](media/72a10097d286bc5f9589df031b60484a.png)

#### **(4)Codice di test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 11
  Ultrasonic follow tank
  http://www.keyestudio.com
*/
#define servoPin 10  //Il pin del servo

#define ML_Ctrl 4  //Definisce il pin di controllo della direzione del motore sinistro
#define ML_PWM 6   //Definisce il pin di controllo PWM del motore sinistro
#define MR_Ctrl 2  //Definisce il pin di controllo della direzione del motore destro
#define MR_PWM 5   //Definisce il pin di controllo PWM del motore destro
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
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
  distance = checkdistance();  //Assegna la distanza misurata dagli ultrasuoni a distance
  if (distance >= 20 && distance <= 50) //vai avanti
  {
    Car_front();
  }
  else if (distance > 10 && distance < 20)  //ferma
  {
    Car_Stop();
  }
  else if (distance <= 10)  //vai indietro
  {
    Car_back();
  }
  else  //In altre condizioni, si ferma
  {
    Car_Stop();
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

//La funzione per controllare i servo
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //Calcola il valore della larghezza dell'impulso    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //Il tempo in livello alto rappresenta la larghezza dell'impulso
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //Poiché il ciclo è 20ms, il tempo rimanente è in livello basso
  }
}
//La funzione per controllare gli ultrasuoni
float checkdistance() 
{
  static float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //Il 58.20 qui deriva da 2*29.1=58.2
  delay(10);
  return distance;
}
```

#### **(5)Risultati del test:**

Caricato con successo il codice di test, effettuati i collegamenti, spostato il commutatore DIP verso destra, alimentato il sistema e impostato il servo a 90°, il robot auto intelligente segue l'ostacolo nei suoi movimenti.

![](./media/img-20240117090457.png)