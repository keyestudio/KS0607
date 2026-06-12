### Projet 14 : Tank Suiveur de Ligne


#### **(1) Description :**

Le projet précédent a présenté comment confiner la voiture intelligente pour qu'elle se déplace dans un certain espace. Dans ce projet, nous allons utiliser les connaissances acquises précédemment pour en faire une voiture intelligente suiveur de ligne. Dans l'expérience, nous utilisons le capteur de suivi de ligne pour détecter s'il y a une ligne noire autour de la voiture intelligente, puis nous contrôlons la rotation des deux moteurs en fonction des résultats de détection, afin de faire se déplacer la voiture intelligente le long de la ligne noire.

La logique spécifique de la voiture intelligente est présentée dans le tableau ci-dessous :

|               Capteur               |                          Détection                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Capteur de suivi de ligne au milieu | Ligne noire détectée : niveau haut<br />Ligne blanche détectée : niveau bas |
|  Capteur de suivi de ligne à gauche  | Ligne noire détectée : niveau haut<br />Ligne blanche détectée : niveau bas |
| Capteur de suivi de ligne à droite  | Ligne noire détectée : niveau haut<br />Ligne blanche détectée : niveau bas |

|                         Condition 1                          |                         Condition 2                          |   Mouvement   |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------: |
| Le capteur de suivi de ligne <br />au milieu <br />détecte la ligne noire | Le capteur de suivi de ligne à gauche détecte la ligne noire<br />celui à droite détecte des lignes blanches | Tourner à gauche  |
| Le capteur de suivi de ligne <br />au milieu <br />détecte la ligne noire | Le capteur de suivi de ligne à gauche détecte des lignes blanches<br />celui à droite détecte la ligne noire | Tourner à droite |
| Le capteur de suivi de ligne <br />au milieu <br />détecte la ligne noire | Les capteurs de suivi de ligne gauche et droit détectent tous deux des lignes blanches<br />Les capteurs de suivi de ligne gauche et droit détectent tous deux la ligne noire | Avancer |
| Le capteur de suivi de ligne<br />au milieu <br />détecte des lignes blanches | Le capteur de suivi de ligne à gauche détecte la ligne noire<br />celui à droite détecte des lignes blanches | Tourner à gauche  |
| Le capteur de suivi de ligne<br />au milieu <br />détecte des lignes blanches | Le capteur de suivi de ligne à gauche détecte des lignes blanches<br />celui à droite détecte la ligne noire | Tourner à droite |
| Le capteur de suivi de ligne<br />au milieu <br />détecte des lignes blanches | Les capteurs de suivi de ligne gauche et droit détectent tous deux des lignes blanches<br />Les capteurs de suivi de ligne gauche et droit détectent tous deux la ligne noire |     Arrêt     |

#### **(2) Organigramme :**

![](media/wps11.png)

#### **(3) Schéma de connexion :**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4) Code de test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

（7）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（8）![](media/fec93c7b8b089de709fd50575931519c.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, ce qui peut provoquer des conflits avec la communication série Bluetooth et entraîner l'échec du téléversement.)

![](media/294ae4c01072e34b58a334912c90083a.png)


#### **(5) Résultats du test :**

Après avoir téléversé le code de test avec succès et mis sous tension, la voiture intelligente se déplace le long de la ligne noire.

![](./media/img-20240117094129.png)