### Projet 20 : Ventilateur

#### **(1)Description :**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Ce module ventilateur utilise une puce de contrôle de moteur HR1124S, une puce pilote H-bridge à canal unique contenant des tubes d'alimentation PMOS et NMOS à faible résistance de conductivité. La faible résistance de conductivité peut réduire la consommation d'énergie, contribuant ainsi au fonctionnement sûr de la puce pendant une durée plus longue.

De plus, son faible courant en veille et son faible courant de fonctionnement statique le rendent applicable aux jouets. Nous pouvons contrôler le sens de rotation et la vitesse du ventilateur en émettant des signaux IN+ et IN- ainsi que des signaux PWM.

#### **(2)Paramètres :**

- Tension de fonctionnement : 5V

- Courant : 200mA

- Puissance maximale : 2W

- Température de fonctionnement : -10°C à +50 degrés Celsius

- Taille : 47.6mm \* 23.8mm

#### **(3)Schéma de connexion :**

Le module ventilateur nécessite un courant important pour fonctionner ; par conséquent, nous installons un support de batterie.

![](media/2bd9aa5cc21e274458328958561f1915.png)

Les broches GND, VCC, IN+ et IN- du module ventilateur sont connectées aux broches G, V, 12 et 13 du shield.

#### **(4)Code de test :**

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/1360090880c1cd9b20671c17604f4108.png)

![](media/4e9354e674060efe6cf540a3e1b87813.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut provoquer l'échec du téléversement.)

![](media/cbb8f153dd0d114bdd350577af7a1f02.png)

#### **(5)Résultats du test :**

Téléversez le code, connectez les composants, mettez sous tension et réglez l'interrupteur DIP sur ON. Le petit ventilateur tournera dans le sens horaire pendant 2s, s'arrêtera pendant 2s et tournera dans le sens antihoraire pendant 2s.

![](./media/img-20240117100504.png)

#### **(6)Pratique d'extension :**

Nous avons compris le principe de fonctionnement du capteur de flamme. Ensuite, connectez un capteur de flamme dans le circuit, comme indiqué ci-dessous. Puis contrôlez le ventilateur pour éteindre le feu à l'aide du capteur de flamme.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)


Vous pouvez faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut provoquer l'échec du téléversement.)

![](media/74ddb07daf4063f0640c31f4243a0864.png)


Après avoir téléversé le code, activez l'interrupteur d'alimentation du shield de pilotage du moteur, vous pouvez allumer le ventilateur lorsqu'une flamme est détectée par le capteur de flamme gauche du robot.

![](./media/img-20240117102303.png)