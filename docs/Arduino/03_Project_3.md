### Projet 3 : Photorésistance

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1) Description :**

La résistance photosensible est une résistance spéciale fabriquée à partir d'un matériau semi-conducteur tel qu'un sulfure ou du sélénium, et une résine imperméable à l'humidité est également appliquée avec un effet photoconduisant. La résistance photosensible est très sensible à la lumière ambiante ; selon l'intensité lumineuse, la valeur de la résistance photosensible est différente. Nous utilisons la résistance photosensible pour concevoir le module de résistance photosensible.

Le signal du module est connecté au port analogique du microcontrôleur. Lorsque l'intensité lumineuse est plus forte, la tension du port analogique est plus élevée, c'est-à-dire que la valeur de simulation du microcontrôleur est également plus grande ; à l'inverse, lorsque l'intensité lumineuse est plus faible, la tension du port analogique est plus basse, c'est-à-dire que la valeur de simulation du microcontrôleur est également plus petite.

De cette façon, nous pouvons lire la valeur analogique correspondante à l'aide du module de résistance photosensible, et ainsi mesurer l'intensité de la lumière dans l'environnement.

![](media/7784e14e15402644cdbe674d500327c4.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2) Paramètres :**

Valeur de résistance de la photorésistance : 5K Ω - 0,5 MΩ

Type d'interface : port de simulation A0, A1

Tension de fonctionnement : 3,3 V - 5 V

Espacement des broches : 2,54 mm


#### **(3) Schéma de connexion :**

Ce que nous allons tester ensuite est le module photorésistance situé sur le côté gauche du robot.

![](./media/img-20240117091559.png)

La photorésistance gauche est connectée à A1/P3 du shield de pilotage moteur.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)

#### **(4) Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut créer des conflits avec la communication série Bluetooth et provoquer l'échec du téléversement.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.1

photocell

http://www.keyestudio.com

*/

int sensorPin = A1; // A1 est la broche d'entrée de la photorésistance

int sensorValue = 0; // sauvegarder la valeur de la photorésistance

void setup() 
{
	Serial.begin(9600); // Ouvrir le moniteur du port série et régler le débit en bauds à 9600
}

void loop() 
{
	sensorValue = analogRead(sensorPin); // Lire la valeur analogique du capteur photorésistance
	Serial.println(sensorValue); // Le port série affiche la valeur de la photorésistance
	delay(500); // Délai de 500 ms
}
```

#### **(5) Résultats du test :**

![](media/54b92578e3210999e23f5fb8138f0fa0.png)

En couvrant la photorésistance, la valeur diminue ; sinon, la valeur augmente.

#### **(6) Explication du code :**

**analogRead(sensorPin)** : lit la valeur analogique de la photorésistance

**Serial.begin(9600)** : initialise le port série et règle le débit en bauds à 9600

**Serial.println** : affichage série

#### **(7) Pratique avancée :**

Le code ci-dessus se contente de lire la valeur de la photorésistance. Nous pouvons combiner la photosensibilité et une LED pour modifier la LED. Que diriez-vous de contrôler la luminosité de la LED grâce à elle ?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

La luminosité de la LED est contrôlée par PWM. Par conséquent, nous connectons la LED à la broche PMW (broche 9) du shield.

**Code de test**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut créer des conflits avec la communication série Bluetooth et provoquer l'échec du téléversement.)

```c
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.2

photocell-analog output

http://www.keyestudio.com

*/

int analogInPin = A1; // A1 est la broche d'entrée de la photorésistance

int analogOutPin = 9; // Le port numérique 9 est la sortie du PMW

int sensorValue = 0; // sauvegarder la variable de la valeur de résistance de la photorésistance

int outputValue = 0; // Valeur de sortie vers le PMW

void setup() 
{
	Serial.begin(9600); // Ouvrir le moniteur du port série et régler le débit en bauds à 9600
}

void loop() 
{
    sensorValue = analogRead(analogInPin); // Lire la valeur analogique du capteur photorésistance
    // Mapper les valeurs analogiques 0\~1023 vers les valeurs de sortie PWM 255\~0
    outputValue = map(sensorValue, 0, 1023, 255, 0);
    // Modifier la sortie analogique
    analogWrite(analogOutPin, outputValue);
    Serial.println(sensorValue); // Le port série affiche la valeur de la photorésistance
    delay(2);
}
```

Téléversez le code sur la carte de développement, puis couvrez la photorésistance et observez la luminosité de la LED.

![](./media/img-20240117091105.png)