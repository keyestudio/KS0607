### Projet 2 : Régler la luminosité de la LED

#### **(1)Description :**

Dans la leçon précédente, nous avons contrôlé l'allumage et l'extinction de la LED et l'avons fait clignoter.

Dans ce projet, nous allons contrôler la luminosité de la LED via PWM en simulant un effet de respiration. De même, vous pouvez modifier la longueur du pas et le temps de délai dans le code afin de démontrer différents effets de respiration.

Le PWM est un moyen de contrôler la sortie analogique par des moyens numériques. Le contrôle numérique est utilisé pour générer des ondes carrées avec différents rapports cycliques (un signal qui bascule constamment entre des niveaux haut et bas) pour contrôler la sortie analogique.

En général, les tensions d'entrée des ports sont 0V et 5V. Que faire si 3V est requis ? Ou une alternance entre 1V, 3V et 3,5V ? Nous ne pouvons pas changer les résistances en permanence. C'est pourquoi nous avons recours au PWM.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Pour les sorties de tension des ports numériques Arduino, il n'existe que des niveaux BAS et HAUT, qui correspondent respectivement aux sorties de tension de 0V et 5V. Vous pouvez définir BAS comme « 0 » et HAUT comme « 1 », et laisser l'Arduino émettre cinq cents « 0 » ou « 1 » en 1 seconde. Si l'on émet cinq cents « 1 », cela correspond à 5V ; si tout est « 0 », cela correspond à 0V ; si l'on émet 250 fois le motif 01, cela correspond à 2,5V.

Ce processus peut être comparé à la projection d'un film. Les films que nous regardons ne sont pas complètement continus. En réalité, ils génèrent 25 images par seconde, ce que l'œil humain ne peut pas distinguer. Nous les confondons donc avec un processus continu. Le PWM fonctionne de la même manière. Pour produire différentes tensions, nous devons contrôler le rapport entre les 0 et les 1. Plus il y a de « 0 » ou de « 1 » émis par unité de temps, plus le contrôle est précis.

#### **(2)Paramètres :**

![](./media/image-20250709104949184.png)

Interface de contrôle : Port numérique 3

Tension de fonctionnement : DC 3,3-5V

Espacement des broches : 2,54mm

Couleur d'affichage de la LED : jaune

#### **(3)Schéma de connexion :**

Les broches PWM de l'Arduino sont connectées aux broches 3, 5, 6, 9, 10 et 11. Laissez la broche 9 inchangée.

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4)Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.1

pwm

http://www.keyestudio.com

*/

int LED = 9; // Définir la broche de la LED comme 9

void setup () 
{
	pinMode(LED, OUTPUT); // Définir la broche de la LED en SORTIE
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED allumée
		delay(5); // délai de 5ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // La LED s'assombrit
		delay(5); // délai de 5ms
	}
}
```

#### **(5)Résultats du test :**

Une fois le code de test téléversé avec succès, la LED passe progressivement du brillant à l'obscur, comme la respiration humaine, plutôt que de s'allumer et de s'éteindre instantanément.

#### **(6)Explication du code :**

Pour répéter certaines instructions, nous pouvons utiliser l'instruction FOR. Le format de l'instruction FOR est présenté ci-dessous :

![图1(1)](media/65da124bdd0ea488291c71c6b879fe95.jpeg)

Séquence de la boucle FOR :

Tour 1 : 1 → 2 → 3 → 4

Tour 2 : 2 → 3 → 4

…

Jusqu'à ce que la condition 2 ne soit plus vérifiée, la boucle « for » se termine.

Après avoir compris cet ordre, revenons au code :

**for (int value = 0; value \< 255; value=value+1){**

**...}**

**for (int value = 255; value \>0; value=value-1){**

**...}**

Les deux instructions « for » font augmenter la valeur de 0 à 255, puis diminuer de 255 à 0, puis augmenter à nouveau jusqu'à 255, ... en boucle infinie.

Il y a une nouvelle fonction dans ce qui suit ----- analogWrite()

Nous savons que le port numérique n'a que deux états : 0 et 1. Alors comment envoyer une valeur analogique vers une valeur numérique ? C'est ici que cette fonction est nécessaire. Observons la carte Arduino et repérons les 6 broches marquées « \~ » qui peuvent émettre des signaux PWM.

Le format de la fonction est le suivant :

**analogWrite(pin,value)**

analogWrite() est utilisée pour écrire une valeur analogique de 0\~255 pour un port PWM, donc la valeur est dans la plage 0\~255. Notez que vous ne pouvez écrire que sur les broches numériques ayant la fonction PWM, telles que les broches 3, 5, 6, 9, 10, 11.

Le PWM est une technologie permettant d'obtenir une quantité analogique par une méthode numérique. Le contrôle numérique forme une onde carrée, et le signal d'onde carrée n'a que deux états : allumé et éteint (c'est-à-dire des niveaux haut ou bas). En contrôlant le rapport de la durée d'allumage et d'extinction, une tension variant de 0 à 5V peut être simulée. La durée d'allumage (académiquement appelée niveau haut) est appelée largeur d'impulsion, c'est pourquoi le PWM est également appelé modulation de largeur d'impulsion.

À travers les cinq ondes carrées suivantes, approfondissons notre compréhension du PWM.

![](media/553f3d1b6ca04e1aa0479841dd075fa2.png)

Dans la figure ci-dessus, la ligne verte représente une période, et la valeur de analogWrite() correspond à un pourcentage appelé rapport cyclique.

Le rapport cyclique indique que la durée du niveau haut est divisée par la durée du niveau bas dans un cycle. De haut en bas, le rapport cyclique de la première onde carrée est 0% et sa valeur correspondante est 0. La luminosité de la LED est la plus faible, c'est-à-dire éteinte. Plus le niveau haut dure longtemps, plus la LED est lumineuse. Par conséquent, le dernier rapport cyclique est 100%, ce qui correspond à 255, et la LED est la plus lumineuse. Et 25% signifie plus sombre.

Le PWM est principalement utilisé pour régler la luminosité des LED ou la vitesse de rotation des moteurs.

Il joue un rôle essentiel dans le contrôle des robots intelligents à roues. Je suis sûr que vous êtes impatient d'apprendre le prochain projet.

#### **(7)Pratique d'extension :**

Modifions la valeur du délai en laissant la broche inchangée, puis observons comment la LED change.

**Code de test**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.2

pwm-slow

http://www.keyestudio.com

*/

int LED = 9; // Définir la broche de la LED comme 9

void setup() 
{
	pinMode(LED, OUTPUT); // Définir la broche de la LED en SORTIE
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED allumée
		delay(30); // délai de 30ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // La LED s'assombrit
		delay (30); // délai de 30ms
	}
}
```

Téléversez le code sur la carte de développement, la LED clignote plus lentement.