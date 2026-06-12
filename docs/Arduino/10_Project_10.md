### Progetto 10: Tank Insegui-Luce


#### **(1)Descrizione:**

Nei progetti precedenti, abbiamo introdotto in dettaglio l'uso di vari sensori, moduli e schede di espansione sul robot smart car. Ora passiamo ai progetti del robot smart car. I robot smart car insegui-luce, come suggerisce il nome, sono robot smart car in grado di seguire la luce.

Possiamo combinare le conoscenze acquisite nei progetti sul fotoresistore e sulla guida dei motori per realizzare un robot smart car che insegue la luce. Nel progetto, utilizziamo due moduli fotoresistori per rilevare l'intensità luminosa sui lati sinistro e destro del robot smart car, leggiamo i corrispondenti valori analogici, e quindi controlliamo la rotazione dei due motori in base a questi due dati, così da controllare i movimenti del robot smart car.

La logica specifica del robot smart car insegui-luce è mostrata di seguito.

![](./media/image-20250709111733042.png)

#### **(2)Diagramma di flusso:**

![](media/wps8.png)

#### **(3)Schema di collegamento:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Nota:</span> I pin "G", "V" e S del modulo fotoresistore sinistro sono collegati rispettivamente a G (GND), V (VCC), A1;

I pin "G", "V" e S del modulo fotoresistore destro sono collegati rispettivamente a G (GND), V (VCC) e A2.

Il cavo a 4 pin è contrassegnato con A, A1, B1 e B. Il motore posteriore destro è collegato alla porta B della scheda di espansione driver motore 8833 e il motore anteriore sinistro è collegato alla porta A della scheda di espansione driver motore 8833.

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anch'esso la comunicazione seriale, e potrebbero verificarsi conflitti con la comunicazione seriale Bluetooth, che possono causare il fallimento del caricamento.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 10
  light follow tank
  http://www.keyestudio.com
*/
#define light_L_Pin A1   // Definisce il pin del sensore fotosensibile a sinistra
#define light_R_Pin A2   // Definisce il pin del sensore fotosensibile a destra
#define ML_Ctrl 4  // Definisce il pin di controllo della direzione del motore sinistro
#define ML_PWM 6   // Definisce il pin di controllo PWM del motore sinistro
#define MR_Ctrl 2  // Definisce il pin di controllo della direzione del motore destro
#define MR_PWM 5   // Definisce il pin di controllo PWM del motore destro
int left_light;
int right_light;
void setup() 
{
  Serial.begin(9600);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop() 
{
  left_light = analogRead(light_L_Pin);
  right_light = analogRead(light_R_Pin);
  Serial.print("left_light_value = ");
  Serial.println(left_light);
  Serial.print("right_light_value = ");
  Serial.println(right_light);
  if (left_light > 650 && right_light > 650) // vai avanti
  {
    Car_front();
  }
  else if (left_light > 650 && right_light <= 650)  // gira a sinistra
  {
    Car_left();
  }
  else if (left_light <= 650 && right_light > 650) // gira a destra
  {
    Car_right();
  }
  else  // altrimenti, fermati
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
```

#### **(5)Risultato del Test**

Dopo aver caricato con successo il codice di test, collegato secondo lo schema di cablaggio, spostato il selettore DIP verso destra e alimentato il dispositivo, il robot smart car si muove seguendo la luce.

![Img](./media/img-20240117090537.png)