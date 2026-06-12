### Proyecto 21: Ventilador

#### **(1)Descripción：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Este módulo de ventilador utiliza un chip de control de motor HR1124S, un chip controlador H-bridge de un solo canal que contiene tubos de potencia PMOS y NMOS de baja resistencia de conductividad. La baja resistencia de conducción puede reducir el consumo de energía, contribuyendo al funcionamiento seguro del chip durante más tiempo.

Además, su bajo consumo de corriente en espera y su bajo consumo de corriente estática en funcionamiento lo hacen apto para juguetes. Podemos controlar la dirección de rotación y la velocidad del ventilador mediante la salida de señales IN+ e IN- y señales PWM.

#### **(2)Especificaciones:**

Voltaje de trabajo: 5V

Corriente: 200MA

Potencia máxima: 2W

Temperatura de funcionamiento: -10 grados Celsius a +50 grados Celsius

Tamaño: 47.6MM \*23.8MM

#### **(3)Diagrama de Conexión:**

El módulo de ventilador necesita ser impulsado por una corriente elevada; por lo tanto, instalamos un soporte de baterías.

![](media/2bd9aa5cc21e274458328958561f1915.png)

Los pines GND, VCC, IN+ e IN- del módulo ventilador están conectados a los pines G, V, D12 y D13 del shield.

#### **(4)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.1
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;

void setup()
{
    pinMode(INA, OUTPUT);//Configura el puerto digital INA como salida
    pinMode(INB, OUTPUT);//Configura el puerto digital INB como salida
}

void loop() 
{
    //Configura el ventilador para girar en sentido antihorario durante 3s
    digitalWrite(INA, LOW);
    digitalWrite(INB, HIGH);
    delay(3000);
    //Configura el ventilador para detenerse durante 1s
    digitalWrite(INA, LOW);
    digitalWrite(INB, LOW);
    delay(1000);
    //Configura el ventilador para girar en sentido horario durante 3s
    digitalWrite(INA, HIGH);
    digitalWrite(INB, LOW);
    delay(3000);
}
```

#### **(5)Resultados de la Prueba：**

Cargue el código, conecte los componentes y conecte la alimentación. El pequeño ventilador girará en sentido antihorario durante 3000ms, se detendrá durante 1000ms y girará en sentido horario durante 300ms.

![](./media/img-20240117085032.png)

#### **(6)Práctica de Extensión:**

Hemos comprendido el principio de funcionamiento del sensor de llama. A continuación, conecte un sensor de llama en el circuito, como se muestra a continuación. Luego controle el ventilador para apagar el fuego con el sensor de llama.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.2
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;
int flame = A1; //Define el pin de llama como pin analógico A1
int val = 0; //Define variables digitales

void setup() 
{
    pinMode(INA, OUTPUT);//Configura el puerto digital INA como salida
    pinMode(INB, OUTPUT);//Configura el puerto digital INB como salida
    pinMode(flame, INPUT); //Define la llama como fuente de entrada
}

void loop() 
{
    val = analogRead(flame); //Lee el valor analógico del sensor de llama
    if (val <= 700)  //Cuando el valor analógico≤700, el ventilador se enciende
    {
        //Enciende el ventilador cuando se detecta llama
        digitalWrite(INA, LOW);
        digitalWrite(INB, HIGH);
    } 
    else 
    {
        //De lo contrario, deja de funcionar
        digitalWrite(INA, LOW);
        digitalWrite(INB, LOW);
    }
}
```

Después de cargar el código, encienda el interruptor de alimentación del shield de control de motor; podrá encender el ventilador cuando se detecte llama desde el sensor de llama izquierdo del robot.

![](./media/image-20250709115926832.png)