### Proyecto 19: Sensor de Llama

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Descripción:**

El sensor de llama utiliza un tubo receptor de infrarrojos para detectar llamas. Convierte el brillo de la llama en señales de nivel alto y bajo y las introduce en el procesador central para el procesamiento correspondiente del programa. El valor de voltaje del puerto analógico varía dependiendo de si hay una llama cerca o no hay ninguna llama.

Si no hay llama, el puerto analógico lee aproximadamente 0.3V; cuando hay llama, el puerto analógico lee aproximadamente 1.0V. Cuanto más cerca esté la llama, mayor será el valor de voltaje. Se puede usar para detectar una fuente de fuego o para construir un robot inteligente.

Tenga en cuenta que la sonda del sensor de llama solo puede soportar temperaturas entre -25℃ y 85℃.

Durante su uso, asegúrese de mantener el sensor de llama a una distancia segura del fuego para evitar dañarlo.

#### **(2)Parámetros:**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Voltaje de trabajo: 3.3V-5V (DC)

- Corriente: 100mA

- Potencia máxima: 0.5W

- Temperatura de trabajo: -10°C a +50 grados Celsius

- Tamaño del sensor: 31.6mmx23.7mm

- Interfaz: interfaz de 4 pines a 3 pines

- Señal de salida: señales analógicas A0, A1

#### **(3)Diagrama de Conexión:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

El pin A de dos fotorresistencias está conectado a A1 y A2. Conectamos el sensor de llama a A1 y A2. Reemplazamos dos fotorresistencias y el sensor ultrasónico con dos sensores de llama y un ventilador, y se crea un coche extintor.

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Este experimento requiere el uso de una fuente de fuego. Por favor, manténgala alejada de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo la supervisión de un adulto. Si no puede confirmar que está seguro, por favor abandone el experimento.
2）**El sensor de llama no es ignífugo, por favor no lo queme directamente con llama.**

#### **(4)Código de Prueba:**

También puede arrastrar bloques para editar su código, como se muestra a continuación

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/4bc6c8a4d6e964fd078a6aeb0dd51ff4.png)

#### **(5)Resultados de la Prueba:**

Conecte los componentes, cargue el código, abra el monitor serial y configure la velocidad de baudios a 9600.

Puede ver el valor de simulación del sensor de llama.

Cuanto más cerca esté la llama, menor será el valor de simulación.

Ajuste el potenciómetro del módulo para mantener el LED en el punto crítico. Cuando el sensor no detecta llama, el LED estará apagado, pero si el sensor detecta llama, el LED se encenderá.

![](./media/img-20240117100139.png)

![](media/60d0ce2044a504135af3b1113a1a4c7d.png)

#### **(6)Práctica de Extensión:**

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Este experimento requiere el uso de una fuente de fuego. Por favor, manténgala alejada de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo la supervisión de un adulto. Si no puede confirmar que está seguro, por favor abandone el experimento.
2）El sensor de llama no es ignífugo, por favor no lo queme directamente con llama.
Podemos controlar un LED externo con el sensor de llama. El LED sigue conectado a D9. Cuando se detecta fuego, el LED se encenderá.

![](media/814c315d3bb44278b476a754d3681227.png)

Puede arrastrar bloques para editar su código, como se muestra a continuación

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/9d2f5915e4a6991ed4549b39ec853fa5.png)

Puede usar la llama de un encendedor cerca del sensor de llama izquierdo. Cuando el sensor de llama detecte una llama, el módulo LED se encenderá como alarma.

![](./media/img-20240117100333.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Por favor, manténgala alejada de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo la supervisión de un adulto. Si no puede confirmar que está seguro, por favor abandone el experimento. El sensor de llama no es ignífugo, por favor no lo queme directamente con llama.