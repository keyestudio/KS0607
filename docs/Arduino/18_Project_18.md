### Progetto 18: Robot con Controllo di Velocità BT

#### (1)**Descrizione:**

Nel progetto precedente, abbiamo imparato come controllare il carro armato intelligente con il Bluetooth. Il valore PWM del motore che abbiamo utilizzato in precedenza è 200 (la velocità è 200).

In questa lezione, utilizzeremo il Bluetooth per regolare la velocità dell'auto intelligente. Non è limitata alla velocità fissa di 200. Definiamo due variabili per memorizzare rispettivamente i valori di velocità dei motori sinistro e destro. Attraverso lo studio precedente, sappiamo che l'intervallo di questo valore può assumere solo valori da 0 a 255.

#### **(2)Diagramma di flusso:**

![](media/image-20230427102042028.png)

#### **(3)Schema di collegamento:**

![](media/930a8024364e07505e845624a94c27bd.png)

GND, VCC, SDA e SCL della matrice di LED 8x16 sono collegati rispettivamente a -(GND), +(VCC), SDA, SCL della scheda di espansione;

#### **(4)Codice di Test:**

(<span style="color: rgb(255, 76, 65);">Nota:</span> Durante il caricamento del codice, il modulo Bluetooth deve essere scollegato, e il Bluetooth può essere riconnesso dopo il completamento del processo di caricamento. Altrimenti il codice potrebbe non essere programmato correttamente.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 18
  bluetooth control speed tank
  http://www.keyestudio.com
*/

// Array, utilizzato per salvare i dati delle immagini, può essere calcolato manualmente o ottenuto dallo strumento di modulo
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char speed_a[] = {0x00, 0x00, 0x00, 0x20, 0x10, 0x08, 0x04, 0x02, 0xff, 0x02, 0x04, 0x08, 0x10, 0x20, 0x00, 0x00};
unsigned char speed_d[] = {0x00, 0x00, 0x00, 0x04, 0x08, 0x10, 0x20, 0x40, 0xff, 0x40, 0x20, 0x10, 0x08, 0x04, 0x00, 0x00};
#define SCL_Pin  A5  // imposta il pin del clock su A5
#define SDA_Pin  A4  // A4 imposta il pin dei dati su A4

#define ML_Ctrl 4  // definisce il pin di controllo della direzione del motore sinistro
#define ML_PWM 6   // definisce i pin di controllo PWM del motore sinistro
#define MR_Ctrl 2  // definisce il pin di controllo della direzione del motore destro
#define MR_PWM 5   // definisce il pin di controllo PWM del motore destro
char ble_val;      // definisce il pin di controllo PWM del motore destro
byte speeds_L = 200; // La velocità iniziale del motore sinistro è 200
byte speeds_R = 200; // La velocità iniziale del motore destro è 200
String speeds_l, speeds_r; // Riceve una stringa PWM da convertire in un valore intero PWM

void setup() 
{
  Serial.begin(9600);

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // cancella lo schermo
  matrix_display(start01);  // mostra l'immagine di avvio
}

void loop() 
{
  if (Serial.available() > 0) 
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
    switch (ble_val) 
    {
      case 'F':  // il comando per andare avanti
        Car_front();
        break;
      case 'B':  // il comando per andare indietro
        Car_back();
        break;
      case 'L':  // il comando per girare a sinistra
        Car_left();
        break;
      case 'R':  // il comando per girare a destra
        Car_right();
        break;
      case 'S':  // il comando per fermarsi
        Car_Stop();
        break;
      case 'u':  // Riceve una stringa che inizia con u e termina con #, e la converte in un valore intero
        speeds_l = Serial.readStringUntil('#');
        speeds_L = String(speeds_l).toInt();
        break;
      case 'v':  // Riceve una stringa che inizia con v e termina con #, e la converte in un valore intero
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt();
        break;
    }
  }
}

/***************La funzione per azionare il motore***************/

void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  // Va indietro
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  // mostra l'immagine per andare avanti
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  // mostra l'immagine per girare a sinistra
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(right);  // mostra l'immagine per girare a destra
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // mostra l'immagine di stop
}

// Questa funzione è utilizzata per la visualizzazione sulla schermata a matrice di punti
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Funzione per richiamare la condizione di inizio trasferimento dati
  IIC_send(0xc0);  // Sceglie un indirizzo
  for (int i = 0; i < 16; i++) // I dati del pattern hanno 16 byte
  {
    IIC_send(matrix_value[i]); // trasferisce i dati del pattern
  }
  IIC_end();   // Termina il trasferimento dei dati del pattern
  IIC_start();
  IIC_send(0x8A);  // controllo del display, seleziona la larghezza dell'impulso come 4/16
  IIC_end();
}

// Condizioni per l'inizio del trasferimento dati
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// il segno di fine trasmissione dati
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

// trasferisce i dati
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // ogni carattere ha 8 cifre, che vengono rilevate una per una
  {
    if (send_data & mask)  // imposta livelli alti o bassi in base a ogni bit (0 o 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Porta il pin del clock SCL_Pin alto per interrompere la trasmissione dei dati
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // abbassa il pin del clock SCL_Pin per cambiare i segnali di SDA
  }
}
```

#### **(5)Risultati del Test:**

Dopo aver caricato con successo il codice di test, spostando il selettore DIP verso destra, alimentando il dispositivo e abbinando l'APP con il Bluetooth, l'auto intelligente può essere controllata per muoversi tramite l'APP. E la velocità dell'auto può essere regolata tirando i cursori di velocità dei motori sinistro e destro.

![](media/b9c902b937801f829b9ce2fd254b1849.jpeg)

(È possibile fare riferimento alla tabella delle funzioni nel progetto 17)