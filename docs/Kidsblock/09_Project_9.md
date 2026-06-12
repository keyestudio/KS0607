### Proyecto 9: Matriz de puntos LED de expresión facial 8*16

#### **(1)Descripción:**

¿No sería divertido agregar una pantalla de expresiones al robot? Y la matriz de puntos LED 8*16 de Keyestudio puede hacerlo. Con su ayuda, podrías diseñar expresiones faciales, imágenes, patrones y otras pantallas por ti mismo.

La placa LED 8*16 viene con 128 LEDs. Los datos del microprocesador (Arduino) se comunican con el AiP1640 a través de una interfaz de bus de dos hilos. Por lo tanto, puede controlar el encendido y apagado de los 128 LEDs en el módulo, de modo que la matriz de puntos en el módulo muestre el patrón que necesitas. Se proporciona un cable HX-2.54 4Pin para tu comodidad al conectar los cables.

#### **(2)Parámetros:**

-   Voltaje de trabajo: DC 3.3-5V

-   Pérdida de potencia: 400mW

-   Frecuencia de oscilación: 450KHz

-   Corriente de conducción: 200mA

-   Temperatura de trabajo: -40\~80℃

-   Modo de comunicación: bus de dos hilos

#### **(3)Conocimientos:**

**Circuito de la matriz de puntos LED 8\*16**

![](media/edf6c77d05904eebbaa89d557e9e9c1a.png)

**Principio de la matriz de puntos LED 8\*16**

¿Cómo controlar cada LED de la matriz de puntos 8\*16? Se sabe que cada byte tiene 8 bits y cada bit es 0 o 1. Cuando es 0, el LED está apagado, mientras que cuando es 1, el LED está encendido. Un byte puede controlar una columna del LED, y naturalmente 16 bytes pueden controlar 16 columnas de LEDs, eso es la matriz de puntos 8\*16.

**Descripción de pines y protocolo de comunicación**

Los datos del microprocesador (Arduino) se comunican con el AiP1640 a través de un cable de bus de dos hilos.

El diagrama del protocolo de comunicación es el siguiente: (SCLK) es SCL, (DIN) es SDA.

![](media/ea2bab37f23c09453c680590b84653d6.png)

①La condición de inicio para la entrada de datos: SCL está en nivel alto y SDA cambia de alto a bajo.

②Para la configuración del comando de datos, hay métodos como se muestra en la figura a continuación.

En nuestro programa de ejemplo, selecciona la forma de **agregar 1 a la dirección automáticamente**, el valor binario es 0100 0000 y el valor hexadecimal correspondiente es 0x40.

![](media/image-20230907161100692.png)

③Para la configuración del comando de dirección, la dirección se puede seleccionar como se muestra a continuación.

El primer 00H se selecciona en nuestro programa de ejemplo, y el número binario 1100 0000 corresponde al hexadecimal 0xc0.

![](media/image-20230907161152467.png)


④El requisito para la entrada de datos es que cuando SCL está en nivel alto al ingresar datos, la señal en SDA debe permanecer sin cambios. Solo cuando la señal de reloj en SCL está en nivel bajo, puede cambiarse la señal en SDA. La entrada de datos es primero el bit menos significativo y luego el bit más significativo.

⑤La condición para el fin de la transmisión de datos es que cuando SCL está en nivel bajo, SDA en nivel bajo y SCL en nivel alto, el nivel de SDA se vuelve alto.

⑥Control de pantalla, configurar diferentes anchos de pulso; el ancho de pulso se puede seleccionar como se muestra en la figura a continuación.

En el ejemplo, el ancho de pulso es 4/16, y el hexadecimal correspondiente a 1000 1010 es 0x8A.

![](media/image-20230907161220995.png)

**Instrucciones para el uso de la herramienta de módulo**

La herramienta de matriz de puntos utiliza la versión en línea, y el enlace es: <http://dotmatrixtool.com/#>

①Ingresa el enlace y la página aparece como se muestra a continuación

![](media/354693b5679a2615c62e99b7025d6355.png)

②La matriz de puntos es 8\*16, por lo que ajusta la altura a 8 y el ancho a 16, como se muestra en la figura a continuación.

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③Generar datos hexadecimales a partir del patrón.

Como se muestra en la figura a continuación, presiona el botón izquierdo del ratón para seleccionar, haz clic derecho para cancelar; dibuja el patrón que deseas, haz clic en Generate, y se generarán los datos hexadecimales que necesitamos.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4)Diagrama de conexión:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

El GND, VCC, SDA y SCL de la placa de luz LED 8x16 están conectados respectivamente al G(GND), V (VCC), A4 y A5 de la placa de expansión para comunicación serie de dos hilos.

(<span style="color: rgb(255, 76, 65);">Nota:</span> aunque está conectado con el pin IIC de Arduino, este módulo no es para comunicación IIC. Y el puerto IO aquí es para simular la comunicación I2C y puede conectarse con cualquier dos pines)

#### **(5)Código de prueba:**


También puedes arrastrar bloques para editar tu código, como se muestra a continuación

![](media/e346413e7f38f5f6368dd8262f173514.png)

![](media/8ecfff600093779602b37d2202493057.png)

![](media/0f0df06e3ed2adbbe3ffaa20dd3fa0a5.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serie, y puede haber conflictos con la comunicación serie Bluetooth, lo que puede causar que la carga falle.)

![](media/75e6f65c9a299868d37544ac42c54f66.png)

#### **(6)Resultados de la prueba:**

Después de cargar el código de prueba exitosamente, conecta los cables, gira el interruptor DIP al extremo ON y enciende, un patrón en forma de sonrisa aparece en la matriz de puntos.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7)Práctica de extensión:**

Usamos la herramienta de módulo que acabamos de aprender, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), para hacer que la matriz de puntos muestre el patrón de inicio, avanzar y detener, y luego limpiar el patrón. El intervalo de tiempo es de 2000 ms.

![](media/31ab1346c58438ca95c990e4ff963c0d.png)

Bloque para mostrar cara sonriente![](media/1702a82ce685e3e7da7b136cbc51e718.png)

Código para mostrar expresión![](media/bae6801afc8fbcc0e7a70c243559c266.png)

Bloque para mostrar corazón![](media/dcaa414f16d10068d2c3627959141da6.png)

Código para avanzar![](media/8fc218e6b35826aa31f5e00f61414651.png)

Bloque para retroceder![](media/043abae4540c578f93772ed9b6648e60.png)

Bloque para girar a la izquierda![](media/7b3d80a76228ee5b23555af17269a02d.png)

Bloque para girar a la derecha![](media/5a84b3538a62367a8f35cc59071c0bda.png)

Bloque para detenerse![](media/733bd1f96e1c9d116033a317cb507fac.png)

Bloque para limpiar![](media/06d37680acd61c9c5c4113c78c985eca.png)

También puedes arrastrar bloques para editar tu código, como se muestra a continuación.

（1）![](media/e346413e7f38f5f6368dd8262f173514.png)

（2）![](media/840217b5879f1fce9e36566dc76914a4.png)

（3）![](media/e72e75122897b0ef930196f762080623.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serie, y puede haber conflictos con la comunicación serie Bluetooth, lo que puede causar que la carga falle.)

![](media/dee30ed46775feb634d4e8e4ec0a189a.png)

Carga el código en la placa de desarrollo, la placa 8\*16 mostrará los siguientes patrones.

![](./media/image-20250709134319784.png)

![](./media/image-20250709134332835.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)