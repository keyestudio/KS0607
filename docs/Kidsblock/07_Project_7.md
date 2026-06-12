### Projet 7 : Réception infrarouge

#### **(1) Description :**

![](./media/image-20250709133757050.png)

Il va sans dire que la télécommande infrarouge est omniprésente dans la vie quotidienne. Elle est utilisée pour contrôler divers appareils électroménagers, tels que les téléviseurs, les chaînes stéréo, les magnétoscopes et les récepteurs de signal satellite. La télécommande infrarouge est composée d'un système d'émission infrarouge et d'un système de réception infrarouge, c'est-à-dire une télécommande infrarouge, un module de réception infrarouge et un microcontrôleur capable de décoder.

Le signal porteur infrarouge 38K émis par la télécommande est encodé par la puce d'encodage dans la télécommande. Il est composé d'une section de code pilote, d'un code utilisateur, d'un code utilisateur inverse, d'un code de données et d'un code de données inverse. L'intervalle de temps des impulsions est utilisé pour distinguer s'il s'agit d'un signal 0 ou 1, et le codage est composé de ces signaux 0 et 1.

Le code utilisateur de la même télécommande reste inchangé, tandis que le code de données permet de distinguer la touche.

Lorsque le bouton de la télécommande est pressé, celle-ci envoie un signal porteur infrarouge. Lorsque le récepteur IR reçoit le signal, le programme décode le signal porteur et détermine quelle touche est pressée. Le MCU décode le signal 01 reçu, déterminant ainsi quelle touche de la télécommande est pressée.

![](media/5ad0f889b39646ecb13664511479efc8.png)

Le récepteur infrarouge que nous utilisons est un module récepteur infrarouge. Principalement composé d'une tête réceptrice infrarouge, qui est un dispositif intégrant la réception, l'amplification et la démodulation. Son circuit intégré interne a effectué la démodulation et peut réaliser la réception infrarouge jusqu'à la sortie, compatible avec les signaux TTL. De plus, il est adapté à la télécommande infrarouge et à la transmission de données infrarouge. Le module de réception infrarouge fabriqué par le récepteur ne possède que trois broches : la ligne de signal, VCC et GND. Il est très pratique pour communiquer avec Arduino et d'autres microcontrôleurs.

#### **(2) Paramètres :**

- Tension de fonctionnement : 3,3-5V (DC)
- Interface : 3 broches
- Signal de sortie : Signal numérique
- Angle de réception : 90 degrés
- Fréquence : 38 kHz
- Distance de réception : 10 m

Récepteur infrarouge intégré sur la carte de commande moteur :

![](./media/image-20250709133832650.png)

<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Étant donné que le récepteur IR est intégré dans la carte d'extension de commande moteur Keyestudio 8833, aucun câblage supplémentaire n'est requis. Les broches du récepteur IR sur la carte d'extension de commande moteur Keyestudio 8833 sont G (GND), V (VCC) et D3.

#### **(4) Code de test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous

![](media/cfe0841bcc9404c29519ed623195ca6a.png)

![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

![](media/5a48421831518ea8e0c00be83cf4edf4.png)

![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/90978855cddd94c161f9ed02f85b0674.png)

#### **(5) Résultats du test :**

Téléversez le code sur la carte de développement et réglez le débit en bauds sur 9600. Sortez la télécommande, dirigez-la vers le capteur de réception infrarouge et appuyez sur un bouton pour envoyer le signal. Vous verrez la valeur de touche correspondante. Si la touche est maintenue enfoncée trop longtemps, un caractère parasite « FFFFFFFF » peut facilement apparaître.

![](media/5c01c594a5a11511cf52466eb5f27e45.png)

Ci-dessous, nous avons listé chaque valeur de touche de la télécommande Keyestudio. Vous pouvez la conserver comme référence.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

#### **(6) Pratique avancée :**

Nous venons de décoder les valeurs des touches de la télécommande IR. Maintenant, utilisons-les pour contrôler l'allumage et l'extinction d'une LED. Nous devons connecter un module LED à la broche D9, tandis que la position de la broche du récepteur infrarouge reste inchangée. Lorsque le bouton OK de la télécommande est pressé, la LED connectée à D9 s'allume, et lorsque le bouton OK est pressé à nouveau, la LED s'éteint.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)


Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous

（1）![](media/cfe0841bcc9404c29519ed623195ca6a.png)

（2）![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

（3）![](media/ba67c48d67b1c9753fca82964c9dddc7.png)

(4) ![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

（5）![](media/f8b75df8ccea3efe1cd3ea383b0f88f2.png)

（6）![](media/7406d60c93cdba0b13ded27cba718ec7.png)

（7）![](media/d7be3fa06a1456d46472fffd61823c73.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/57149c79243ff22aa00ff2c54dd4f70b.png)

Téléversez le code sur la carte de développement et appuyez sur la touche « OK » de la télécommande pour allumer et éteindre la LED.

![](./media/img-20240117092532.png)