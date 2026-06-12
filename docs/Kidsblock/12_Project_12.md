### Projet 12 : Char à évitement d'obstacles par ultrasons

#### **(1)Description :**

Dans le projet précédent, nous avons fabriqué une voiture intelligente à suivi de son par ultrasons. En réalité, en utilisant les mêmes composants et la même méthode de câblage, nous n'avons besoin que de modifier le code de test pour le transformer en une voiture intelligente à évitement d'obstacles par ultrasons. Cette voiture intelligente peut se déplacer en fonction du mouvement des mains humaines.

Nous utilisons des capteurs ultrasoniques pour détecter la distance entre la voiture intelligente et l'obstacle devant elle, puis nous contrôlons la rotation des deux moteurs en fonction de ces données afin de contrôler les mouvements de la voiture intelligente.

|                          Détection                           |         |
| :----------------------------------------------------------: | :-----: |
| Distance mesurée par le capteur ultrasonique entre la voiture et l'obstacle devant <br />（régler l'angle du servo à 90°） | a (cm)  |
| Distance mesurée par le capteur ultrasonique entre la voiture et l'obstacle à droite <br />（régler l'angle du servo à 0°） | a2 (cm) |
| Distance mesurée par le capteur ultrasonique entre la voiture et l'obstacle à gauche <br />（régler l'angle du servo à 180°） | a1 (cm) |

**Réglage : régler l'angle de départ du servo à 90°**

| Condition 1 |        Condition 2         |      Condition 3       | Mouvement                                                     |
| :---------: | :------------------------: | :--------------------: | :----------------------------------------------------------- |
|    a＜20    |                            |                        | Arrêt pendant 500ms ; régler l'angle du servo à 180°, lire a1, délai de 100ms ; régler l'angle du servo à 0°, lire a2, délai de 0.1s. |
|             | a1＜50<br />ou<br />a2＜50 | **Comparer a1 avec a2** |                                                              |
|             |                            |         a1＞a2         | Régler l'angle du servo à 90°, tourner à gauche pendant 700ms（régler PWM à 255）, et avancer（régler PWM à 200）. |
|             |                            |         a1＜a2         | Régler l'angle du servo à 90°, tourner à droite pendant 700ms（régler PWM à 255）, et avancer（régler PWM à 200）. |
|             | a1≥50<br />et<br />a2≥50  |         Aléatoire         | Régler l'angle du servo à 90°, tourner à gauche pendant 500ms（régler PWM à 255）, et avancer（régler PWM à 200）.<br /><br />Régler l'angle du servo à 90°, tourner à droite pendant 500ms（régler PWM à 255）, et avancer（régler PWM à 200）. |
|    a≥20     |                            |                        | Avancer（régler PWM à 100）                               |

#### **(2)Organigramme :**

![](media/wps119.png)

#### **(3)Schéma de connexion :**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

(<span style="color: rgb(255, 76, 65);">Remarque :</span> les fils marron, rouge et orange du servo sont respectivement connectés à G (GND), V（5V）et D10 de la carte d'extension ; et pour le capteur ultrasonique, la broche VCC est connectée au 5v (V), la broche Trig au numérique 12 (S), la broche Echo au numérique 13 (S), et la broche Gnd à Gnd (G) ; identique au projet précédent.）

#### **(4)Code de test :**


Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/5dcbd405806b8e341505d7316246dbdd.png)

（3）![](media/996c8d4e5dd9620757dfb097329e7d5d.png)

（4）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

（10）![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

（11）![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et des conflits peuvent survenir avec la communication série Bluetooth, ce qui peut provoquer l'échec du téléversement.)

![](media/4360f9642a8c6b2488767c079d481482.png)

#### **(5)Résultats du test :**

Après avoir téléversé le code de test avec succès, effectuez le câblage, basculez le commutateur DIP sur la position ON et mettez sous tension. La voiture intelligente avancera et évitera automatiquement les obstacles.

![](./media/img-20240117093950.png)