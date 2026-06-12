# 3. Installation des pilotes

## 3.1 Système Windows

**Vérification du pilote**

1. Connectez la carte mère à l'ordinateur.

![](./media/1.jpg)

2. Ouvrez le Gestionnaire de périphériques. Si le message **"Silicon Labs CP210x USB to UART Bridge (COMx)"** apparaît, cela prouve que le pilote est installé, et vous pouvez ignorer la partie **"Installation du pilote"**.

![](./media/Animation.gif)

**Installation manuelle du pilote**

1. Téléchargement du pilote

- Système Windows : [Pilote pour système Windows](./Windows.7z)

2. Connectez la carte mère à l'ordinateur et ouvrez le Gestionnaire de périphériques. Si un point d'exclamation jaune apparaît devant le pilote dans l'image, cela prouve que le pilote n'est pas installé. Veuillez télécharger le pilote et l'installer manuellement.

![](./media/Animation-1750921346712-3.gif)

## 3.2 Système MAC

**1 Vérification du pilote**

Connectez la carte de développement à l'ordinateur, puis allez dans [Outils] ---> [Port] pour sélectionner le port de la carte de développement. (Remarque : Si vous ne pouvez pas confirmer quel port correspond à la carte de développement, veuillez connecter la carte mère et prendre une photo pour enregistrer tous les ports, puis débranchez la carte de développement et prenez une autre photo. Comparez les deux photos pour trouver le port disparu, qui est le port de la carte, puis sélectionnez-le.) Si vous ne pouvez pas reconnaître le port, veuillez changer le port USB de l'ordinateur ou le câble USB pour reconnaître à nouveau le port. Si cela ne fonctionne toujours pas, reportez-vous aux étapes suivantes pour installer le pilote.

![](./media/20250626154343.png)

**2 Installation manuelle du pilote**

1. Téléchargement du pilote

​       Système Mac : [Pilote pour système Mac](./Mac.7z)

2. Double-cliquez pour décompresser le fichier zip du pilote téléchargé.

![](./media/image-20250417083615847-1749262759458-8.png)

![](./media/image-20250417083758947-1749262759458-7.png)

![](./media/image-20250417083918581-1749262759458-5.png)

3. Ensuite, continuez à cliquer sur **"Suivant"** jusqu'à ce que l'installation soit terminée.

![](./media/7cca827fe946096f228797dadce10661.png)

À ce stade, le port peut être reconnu en branchant à nouveau la carte.

4. Ensuite, allez dans l'Arduino IDE, cliquez sur "Outils", et sélectionnez la carte Arduino Uno ainsi que le port de la carte de développement reconnu.

![](./media/2.png)

5. Cliquez sur ![image-20250417085312966](./media/image-20250417085312966-1749262759459-18.png) pour téléverser le code. Le message "Done uploading" s'affichera une fois terminé.

![](./media/3.png)