### Projet 22 : Robot Extincteur à Fonctions Multiples

#### **(1)Description :**

Le véhicule intelligent n'a exécuté qu'une seule fonction dans chacun des projets précédents.

Peut-il afficher plusieurs fonctions à la fois ? Oui, il le peut.

Dans ce grand projet final, nous avons l'intention d'utiliser un code complet pour contrôler le véhicule intelligent afin de démontrer toutes les fonctions mentionnées dans les projets précédents. Nous utilisons les touches de l'application Bluetooth pour basculer automatiquement entre les différentes fonctions, ce qui est assez simple et pratique.

#### **(2)Diagramme de flux :**

<span style="color: rgb(255, 76, 65);">**Veuillez vous référer au Projet 16 pour installer et configurer l'application Bluetooth**</span>

![](media/wps122.png)

#### **(3)Schéma de connexion :**

![](media/e7ac834ba04aa2e8862995d2d33ce935.png)

1\. GND, VCC, SDA et SCL de la carte 8x16 sont connectés à G (GND), + (VCC), A4 et A5 de la carte d'extension.

2\. VCC, IN+, IN- et Gnd du module ventilateur sont connectés à 5V (V), 12 (S), 13 (S) et Gnd (G).

3\. Le fil marron, le fil rouge et le fil orange du servomoteur sont connectés à Gnd (G), 5v (V) et D10.

4\. RXD, TXD, GND et VCC du module BT sont connectés à TX, RX, G (GND) et 5V (VCC). STATE et BRK n'ont pas besoin d'être interfacés.

5\. Les broches « G », « V » et A du capteur de flamme gauche sont connectées respectivement à G (GND), V (VCC) et A1 ; Le capteur de flamme droit est connecté à G (GND), V (VCC) et A2, respectivement.

6\. Les ports distaux du capteur de suivi de ligne sont 11, 7 et 8.

#### **(4)Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)
<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Vous ne pouvez pas accélérer le véhicule via l'application.

![](media/b1527b806741e28e8f2af5107db505fe.png)


#### **(5)Résultat du test :**

Avant de téléverser le code du programme, le module Bluetooth doit être retiré ; sinon, le téléversement du code échouera.

Après avoir téléversé le code avec succès, activez les services de localisation sur votre appareil, puis connectez le module Bluetooth.

Une fois que le module Bluetooth est branché et sous tension, et que l'application mobile est connectée avec succès au Bluetooth, nous pouvons utiliser l'application mobile pour contrôler le robot tank.

![](media/13656cfee75dc5acbeba18a90a084e159.jpg)