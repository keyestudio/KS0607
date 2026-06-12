### Projet 9 : Matrice de points LED 8*16 pour expressions faciales

![](./media/image-20250709110751263.png)

#### **(1) Description :**

Ne serait-il pas amusant d'ajouter un tableau d'expressions au robot ? La matrice de points LED 8*16 de Keyestudio peut faire exactement cela. Grâce à elle, vous pouvez concevoir des expressions faciales, des images, des motifs et d'autres affichages par vous-mêmes.

La carte LED 8*16 est équipée de 128 LEDs. Les données du microprocesseur (Arduino) communiquent avec l'AiP1640 via une interface de bus à deux fils. Par conséquent, elle peut contrôler l'allumage et l'extinction des 128 LEDs du module, permettant ainsi à la matrice de points du module d'afficher le motif souhaité. Un câble HX-2.54 4 broches est fourni pour faciliter le câblage.

#### **(2) Paramètres :**

- Tension de fonctionnement : DC 3,3-5V
- Perte de puissance : 400mW
- Fréquence d'oscillation : 450KHz
- Courant d'entraînement : 200mA
- Température de fonctionnement : -40\~80℃
- Mode de communication : bus à deux fils

#### **(3) Connaissances :**

**Principe de la matrice de points LED 8\*16**

Comment contrôler chaque LED de la matrice de points 8\*16 ? On sait que chaque octet possède 8 bits et que chaque bit est 0 ou 1. Quand il est 0, la LED est éteinte, quand il est 1, la LED est allumée. Un octet peut contrôler une colonne de LEDs, et naturellement 16 octets peuvent contrôler 16 colonnes de LEDs, ce qui correspond à la matrice de points 8\*16.

![](media/image-20230427082712905.png)

**Description des broches et protocole de communication**

Les données du microprocesseur (Arduino) communiquent avec l'AiP1640 via un câble de bus à deux fils.

Le schéma du protocole de communication est le suivant (SCLK) est SCL, (DIN) est SDA

![](media/ea2bab37f23c09453c680590b84653d6.png)

①La condition de départ pour l'entrée des données : SCL est au niveau haut et SDA passe du niveau haut au niveau bas.

②Pour le réglage des commandes de données, les méthodes sont présentées dans la figure ci-dessous

Dans notre programme d'exemple, sélectionnez la méthode d'**incrémentation automatique de l'adresse**, la valeur binaire est 0100 0000 et la valeur hexadécimale correspondante est 0x40

![](media/image-20230427083500152.png)

③Pour le réglage des commandes d'adresse, l'adresse peut être sélectionnée comme indiqué ci-dessous.

Le premier 00H est sélectionné dans notre programme d'exemple, et le nombre binaire 1100 0000 correspond à l'hexadécimal 0xc0

![](media/image-20230427083716284.png)


④La condition requise pour l'entrée des données est que lorsque SCL est au niveau haut lors de la saisie des données, le signal sur SDA doit rester inchangé. Ce n'est que lorsque le signal d'horloge sur SCL est au niveau bas que le signal sur SDA peut être modifié. La saisie des données se fait d'abord par le bit de poids faible, puis par le bit de poids fort.

⑤La condition de fin de transmission de données est que lorsque SCL est au niveau bas, SDA est au niveau bas et SCL est au niveau haut, le niveau de SDA devient haut.

⑥Contrôle de l'affichage, réglage de différentes largeurs d'impulsion, la largeur d'impulsion peut être sélectionnée comme indiqué dans la figure ci-dessous. Dans l'exemple, la largeur d'impulsion est 4/16, et l'hexadécimal correspondant à 1000 1010 est 0x8A

![](media/image-20230427084941994.png)



**Instructions pour l'utilisation de l'outil de génération de modules**

L'outil de matrice de points utilise la version en ligne, et le lien est : [http://dotmatrixtool.com/#]( http://dotmatrixtool.com/#)

①Entrez le lien et la page apparaît comme indiqué ci-dessous

![](media/354693b5679a2615c62e99b7025d6355.png)

②La matrice de points est de 8\*16, donc ajustez la hauteur à 8 et la largeur à 16, comme indiqué dans la figure ci-dessous

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③Générer des données hexadécimales à partir du motif

Comme indiqué dans la figure ci-dessous, appuyez sur le bouton gauche de la souris pour sélectionner, clic droit pour annuler ; dessinez le motif souhaité, cliquez sur Generate, et les données hexadécimales dont nous avons besoin seront générées.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4) Schéma de connexion :**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

Le GND, VCC, SDA et SCL de la carte LED 8x16 sont respectivement connectés à la carte d'extension de capteur keyestudio -(GND), +(VCC), A4, A5 pour la communication série à deux fils.

(<span style="color: rgb(255, 76, 65);">Remarque :</span> bien qu'elle soit connectée à la broche IIC de l'Arduino, ce module n'est pas destiné à la communication IIC. Le port IO ici simule la communication I2C et peut être connecté à n'importe quelles deux broches)

#### **(5) Code de test :**

Le code pour afficher le visage souriant

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.1
  Matrix face
  http://www.keyestudio.com
*/
// obtenir les données de l'image souriante depuis un outil de génération de modules
unsigned char smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};

#define SCL_Pin  A5  // définir une broche d'horloge sur A5
#define SDA_Pin  A4  // définir une broche de données sur A4

void setup() {
  // définir la broche en SORTIE
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // effacer l'écran
  //matrix_display(clear);
}
void loop() {
  matrix_display(smile);  // afficher l'image souriante
}
// cette fonction est utilisée pour l'affichage de la matrice de points
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // utiliser la fonction pour commencer à transmettre des données
  IIC_send(0xc0);  // sélectionner une adresse

  for (int i = 0; i < 16; i++) // les données d'image comportent 16 caractères
  {
    IIC_send(matrix_value[i]); // données pour transmettre les images
  }

  IIC_end();   // terminer la transmission des données d'images

  IIC_start();
  IIC_send(0x8A);  // contrôle d'affichage et sélection de la largeur d'impulsion 4/16
  IIC_end();
}

// la condition de démarrage de la transmission des données
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// le signe que la transmission des données se termine
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

// transmettre des données
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // chaque caractère a 8 chiffres, détectés un par un
  {
    if (send_data & mask) { // définir des niveaux haut ou bas en fonction de chaque bit (0 ou 1)
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // tirer vers le haut la broche d'horloge SCL_Pin pour terminer la transmission des données
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // tirer vers le bas la broche d'horloge SCL_Pin pour changer les signaux de SDA
  }
}
```

#### **(6) Résultats du test :**

Après avoir téléversé avec succès le code de test, en effectuant le câblage selon le schéma de connexion, en basculant le commutateur DIP vers la droite et en mettant sous tension, un motif en forme de sourire s'affiche sur la matrice de points.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7) Projet d'extension :**

Nous utilisons l'outil de génération de modules que nous venons d'apprendre, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), pour faire afficher à la matrice de points les motifs de démarrage, d'avance, d'arrêt, puis d'effacement du motif. L'intervalle de temps est de 2000 ms.

![](media/9866c73416df7466b5fe8be3712e6eb3.png)

![](media/1c7ab4b08636c2fe61deaf6c784da7d8.png)

![](media/b0a961f27eb5f0b66603abe23d6bb56a.png)


**Code obtenu depuis l'outil de module ：**

**Code pour le motif de démarrage :**

0x01,0x02,0x04,0x08,0x10,0x20,0x40,0x80,0x80,0x40,0x20,0x10,0x08,0x04,0x02,0x01

**Code pour le motif d'avance :**

0x00,0x00,0x00,0x00,0x00,0x24,0x12,0x09,0x12,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**Code pour le motif de marche arrière :**

0x00,0x00,0x00,0x00,0x00,0x24,0x48,0x90,0x48,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**Code pour le motif de virage à gauche ：**

0x00,0x00,0x00,0x00,0x00,0x00,0x44,0x28,0x10,0x44,0x28,0x10,0x44,0x28,0x10,0x00

**Code pour le motif de virage à droite ：**

0x00,0x10,0x28,0x44,0x10,0x28,0x44,0x10,0x28,0x44,0x00,0x00,0x00,0x00,0x00,0x00

**Code pour le motif d'arrêt ：**

0x2E,0x2A,0x3A,0x00,0x02,0x3E,0x02,0x00,0x3E,0x22,0x3E,0x00,0x3E,0x0A,0x0E,0x00

**Code pour effacer l'écran ：**

0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00

**Code de test**


(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
  keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.2
  Matrix face
  http://www.keyestudio.com
*/

// Tableau, utilisé pour sauvegarder les données des images, peut être calculé soi-même ou obtenu depuis l'outil de génération de modules
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  // définir une broche d'horloge sur A5
#define SDA_Pin  A4  // définir une broche de données sur A4

void setup() {
  // définir la broche en SORTIE
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // effacer l'écran
  matrix_display(clear);
}
void loop() {
  matrix_display(start01);  // afficher l'image "Démarrage"
  delay(2000);
  matrix_display(front);    // afficher l'image "Avance"
  delay(2000);
  matrix_display(STOP01);   // afficher l'image "STOP01"
  delay(2000);
  matrix_display(clear);    // afficher l'image "Effacement"
  delay(2000);
}
// cette fonction est utilisée pour l'affichage de la matrice de points
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // utiliser la fonction pour commencer à transmettre des données
  IIC_send(0xc0);  // sélectionner une adresse

  for (int i = 0; i < 16; i++) // les données d'image comportent 16 caractères
  {
    IIC_send(matrix_value[i]); // données pour transmettre les images
  }

  IIC_end();   // terminer la transmission des données d'images

  IIC_start();
  IIC_send(0x8A);  // contrôle d'affichage et sélection de la largeur d'impulsion 4/16
  IIC_end();
}

// la condition de démarrage de la transmission des données
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// le signe que la transmission des données se termine
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

// transmettre des données
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // chaque caractère a 8 chiffres, détectés un par un
  {
    if (send_data & mask) { // définir des niveaux haut ou bas en fonction de chaque bit (0 ou 1)
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // tirer vers le haut la broche d'horloge SCL_Pin pour terminer la transmission des données
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // tirer vers le bas la broche d'horloge SCL_Pin pour changer les signaux de SDA
  }
}
```

Après le téléversement du code de test, le tableau d'expressions faciales affiche ces motifs dans l'ordre et répète cette séquence.

![](media/e7ba47508826acc25d348182a0530c05.png)

![](media/831b7e0e07250cbc7bdc4fa509c5a0a3.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)