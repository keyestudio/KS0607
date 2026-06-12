### Projet 15 : Char Télécommandé par Infrarouge

![](./media/image-20250709134800790.png)

#### **(1)Description :**

La télécommande infrarouge est l'une des applications de télécommande les plus courantes que l'on trouve dans les moteurs électriques, les ventilateurs électriques et de nombreux autres appareils électroménagers. Dans ce projet, nous utilisons les connaissances acquises précédemment pour fabriquer une voiture intelligente à télécommande infrarouge.

Dans la 9ème leçon, nous avons testé la valeur de touche correspondante à chaque touche de la télécommande infrarouge. Dans ce projet, nous pouvons définir le code (valeur de touche) pour que le bouton correspondant contrôle les mouvements de la voiture intelligente, et afficher les schémas de mouvement sur la matrice de LED 8X16.

La logique spécifique de la voiture intelligente est présentée dans le tableau ci-dessous :

|                 Touche ultrasonique                  | Valeur de touche | Instructions des touches                                       |
| :---------------------------------------------: | :-------: | ------------------------------------------------------------ |
| ![](media/b11dc5ffa6cccebc6088e5d557d76daf.png) |  FF629D   | Avancer（régler le PWM à 200）<br />afficher le schéma d'avancement |
| ![](media/ae8110034aacb083151cfd882ee599ba.png) |  FFA857   | Reculer（régler le PWM à 200）<br />afficher le schéma de recul |
| ![](media/bce9cba2c6d2465fbcce570ad4210eba.png) |  FF22DD   | Tourner à gauche<br />afficher le schéma"STOP"                     |
| ![](media/ad907a618af86f30d52986bbbd57ba76.png) |  FFC23D   | Tourner à droite<br />afficher le schéma de virage à gauche          |
| ![](media/9716a4ed61a4064d2f47a7b73eccaf87.png) |  FF02FD   | Arrêter<br />afficher le schéma"STOP"                          |

**Réglage initial : la matrice de LED 8X16 affiche le schéma"![](media/dc59c5fcb4fcf6af4d4a5ebb14b7a919.png)"**



#### **(2)Organigramme :**

![](media/wps121.png)

#### **(3)Schéma de connexion :**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Remarque :</span>

GND, VCC, SDA et SCL du panneau LED 8x16 sont connectés à G（GND), V（VCC). A4 et A5 de la carte d'extension.

Étant donné que la carte 8833 intègre le récepteur IR, vous n'avez pas besoin de le câbler. Les broches du récepteur IR sont G（GND), V（VCC) et D3.

#### **(4)Code de test :**

Vous pouvez modifier des blocs pour construire votre code

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/a9042e77ebe3009fbb7653bef3429b66.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6）![](media/51e30aa2aca3a7da67ee4f0f81c7dad1.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/7ab62148fa2a23259b8039475978d8fc.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/fae6c22640ced038daca9cb6721ab95e.png)

#### **(5)Résultats du test :**

Après avoir téléversé le code de test avec succès et mis sous tension, la voiture intelligente peut être contrôlée pour se déplacer par télécommande IR et la matrice 8\*16 affiche les schémas correspondants à ses mouvements.

![](./media/img-20240117094223.png)