### Projet 21 : Ventilateur

#### **(1) Description :**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Ce module ventilateur utilise une puce de contrôle moteur HR1124S, une puce de driver H-bridge à canal unique contenant des tubes de puissance PMOS et NMOS à faible résistance de conductivité. La faible résistance de conduite permet de réduire la consommation d'énergie, contribuant au fonctionnement sécurisé de la puce sur une plus longue durée.

De plus, son faible courant de veille et son faible courant de fonctionnement statique le rendent adapté aux jouets. Nous pouvons contrôler le sens de rotation et la vitesse du ventilateur en émettant les signaux IN+ et IN- ainsi que des signaux PWM.

#### **(2) Spécifications :**

Tension de fonctionnement : 5V

Courant : 200MA

Puissance maximale : 2W

Température de fonctionnement : -10 degrés Celsius à +50 degrés Celsius

Taille : 47.6MM \*23.8MM

#### **(3) Schéma de connexion :**

Le module ventilateur nécessite un courant important pour fonctionner ; c'est pourquoi nous installons un support de batterie.

![](media/2bd9aa5cc21e274458328958561f1915.png)

Les broches GND, VCC, IN+ et IN- du module ventilateur sont connectées aux broches G, V, D12 et D13 du shield.

#### **(4) Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et des conflits avec la communication série Bluetooth pourraient survenir, entraînant l'échec du téléversement.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.1
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;

void setup()
{
    pinMode(INA, OUTPUT);//Définir le port numérique INA comme sortie
    pinMode(INB, OUTPUT);//Définir le port numérique INB comme sortie
}

void loop() 
{
    //Faire tourner le ventilateur dans le sens antihoraire pendant 3s
    digitalWrite(INA, LOW);
    digitalWrite(INB, HIGH);
    delay(3000);
    //Arrêter le ventilateur pendant 1s
    digitalWrite(INA, LOW);
    digitalWrite(INB, LOW);
    delay(1000);
    //Faire tourner le ventilateur dans le sens horaire pendant 3s
    digitalWrite(INA, HIGH);
    digitalWrite(INB, LOW);
    delay(3000);
}
```

#### **(5) Résultats du test :**

Téléversez le code, connectez les composants et branchez l'alimentation. Le petit ventilateur tournera dans le sens antihoraire pendant 3000ms, s'arrêtera pendant 1000ms, puis tournera dans le sens horaire pendant 300ms.

![](./media/img-20240117085032.png)

#### **(6) Pratique d'extension :**

Nous avons compris le principe de fonctionnement du capteur de flamme. Ensuite, connectez un capteur de flamme dans le circuit, comme illustré ci-dessous. Puis contrôlez le ventilateur pour éteindre le feu à l'aide du capteur de flamme.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et des conflits avec la communication série Bluetooth pourraient survenir, entraînant l'échec du téléversement.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.2
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;
int flame = A1; //Définir la broche de flamme comme broche analogique A1
int val = 0; //Définir les variables numériques

void setup() 
{
    pinMode(INA, OUTPUT);//Définir le port numérique INA comme sortie
    pinMode(INB, OUTPUT);//Définir le port numérique INB comme sortie
    pinMode(flame, INPUT); //Définir la flamme comme source d'entrée
}

void loop() 
{
    val = analogRead(flame); //Lire la valeur analogique du capteur de flamme
    if (val <= 700)  //Lorsque la valeur analogique≤700, le ventilateur est allumé
    {
        //Allumer le ventilateur lorsqu'une flamme est détectée
        digitalWrite(INA, LOW);
        digitalWrite(INB, HIGH);
    } 
    else 
    {
        //Sinon il s'arrête de fonctionner
        digitalWrite(INA, LOW);
        digitalWrite(INB, LOW);
    }
}
```

Après avoir téléversé le code, allumez l'interrupteur d'alimentation du shield de commande moteur, vous pouvez allumer le ventilateur lorsqu'une flamme est détectée par le capteur de flamme gauche du robot.

![](./media/image-20250709115926832.png)