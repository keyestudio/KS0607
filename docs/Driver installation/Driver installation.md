# 3. Instalación del controlador

## 3.1 Sistema Windows

**Verificación del controlador**

1. Conecta la placa base al ordenador.

![](./media/1.jpg)

2. Abre el Administrador de dispositivos. Si aparece el mensaje **"Silicon Labs CP210x USB to UART Bridge (COMx)"**, significa que el controlador ya está instalado y puedes omitir la sección **"Instalación del controlador"**.

![](./media/Animation.gif)

**Instalación manual del controlador**

1. Descarga del controlador

- Sistema Windows: [Controlador para sistema Windows](./Windows.7z)

2. Conecta la placa base al ordenador y abre el Administrador de dispositivos. Si aparece un signo de exclamación amarillo delante del controlador en la imagen, significa que el controlador no está instalado. Por favor, descarga el controlador e instálalo manualmente.

![](./media/Animation-1750921346712-3.gif)

## 3.2 Sistema MAC

**1 Verificación del controlador**

Conecta la placa de desarrollo al ordenador y ve a [Herramientas] ---> [Puerto] para seleccionar el puerto de la placa de desarrollo. (Nota: Si no puedes confirmar cuál es el puerto de la placa de desarrollo, conecta la placa base y toma una captura de pantalla para registrar todos los puertos, luego desconecta la placa de desarrollo y toma otra captura. Compara las dos imágenes para encontrar el puerto que desapareció, que es el puerto de la placa, y selecciónalo.) Si no puedes reconocer el puerto, intenta cambiar el puerto USB del ordenador o el cable USB para volver a reconocerlo. Si aún no funciona, consulta los siguientes pasos para instalar el controlador.

![](./media/20250626154343.png)

**2 Instalación manual del controlador**

1. Descarga del controlador

​       Sistema Mac: [Controlador para sistema Mac](./Mac.7z)

2. Haz doble clic para descomprimir el paquete zip del controlador descargado.

![](./media/image-20250417083615847-1749262759458-8.png)

![](./media/image-20250417083758947-1749262759458-7.png)

![](./media/image-20250417083918581-1749262759458-5.png)

3. Después, sigue haciendo clic en **"Siguiente"** hasta que la instalación se complete.

![](./media/7cca827fe946096f228797dadce10661.png)

En este punto, el puerto podrá ser reconocido al volver a conectar la placa.

4. Luego ve al Arduino IDE, haz clic en "Herramientas" y selecciona la placa Arduino Uno y el puerto de la placa de desarrollo reconocido.

![](./media/2.png)

5. Haz clic en ![image-20250417085312966](./media/image-20250417085312966-1749262759459-18.png) para cargar el código. Mostrará "Done uploading" cuando haya terminado.

![](./media/3.png)