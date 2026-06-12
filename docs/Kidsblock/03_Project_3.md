### Projet 3 : Photorésistance

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Description :**

La résistance photosensible est une résistance spéciale fabriquée à partir d'un matériau semiconducteur tel qu'un sulfure ou du sélénium, et une résine imperméable à l'humidité est également appliquée avec un effet photoconducteur. La résistance photosensible est très sensible à la lumière ambiante ; selon l'intensité lumineuse, la résistance de la photorésistance varie. Nous utilisons la résistance photosensible pour concevoir le module de résistance photosensible.

Le signal du module est connecté au port analogique du microcontrôleur. Lorsque l'intensité lumineuse est plus forte, la tension du port analogique est plus élevée, c'est-à-dire que la valeur de simulation du microcontrôleur est également plus grande ; à l'inverse, lorsque l'intensité lumineuse est plus faible, la tension du port analogique est plus basse, c'est-à-dire que la valeur de simulation du microcontrôleur est également plus petite.

Ainsi, nous pouvons lire la valeur analogique correspondante à l'aide du module de résistance photosensible, et mesurer l'intensité de la lumière dans l'environnement.

![](./media/image-20250709122809574.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Paramètres :**

- Valeur de résistance de la résistance photosensible : 5K Ω - 0,5 MΩ

- Type d'interface : port de simulation A0, A1

- Tension de fonctionnement : 3,3V - 5V

- Espacement des broches : 2,54mm

#### **(3)Schéma de connexion :**

Ce que nous allons tester ensuite est le module de photorésistance situé sur le côté gauche du robot.

![](./media/img-20240117091730.png)

La photorésistance gauche est connectée à A1/P3 du bouclier de commande moteur.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)


#### **(4)Code de test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut entraîner des conflits avec la communication série Bluetooth et provoquer un échec du téléversement.)

![](media/f29c7da2238bcc2bc70cb4b2c773b50d.png)

#### **(5)Résultats du test :**

Téléversez le code sur la carte de développement. Cliquez sur ![](media/9011f20d83897d7a5936793c4ae142fc.png) pour régler le débit en bauds à 9600. Lorsque vous la couvrez avec votre main, la valeur diminue ; sinon, la valeur augmente.

![](media/53e2fc37ee5bb2c6ec187c309c431c47.png)



#### **(6)Pratique d'extension :**

Le code ci-dessus lit simplement la valeur de la photorésistance. Nous pouvons combiner le capteur photosensible et une LED pour modifier la LED. Que diriez-vous de contrôler la luminosité de la LED grâce à elle ?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

Le PWM peut modifier la luminosité de la LED, c'est-à-dire que la LED doit être connectée au PWM de la carte de développement.

Connectez la LED à D9 et laissez les autres broches inchangées, puis éditez le code.

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/b94c3789429c5fed4fd38467cb9792dd.png)

![](media/9ecdfd77e2a69dea5a8df04e7d56a13a.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut entraîner des conflits avec la communication série Bluetooth et provoquer un échec du téléversement.)

![](media/b23bcae806e8e27382b162909d30f3c0.png)

Téléversez le code sur la carte de développement, puis appuyez sur la photorésistance pour observer si la luminosité de la LED a changé.

![](./media/img-20240117091759.png)