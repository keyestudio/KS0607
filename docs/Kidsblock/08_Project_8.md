### Projet 8 : Commande et Contrôle de Vitesse du Moteur

#### **(1) Description :**

Il existe de nombreuses façons de piloter des moteurs. Notre voiture intelligente utilise la solution la plus courante appelée L298P. Le L298P, fabriqué par STMicroelectronics, est un excellent circuit de commande spécialement conçu pour piloter des moteurs haute puissance. Il peut piloter directement des moteurs à courant continu, des moteurs biphasés et quadriphasés avec un courant de commande atteignant 2A. La borne de sortie du moteur utilise 8 diodes Schottky haute vitesse comme protection. Nous avons conçu une carte d'extension basée sur le circuit L298P dont la conception empilable peut être directement branchée sur la carte UNO R3, réduisant ainsi les difficultés techniques pour les utilisateurs dans l'utilisation et la commande du moteur.

Empilez la carte d'extension sur la carte, alimentez la BAT, tournez le commutateur DIP sur la position ON, et alimentez simultanément la carte d'extension et la carte UNO R3 via une alimentation externe. Pour faciliter le câblage, la carte d'extension est équipée d'interfaces anti-inversion (PH2.0 -2P -3P -4P -5P) et peut ainsi être branchée directement avec des moteurs, une alimentation et des capteurs/modules. L'interface Bluetooth de la carte d'extension de commande est entièrement compatible avec le module Bluetooth Keyestudio HM-10. Par conséquent, il suffit d'insérer le module Bluetooth HM-10 dans l'interface correspondante lors de la connexion. En même temps, la carte d'extension de commande utilise également des connecteurs à broches 2.54 pour étendre certains ports numériques et analogiques disponibles, vous permettant ainsi d'ajouter d'autres capteurs et de réaliser des expériences d'extension.

La carte d'extension peut être connectée à 4 moteurs à courant continu. Dans le mode de connexion par cavalier par défaut, les moteurs des interfaces A et A1, B et B1 sont connectés en parallèle, et leur mode de fonctionnement est identique. 8 cavaliers peuvent être utilisés pour contrôler le sens de rotation des 4 interfaces moteur. Par exemple, lorsque les deux cavaliers devant l'interface du moteur A sont changés d'une connexion horizontale à une connexion verticale, le sens de rotation du moteur A est alors opposé au sens de rotation d'origine.

![](media/6c3731f639e113c8f32fe1829f239898.png)

![](media/62ee9578858ecc8e27b824af65fb22bb.png)

#### **(2) Paramètres :**

-   Tension d'entrée de la partie logique : DC 5V

-   Tension d'entrée de la partie de commande : DC 7-12V

-   Courant de fonctionnement de la partie logique : ≤36mA

-   Courant de fonctionnement de la partie de commande : ≤ 2A

-   Puissance de dissipation maximale : 25W (T=75℃)

-   Niveau du signal de commande en entrée :

    Niveau haut : 2.3V ≤ Vin ≤ 5V

    Niveau bas : 0V ≤ Vin ≤ 1.5V

-   Température de fonctionnement : -25℃～＋130℃

#### **(3) Faire avancer le robot :**

La broche de direction du moteur A est D2, la broche de contrôle de vitesse est D5 ; la broche de direction du moteur B est D4 et la broche de contrôle de vitesse est D6.

D'après le tableau ci-dessous, nous pouvons savoir comment contrôler le mouvement du robot en contrôlant la rotation de deux moteurs via les ports numériques et les ports PWM. Parmi ceux-ci, la plage de valeur PWM est de 0 à 255. Plus la valeur est grande, plus le moteur tourne vite.

|     Fonction     |  D4  | D6（PWM） | Moteur（gauche）B |  D2  | D5（PWM） | Moteur（droite）A |
| :--------------: | :--: | :-------: | :---------------: | :--: | :-------: | :---------------: |
|    Avancer       | HIGH |     0     |   Rotation gauche | HIGH |     0     |   Rotation gauche |
|    Reculer       | LOW  |    255    |  Rotation droite  | LOW  |    255    |  Rotation droite  |
| Tourner à gauche | LOW  |    255    |  Rotation droite  | HIGH |    100    |   Rotation gauche |
| Tourner à droite | HIGH |    100    |   Rotation gauche | LOW  |    255    |  Rotation droite  |
|     Arrêt        | LOW  |     0     |       Arrêt       | LOW  |     0     |       Arrêt       |

#### **(4) Schéma de connexion :**

![](./media/image-20250709134029403.png)

<span style="color: rgb(255, 76, 65);">Remarque :</span>

Le connecteur à 4 broches est marqué A, A1, B1 et B. Le moteur arrière droit est connecté à B de la carte 8833 et celui avant gauche est connecté au port A.

#### **(5) Code de test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous.

（1）![](media/7cbc4d14c2e2dac956f2e9f145f01f31.png)

（2）![](media/0067d367772d4e3005bfc097ba3b59b0.png)

（3）![](media/f0c505e8268454c7996b755f97c6322b.png)

（4）![](media/b7215c8a4997a188947e80fdee1a8cd9.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut provoquer l'échec du téléversement.)

![](media/332229f3dc01a38de898367f52531b28.png)


#### **(6) Résultats du test :**

Après avoir effectué le câblage selon le schéma, téléversé le code de test et mis sous tension.

![](./media/img-20240117092625.png)

La voiture intelligente avance pendant 2s, recule pendant 2s, tourne à gauche pendant 2s, tourne à droite pendant 2s et s'arrête pendant 2s.