### Projet 4 : Capteur de Suivi de Ligne

#### **(1) Description :**

![](media/d37c24e508361ab86b019135ab6950a9.png)

Le capteur de suivi est en réalité un capteur infrarouge. Le composant utilisé ici est le tube infrarouge TCRT5000.

Son principe de fonctionnement consiste à utiliser la différence de réflectivité de la lumière infrarouge selon les couleurs, puis à convertir l'intensité du signal réfléchi en signal de courant.

Lors du processus de détection, le noir est actif au niveau HAUT (HIGH) tandis que le blanc est actif au niveau BAS (LOW). La hauteur de détection est de 0 à 3 cm.

Le module de suivi de ligne 3 canaux de Keyestudio intègre 3 ensembles de tubes infrarouges TCRT5000 sur une seule carte, ce qui facilite le câblage et le contrôle.

Si le capteur de suivi de ligne ne fonctionne pas comme prévu, vous devrez utiliser un tournevis pour ajuster son potentiomètre afin de le rendre plus sensible. Lorsque votre doigt est proche du capteur, son voyant LED s'allume, et lorsque votre doigt s'éloigne, son voyant LED s'éteint. À ce moment, sa sensibilité est relativement bonne.

![](./media/img-20240117090858.png)

#### **(2) Paramètres :**

- Tension de fonctionnement : 3,3-5V (DC)

- Interface : 5PIN

- Signal de sortie : Signal numérique

- Hauteur de détection : 0-3 cm


Remarque spéciale : avant le test, tournez le potentiomètre sur le capteur pour ajuster la sensibilité de détection. Lorsque vous réglez la LED au seuil entre ON et OFF, la sensibilité est optimale.

<span style="color: rgb(255, 76, 65);">Remarque :</span> le capteur de suivi de ligne est installé sous le bas du robot.

#### **(3) Schéma de Connexion :**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4) Code de Test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.1

Line Track sensor

http://www.keyestudio.com

*/

// Câblage des capteurs de suivi de ligne

#define L_pin 11 // gauche

#define M_pin 7 // milieu

#define R_pin 8 // droite

void setup()
{
    Serial.begin(9600); // Définir le débit en bauds à 9600
    pinMode(L_pin, INPUT); // Définir toutes les broches des capteurs de suivi de ligne en mode entrée
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); // Lire la valeur du capteur gauche
    int M_val = digitalRead(M_pin); // Lire la valeur du capteur central
    int R_val = digitalRead(R_pin); // Lire la valeur du capteur droit

    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); // délai de 100ms
}
```

#### **(5) Résultats du Test :**

Téléversez le code sur la carte de développement, ouvrez le moniteur série pour vérifier les capteurs de suivi de ligne. La valeur affichée est 1 (niveau haut) lorsqu'aucun signal n'est reçu. La valeur passe à 0 lorsque le capteur est recouvert de papier.

![](./media/img-20240117090920.png)


![](media/b9319753c148f66aabc9bf648ed93da1.png)

#### **(6) Explication du Code :**

**Serial.begin(9600)** - Initialise le port série, définit le débit en bauds à 9600

**pinMode -** Définit la broche en mode entrée ou sortie

**digitalRead -** Lit l'état de la broche, qui est généralement au niveau HAUT (HIGH) ou BAS (LOW)

#### **(7) Pratique d'Extension :**

Après avoir compris son principe de fonctionnement, vous pouvez connecter une LED à D9, afin de contrôler la LED par le capteur de suivi de ligne.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

**Code de Test**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.2

Line Track sensor

http://www.keyestudio.com

*/

// Broche LED

#define LED 9
// Câblage des capteurs de suivi de ligne
#define L_pin 11 // gauche
#define M_pin 7 // milieu
#define R_pin 8 // droite

void setup()
{
    Serial.begin(9600); // Définir le débit en bauds à 9600
    pinMode(LED, OUTPUT); // Définir LED en mode sortie
    pinMode(L_pin, INPUT); // Définir toutes les broches des capteurs de suivi de ligne en mode entrée
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); // Lire la valeur du capteur gauche
    int M_val = digitalRead(M_pin); // Lire la valeur du capteur central
    int R_val = digitalRead(R_pin); // Lire la valeur du capteur droit
    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); // Délai

    if (L_val == 0 || M_val == 0 || R_val == 0) 
    {
    	digitalWrite(LED, HIGH);
    }
    else 
    {
    	digitalWrite(LED, LOW);
    }
}
```