### Proyecto 14: Tanque Seguidor de Línea


#### **(1)Descripción:**

El proyecto anterior ha presentado cómo confinar el carro inteligente para que se mueva en un espacio determinado. En este proyecto, podemos usar los conocimientos aprendidos anteriormente para convertirlo en un carro inteligente seguidor de línea. En el experimento, usamos el sensor de seguimiento de línea para detectar si hay una línea negra alrededor del carro inteligente, y luego controlar la rotación de los dos motores según los resultados de la detección, para que el carro inteligente se mueva a lo largo de la línea negra.

La lógica específica del carro inteligente seguidor de línea se muestra en la tabla a continuación:

|               Sensor               |                          Detección                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Sensor de seguimiento de línea central | Línea negra detectada: en nivel alto<br />Línea blanca detectada: en nivel bajo |
|  Sensor de seguimiento de línea izquierdo  | Línea negra detectada: en nivel alto<br />Línea blanca detectada: en nivel bajo |
| Sensor de seguimiento de línea derecho  | Línea negra detectada: en nivel alto<br />Línea blanca detectada: en nivel bajo |

|                         Condición 1                          |                         Condición 2                          |             Movimiento             |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :------------------------------: |
| El sensor de seguimiento de línea central <br />detecta la línea negra | El sensor de seguimiento de línea izquierdo detecta la línea negra <br />y <br />el derecho detecta línea blanca | Girar a la izquierda<br />establecer PWM a 200  |
| El sensor de seguimiento de línea central <br />detecta la línea negra | El sensor de seguimiento de línea izquierdo detecta línea blanca <br />y <br />el derecho detecta la línea negra | Girar a la derecha<br />establecer PWM a 200 |
| El sensor de seguimiento de línea central <br />detecta la línea negra | Ambos sensores izquierdo y derecho detectan línea blanca<br />o<br />Ambos detectan la línea negra |           Avanzar           |
| El sensor de seguimiento de línea central <br />detecta línea blanca  | El sensor de seguimiento de línea izquierdo detecta la línea negra <br />y <br />el derecho detecta línea blanca | Girar a la izquierda<br />establecer PWM a 200  |
| El sensor de seguimiento de línea central <br />detecta línea blanca  | El sensor de seguimiento de línea izquierdo detecta línea blanca<br />y <br />el derecho detecta la línea negra | Girar a la derecha<br />establecer PWM a 200 |
| El sensor de seguimiento de línea central <br />detecta línea blanca  | Ambos sensores izquierdo y derecho detectan línea blanca<br />o<br />Ambos sensores izquierdo y derecho detectan la línea negra |               Detener               |

#### **(2)Diagrama de flujo:**

![](media/wps11.png)

#### **(3)Diagrama de cableado:**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)Código de prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 14
  Line track tank
  http://www.keyestudio.com
*/

//El cableado del sensor de seguimiento de línea
#define L_pin  11  //izquierdo
#define M_pin  7  //central
#define R_pin  8  //derecho
#define ML_Ctrl 4  //Definir el pin de control de dirección del motor izquierdo
#define ML_PWM 6   //Definir el pin de control PWM del motor izquierdo
#define MR_Ctrl 2  //Definir el pin de control de dirección del motor derecho
#define MR_PWM 5   //Definir el pin de control PWM del motor derecho
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); //Establecer la velocidad de baudios a 9600
  pinMode(L_pin, INPUT); //Establecer todos los pines del sensor de seguimiento de línea como modo de entrada
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); //Leer el valor del sensor izquierdo
  M_val = digitalRead(M_pin); //Leer el valor del sensor central
  R_val = digitalRead(R_pin); //Leer el valor del sensor derecho
  if (M_val == 1) { //el central detecta líneas negras
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
  else  //El central no detecta líneas negras
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

//avanzar
void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

//retroceder
void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

//girar a la izquierda
void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

//girar a la derecha
void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

//detenerse
void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Resultado de la prueba:**

Después de cargar el código de prueba correctamente y encenderlo, el carro inteligente se mueve a lo largo de la línea negra.

![](./media/img-20240117085916.png)