### Proyecto 10: Tanque Seguidor de Luz


#### **(1)Descripción:**

En proyectos anteriores, presentamos en detalle el uso de varios sensores, módulos y placas de expansión en el auto inteligente. Ahora pasemos a los proyectos del auto inteligente. Los autos inteligentes seguidores de luz, como su nombre lo indica, son autos inteligentes que pueden seguir la luz.

Podemos combinar los conocimientos de los proyectos de fotoresistencia y control de motores para crear un auto inteligente buscador de luz. En el proyecto, usamos dos módulos fotoresistores para detectar la intensidad de la luz en los lados izquierdo y derecho del auto inteligente, leemos los valores analógicos correspondientes y luego controlamos la rotación de los dos motores basándonos en estos dos datos para así controlar los movimientos del auto inteligente.

La lógica específica del auto inteligente seguidor de luz se muestra a continuación.

![](./media/image-20250709111733042.png)

#### **(2)Diagrama de flujo:**

![](media/wps8.png)

#### **(3)Diagrama de conexión:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Nota:</span> Los pines "G", "V" y S del módulo fotoresistor izquierdo están conectados a G (GND), V (VCC) y A1 respectivamente;

Los pines "G", "V" y S del módulo fotoresistor derecho están conectados a G (GND), V (VCC) y A2 respectivamente.

El cable de 4 pines está marcado con A, A1, B1 y B. El motor trasero derecho está conectado al puerto B de la placa de expansión del controlador de motores 8833 y el motor delantero izquierdo está conectado al puerto A de la placa de expansión del controlador de motores 8833.

#### **(4)Código de prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 10
  light follow tank
  http://www.keyestudio.com
*/
#define light_L_Pin A1   //Define el pin del sensor fotosensible de la izquierda
#define light_R_Pin A2   //Define el pin del sensor fotosensible de la derecha
#define ML_Ctrl 4  //Define el pin de control de dirección del motor izquierdo
#define ML_PWM 6   //Define el pin de control PWM del motor izquierdo
#define MR_Ctrl 2  //Define el pin de control de dirección del motor derecho
#define MR_PWM 5   //Define el pin de control PWM del motor derecho
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
  if (left_light > 650 && right_light > 650) //avanzar
  {
    Car_front();
  }
  else if (left_light > 650 && right_light <= 650)  //girar a la izquierda
  {
    Car_left();
  }
  else if (left_light <= 650 && right_light > 650) //girar a la derecha
  {
    Car_right();
  }
  else  //de lo contrario, detenerse
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

#### **(5)Resultado de la prueba**

Después de cargar el código de prueba exitosamente, conectar según el diagrama de cableado, deslizar el interruptor DIP hacia el extremo derecho y encenderlo, el auto inteligente sigue la luz para moverse.

![Img](./media/img-20240117090537.png)