### Projet 11 : Char Suiveur à Ultrasons


#### **(1) Description :**

Dans la leçon précédente, nous avons appris à propos de la voiture intelligente suiveuse de lumière. Dans cette leçon, nous pouvons combiner les connaissances pour fabriquer une voiture suiveuse à ultrasons. Dans ce projet, nous utilisons des capteurs à ultrasons pour détecter la distance entre la voiture et l'obstacle en face, puis nous contrôlons la rotation des deux moteurs en fonction de ces données afin de contrôler les mouvements de la voiture intelligente.

La logique spécifique de la voiture intelligente suiveuse à ultrasons est présentée dans le tableau ci-dessous :

|                        Détection                        |              Paramètre              |
| :-----------------------------------------------------: | :-------------------------------: |
| La distance (cm) entre la voiture et l'obstacle en face | Régler l'angle du servo à 90° |
|                      **Condition**                      |           **Mouvement**            |
|               distance≥20 et distance≤50               |             Avancer              |
|            10＜distance＜20<br/>distance＞50            |               Arrêt                |
|                       distance≤10                       |              Reculer              |

#### **(2) Organigramme :**

![](media/wps118.png)

#### **(3) Schéma de connexion :**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

<span style="color: rgb(255, 76, 65);">Remarque :</span> Le câblage du capteur à ultrasons, du servo et du moteur est le même que dans l'expérience du projet précédent. Le GND, VCC, SDA et SCL du panneau LED 8x16 sont respectivement connectés à G (GND), V (VCC), A4 et A5 sur la carte d'extension.

#### **(4) Code de test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous.

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/f6fb93211f786d023eb77eb210eae454.png)

（3）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

(7) ![](media/4b40151c7482ff9371570978b8ef9c77.png)

(8) ![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

(9) ![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

(10) ![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/b895ca60e3249e09d4c15c356c60099a.png)


#### **(5) Résultat du test :**

Téléversez le code, mettez sous tension et positionnez l'interrupteur DIP sur ON. Le servo tournera de 90°, le panneau LED 8X16 affichera ![](media/fdd4ae50b3372cc9c4ef27f6bddda387.png), et la voiture suivra l'obstacle pour se déplacer.

![](./media/img-20240117093900.png)