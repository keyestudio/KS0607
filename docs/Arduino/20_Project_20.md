### Projet 20 : Capteur de flamme

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Description :**

Le capteur de flamme utilise un tube récepteur infrarouge pour détecter les flammes. Il convertit la luminosité de la flamme en signaux de niveau haut et bas et les transmet au processeur central pour un traitement de programme correspondant. La valeur de tension du port analogique varie selon qu'une flamme est proche ou absente.

S'il n'y a pas de flamme, le port analogique lit environ 0,3V ; lorsqu'il y a une flamme, le port analogique lit environ 1,0V. Plus la flamme est proche, plus la valeur de tension est élevée. Il peut être utilisé pour détecter une source de feu ou pour construire un robot intelligent.

Notez que la sonde du capteur de flamme ne peut supporter que des températures comprises entre -25℃ et 85℃.

Pendant l'utilisation, assurez-vous de maintenir le capteur de flamme à une distance sûre du feu pour éviter de l'endommager.

#### **(2)Paramètres :**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Tension de fonctionnement : 3,3V-5V (DC)

- Courant : 100mA

- Puissance maximale : 0,5W

- Température de fonctionnement : -10°C à +50 degrés Celsius

- Taille du capteur : 31,6mm x 23,7mm

- Interface : interface 4 broches vers 3 broches

- Signal de sortie : signaux analogiques A0, A1



#### **(3)Schéma de connexion :**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

Les capteurs de flamme sont connectés à A1 et A2.

Lorsque nous retirons les capteurs à ultrasons et les photorésistances, puis ajoutons des capteurs de flamme et des modules de ventilateur, le robot extincteur est créé.

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
1) Cette expérience nécessite l'utilisation d'une source de feu. Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer votre sécurité, veuillez abandonner l'expérience.
2) **Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.**


#### **(4)Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.1

flame sensor

http://www.keyestudio.com

*/

int flame = A1; // Définir la broche de flamme comme broche analogique A1
int val = 0; // Définir les variables numériques

void setup() 
{
	pinMode(flame, INPUT); // Définir le buzzer comme source d'entrée
    Serial.begin(9600); // Régler le débit en bauds à 9600
}

void loop() 
{
	val = analogRead(flame); // Lire la valeur analogique du capteur de flamme
	Serial.println(val); // Afficher la valeur analogique et l'imprimer
	delay(100); // Délai de 100ms
}
```

#### **(5)Résultat du test :**

Connectez les composants, téléversez le code, ouvrez le moniteur série et réglez le débit en bauds à 9600.

Vous pouvez visualiser la valeur de simulation du capteur de flamme.

Plus la flamme est proche, plus la valeur de simulation est faible.

Ajustez le potentiomètre sur le module pour maintenir D1 au point critique. Lorsque le capteur ne détecte pas de flamme, D1 sera éteint, mais si le capteur détecte une flamme, D1 s'allumera.

![](./media/img-20240117085629.png)

![](media/05db06b3e205dfca63c2ba3aa7ff528e.png)

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer votre sécurité, veuillez abandonner l'expérience. Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.

#### **(6)Pratique avancée :**

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
1) Cette expérience nécessite l'utilisation d'une source de feu. Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer votre sécurité, veuillez abandonner l'expérience.
2) Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.

Ensuite, connectez une LED à la broche 9 et nous pouvons la contrôler avec un capteur de flamme, comme indiqué ci-dessous :

![](media/814c315d3bb44278b476a754d3681227.png)

**Code de test**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.2

flame sensor

http://www.keyestudio.com

*/

int flame = A1; // Définir la broche de flamme comme broche analogique A1
int LED = 9; // Définir la LED comme port numérique 9
int val = 0; // Définir les variables numériques

void setup() 
{
    pinMode(flame, INPUT); // Définir la flamme comme source d'entrée
    pinMode(LED, OUTPUT); // Régler la LED en mode sortie
    Serial.begin(9600); // Régler le débit en bauds à 9600
}

void loop() 
{
    val = analogRead(flame); // Lire la valeur analogique du capteur de flamme
    Serial.println(val); // Afficher la valeur analogique et l'imprimer
    if (val < 300)  // Lorsque la valeur analogique est inférieure à 300, la LED s'allume
    {
    	digitalWrite(LED, HIGH); // La LED s'allume
    } 
    else 
    {
    	digitalWrite(LED, LOW); // La LED s'éteint
    }
    delay(50); // Délai de 50ms
}
```

#### **(8)Résultats du test :**

Vous pouvez utiliser la flamme d'un briquet près du capteur de flamme gauche. Lorsque le capteur de flamme détecte une flamme, le module LED s'allumera comme alarme.

![](./media/img-20240117085131.png)

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer votre sécurité, veuillez abandonner l'expérience. Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.