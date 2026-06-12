### Projet 5 : Contrôle du Servomoteur

#### **(1)Description :**

Un servomoteur est un actionneur rotatif de contrôle de position. Il se compose principalement d'un boîtier, d'une carte de circuit imprimé, d'un moteur sans noyau, d'un engrenage et d'un capteur de position. Son principe de fonctionnement est que le servo reçoit le signal envoyé par le MCU ou le récepteur et produit un signal de référence avec une période de 20ms et une largeur de 1,5ms. Il compare ensuite la tension de polarisation CC acquise à la tension du potentiomètre et obtient la sortie de différence de tension.

Lorsque la vitesse du moteur est constante, le potentiomètre est entraîné en rotation par l'engrenage de réduction en cascade, ce qui fait que la différence de tension est 0, et le moteur s'arrête de tourner. En général, la plage d'angle de rotation du servo est de 0° à 180°.

L'angle de rotation du servomoteur est contrôlé en réglant le rapport cyclique du signal PWM (Modulation de Largeur d'Impulsion). La période standard du signal PWM est de 20ms (50Hz). Théoriquement, la largeur est distribuée entre 1ms et 2ms, mais en pratique, elle est entre 0,5ms et 2,5ms. La largeur correspond à l'angle de rotation de 0° à 180°. Notez que pour différentes marques de moteurs, le même signal peut entraîner des angles de rotation différents.

![](media/69be958142b773acdae33eeef12afed7.png)

En général, le servo possède trois fils de couleur marron, rouge et orange. Le fil marron est la masse, le rouge est le fil du pôle positif et l'orange est le fil du signal.

![](media/49467dfa70799401a5a5acc691014aee.png)

L'angle du servo :

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Paramètres :**

- Tension de fonctionnement : DC 4,8V \~ 6V

- Plage d'angle de fonctionnement : environ 180° (à 500 → 2500 μsec)

- Plage de largeur d'impulsion : 500 → 2500 μsec

- Vitesse à vide : 0,12 ± 0,01 sec / 60 (DC 4,8V) 0,1 ± 0,01 sec / 60 (DC 6V)

- Courant à vide : 200 ± 20mA (DC 4,8V) 220 ± 20mA (DC 6V)

- Couple d'arrêt : 1,3 ± 0,01kg · cm (DC 4,8V) 1,5 ± 0,1kg · cm (DC 6V)

- Courant d'arrêt : ≦ 850mA (DC 4,8V) ≦ 1000mA (DC 6V)

- Courant de veille : 3 ± 1mA (DC 4,8V) 4 ± 1mA (DC 6V)

#### **(3)Schéma de Connexion :**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Les fils marron, rouge et orange du servo sont respectivement connectés à Gnd(G), 5v(V) et D10 du shield. N'oubliez pas de connecter une alimentation externe en raison du courant élevé du servo. Sinon, la carte de développement sera endommagée.

#### **(4)Code de Test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous

![](media/5b04350e0310955ee2ecd48338f556a3.png)

![](media/7dd97d17b785de17e6c9362fa32e2a74.png)

![](media/69724a2063fa25e0f142e1eb48efd40f.png)

![](media/e149b45054fe94196dea220b319cb0bf.png)

**Code de Test Complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/26e37037daf84d69320b76dd13346cd1.png)

#### **(6)Résultats du Test :**

Téléversez le code, branchez l'alimentation et le servo se déplace dans la plage de 0° à 180°.

![](./media/img-20240117092225.png)