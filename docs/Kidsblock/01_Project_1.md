### Projet 1 : Clignotement de LED

#### (1) Description :

![](./media/image-20250709122631704.png)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Pour les débutants et les passionnés, le clignotement de LED est un programme fondamental. LED, l'abréviation de diodes électroluminescentes, est composée de composés chimiques Ga, As, P, N, etc. La LED peut clignoter en différentes couleurs en modifiant le temps de délai dans le code de test. En mode de contrôle, alimentez GND et VCC. La LED s'allumera si l'extrémité S est à un niveau haut ; sinon, elle s'éteindra.

#### **(2) Paramètres :**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Interface de contrôle : port numérique
- Tension de fonctionnement : DC 3.3-5V
- Espacement des broches : 2.54mm
- Couleur d'affichage de la LED : jaune

#### (3) Composants nécessaires :

![](./media/image-20250709122437613.png)

#### **(4) Carte d'extension du pilote moteur 8833 :**

La carte d'extension du pilote moteur Keyestudio 8833 est compatible avec la carte de développement Arduino UNO. Il suffit de l'empiler sur la carte de développement lors de son utilisation.

![](media/d8696e83ade31f2b7c56cc5911eacbd7.GIF)

#### **(5) Schéma de connexion :**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](./media/image-20250709122655936.png)

<span style="color: rgb(255, 76, 65);">**REMARQUE :**</span> La LED est connectée au port D9. N'oubliez pas d'installer les cavaliers sur le shield.

#### **(6) Code de test :**

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.

![](media/cc43ba357acb68a4961adb7e5041b6fe.png)

![](media/26b69cd46ad24e1c900c4fb316430353.png)

![](media/21dc3c24da4271aa7ec2bfdac732eeb3.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et des conflits peuvent survenir avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/ba4723bab640078eccbe1811da138bc3.png)

#### **(7) Résultats du test :**

Téléversez le programme, la LED clignote à un intervalle de 1s.

#### **(8) Pratique d'extension :**

Nous savons maintenant comment contrôler la LED, alors changeons la fréquence de la LED.

Nous pouvons modifier la fréquence de la LED sans changer la broche de la LED. Modifions le code.

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et des conflits peuvent survenir avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/58c76be4c719a885afb500e8f3b80b85.png)

Le résultat du test montre que la LED clignote plus rapidement. Par conséquent, nous pouvons conclure que les broches et le temps de délai influencent la fréquence de clignotement.