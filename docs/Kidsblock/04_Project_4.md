### Proyecto 4: Sensor de Seguimiento de Línea

#### **(1)Descripción:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

El sensor de seguimiento es en realidad un sensor infrarrojo. El componente utilizado aquí es el tubo infrarrojo TCRT5000.

Su principio de funcionamiento es usar la diferente reflectividad de la luz infrarroja a los colores, luego convertir la intensidad de la señal reflejada en una señal de corriente.

Durante el proceso de detección, el negro está activo en nivel ALTO mientras que el blanco está activo en nivel BAJO. La altura de detección es de 0 a 3 cm.

El módulo de seguimiento de línea de 3 canales de Keyestudio ha integrado 3 conjuntos de tubos infrarrojos TCRT5000 en una sola placa, lo que resulta más conveniente para el cableado y el control.

Si el Sensor de Seguimiento de Línea no funciona como se espera, deberá usar un destornillador para ajustar su potenciómetro para hacerlo más sensible. Cuando su dedo se acerca al sensor, su LED incorporado se enciende, y cuando su dedo se aleja, su LED incorporado se apaga. En ese momento, su sensibilidad es relativamente buena.

![](./media/img-20240117091947.png)

#### **(2)Parámetros:**

- Voltaje de operación: 3.3-5V (DC)
- Interfaz: 5PIN
- Señal de salida: Señal digital
- Altura de detección: 0-3 cm

Nota especial: antes de realizar las pruebas, gire el potenciómetro del sensor para ajustar la sensibilidad de detección. Cuando ajuste el LED en el umbral entre ENCENDIDO y APAGADO, la sensibilidad es la mejor.

<span style="color: rgb(255, 76, 65);">Nota:</span> el sensor de seguimiento de línea está instalado en la parte inferior del robot.

#### **(3)Diagrama de Conexión:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4)Código de Prueba:**

También puede arrastrar bloques para editar su código, como se muestra a continuación.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/700cb0ecc14cbccd6e367c5098360f08.png)

![](media/271423c55b5f147796beb344eed7e9cf.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/5298cdfb6fd7c71df155c969c80450cd.png)

#### **(5)Resultados de la Prueba:**

Cargue el código en la placa de desarrollo, abra el monitor serial a 9600 y verifique los sensores de seguimiento de línea. El valor mostrado es 1 (nivel alto) cuando no se reciben señales. El valor cambia a 0 cuando el sensor es cubierto con papel.

![](media/5630032421adf9446d51b770f0e7f8af.png)

#### **(6)Práctica de Extensión:**

Podemos controlar un LED con este sensor. El LED está conectado a D9. Si lo cubrimos, el LED se encenderá.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

También puede arrastrar bloques para editar su código, como se muestra a continuación.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/574854f4d96c40a85e1db549d85f14f4.png)

![](media/9077c0d059f7a4d3277f10ccb4e962fb.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

![](media/80e9c514357c63f4791c72220829b673.png)

![](media/b10e1897e99af2c1ade6c09da6c30dba.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/b5a4b5a04cdee9f79d6e18a5c48cbe48.png)

Cuando un objeto (como papel o un dedo) se acerca al sensor de seguimiento de línea, el sensor detecta la señal de retorno emitida por sí mismo, y el módulo LED se enciende. Cuando el sensor no detecta ninguna señal de retorno, el módulo LED se apaga.

![](./media/img-20240117092116.png)