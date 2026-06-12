### Project 22: Brandblusser Tank


#### **(1)Beschrijving:**

De lijnvolgfunctie van de slimme tank is uitgelegd in het vorige project. In dit project gebruiken we de vlamsensor om een brandblussende robot te maken.

Wanneer de auto vlammen tegenkomt, zal de motor van de ventilator draaien om het vuur te blussen. Natuurlijk moeten we eerst de ultrasone sensor en twee fotoresistoren vervangen door een ventilatormodule en vlamsensoren.

De specifieke logica van de lijnvolgende slimme auto wordt weergegeven in de onderstaande tabel:

| Linker Vlamsensor | Rechter Vlamsensor | Status                                                        |
| :---------------: | :----------------: | :------------------------------------------------------------ |
|       ≤700        |        ≤700        | Auto stopt, ventilator begint te draaien om vlam te blussen   |
|       ≥700        |        ≥700        | Auto stopt, ventilator begint te draaien om vlam te blussen   |
|       ≥700        |        ≥700        | Auto stopt, ventilator begint te draaien om vlam te blussen   |
|       ＞700       |        ＞700       | Ventilator stopt, auto rijdt verder                           |

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
1）Dit experiment vereist het gebruik van een vuurzaak. Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment uit te voeren onder toezicht van een volwassene. Als u niet zeker weet of het veilig is, sla het experiment dan over.
2）De vlamsensor is niet vuurbestendig, verbrand hem niet direct met een vlam.
We kunnen een externe LED bedienen met de vlamsensor. De LED is nog steeds verbonden met D9. Wanneer er vuur wordt gedetecteerd, gaat de LED aan.

#### **(2)Stroomdiagram:**

![](media/wps12.png)

#### **(3)Aansluitschema:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

#### **(4)Testcode:**

(<span style="color: rgb(255, 76, 65);">**Opmerking:**</span> Sluit de Bluetooth-module niet aan voordat u de code uploadt, omdat het uploaden van de code ook gebruik maakt van seriële communicatie, en er mogelijk conflicten optreden met de Bluetooth seriële communicatie, waardoor het uploaden mislukt.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 22
  Fire extinguishing tank
  http://www.keyestudio.com
*/

int flame_L = A1; // Definieer de vlam-interface links als analoge pin A1
int flame_R = A2; // Definieer de vlam-interface rechts als analoge pin A2
// De bedrading van de lijnvolgsensor
#define L_pin  11  // links
#define M_pin  7  // midden
#define R_pin  8  // rechts
// De pin van de servo 130
int INA = 12;
int INB = 13;
#define ML_Ctrl 4  // Definieer de richtingsbesturingspin van de linkermotor
#define ML_PWM 6   // Definieer de PWM-besturingspin van de linkermotor
#define MR_Ctrl 2  // Definieer de richtingsbesturingspin van de rechtermotor
#define MR_PWM 5   // Definieer de PWM-besturingspin van de rechtermotor
int L_val, M_val, R_val, flame_valL, flame_valR;

void setup()
{
  Serial.begin(9600);
  // Stel alle pinnen van de lijnvolgsensor in als invoermodus
  pinMode(L_pin, INPUT);
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  // Definieer de vlamsensor als INPUT
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
  // Definieer de motor als OUTPUT
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  pinMode(INA, OUTPUT);// Stel digitale poort INA in als OUTPUT
  pinMode(INB, OUTPUT);// Stel digitale poort INB in als OUTPUT
}

void loop () 
{
  // Lees de analoge waarde van de vlamsensoren
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
    L_val = digitalRead(L_pin); // Lees de waarde van de linkersensor
    M_val = digitalRead(M_pin); // Lees de waarde van de middelste sensor
    R_val = digitalRead(R_pin); // Lees de waarde van de rechtersensor
    
    if (M_val == 1)  // de middelste detecteert zwarte lijnen
    {
      if (L_val == 1 && R_val == 0)  // Als een zwarte lijn links wordt gedetecteerd, maar niet rechts, draai links
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  // Als een zwarte lijn rechts wordt gedetecteerd, niet links, draai rechts
      {
        Car_right();
      }
      else  // anders, ga vooruit
      {
        Car_front();
      }
    }
    else  // De middelste detecteert geen zwarte lijnen
    {
      if (L_val == 1 && R_val == 0)  // Als een zwarte lijn links wordt gedetecteerd, maar niet rechts, draai links
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  // Als een zwarte lijn rechts wordt gedetecteerd, niet links, draai rechts
      {
        Car_right();
      }
      else  // anders, stop
      {
        Car_Stop();
      }
    }
  }
}

void fan_stop() 
{
  // stop met draaien
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

void fan_begin() 
{
  // ventilator draait
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

#### **(5)Testresultaat:**

Na het succesvol uploaden van de testcode en het inschakelen van de voeding, blust de slimme auto het vuur wanneer het vlammen detecteert en blijft het langs de zwarte lijn rijden.

![](media/694677ab33053846ec588667dc40ecfa.jpeg)

<span style="color: rgb(255, 76, 65);">**Opmerking:**</span>
Houd het uit de buurt van brandbare materialen om brand te voorkomen. Kinderen dienen het experiment uit te voeren onder toezicht van een volwassene. Als u niet zeker weet of het veilig is, sla het experiment dan over. De vlamsensor is niet vuurbestendig, verbrand hem niet direct met een vlam.