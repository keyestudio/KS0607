### Proyecto 20: Sensor de Llama

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Descripción：**

El sensor de llama utiliza un tubo receptor de infrarrojos para detectar llamas. Convierte el brillo de la llama en señales de nivel alto y bajo y las introduce en el procesador central para el procesamiento del programa correspondiente. El valor de voltaje del puerto analógico varía dependiendo de si hay una llama cerca o no.

Si no hay llama, el puerto analógico lee aproximadamente 0.3V; cuando hay una llama, el puerto analógico lee aproximadamente 1.0V. Cuanto más cerca esté la llama, mayor será el valor de voltaje. Puede utilizarse para detectar una fuente de fuego o para construir un robot inteligente.

Tenga en cuenta que la sonda del sensor de llama solo puede soportar temperaturas entre -25℃ y 85℃.

Durante el uso, asegúrese de mantener el sensor de llama a una distancia segura del fuego para evitar dañarlo.

#### **(2)Parámetros：**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Voltaje de funcionamiento: 3.3V-5V (DC)

- Corriente: 100mA

- Potencia máxima: 0.5W

- Temperatura de trabajo: -10°C a +50 grados Celsius

- Tamaño del sensor: 31.6mmx23.7mm

- Interfaz: interfaz de 4pin a 3PIN

- Señal de salida: señales analógicas A0, A1



#### **(3)Diagrama de Conexión:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

Los sensores de llama están conectados a A1 y A2.

Cuando retiramos los sensores ultrasónicos y las fotorresistencias, y luego añadimos sensores de llama y módulos de ventilador, se crea el robot extintor de incendios.

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Este experimento requiere el uso de una fuente de fuego. Por favor, manténgala alejada de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo supervisión adulta. Si no puede confirmar que está seguro, abandone el experimento.
2）**El sensor de llama no es ignífugo, por favor no lo queme directamente con llama.**


#### **(4)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.1

flame sensor

http://www.keyestudio.com

*/

int flame = A1; //Define el pin de llama como pin analógico A1
int val = 0; //Define variables digitales

void setup() 
{
	pinMode(flame, INPUT); //Define el buzzer como fuente de entrada
    Serial.begin(9600); //Establece la velocidad de baudios a 9600
}

void loop() 
{
	val = analogRead(flame); //Lee el valor analógico del sensor de llama
	Serial.println(val);//Muestra el valor analógico y lo imprime
	delay(100); //Retardo de 100ms
}
```

#### **(5)Resultado de la Prueba：**

Conecte los componentes, cargue el código, abra el monitor serial y establezca la velocidad de baudios a 9600.

Puede ver el valor de simulación del sensor de llama.

Cuanto más cerca esté la llama, menor será el valor de simulación.

Ajuste el potenciómetro en el módulo para mantener D1 en el punto crítico. Cuando el sensor no detecta llama, D1 estará apagado, pero si el sensor detecta llama, D1 se encenderá.

![](./media/img-20240117085629.png)

![](media/05db06b3e205dfca63c2ba3aa7ff528e.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Por favor, manténgalo alejado de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo supervisión adulta. Si no puede confirmar que está seguro, abandone el experimento. El sensor de llama no es ignífugo, por favor no lo queme directamente con llama.

#### **(6)Práctica de Extensión:**

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Este experimento requiere el uso de una fuente de fuego. Por favor, manténgala alejada de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo supervisión adulta. Si no puede confirmar que está seguro, abandone el experimento.
2）El sensor de llama no es ignífugo, por favor no lo queme directamente con llama.

A continuación, conecte un LED al pin 9 y podremos controlarlo mediante un sensor de llama, como se muestra a continuación;

![](media/814c315d3bb44278b476a754d3681227.png)

**Código de Prueba**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.2

flame sensor

http://www.keyestudio.com

*/

int flame = A1; //Define el pin de llama como pin analógico A1
int LED = 9; //Define el LED como puerto digital 9
int val = 0; //Define variables digitales

void setup() 
{
    pinMode(flame, INPUT); //Define la llama como fuente de entrada
    pinMode(LED, OUTPUT); //Establece el LED en modo de salida
    Serial.begin(9600); //Establece la velocidad de baudios a 9600
}

void loop() 
{
    val = analogRead(flame); //Lee el valor analógico del sensor de llama
    Serial.println(val);//Muestra el valor analógico y lo imprime
    if (val < 300)  //Cuando el valor analógico es menor que 300, el LED se enciende
    {
    	digitalWrite(LED, HIGH); //El LED se enciende
    } 
    else 
    {
    	digitalWrite(LED, LOW); //El LED se apaga
    }
    delay(50); //Retardo de 50ms
}
```

#### **(8)Resultados de la Prueba：**

Puede usar la llama de un encendedor cerca del sensor de llama izquierdo. Cuando el sensor de llama detecta una llama, el módulo LED se encenderá como alarma.

![](./media/img-20240117085131.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Por favor, manténgalo alejado de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo supervisión adulta. Si no puede confirmar que está seguro, abandone el experimento. El sensor de llama no es ignífugo, por favor no lo queme directamente con llama.