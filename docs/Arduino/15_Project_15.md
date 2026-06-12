### Progetto 15: Carro Armato con Telecomando IR

![](./media/image-20250709113214889.png)


#### **(1)Descrizione:**

Il telecomando a infrarossi è uno dei sistemi di controllo remoto più comuni, utilizzato in motori elettrici, ventilatori elettrici e molti altri elettrodomestici. In questo progetto, utilizziamo le conoscenze apprese in precedenza per realizzare un'auto intelligente controllata a infrarossi.

Nella 9ª lezione, abbiamo testato il valore del tasto corrispondente a ciascun pulsante del telecomando a infrarossi. In questo progetto, possiamo impostare il codice (valore del tasto) per fare in modo che il pulsante corrispondente controlli i movimenti dell'auto intelligente e visualizzi i pattern di movimento sulla matrice LED 8X16.

La logica specifica dell'auto intelligente con telecomando a infrarossi è mostrata nella tabella:

|                        Tasto ultrasonico                        | Valore tasto |                    Istruzioni dai tasti                    |
| :----------------------------------------------------------: | :-------: | :----------------------------------------------------------: |
| ![image-20230427094710725](media/image-20230427094710725.png) |  FF629D   | Avanza（impostare PWM a 200）<br />visualizza il pattern di avanzamento |
| ![image-20230427094716639](media/image-20230427094716639.png) |  FFA857   | Vai indietro（impostare PWM a 200）<br />visualizza il pattern di retromarcia |
| ![image-20230427094720417](media/image-20230427094720417.png) |  FF22DD   |           Gira a sinistra<br />visualizza il pattern "STOP"           |
| ![image-20230427094725151](media/image-20230427094725151.png) |  FFC23D   |     Gira a destra<br />visualizza il pattern di svolta a sinistra      |
| ![image-20230427094729839](media/image-20230427094729839.png) |  FF02FD   |             Ferma<br />visualizza il pattern "STOP"              |

**Impostazione iniziale**: la matrice LED 8X16 mostra il pattern "![](media/wps20.jpg)".



#### **(2)Diagramma di flusso:**

![](media/wps21.png)

#### **(3)Schema di collegamento:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

GND, VCC, SDA e SCL del pannello LED 8x16 sono collegati a G（GND), V（VCC), SDA e SCL della scheda di espansione.

Poiché la scheda 8833 integra il ricevitore IR, non è necessario collegarlo. I pin del ricevitore IR sono G（GND), V（VCC) e D3.

#### (4)**Codice di Test:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Non collegare il modulo Bluetooth prima di caricare il codice, perché il caricamento del codice utilizza anche la comunicazione seriale, e potrebbero esserci conflitti con la comunicazione seriale Bluetooth, causando il fallimento del caricamento.)

```C
/*
 Keyestudio Mini Tank Robot V3 (Popular Edition)
 lesson 15
 IRremote Control Tank
 http://www.keyestudio.com
*/
#include <IRremote.h>
IRrecv irrecv(3);  //
decode_results results;
long ir_rec;  // Utilizzato per memorizzare i valori infrarossi ricevuti

// Array, utilizzato per salvare i dati delle immagini, può essere calcolato manualmente o ottenuto dallo strumento di modulo
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  // Imposta il pin del clock come A5
#define SDA_Pin  A4  // Imposta il pin dei dati come A4

#define ML_Ctrl 4  // Definisce il pin di controllo della direzione del motore sinistro
#define ML_PWM 6   // Definisce il pin di controllo PWM del motore sinistro
#define MR_Ctrl 2  // Definisce il pin di controllo della direzione del motore destro
#define MR_PWM 5    // Definisce il pin di controllo PWM del motore destro

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  // Inizializza la libreria del ricevitore a infrarossi

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // pulisce lo schermo
  matrix_display(start01);  // mostra l'immagine di avvio
}

void loop() 
{
  if (irrecv.decode(&results))  // Riceve il valore del telecomando a infrarossi
  {
    ir_rec = results.value;
    String type = "UNKNOWN";
    String typelist[14] = {"UNKNOWN", "NEC", "SONY", "RC5", "RC6", "DISH", "SHARP", "PANASONIC", "JVC", "SANYO", "MITSUBISHI", "SAMSUNG", "LG", "WHYNTER"};
    if (results.decode_type >= 1 && results.decode_type <= 13) 
    {
      type = typelist[results.decode_type];
    }
    Serial.print("IR TYPE:" + type + "  ");
    Serial.println(ir_rec, HEX);
    irrecv.resume();
  }

  switch (ir_rec) 
  {
    case 0xFF629D: Car_front();     break;   // comando per andare avanti
    case 0xFFA857: Car_back();      break;   // comando per andare indietro
    case 0xFF22DD: Car_T_left();    break;   // comando per girare a sinistra
    case 0xFFC23D: Car_T_right();   break;   // comando per girare a destra
    case 0xFF02FD: Car_Stop();      break;   // comando per fermarsi
    case 0xFF30CF: Car_left();      break;   // comando per ruotare a sinistra
    case 0xFF7A85: Car_right();     break;   // comando per ruotare a destra
    default: break;
  }
}

/***************Funzione per azionare il motore***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  // Vai indietro
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(front);  // mostra l'immagine per andare avanti
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  // mostra l'immagine per girare a sinistra
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  // mostra l'immagine per girare a destra
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // mostra l'immagine per fermarsi
}

void Car_T_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
  matrix_display(left);  // mostra l'immagine per girare a sinistra
}

void Car_T_right() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 0);
  matrix_display(right);  // mostra l'immagine per girare a destra
}

// Questa funzione viene utilizzata per la visualizzazione sulla matrice di punti
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Funzione per richiamare la condizione di inizio trasmissione dati
  IIC_send(0xc0);  // Scegli un indirizzo
  for (int i = 0; i < 16; i++) // I dati del pattern hanno 16 byte
  {
    IIC_send(matrix_value[i]); // trasferisce i dati del pattern
  }
  IIC_end();   // Termina il trasferimento dei dati del pattern
  IIC_start();
  IIC_send(0x8A);  // controllo del display, seleziona la larghezza di impulso come 4/16
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

// Il segno della fine della trasmissione dati
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
  for (byte mask = 0x01; mask != 0; mask <<= 1) // ogni carattere ha 8 cifre, rilevate una per una
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
    digitalWrite(SCL_Pin, HIGH); // Porta il pin del clock SCL_Pin alto per interrompere la trasmissione dati
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // Abbassa il pin del clock SCL_Pin per cambiare i segnali di SDA
  }
}
```

#### **(5)Risultato del Test:**

Dopo aver caricato il codice, attivare l'interruttore di alimentazione dello shield del motore. Posizionare il robot sul pavimento, fare riferimento alla tabella sopra e premere i diversi pulsanti: il robot si muoverà nella direzione preimpostata corrispondente.

![](./media/img-20240117090114.png)