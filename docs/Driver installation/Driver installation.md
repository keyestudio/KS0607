# 3. Installazione del driver

## 3.1 Sistema Windows

**Verifica del driver**

1. Collegare la scheda madre al computer.

![](./media/1.jpg)

2. Aprire il Gestione dispositivi. Se appare il messaggio **"Silicon Labs CP210x USB to UART Bridge (COMx)"**, significa che il driver è già installato e puoi saltare la sezione **"Installazione del driver"**.

![](./media/Animation.gif)

**Installazione manuale del driver**

1. Download del driver

- Sistema Windows: [Driver per sistema Windows](./Windows.7z)

2. Collegare la scheda madre al computer e aprire il Gestione dispositivi. Se davanti al driver nell'immagine è presente un punto esclamativo giallo, significa che il driver non è installato. Si prega di scaricare il driver e installarlo manualmente.

![](./media/Animation-1750921346712-3.gif)

## 3.2 Sistema MAC

**1 Verifica del driver**

Collegare la scheda di sviluppo al computer e andare su [Strumenti] ---> [Porta] per selezionare la porta della scheda di sviluppo. (Nota: Se non si riesce a confermare quale porta corrisponde alla scheda di sviluppo, collegare la scheda madre e scattare una foto per registrare tutte le porte, quindi scollegare la scheda di sviluppo e scattare un'altra foto. Confrontare le due foto per trovare la porta scomparsa, che è la porta della scheda, e selezionarla.) Se non si riesce a riconoscere la porta, sostituire la porta USB del computer o il cavo USB per tentare un nuovo riconoscimento. Se il problema persiste, fare riferimento ai passaggi seguenti per installare il driver.

![](./media/20250626154343.png)

**2 Installazione manuale del driver**

1. Download del driver

​       Sistema Mac: [Driver per sistema Mac](./Mac.7z)

2. Fare doppio clic per decomprimere il pacchetto zip del driver scaricato.

![](./media/image-20250417083615847-1749262759458-8.png)

![](./media/image-20250417083758947-1749262759458-7.png)

![](./media/image-20250417083918581-1749262759458-5.png)

3. Successivamente, continuare a fare clic su **"Avanti"** fino al completamento dell'installazione.

![](./media/7cca827fe946096f228797dadce10661.png)

A questo punto, la porta può essere riconosciuta ricollegando la scheda.

4. Aprire quindi l'Arduino IDE, fare clic su "Strumenti" e selezionare la scheda Arduino Uno e la porta della scheda di sviluppo riconosciuta.

![](./media/2.png)

5. Fare clic su ![image-20250417085312966](./media/image-20250417085312966-1749262759459-18.png) per caricare il codice. Al termine verrà visualizzato il messaggio "Done uploading".

![](./media/3.png)