### Projet 6 : Capteur Ultrasonique

#### **(1) Description :**

![](media/0180b169a1c3b228394b43df704fac32.png)

Le capteur ultrasonique HC-SR04 utilise le sonar pour déterminer la distance d'un objet, à la manière des chauves-souris. Il offre une excellente détection de distance sans contact, avec une haute précision et des mesures stables, dans un boîtier facile à utiliser. Il est livré complet avec des modules émetteur et récepteur ultrasoniques.

Le HC-SR04, ou capteur ultrasonique, est utilisé dans une large gamme de projets électroniques pour créer des applications de détection d'obstacles et de mesure de distance, ainsi que diverses autres applications. Nous présentons ici la méthode simple pour mesurer la distance avec Arduino et un capteur ultrasonique, et comment utiliser le capteur ultrasonique avec Arduino.

![](./media/image-20250709133626194.png)

#### **(2) Paramètres :**

- Alimentation : +5V DC

- Courant au repos : \<2mA

- Courant de fonctionnement : 15mA

- Angle effectif : \<15°

- Distance de mesure : 2cm – 400 cm

- Résolution : 0.3 cm

- Angle de mesure : 30 degrés

- Largeur d'impulsion d'entrée du déclencheur : 10uS

#### **(3) Principe du capteur ultrasonique :**

Comme le montre l'image ci-dessus, il ressemble à deux yeux. L'un est l'extrémité émettrice, l'autre est l'extrémité réceptrice.

Le module ultrasonique émet des ondes ultrasoniques après le déclenchement d'un signal. Lorsque les ondes ultrasoniques rencontrent un objet et sont réfléchies, le module génère un signal d'écho, ce qui lui permet de déterminer la distance de l'objet à partir de la différence de temps entre le signal de déclenchement et le signal d'écho.

Ici, t est le temps entre l'émission du signal jusqu'à ce qu'il rencontre l'obstacle et revienne. La vitesse de propagation du son dans l'air est d'environ 343 m/s, et distance = vitesse × temps. Cependant, comme l'onde ultrasonique se déplace jusqu'à l'obstacle et revient, le temps représente deux fois la distance. Il faut donc diviser par 2. La distance mesurée par l'**onde ultrasonique = (vitesse × temps) / 2**.

1. Méthode d'utilisation et chronogramme du module ultrasonique :

2. Régler le temps de délai de la broche Trig du SR04 à au moins 10μs, ce qui permet de le déclencher pour détecter la distance.

3. Après le déclenchement, le module envoie automatiquement huit impulsions ultrasoniques à 40KHz et détecte s'il y a un signal de retour. Cette étape est effectuée automatiquement par le module.

4. Si le signal revient, la broche Echo génère un niveau haut, et la durée du niveau haut correspond au temps de transmission de l'onde ultrasonique jusqu'à son retour.

![](media/image-20230525110337646.png)

Schéma du circuit du capteur ultrasonique :

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4) Schéma de connexion :**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Note de câblage :</span> La broche VCC du module capteur ultrasonique est connectée au 5v(V) de la carte d'extension de pilotage de moteur Keyestudio 8833, la broche Trig est connectée au numérique D12, la broche Echo est connectée au numérique D13, et la broche Gnd est connectée à Gnd(G) ;

#### **(5) Code de test :**

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/128e0b4ee7d3448410d72312175bc6da.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/a6df8829b69f7faed26a73d01da8d50d.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/eca0805413af12957d319c706d3e7cdb.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut entraîner des conflits avec la communication série Bluetooth et provoquer l'échec du téléversement.)

![](media/569aff5ff2cbd2f3605f217ebb5ed50b.png)

#### **(6) Résultats du test :**

Téléversez le code de test sur la carte de développement, ouvrez le moniteur série et réglez le débit en bauds sur 9600. La distance détectée sera affichée en centimètres et en pouces. Lorsque vous obstruez le capteur ultrasonique avec votre main, la valeur de distance affichée diminue.

![](media/4f77acbf5b226e20e3cdd70c0f90602e.png)

#### **(7) Pratique avancée :**

Nous venons de mesurer la distance affichée par l'ultrason. Que diriez-vous de contrôler une LED avec la distance mesurée ? Essayons et connectons un module LED à la broche D9.

![](media/291ac1db0f38418772d11bb1786b7314.png)


Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/49d5523ae565e1d4dfc3504d1e1748d4.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/8d5fc923f5ded5305f36b1379c1ba38e.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/a6205e42e005084c33c247fe564bdcad.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut entraîner des conflits avec la communication série Bluetooth et provoquer l'échec du téléversement.)

![](media/065eac0ad9cfa8f07aeb5e648698bdb5.png)

Téléversez le code de test sur la carte de développement, approchez votre main du capteur ultrasonique et vérifiez si la LED s'allume.

![](./media/img-20240117092413.png)