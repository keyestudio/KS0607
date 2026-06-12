# 3. Stuurprogramma-installatie

## 3.1 Windows-systeem

**Het stuurprogramma controleren**

1. Sluit het moederbord aan op de computer.

![](./media/1.jpg)

2. Open de Apparaatbeheer. Als de melding **"Silicon Labs CP210x USB to UART Bridge (COMx)"** verschijnt, betekent dit dat het stuurprogramma is geïnstalleerd en kunt u het gedeelte **"Stuurprogramma-installatie"** overslaan.

![](./media/Animation.gif)

**Handmatige stuurprogramma-installatie**

1. Stuurprogramma downloaden

- Windows-systeem: [Windows-systeem stuurprogramma](./Windows.7z)

2. Sluit het moederbord aan op de computer en open de Apparaatbeheer. Als er een geel uitroepteken voor het stuurprogramma in de afbeelding staat, betekent dit dat het stuurprogramma niet is geïnstalleerd. Download het stuurprogramma en installeer het handmatig.

![](./media/Animation-1750921346712-3.gif)

## 3.2 MAC-systeem

**1 Het stuurprogramma controleren**

Sluit het ontwikkelbord aan op de computer en ga naar [Extra] ---> [Poort] om de poort van het ontwikkelbord te selecteren. (Opmerking: Als u niet zeker weet welke poort het ontwikkelbord is, sluit dan het moederbord aan en maak een foto om alle poorten te registreren. Koppel vervolgens het ontwikkelbord los en maak nog een foto. Vergelijk de twee foto's om de verdwenen poort te vinden; dat is de poort van het bord. Selecteer deze vervolgens.) Als u de poort niet herkent, vervang dan de USB-poort van de computer of de USB-kabel om de poort opnieuw te herkennen. Als het nog steeds niet werkt, raadpleeg dan de volgende stappen om het stuurprogramma te installeren.

![](./media/20250626154343.png)

**2 Handmatige stuurprogramma-installatie**

1. Stuurprogramma downloaden

​       Mac-systeem: [Mac-systeem stuurprogramma](./Mac.7z)

2. Dubbelklik om het gedownloade stuurprogramma zip-pakket te decomprimeren.

![](./media/image-20250417083615847-1749262759458-8.png)

![](./media/image-20250417083758947-1749262759458-7.png)

![](./media/image-20250417083918581-1749262759458-5.png)

3. Klik daarna steeds op **"Volgende"** totdat de installatie is voltooid.

![](./media/7cca827fe946096f228797dadce10661.png)

Op dit punt kan de poort worden herkend door het bord opnieuw in te pluggen.

4. Ga vervolgens naar de Arduino IDE, klik op "Extra" en selecteer het bord Arduino Uno en de herkende poort van het ontwikkelbord.

![](./media/2.png)

5. Klik op ![image-20250417085312966](./media/image-20250417085312966-1749262759459-18.png) om de code te uploaden. Wanneer het klaar is, verschijnt "Done uploading".

![](./media/3.png)