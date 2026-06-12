### Projet 16 : Télécommande Bluetooth

![](./media/image-20250709134858245.png)

#### **(1) Description :**

Au cours des dernières décennies, le Bluetooth est devenu le module de communication sans fil le plus populaire car il est facile à utiliser et a trouvé de nombreuses applications dans la plupart des appareils alimentés par batterie.

Afin de s'adapter à l'époque, à la réalité et aux besoins des clients, le Bluetooth a été mis à niveau plusieurs fois. Ces dernières années, il a connu de nombreuses transformations en termes de débit de transfert de données, de consommation d'énergie des appareils portables et des appareils IoT, de systèmes de sécurité et autres. Ici, nous prévoyons d'étudier le DX-BT24 avec la carte Arduino.

#### **(2) Paramètres :**

- Protocole Bluetooth : Bluetooth Specification V5.1 BLE
- Distance de fonctionnement : Dans un environnement ouvert, atteint une distance ultra-longue de 40 m
- Fréquence de fonctionnement de communication : bande ISM 2,4 GHz
- Interface de communication : UART
- Certification Bluetooth : conforme aux normes de certification FCC CE ROHS REACH
- Paramètres du port série : 9600, 8 bits de données, 1 bit d'arrêt, bit non valide, pas de contrôle de flux
- Alimentation : 5 V DC
- Température de fonctionnement : –10 à +65 degrés Celsius


#### **(3) Application :**

Le module DX-BT24 prend également en charge le protocole BT5.1 BLE, qui peut être directement connecté aux appareils iOS dotés de la fonction Bluetooth BLE, et prend en charge l'exécution en arrière-plan des programmes résidents. Principalement utilisé dans le domaine de la transmission de données sans fil à courte distance. Évite les connexions câblées encombrantes et peut remplacer directement les câbles série. Domaines d'application réussis des modules BT24 :

※ Transmission de données sans fil Bluetooth ;

※ Téléphone mobile, équipements périphériques informatiques ;

※ Équipement POS portable ;

※ Transmission de données sans fil d'équipements médicaux ;

※ Contrôle de maison intelligente ;

※ Imprimante Bluetooth ;

※ Jouets télécommandés Bluetooth ;

※ Vélos partagés ;

#### **(4) Description des broches :**

![](media/cd97cf79ff5cdd5bbd78f4cc960d38e5.png)

①STATE : broche d'état

②RX : broche de réception

③TX : broche d'émission

④GND : mise à la terre

⑤VCC : broche d'alimentation

⑥EN : broche d'activation

Connecter le Bluetooth à la carte de développement

| Uno  | BT24 |
| :--: | :--: |
|  TX  |  RX  |
|  RX  |  TX  |
| VCC  |  5V  |
| GND  | GND  |

#### **(5) Schéma de connexion :**

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)

#### **(6) Téléchargement de l'APP :**

##### **Pour le système iOS**

1\. Ouvrir l'App Store.

2\. Rechercher <span style="color: rgb(61, 167, 66);">KeyesRobot</span> dans l'Apple Store et cliquer sur télécharger.

![](./media/img-20240111141301.png)

3\. Une fois l'application installée, vous verrez l'icône suivante sur le bureau de votre téléphone.

![](./media/img-20240111141412.png)

**Comment connecter un téléphone iOS au module Bluetooth :**

1\. Activer le Bluetooth et les services de localisation sur le téléphone via les paramètres.

![](./media/img-20240111141943.png)

2\. Autoriser l'application KeyesRobot à accéder au Bluetooth via les paramètres.

![](./media/img-20240111142052.png)

3\. Cliquer pour ouvrir l'application KeyesRobot.

![](./media/img-20240111142140.png)

4\. L'application KeyesRobot est une APP universelle, applicable à plusieurs robots keyestudio. Si l'interface n'affiche pas "TANK ROBOT", vous pouvez cliquer sur les boutons gauche et droit pour trouver "TANK ROBOT".

5\. Cliquer sur le <span style="color: rgb(61, 167, 66);">bouton Bluetooth</span>![](./media/img-20240111142336.png) dans le coin supérieur droit pour scanner le Bluetooth

![](./media/img-20240111142415.png)

6\. Vous verrez un Bluetooth nommé <span style="color: rgb(0, 209, 0);">**BT24**</span>, cliquer sur le bouton <span style="color: rgb(255, 169, 0);">Connecter</span>.

![](./media/img-20240111142536.png)

7\. Si la LED embarquée du module Bluetooth cesse de clignoter et reste allumée, cela signifie que votre téléphone est connecté avec succès au module Bluetooth.

![](./media/img-20240111142702.png)


##### **Pour le système Android**

1\. Rechercher <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> sur Google Play, ou ouvrir le lien suivant pour télécharger et installer l'application.

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Activer le Bluetooth et les services de localisation du téléphone mobile

![](./media/img-20240111143354.png)

3\. Trouver l'application Bluetooth KeyesRobot dans les paramètres, cliquer sur les options d'autorisation de l'application, et
activer les autorisations de localisation et d'appareils à proximité. (<span style="color: rgb(255, 76, 65);">Remarque :</span> Certains téléphones mobiles ne disposent pas de la fonction d'autorisation des appareils à proximité.)

![](./media/img-20240111143451.png)

4\. Cliquer pour ouvrir l'application KeyesRobot.

![](./media/img-20240111143529.png)

5\. L'application KeyesRobot est une APP universelle, applicable à plusieurs robots keyestudio. Si l'interface n'affiche pas "TANK ROBOT", vous pouvez cliquer sur les boutons gauche et droit pour trouver "TANK ROBOT".

6\. Cliquer sur le <span style="color: rgb(61, 167, 66);">bouton Bluetooth</span>![](./media/img-20240111142336.png) dans le coin supérieur droit pour scanner le Bluetooth

![](./media/img-20240111142415.png)

7\. Vous verrez un Bluetooth nommé <span style="color: rgb(0, 209, 0);">**BT24**</span>, cliquer sur le bouton <span style="color: rgb(255, 169, 0);">Connecter</span>.![](./media/img-20240111143910.png)

8\. Lorsque votre téléphone est connecté avec succès au module Bluetooth, la LED embarquée du module Bluetooth cessera de clignoter et restera allumée.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(7) Code de test BT :**

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/19a90ffb7565966f7d40462abed876a7.png)

（5）![](media/c8228c5040a43ae322612b312c995ac3.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et des conflits avec la communication série Bluetooth peuvent survenir, ce qui peut entraîner l'échec du téléversement.)

![](media/4766ada3bf48bb35522f292d9352bb78.png)


Téléverser le code sur la carte de développement, puis brancher le module Bluetooth, puis connecter le téléphone mobile au module Bluetooth.

Une fois le téléphone mobile connecté avec succès au module Bluetooth, cliquer pour ouvrir l'application Bluetooth et cliquer sur le bouton <span style="color: rgb(0, 252, 255);">Sélectionner</span> sur la <span style="color: rgb(0, 252, 255);">page d'accueil</span>.

![](./media/img-20240111144744.png)

L'interface principale de l'application Bluetooth est illustrée dans la figure ci-dessous.

![](./media/img-20240111144859.png)

Cliquer sur ![Img](./media/img-20240111171312.png) et régler le débit en bauds sur 9600. Cliquer sur l'icône dans l'interface de l'APP et le moniteur série affichera la commande envoyée par le bouton.

![](media/f5004f5334fb4885ac0096f99e4133f9.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Remarque : La méthode de connexion de l'APP est identique à celle décrite ci-dessous.**</span>
<br>
<br>


#### **(8) Pratique d'extension :**

Dans le projet ci-dessus, le Bluetooth reçoit le signal envoyé par le téléphone mobile et l'affiche sur le port série de la carte de développement. Ici, nous utilisons la commande envoyée par le téléphone mobile pour allumer ou éteindre une LED. En regardant le schéma de câblage, une LED est connectée à la broche D9,

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)


Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/aa78663af261ff1d9bc8ffa6ad7a65bc.png)

(5）![](media/c8228c5040a43ae322612b312c995ac3.png)

（6）![](media/4164bcf66d3d2415f43a0efcd1ce4243.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et des conflits avec la communication série Bluetooth peuvent survenir, ce qui peut entraîner l'échec du téléversement.)

![](media/91fd9d6f85e291fe90a63e5095ed7f44.png)

Une fois le code ci-dessus téléversé avec succès. Cliquer sur ![](media/d5e59839bafc63f8b35c78c60573d1fc.png) pour contrôler la LED.

![](./media/img-20240117094418.png)


Une fois le projet BT terminé, le retirer.