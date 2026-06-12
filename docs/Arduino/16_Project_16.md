### Projet 16 : Télécommande Bluetooth

![](./media/img-20240111140012.png)

#### **(1) Description :**

Au cours des dernières décennies, le Bluetooth est devenu le module de communication sans fil le plus populaire car il est facile à utiliser et a trouvé de nombreuses applications dans la plupart des appareils alimentés par des batteries.

Afin de s'adapter à l'époque, à la réalité et aux besoins des clients, le Bluetooth a été mis à niveau plusieurs fois. Ces dernières années, il a connu de nombreuses transformations en termes de débit de transfert de données, de consommation d'énergie des appareils portables et des appareils IoT, de systèmes de sécurité et autres. Nous prévoyons ici d'apprendre à utiliser le DX-BT24 avec une carte Arduino.

#### **(2) Paramètres :**

- Protocole Bluetooth : Bluetooth Specification V5.1 BLE

- Envoi et réception par port série sans limite d'octets

- Distance de communication : 40 m (environnement ouvert)

- Fréquence de fonctionnement : bande ISM 2,4 GHz

- Méthode de modulation : GFSK (Gaussian Frequency Shift Keying)

- Fonctions de sécurité : Authentification et Chiffrement

- Services pris en charge : UUIDs Central et Peripheral FFE0, FFE1, FFE2

- Consommation d'énergie : mode veille automatique, courant de veille 400uA\~800uA, 8,5 mA lors de la transmission.

- Alimentation : 5 V

- Température de fonctionnement : –10 à +65 degrés Celsius

#### **(3) Schéma de connexion :**

1. STATE est la broche de test d'état connectée à la diode électroluminescente interne et reste généralement non connectée.

2. RXD est l'interface de port série pour le terminal de réception.

3. TXD est l'interface de port série pour le terminal d'émission.

4. GND est la masse.

5. VCC est le pôle positif.

6. EN/BRK : sa déconnexion entraîne la déconnexion du Bluetooth et elle reste généralement non connectée.

(Remarque : ici le Bluetooth est directement lié au shield V2 et **veuillez faire attention au sens**)

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)


#### **(4) Télécharger et installer l'APP :**

##### **Pour le système iOS**

1\. Ouvrir l'App Store.

2\. Rechercher <span style="color: rgb(61, 167, 66);">KeyesRobot</span> dans l'Apple Store et cliquer sur télécharger.

![](./media/img-20240111141301.png)

3\. Une fois l'application installée, vous verrez l'icône suivante sur le bureau de votre téléphone.

![](./media/img-20240111141412.png)

**Comment connecter un iPhone iOS au module Bluetooth :**

1\. Activer le Bluetooth et les services de localisation sur le téléphone via les paramètres.

![](./media/img-20240111141943.png)

2\. Autoriser l'application KeyesRobot à accéder au Bluetooth via les paramètres.

![](./media/img-20240111142052.png)

3\. Cliquer pour ouvrir l'application KeyesRobot.

![](./media/img-20240111142140.png)

4\. L'application KeyesRobot est une application universelle, applicable à plusieurs robots keyestudio. Si l'interface n'affiche pas « TANK ROBOT », vous pouvez cliquer sur les boutons gauche et droit pour trouver « TANK ROBOT ».

5\. Cliquer sur le bouton <span style="color: rgb(61, 167, 66);">Bluetooth</span> ![](./media/img-20240111142336.png) dans le coin supérieur droit pour scanner le Bluetooth.

![](./media/img-20240111142415.png)

6\. Vous verrez un Bluetooth nommé <span style="color: rgb(0, 209, 0);">**BT24**</span>, cliquer sur le bouton <span style="color: rgb(255, 169, 0);">Connect</span>.

![](./media/img-20240111142536.png)

7\. Si la LED embarquée sur le module Bluetooth cesse de clignoter et reste allumée, cela signifie que votre téléphone est correctement connecté au module Bluetooth.

![](./media/img-20240111142702.png)


##### **Pour le système Android**

1\. Rechercher <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> sur Google Play, ou ouvrir le lien suivant pour télécharger et installer l'application.

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Activer le Bluetooth et les services de localisation du téléphone mobile.

![](./media/img-20240111143354.png)

3\. Trouver l'application Bluetooth KeyesRobot dans les paramètres, cliquer sur les options de permissions de l'application et activer les permissions de Localisation et des appareils à proximité. (<span style="color: rgb(255, 76, 65);">Remarque :</span> Certains téléphones mobiles ne disposent pas de la fonction de permissions des appareils à proximité.)

![](./media/img-20240111143451.png)

4\. Cliquer pour ouvrir l'application KeyesRobot.

![](./media/img-20240111143529.png)

5\. L'application KeyesRobot est une application universelle, applicable à plusieurs robots keyestudio. Si l'interface n'affiche pas « TANK ROBOT », vous pouvez cliquer sur les boutons gauche et droit pour trouver « TANK ROBOT ».

6\. Cliquer sur le bouton <span style="color: rgb(61, 167, 66);">Bluetooth</span> ![](./media/img-20240111142336.png) dans le coin supérieur droit pour scanner le Bluetooth.

![](./media/img-20240111142415.png)

7\. Vous verrez un Bluetooth nommé <span style="color: rgb(0, 209, 0);">**BT24**</span>, cliquer sur le bouton <span style="color: rgb(255, 169, 0);">Connect</span>.

![](./media/img-20240111143910.png)

8\. Lorsque votre téléphone est correctement connecté au module Bluetooth, la LED embarquée sur le module Bluetooth cessera de clignoter et restera allumée.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(5) Tester l'application Bluetooth :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.1
Bluetooth
http://www.keyestudio.com
*/

char ble_val; // Variable de type caractère (utilisée pour stocker la valeur reçue par Bluetooth)

void setup() 
{
	Serial.begin(9600);
}

void loop() 
{
    if (Serial.available() > 0) // Déterminer s'il y a des données dans le tampon du port série
    {
        ble_val = Serial.read(); // Lire les données dans le tampon du port série
        Serial.println(ble_val); // Afficher
    }
}
```

Téléverser le code sur la carte de développement, puis brancher le module Bluetooth, puis connecter le téléphone mobile au module Bluetooth.

Une fois le téléphone mobile correctement connecté au module Bluetooth, cliquer pour ouvrir l'application Bluetooth et cliquer sur le bouton <span style="color: rgb(0, 252, 255);">Select</span> sur la <span style="color: rgb(0, 252, 255);">page d'accueil</span>.

![](./media/img-20240111144744.png)

L'interface principale de l'application Bluetooth est illustrée dans la figure ci-dessous.

![](./media/img-20240111144859.png)

Une fois le code ci-dessus téléversé avec succès, ouvrir le moniteur série de l'IDE Arduino et régler le débit en bauds à 9600. Cliquer sur l'icône dans l'interface de l'application et le moniteur série affichera la commande envoyée par le bouton.

![](media/805f8ee5c8998a5d6cb8bcef9da09186.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Remarque : La méthode de connexion de l'application est la même que ci-dessous.**</span>
<br>
<b>

#### **(6) Explication du code :**

**Serial.available()** représente le nombre de caractères actuellement restants dans le tampon du port série.

Cette fonction est généralement utilisée pour déterminer s'il y a des données dans cette zone. Lorsque Serial.available()\>0, cela signifie que le port série a reçu des données et qu'elles peuvent être lues.

**Serial.read()** fait référence à l'extraction et à la lecture d'un octet de données du tampon du port série. Par exemple, si un appareil envoie des données à l'Arduino via le port série, nous pouvons utiliser Serial.read() pour lire les données envoyées.

#### **(7) Projet d'extension :**

Ici, nous utilisons la commande envoyée par le téléphone mobile pour allumer ou éteindre une LED. En regardant le schéma de câblage, une LED est connectée à la broche D9.

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)

**Code de test**

(<span style="color: rgb(255, 76, 65);">Remarque : </span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série du Bluetooth, ce qui peut entraîner l'échec du téléversement du code.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.2
Bluetooth
http://www.keyestudio.com
*/

int LED = 9;
char ble_val; // Variable entière utilisée pour stocker la valeur reçue par Bluetooth

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);
}

void loop() 
{

    if (Serial.available() > 0) // Déterminer s'il y a des données dans le tampon du port série
    {
        ble_val = Serial.read(); // Lire les données du tampon du port série
        Serial.print("DATA RECEIVED:");
        Serial.println(ble_val);
        if (ble_val == 'a') 
        {
            digitalWrite(LED, HIGH);
            Serial.println("led on");
        }
        if (ble_val == 'b') 
        {
            digitalWrite(LED, LOW);
            Serial.println("led off");
        }
    }
}
```

![](media/3577f17c526b1dc55d4f587ef95f2d08.png)

Une fois le code ci-dessus téléversé avec succès, ouvrir le moniteur série de l'IDE Arduino et régler le débit en bauds à 9600. Cliquer sur ![](media/3fd6c998c0f665fb607a5827794b9bfe.png) pour contrôler la LED. En cliquant dessus, un caractère a sera envoyé, puis la LED s'allumera. Si ce bouton est pressé à nouveau, la LED s'éteindra.

![](./media/img-20240117094533.png)

![](media/b45c3c46391467218fe07003dbb2f3e3.png)

Vous devez retirer le module BT une fois les projets terminés.