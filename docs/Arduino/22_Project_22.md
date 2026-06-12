### Proyecto 22: Tanque Extintor de Incendios


#### **(1)Descripción:**

La función de seguimiento de línea del tanque inteligente se explicó en el proyecto anterior. En este proyecto utilizamos el sensor de llama para crear un robot extintor de incendios.

Cuando el carro encuentra llamas, el motor del ventilador girará para apagar el fuego. Por supuesto, primero necesitamos reemplazar el sensor ultrasónico y los dos fotorresistores con un módulo de ventilador y sensores de llama.

La lógica específica del carro inteligente seguidor de línea se muestra en la tabla a continuación:

| Sensor de Llama Izquierdo | Sensor de Llama Derecho | Estado                                                         |
| :-----------------------: | :---------------------: | :------------------------------------------------------------- |
|           ≤700            |          ≤700           | El carro se detiene, el ventilador comienza a girar para apagar la llama |
|           ≥700            |          ≥700           | El carro se detiene, el ventilador comienza a girar para apagar la llama |
|           ≥700            |          ≥700           | El carro se detiene, el ventilador comienza a girar para apagar la llama |
|           ＞700           |          ＞700          | El ventilador se detiene, el carro se mueve                    |

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1) Este experimento requiere el uso de una fuente de fuego. Por favor, manténgalo alejado de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo supervisión de adultos. Si no puede confirmar que está seguro, abandone el experimento.
2) El sensor de llama no es ignífugo, por favor no lo queme directamente con una llama.
Podemos controlar un LED externo con el sensor de llama. El LED sigue conectado a D9. Cuando se detecta fuego, el LED se encenderá.

#### **(2)Diagrama de flujo:**

![](media/wps12.png)

#### **(3)Diagrama de Conexión:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

#### **(4)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 22
  Fire extinguishing tank
  http://www.keyestudio.com
*/

int flame_L = A1; //Define la interfaz de llama en el lado izquierdo como el pin analógico A1
int flame_R = A2; //Define la interfaz de llama en el lado derecho como el pin analógico A2
//El cableado del sensor de seguimiento de línea
#define L_pin  11  //izquierda
#define M_pin  7  //centro
#define R_pin  8  //derecha
//El pin del servo 130
int INA = 12;
int INB = 13;
#define ML_Ctrl 4  //Define el pin de control de dirección del motor izquierdo
#define ML_PWM 6   //Define el pin de control PWM del motor izquierdo
#define MR_Ctrl 2  //Define el pin de control de dirección del motor derecho
#define MR_PWM 5   //Define el pin de control PWM del motor derecho
int L_val, M_val, R_val, flame_valL, flame_valR;

void setup()
{
  Serial.begin(9600);
  //Establece todos los pines del sensor de seguimiento de línea como modo de entrada
  pinMode(L_pin, INPUT);
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  //Define la llama como INPUT
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
  //Define el motor como OUTPUT
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  pinMode(INA, OUTPUT);//Establece el puerto digital INA como OUTPUT
  pinMode(INB, OUTPUT);//Establece el puerto digital INB como OUTPUT
}

void loop () 
{
  //Lee el valor analógico de los sensores de llama
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
    L_val = digitalRead(L_pin); //Lee el valor del sensor izquierdo
    M_val = digitalRead(M_pin); //Lee el valor del sensor central
    R_val = digitalRead(R_pin); //Lee el valor del sensor derecho
    
    if (M_val == 1)  //el del centro detecta líneas negras
    {
      if (L_val == 1 && R_val == 0)  //Si se detecta una línea negra a la izquierda, pero no a la derecha, girar a la izquierda
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  //Si se detecta una línea negra a la derecha, no a la izquierda, girar a la derecha
      {
        Car_right();
      }
      else  //de lo contrario, avanzar
      {
        Car_front();
      }
    }
    else  //El del centro no detecta líneas negras
    {
      if (L_val == 1 && R_val == 0)  //Si se detecta una línea negra a la izquierda, pero no a la derecha, girar a la izquierda
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  //Si se detecta una línea negra a la derecha, no a la izquierda, girar a la derecha
      {
        Car_right();
      }
      else  //de lo contrario, detenerse
      {
        Car_Stop();
      }
    }
  }
}

void fan_stop() 
{
  //dejar de girar
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

void fan_begin() 
{
  //el ventilador gira
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

#### **(5)Resultado de la Prueba:**

Después de cargar el código de prueba correctamente y encenderlo, el carro inteligente apaga el fuego cuando detecta llamas y continúa moviéndose a lo largo de la línea negra.

![](media/694677ab33053846ec588667dc40ecfa.jpeg)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Por favor, manténgalo alejado de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo supervisión de adultos. Si no puede confirmar que está seguro, abandone el experimento. El sensor de llama no es ignífugo, por favor no lo queme directamente con una llama.