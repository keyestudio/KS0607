### Projet 17 : Contrôle du Tank par Bluetooth

#### **(1) Description :**

Nous avons appris les connaissances de base du Bluetooth dans le projet précédent. Dans cette leçon, nous allons utiliser le Bluetooth pour contrôler la voiture intelligente. Puisque cela implique le Bluetooth, un émetteur et un récepteur sont nécessaires. Dans le projet, nous utilisons le téléphone mobile comme émetteur (maître), et la voiture intelligente connectée au module Bluetooth HM-10 (esclave) comme récepteur.

Nous avons appris précédemment qu'envoyer un bit peut contrôler des LEDs. Le principe de contrôle de ce robot roulant est le même.

Afin de mieux contrôler le robot tank intelligent, nous avons spécialement créé une APP. Dans cette leçon, nous allons lire toutes les valeurs des touches de cette APP via le code, puis présenter l'APP exclusive de notre robot tank.

#### **(2) Fonctions des Touches de l'APP :**

Le tableau suivant illustre les fonctions des touches correspondantes :

|                      Touches                       |                                                |                          Fonctions                           |
| :---------------------------------------------: | :--------------------------------------------: | :----------------------------------------------------------: |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) |                                                | Associer et connecter le module Bluetooth HM-10 ; cliquer à nouveau pour déconnecter |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) |                                                |                 Sélectionner le robot à utiliser                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) |                                                |       Contrôler les mouvements du robot par boutons       |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) |                                                |      Contrôler les mouvements du robot par joystick       |
| ![](media/3ab61154b4ae730a3757f40171846825.png) |                                                |       Contrôler les mouvements du robot par gravité       |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) |   Envoie "F" quand appuyé et "S" quand relâché    | La voiture avance quand appuyé et s'arrête quand relâché |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) |   Envoie "L" quand appuyé et "S" quand relâché    | La voiture tourne à gauche quand appuyé et s'arrête quand relâché |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) |   Envoie "R" quand appuyé et "S" quand relâché    | La voiture tourne à droite quand appuyé et s'arrête quand relâché |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) |   Envoie "B" quand appuyé et "S" quand relâché    | La voiture recule quand appuyé et s'arrête quand relâché |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) |        Envoie "u"+chiffre+"\#" quand glissé         |          Glisser pour changer la vitesse du moteur gauche          |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) |        Envoie "v"+chiffre+"\#" quand glissé         |         Glisser pour changer la vitesse du moteur droit          |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) |         Sélectionner pour accéder à la page Fonction          |                                                              |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Envoie "G" quand appuyé et "S" quand appuyé à nouveau | Entrer en mode évitement d'obstacles quand appuyé et quitter quand appuyé à nouveau |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Envoie "h" quand appuyé et "S" quand appuyé à nouveau | Entrer en mode suivi quand appuyé et quitter quand appuyé à nouveau |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Envoie "e" quand appuyé et "S" quand appuyé à nouveau | Entrer en mode suivi de ligne quand appuyé et quitter quand appuyé à nouveau |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Envoie "f" quand appuyé et "S" quand appuyé à nouveau | Entrer en mode déplacement dans un espace confiné quand appuyé et quitter quand appuyé à nouveau |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Envoie "i" quand appuyé et "S" quand appuyé à nouveau | Entrer en mode suivi de lumière quand appuyé et quitter quand appuyé à nouveau |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Envoie "j" quand appuyé et "S" quand appuyé à nouveau | Entrer en mode extinction d'incendie quand appuyé et quitter quand appuyé à nouveau |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Sélectionner pour entrer en mode affichage d'expressions faciales |                                                              |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Envoie "k" quand appuyé et "z" quand appuyé à nouveau | Affiche un motif souriant quand cliqué et efface l'expression quand cliqué à nouveau |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Envoie "l" quand appuyé et "z" quand appuyé à nouveau | Affiche un motif dégoûté quand cliqué et efface l'expression quand cliqué à nouveau |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Envoie "m" quand appuyé et "z" quand appuyé à nouveau | Affiche un visage heureux quand cliqué et efface l'expression quand cliqué à nouveau |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Envoie "n" quand appuyé et "z" quand appuyé à nouveau | Affiche un motif triste quand cliqué et efface l'expression quand cliqué à nouveau |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Envoie "o" quand appuyé et "z" quand appuyé à nouveau | Affiche un motif méprisant quand cliqué et efface l'expression quand cliqué à nouveau |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Envoie "p" quand appuyé et "z" quand appuyé à nouveau | Affiche un motif en forme de cœur quand cliqué et efface l'expression quand cliqué à nouveau |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) |                                                | Choisir d'entrer dans l'interface de fonctions personnalisées ; il y a six touches 1, 2, 3, 4, 5, 6 ; avec ces touches, vous pouvez étendre certaines fonctions par vous-même |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) |               Cliquer pour envoyer "w"                | Cliquer pour afficher la valeur analogique détectée par la photorésistance gauche |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) |                Cliquer pour envoyer "y"                | Cliquer pour afficher la valeur analogique détectée par la photorésistance droite |
| ![](media/a76df707b84409e57a1167889c3510d9.png) |                Cliquer pour envoyer "x"                | Cliquer pour afficher la distance détectée par le capteur à ultrasons (unité : cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Cliquer pour envoyer "c" <br />Cliquer à nouveau pour envoyer "d"  |   Appuyer pour allumer le ventilateur et appuyer à nouveau pour l'éteindre    |

#### **(3) Organigramme :**

![](./media/image-20250709135203165.png)

#### **(4) Schéma de Connexion :**

![](media/930a8024364e07505e845624a94c27bd.png)

<span style="color: rgb(255, 76, 65);">Remarque :</span>

GND, VCC, SDA et SCL du panneau LED 8x16 sont connectés à G（GND), V（5V), A4 et A5 de la carte d'extension. STATE et BRK n'ont pas besoin d'être connectés. Le module BT est inséré dans la carte d'extension.

#### **(5) Code de Test :**

Vous pouvez faire glisser des blocs pour éditer votre code

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/3b4fb768cbf7e0b80fa55cb15aa932b7.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6) ![](media/8a13abc40d27d0470902e528b40170c3.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Code de Test Complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut provoquer des conflits avec la communication série Bluetooth et entraîner l'échec du téléversement.)

![](media/341e0a01bd6a76edb53f9414ef641a75.png)

#### **(6) Résultat du Test :**

Après avoir téléversé le code, connectez le robot au module Bluetooth et associez l'APP Bluetooth. Allumez l'interrupteur d'alimentation du shield de commande des moteurs. Placez le robot sur le sol, vous pouvez utiliser ces boutons de l'APP Bluetooth pour contrôler le robot.

![](media/352d5ec83c4246b980da10b5f99711c5.jpeg)

1. Les flèches haut, bas, gauche et droite contrôlent respectivement le robot pour avancer, reculer, tourner à gauche et tourner à droite.

![](./media/img-20240117095015.png)

2. Cliquez sur le bouton joystick et faites glisser la direction du point noir dans le cercle blanc pour contrôler la direction de déplacement du robot.

![](./media/img-20240117095052.png)

3. Cliquez sur le bouton Gravité et inclinez le téléphone dans les directions avant, arrière, gauche et droite, et le robot se déplacera dans la direction dans laquelle le téléphone est incliné.

![](./media/img-20240117095131.png)