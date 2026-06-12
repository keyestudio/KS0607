### Proyecto 13: Tanque en Movimiento en Espacio Confinado


#### **(1)Descripción:**

Las funciones de seguimiento de sonido ultrasónico y evasión de obstáculos del carro inteligente han sido presentadas en proyectos anteriores. Aquí pretendemos combinar los conocimientos de los cursos anteriores para confinar el carro inteligente a moverse en un espacio determinado.

En el experimento, utilizamos el sensor de seguimiento de línea para detectar si hay una línea negra alrededor del carro inteligente, y luego controlamos la rotación de los dos motores según los resultados de la detección, para así mantener el carro inteligente dentro de un círculo trazado con línea negra.

La lógica específica del carro inteligente seguidor de línea se muestra en la tabla a continuación:

![](./media/image-20250709112523897.png)

|                         Condición                         |                         Movimiento                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Si alguno de los tres sensores de seguimiento de línea detecta líneas negras | Retroceder (establecer PWM en 150) Luego girar a la izquierda (establecer PWM en 150) |
|             Ninguno detecta líneas negras              |               Avanzar (establecer PWM en 100)                |

#### **(2)Diagrama de flujo:**

![](media/image-20230427092708208.png)

#### **(3)Diagrama de conexión:**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)Código de prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 13
  draw a circle for tank
  http://www.keyestudio.com
*/

//El cableado del sensor de seguimiento de línea
#define L_pin  11  //izquierda
#define M_pin  7  //centro
#define R_pin  8  //derecha

#define ML_Ctrl 4  //Define el pin de control de dirección del motor izquierdo
#define ML_PWM 6   //Define el pin de control PWM del motor izquierdo
#define MR_Ctrl 2  //Define el pin de control de dirección del motor derecho
#define MR_PWM 5   //Define el pin de control PWM del motor derecho
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); //Establece la velocidad de baudios en 9600
  pinMode(L_pin, INPUT); //Establece todos los pines del sensor de seguimiento de línea en modo entrada
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); //Lee el valor del sensor izquierdo
  M_val = digitalRead(M_pin); //Lee el valor del sensor central
  R_val = digitalRead(R_pin); //Lee el valor del sensor derecho
  if ( L_val == 0 && M_val == 0 && R_val == 0 )  //cuando no se detectan líneas negras, avanzar
  {
    Car_front();
  }
  else  //se detectan líneas negras, retroceder y luego girar a la izquierda
  {
    Car_back();
    delay(700);
    Car_left();
    delay(800);
  }
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Resultados de la prueba:**

Después de cargar el código de prueba exitosamente y encenderlo, el carro inteligente se mueve en un espacio confinado, el círculo trazado con línea negra.

![](./media/img-20240117090340.png)