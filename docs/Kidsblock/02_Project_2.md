### Projet 2 : Régler la luminosité de la LED

#### **(1)Description :**

Dans la leçon précédente, nous avons contrôlé l'allumage et l'extinction de la LED pour la faire clignoter.

Dans ce projet, nous allons contrôler la luminosité de la LED via PWM en simulant un effet de respiration. De même, vous pouvez modifier la longueur du pas et le temps de délai dans le code afin de démontrer différents effets de respiration.

Le PWM est un moyen de contrôler la sortie analogique par des moyens numériques. Le contrôle numérique est utilisé pour générer des ondes carrées avec différents rapports cycliques (un signal qui bascule constamment entre des niveaux haut et bas) pour contrôler la sortie analogique.

En général, les tensions d'entrée des ports sont de 0V et 5V. Que faire si 3V est requis ? Ou une commutation entre 1V, 3V et 3,5V ? Nous ne pouvons pas changer les résistances en permanence. Pour cette raison, nous recourons au PWM.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Pour les sorties de tension des ports numériques Arduino, il n'y a que des niveaux BAS et HAUT, qui correspondent respectivement aux sorties de tension de 0V et 5V. Vous pouvez définir BAS comme « 0 » et HAUT comme « 1 », et laisser l'Arduino sortir cinq cents « 0 » ou « 1 » en 1 seconde. Si l'on sort cinq cents « 1 », cela correspond à 5V ; si tout est « 0 », cela correspond à 0V ; si l'on sort 250 motifs 01, cela correspond à 2,5V.

Ce processus peut être comparé à la projection d'un film. Les films que nous regardons ne sont pas complètement continus. En réalité, il génère 25 images par seconde, ce que l'œil humain ne peut pas distinguer. Par conséquent, nous le percevons comme un processus continu. Le PWM fonctionne de la même manière. Pour produire différentes tensions, nous devons contrôler le rapport entre 0 et 1. Plus on sort de « 0 » ou de « 1 » par unité de temps, plus le contrôle est précis.

#### **(2)Paramètres :**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Interface de contrôle : Port numérique 3

- Tension de fonctionnement : DC 3,3-5V

- Espacement des broches : 2,54mm

- Couleur d'affichage de la LED : jaune

#### **(3)Schéma de câblage**

Les broches PWM de l'Arduino sont connectées aux broches 3, 5, 6, 9, 10 et 11. Gardez la broche 9 inchangée.

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4)Code de test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous

![](media/de8ccd3cb6621f0eb89a8514a9fd8452.png)

![](media/659b8a45b8e8d271226d9a25034aedfd.png)

![](media/3157917e305c01f1920cf4d06aff4ff9.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/aaab53a06684ab078936ee61f9abcbb3.png)


#### **(5)Résultats du test**

Après avoir téléversé le code de test avec succès, la LED change progressivement du brillant à l'obscur, comme la respiration humaine, plutôt que de s'allumer et de s'éteindre immédiatement.

#### **(6)Pratique d'extension :**


Modifions la valeur du délai tout en gardant la broche inchangée, puis observons comment la LED change.

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/2ff0d71c2688d39695b760a1d0f76965.png)

Téléversez le code sur la carte de développement, la LED clignote plus lentement.