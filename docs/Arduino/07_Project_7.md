### Projet 7 : Réception IR

#### **(1) Description :**

![](media/8969111328604c5358f7c915ac94e474.png)

Il ne fait aucun doute que la télécommande infrarouge est omniprésente dans la vie quotidienne. Elle est utilisée pour contrôler divers appareils électroménagers, tels que les téléviseurs, les chaînes stéréo, les magnétoscopes et les récepteurs de signaux satellitaires. La télécommande infrarouge est composée de systèmes d'émission et de réception infrarouge, c'est-à-dire une télécommande infrarouge, un module de réception infrarouge et un microcontrôleur capable de décoder.

Le signal porteur infrarouge 38K émis par la télécommande est encodé par la puce d'encodage de la télécommande. Il est composé d'une section de code pilote, de code utilisateur, de code inverse utilisateur, de code de données et de code inverse de données. L'intervalle de temps des impulsions est utilisé pour distinguer si c'est un signal 0 ou 1, et l'encodage est constitué de ces signaux 0 et 1.

Le code utilisateur de la même télécommande reste inchangé, tandis que le code de données permet de distinguer les touches.

Lorsque le bouton de la télécommande est pressé, la télécommande envoie un signal porteur infrarouge. Lorsque le récepteur IR reçoit le signal, le programme décode le signal porteur et détermine quelle touche a été pressée. Le MCU décode le signal 01 reçu, déterminant ainsi quelle touche de la télécommande a été pressée.

![](media/image-20230426172824683.png)

Le récepteur infrarouge est soudé sur la carte de commande du moteur. Il intègre la réception, l'amplification et la démodulation, dont le CI interne est déjà réglé pour assurer la réception infrarouge et la sortie, et est compatible avec les signaux TTL. Il génère des signaux numériques et convient à la télécommande infrarouge et à la transmission de données infrarouges. Ce module ne comporte que trois broches, notamment signal, VCC et GND, ce qui le rend très pratique pour se connecter et communiquer avec des microcontrôleurs tels qu'Arduino.

#### **(2) Paramètres :**

Tension de fonctionnement : 3,3-5V (DC)

Interface : 3PIN

Signal de sortie : Signal numérique

Angle de réception : 90 degrés

Fréquence : 38kHz

Distance de réception : 10m

Récepteur infrarouge intégré sur la carte de commande du moteur :

![](./media/img-20240117082433.png)




#### **(3) Code de test :**

Vous devez d'abord importer la bibliothèque IR.

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 7.1

IRremote

http://www.keyestudio.com

*/

#include <IRremote.h> // déclaration de la bibliothèque IRremote

int RECV_PIN = 3; // définir la broche du récepteur IR comme broche 3
IRrecv irrecv(RECV_PIN);
decode_results results; // les résultats du décodage sont stockés dans "result" de "decode results"

void setup() 
{
    Serial.begin(9600);
    irrecv.enableIRIn(); // Activer le récepteur
}

void loop() 
{
    if (irrecv.decode(&results))// décodage réussi, réception d'un ensemble de signaux infrarouges
    {
        Serial.println(results.value, HEX);// Afficher et recevoir le code en hexadécimal 16 bits avec retour à la ligne
        irrecv.resume(); // Recevoir la valeur suivante
    }
    delay(100);
}
```

#### **(4) Résultats du test :**

Téléversez le code de test, ouvrez le moniteur série et réglez le débit en bauds sur 9600, pointez la télécommande vers le récepteur IR. La valeur correspondante sera alors affichée. Si vous maintenez les touches enfoncées un moment, des codes d'erreur apparaîtront.

![](media/a484b81d031c8d6e8addb169136fd45c.png)

Ci-dessous, nous avons listé la valeur de chaque bouton de la télécommande Keyestudio. Vous pouvez la conserver comme référence.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

Le récepteur IR est connecté à D3, donc aucun câblage n'est nécessaire.

#### **(5) Explication du code :**

**irrecv.enableIRIn() :** après l'activation du décodage IR, les signaux IR seront reçus, puis la fonction "decode()" vérifiera continuellement si le décodage a réussi.

**irrecv.decode(&results) :** après un décodage réussi, cette fonction retournera "true" et conservera le résultat dans "results". Après avoir décodé un signal IR, exécutez la fonction resume() pour recevoir le signal suivant.

#### **(6) Pratique d'extension :**

Nous avons décodé la valeur des touches de la télécommande IR. Que diriez-vous de contrôler une LED avec la valeur mesurée ? Nous pourrions concevoir une expérience.

Connectez une LED à D9, puis appuyez sur les touches de la télécommande pour allumer et éteindre la LED.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)

**Code de test**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 7.2
IRremote
http://www.keyestudio.com
*/

#include <IRremote.h> // déclaration IRremote

int RECV_PIN = 3; // définir la broche de la LED comme broche 3
int LED = 9;
bool flag = 0;
IRrecv irrecv(RECV_PIN);
decode_results results; // les résultats du décodage sont stockés dans "result" de "decode results"

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);// régler la LED en sortie
    irrecv.enableIRIn(); // Activer le récepteur
}

void loop() 
{
    if (irrecv.decode(&results)) 
    {
        if (results.value == 0xFF02FD & flag == 0) // Le code de touche ci-dessus, nous utilisons le bouton OK de la télécommande, si vous appuyez sur le bouton OK
        {
            digitalWrite(LED, HIGH); // LED allumée
            flag = 1;
        }

        else if (results.value == 0xFF02FD & flag == 1) // appuyer à nouveau
        {
            digitalWrite(LED, LOW); // LED éteinte
            flag = 0;
        }
        irrecv.resume(); // Recevoir la valeur suivante
    }
}
```

Téléversez le code sur la carte de développement, et appuyez sur la touche "OK" de la télécommande pour allumer et éteindre la LED.

![](./media/img-20240117090645.png)