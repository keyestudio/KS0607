### Projet 13 : Char se déplaçant dans un espace confiné


#### **(1)Description :**

Les fonctions de suivi par ultrasons et d'évitement d'obstacles du véhicule intelligent ont été présentées dans les projets précédents. Ici, nous avons l'intention de combiner les connaissances des cours précédents pour confiner le véhicule intelligent à se déplacer dans un certain espace. Dans l'expérience, nous utilisons le capteur de suivi de ligne pour détecter s'il y a une ligne noire autour du véhicule intelligent, puis nous contrôlons la rotation des deux moteurs en fonction des résultats de détection, afin de confiner le véhicule intelligent dans un cercle tracé avec une ligne noire.

La logique spécifique du véhicule intelligent est présentée dans le tableau ci-dessous :

![](media/image-20230525114604923.png)

|                         Condition                         |                         Mouvement                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Si l'un des trois capteurs de suivi de ligne détecte des lignes noires | Reculer（régler le PWM à 150）Puis tourner à gauche（régler le PWM à 150） |
|             Aucun d'eux ne détecte de lignes noires              |               Avancer（régler le PWM à 100）                |

#### **(2)Organigramme**

![](media/b3c30f92cb78d4c2a4a8bd746aef24e1.png)

#### **(3)Schéma de connexion :**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Code de test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/e48288f5b46e3e1c78489cb9d9b86333.png)

（3）![](media/801d176b32bc87904b8545ecf80874fc.png)

（4）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/b919eb2b47ee87ae36e21099e754e8a1.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/e656126c11bb8ebe7b6b0df8f22e7a79.png)

#### **(5)Résultats du test :**

Après avoir téléversé le code de test avec succès et mis sous tension, le véhicule intelligent se déplace dans un cercle tracé avec une ligne noire.

![](./media/img-20240117094034.png)