### Projet 6 : Capteur Ultrasonique

#### **(1) Description :**

![](media/0180b169a1c3b228394b43df704fac32.png)

Le capteur ultrasonique HC-SR04 utilise le sonar pour déterminer la distance d'un objet, comme le font les chauves-souris. Il offre une excellente détection de distance sans contact, avec une grande précision et des lectures stables, dans un boîtier facile à utiliser. Il est livré complet avec des modules émetteur et récepteur ultrasoniques.

Le HC-SR04 ou le capteur ultrasonique est utilisé dans une large gamme de projets électroniques pour créer des applications de détection d'obstacles et de mesure de distance, ainsi que diverses autres applications. Nous vous proposons ici une méthode simple pour mesurer la distance avec Arduino et le capteur ultrasonique, ainsi que la façon d'utiliser le capteur ultrasonique avec Arduino.

![](./media/image-20250709105712919.png)

#### **(2) Paramètres :**

- Alimentation : +5V DC

- Courant de repos : \<2mA

- Courant de fonctionnement : 15mA

- Angle effectif : \<15°

- Distance de détection : 2cm – 400 cm

- Résolution : 0.3 cm

- Angle de mesure : 30 degrés

- Largeur d'impulsion d'entrée de déclenchement : 10uS


#### **(3) Le principe du capteur ultrasonique :**

Comme le montre l'image ci-dessus, c'est comme deux yeux. L'un est l'extrémité émettrice, l'autre est l'extrémité réceptrice.

Le module ultrasonique émettra les ondes ultrasoniques après le déclenchement d'un signal. Lorsque les ondes ultrasoniques rencontrent l'objet et sont réfléchies en retour, le module produit un signal d'écho, ce qui lui permet de déterminer la distance de l'objet à partir de la différence de temps entre le signal de déclenchement et le signal d'écho.

Le t est le temps que met le signal émis pour rencontrer l'obstacle et revenir. La vitesse de propagation du son dans l'air est d'environ 343m/s, et distance = vitesse * temps. Cependant, l'onde ultrasonique est émise et revient, ce qui représente 2 fois la distance. Par conséquent, il faut diviser par 2 : la distance mesurée par **onde ultrasonique = (vitesse * temps)/2**

1. Méthode d'utilisation et chronogramme du module ultrasonique :

2. Régler le temps de retard de la broche Trig du SR04 à au moins 10μs, ce qui peut le déclencher pour détecter la distance.

3. Après le déclenchement, le module enverra automatiquement huit impulsions ultrasoniques de 40KHz et détectera s'il y a un signal de retour. Cette étape sera effectuée automatiquement par le module.

4. Si le signal revient, la broche Echo produira un niveau haut, et la durée du niveau haut est le temps depuis la transmission de l'onde ultrasonique jusqu'au retour.

![](media/image-20230426172540424.png)

Schéma de circuit du capteur ultrasonique :

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4) Schéma de connexion :**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Remarque :</span> Les broches VCC, Trig, Echo et Gnd du capteur ultrasonique sont respectivement connectées à 5v(V), 12(S), 13(S) et Gnd(G) du shield.

#### **(5) Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.1
Ultrasonic sensor
http://www.keyestudio.com
*/

int trigPin = 12; // La broche Trig est connectée à 12
int echoPin = 13; // La broche Echo est connectée à 13
long duration, cm, inches;

void setup() 
{
    // Démarrage du port série
    Serial.begin(9600);// Définir le débit en bauds à 9600
    // Définir les entrées et sorties
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
}

void loop() 
{
    // Donner une courte impulsion basse au préalable pour assurer une impulsion haute propre
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// Donner au moins 10us de déclenchement par niveau haut
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // Le temps en niveau haut est égal à l'intervalle de temps entre la transmission et le retour du son ultrasonique
    duration = pulseIn(echoPin, HIGH);
    // Conversion en distance
    cm = (duration / 2) / 29.1; // conversion en centimètres
    inches = (duration / 2) / 74; // conversion en pouces
    // Affichage sur le port série
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    delay(50);
}
```

#### **(6) Résultats du test :**

Téléversez le code de test sur la carte de développement, ouvrez le moniteur série et réglez le débit en bauds à 9600. La distance détectée sera affichée en cm et en pouces. Lorsque vous bloquez le capteur ultrasonique avec votre main, la valeur de distance affichée diminuera.

![](media/2ff018e5d9d631a32fce99eb9b4778be.png)

#### **(7) Explication du code :**

**int trigPin = 12;**  cette broche est définie pour transmettre les ondes ultrasoniques, généralement en sortie.

**int echoPin = 13;** celle-ci est définie comme la broche de réception, généralement en entrée

**cm = (duration/2) / 29.1; inches = (duration/2) / 74; par 0.0135**

Nous pouvons calculer la distance en utilisant la formule suivante :

distance = (temps de trajet/2) x vitesse du son

La vitesse du son est : 343m/s = 0.0343 cm/uS = 1/29.1 cm/uS

Ou en pouces : 13503.9in/s = 0.0135in/uS = 1/74in/uS

Nous devons diviser le temps de trajet par 2 car nous devons tenir compte du fait que l'onde a été envoyée, a heurté l'objet, puis est revenue au capteur.

#### **(8) Pratique d'extension :**


Nous venons de mesurer la distance affichée par l'ultrasonique. Que diriez-vous de contrôler une LED avec la distance mesurée ? Essayons et connectons un module de LED à la broche D9.

![](media/291ac1db0f38418772d11bb1786b7314.png)

**Code de test**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.2
Ultrasonic LED
http://www.keyestudio.com
*/

int trigPin = 12; // Trig est connecté à 12
int echoPin = 13; // Echo est connecté à 13
int LED = 9;
long duration, cm, inches;

void setup() 
{
    // démarrage du port série
    Serial.begin (9600);// définir le débit en bauds à 9600
    // définir les entrées et sorties
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(LED, OUTPUT);
}

void loop() 
{
    // Donner une courte impulsion basse au préalable pour assurer une impulsion haute propre
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// Donner au moins 10us de déclenchement par niveau haut
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // La durée du niveau haut est le temps depuis l'émission jusqu'au retour de l'onde ultrasonique
    duration = pulseIn(echoPin, HIGH);
    // conversion en distance
    cm = (duration / 2) / 29.1; // conversion en centimètres
    inches = (duration / 2) / 74; // conversion en pouces
    // Affichage sur le port série
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    if (cm >= 2 && cm <= 10) 
    {
    	digitalWrite(LED, HIGH);// allumer la LED
    } 
    else 
    {
    	digitalWrite(LED, LOW); // éteindre la LED
    }
    delay(50);
}
```

Téléversez le code de test sur la carte de développement et bloquez le capteur ultrasonique avec la main, puis vérifiez si la LED est allumée.

![](./media/img-20240117090734.png)