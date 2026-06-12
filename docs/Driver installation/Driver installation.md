# 3. Treiberinstallation

## 3.1 Windows-System

**Treiber überprüfen**

1. Schließen Sie das Motherboard an den Computer an.

![](./media/1.jpg)

2. Öffnen Sie den Geräte-Manager. Wenn die Meldung **"Silicon Labs CP210x USB to UART Bridge (COMx)"** erscheint, ist der Treiber bereits installiert und Sie können den Abschnitt **"Treiberinstallation"** überspringen.

![](./media/Animation.gif)

**Manuelle Treiberinstallation**

1. Treiber herunterladen

- Windows-System: [Windows-System-Treiber](./Windows.7z)

2. Schließen Sie das Motherboard an den Computer an und öffnen Sie den Geräte-Manager. Wenn ein gelbes Ausrufezeichen vor dem Treiber im Bild angezeigt wird, ist der Treiber nicht installiert. Bitte laden Sie den Treiber herunter und installieren Sie ihn manuell.

![](./media/Animation-1750921346712-3.gif)

## 3.2 MAC-System

**1 Treiber überprüfen**

Schließen Sie das Entwicklungsboard an den Computer an und gehen Sie zu [Tools] ---> [Port], um den Port des Entwicklungsboards auszuwählen. (Hinweis: Wenn Sie nicht sicher sind, welcher Port das Entwicklungsboard ist, schließen Sie das Motherboard an, machen Sie ein Foto, um alle Ports zu dokumentieren, trennen Sie dann das Entwicklungsboard und machen Sie ein weiteres Foto. Vergleichen Sie die beiden Fotos, um den verschwundenen Port zu finden – das ist der Port des Boards – und wählen Sie ihn aus.) Wenn der Port nicht erkannt werden kann, tauschen Sie bitte den USB-Port des Computers oder das USB-Kabel aus, um den Port erneut zu erkennen. Wenn es immer noch nicht funktioniert, folgen Sie den nachstehenden Schritten zur Treiberinstallation.

![](./media/20250626154343.png)

**2 Manuelle Treiberinstallation**

1. Treiber herunterladen

​       Mac-System: [Mac-System-Treiber](./Mac.7z)

2. Doppelklicken Sie auf das heruntergeladene Treiber-Zip-Paket, um es zu entpacken.

![](./media/image-20250417083615847-1749262759458-8.png)

![](./media/image-20250417083758947-1749262759458-7.png)

![](./media/image-20250417083918581-1749262759458-5.png)

3. Klicken Sie anschließend so lange auf **"Weiter"**, bis die Installation abgeschlossen ist.

![](./media/7cca827fe946096f228797dadce10661.png)

An diesem Punkt kann der Port erkannt werden, wenn das Board erneut eingesteckt wird.

4. Gehen Sie dann zur Arduino IDE, klicken Sie auf "Tools" und wählen Sie das Board Arduino Uno sowie den erkannten Entwicklungsboard-Port aus.

![](./media/2.png)

5. Klicken Sie auf ![image-20250417085312966](./media/image-20250417085312966-1749262759459-18.png), um den Code hochzuladen. Nach Abschluss wird "Done uploading" angezeigt.

![](./media/3.png)