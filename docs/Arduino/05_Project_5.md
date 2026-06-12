### Projet 5 : Contrôle du Servomoteur

#### **(1)Description :**

Un servomoteur est un actionneur rotatif de contrôle de position. Il se compose principalement d'un boîtier, d'une carte de circuit, d'un moteur sans noyau, d'un engrenage et d'un capteur de position. Son principe de fonctionnement est que le servo reçoit le signal envoyé par le MCU ou le récepteur et produit un signal de référence avec une période de 20ms et une largeur de 1,5ms. Il compare ensuite la tension de polarisation CC acquise à la tension du potentiomètre et obtient la sortie de différence de tension.

Lorsque la vitesse du moteur est constante, le potentiomètre est entraîné en rotation par l'engrenage de réduction en cascade, ce qui conduit à une différence de tension nulle, et le moteur s'arrête de tourner. En général, la plage d'angle de rotation du servo est de 0° à 180°.

L'angle de rotation du servomoteur est contrôlé en régulant le rapport cyclique du signal PWM (Modulation de Largeur d'Impulsion). La période standard du signal PWM est de 20ms (50Hz). Théoriquement, la largeur est distribuée entre 1ms et 2ms, mais en pratique, elle est entre 0,5ms et 2,5ms. La largeur correspond à l'angle de rotation de 0° à 180°. Notez que pour différentes marques de moteurs, le même signal peut produire des angles de rotation différents.

![](media/69be958142b773acdae33eeef12afed7.png)

En général, le servo possède trois fils de couleur marron, rouge et orange. Le fil marron est la masse, le rouge est le fil du pôle positif et l'orange est le fil de signal.

![](media/49467dfa70799401a5a5acc691014aee.png)

L'angle du servo :

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Paramètres :**

- Tension de fonctionnement : DC 4,8V \~ 6V

- Plage d'angle de fonctionnement : environ 180° (à 500 → 2500 μsec)

- Plage de largeur d'impulsion : 500 → 2500 μsec

- Vitesse à vide : 0,12 ± 0,01 sec / 60 (DC 4,8V) 0,1 ± 0,01 sec / 60 (DC 6V)

- Courant à vide : 200 ± 20mA (DC 4,8V) 220 ± 20mA (DC 6V)

- Couple d'arrêt : 1,3 ± 0,01kg · cm (DC 4,8V) 1,5 ± 0,1kg · cm (DC 6V)

- Courant d'arrêt : ≦ 850mA (DC 4,8V) ≦ 1000mA (DC 6V)

- Courant en veille : 3 ± 1mA (DC 4,8V) 4 ± 1mA (DC 6V)

#### **(3)Schéma de Connexion :**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">Remarque :</span> Les fils marron, rouge et orange du servo sont respectivement connectés à Gnd(G), 5v(V) et 10 du shield. N'oubliez pas de connecter une alimentation externe en raison du courant élevé du servo. Sinon, la carte de développement sera brûlée.

#### **(4)Code de Test 1 :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut provoquer l'échec du téléversement.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.1
Servo
http://www.keyestudio.com
*/

#define servoPin 10 // La broche du servo

int pos; // La variable de l'angle du servo
int pulsewidth; // La variable de la largeur d'impulsion du servo

void setup() 
{
    pinMode(servoPin, OUTPUT); // Définir la broche du servo comme sortie
    procedure(0); // Définir l'angle du servo à 0°
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  // De 1° à 180°
    {
    	// par pas de 1 degré	
        procedure(pos); // Tourner à l'angle 'pos'
        delay(15); // Contrôler la vitesse de rotation
    }
    for (pos = 180; pos >= 0; pos -= 1) // De 180° à 1°
    { 
        procedure(pos); // Tourner à l'angle 'pos'
        delay(15);
    }
}
// La fonction contrôle le servo
void procedure(int myangle) 
{
    pulsewidth = myangle * 11 + 500; // Calculer la valeur de la largeur d'impulsion
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth); // Le temps en niveau haut représente la largeur d'impulsion
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000)); // Comme le cycle est de 20ms, le temps restant est en niveau bas
}
```

Après le téléversement du code, nous verrons le servo se déplacer de 0° à 180°. Dans les chapitres suivants, nous présenterons comment piloter un servo. De plus, nous pouvons contrôler un servo avec une bibliothèque servo d'Arduino.

<span style="color: rgb(255, 76, 65);">Remarque :</span> Ce fichier de bibliothèque servo utilise le timer 1, et la sortie PWM des ports IO 9 et 10 utilise également le timer 1, donc nous ne pouvons pas utiliser cette bibliothèque servo lors de l'utilisation de la sortie PWM de D9 et D10 ultérieurement.

#### **(5)Code de Test 2 :**

(<span style="color: rgb(255, 76, 65);">Remarque : </span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut provoquer l'échec du téléversement du code.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.2
Servo
<http://www.keyestudio.com>
*/

#include <Servo.h>

Servo myservo; // créer des servos
int pos = 0; // Sauvegarder les variables d'angle

void setup() 
{
	myservo.attach(10); // Connecter le servo au port numérique 10
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  // De 0° à 180°
    {
    	// la longueur du pas est de 1
        myservo.write(pos); // Tourner à l'angle 'pos'
        delay(15); // Attendre 15ms pour contrôler la vitesse
    }

    for (pos = 180; pos >= 0; pos -= 1)  // De 180° à 0°
    {
        myservo.write(pos); // Tourner à l'angle 'pos'
        delay(15); // Attendre 15ms pour contrôler la vitesse
    }
}
```

#### **(6)Résultats des Tests :**

Téléversez le code, branchez l'alimentation et le servo se déplace dans la plage de 0° à 180°.

![](./media/img-20240117090810.png)

#### **(7)Explication du Code :**

Arduino est livré avec **\#include \<Servo.h\>** (fonction servo et instructions)

Voici quelques instructions courantes de la fonction servo :

1\. **attach（interface）**——Définir l'interface du servo, les ports 9 et 10 sont disponibles

2\. **write（angle）**——L'instruction pour définir l'angle de rotation du servo, la plage d'angle est de 0° à 180°

3\. **read（）**——L'instruction pour lire l'angle du servo, lit la valeur de commande de "write()"

4\. **attached（）**——Vérifier si le paramètre du servo est envoyé à son interface

Remarque : Le format d'écriture ci-dessus est "nom de variable du servo, instruction spécifique（）", par exemple : myservo.attach(10)