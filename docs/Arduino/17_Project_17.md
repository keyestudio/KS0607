### Projet 17 : Char d'assaut contrôlé par Bluetooth


#### **(1)Description :**

Nous avons appris les connaissances de base sur le Bluetooth dans le projet précédent. Dans cette leçon, nous allons utiliser le Bluetooth pour contrôler la voiture intelligente. Puisqu'il s'agit de Bluetooth, un émetteur et un récepteur sont nécessaires. Dans ce projet, nous utilisons le téléphone mobile comme émetteur (maître), et la voiture intelligente connectée au module Bluetooth HM-10 (esclave) comme récepteur.

Nous avons appris précédemment qu'envoyer un bit peut contrôler des LED. Le principe de contrôle de ce robot roulant est le même.

Nous allons d'abord comprendre la fonction de chaque bouton sur l'application, puis utiliser les boutons de l'application pour contrôler le char.

#### **(2)Fonctions principales des boutons de l'application**

Le tableau suivant illustre les fonctions des touches correspondantes :

|                      TOUCHES                       | FONCTIONS                                                    |
| :---------------------------------------------: | ------------------------------------------------------------ |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) | Associer et connecter le module Bluetooth HM-10 ; cliquer à nouveau pour déconnecter |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) | Sélectionner le robot à utiliser                                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) | Contrôler les mouvements du robot par boutons             |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) | Contrôler les mouvements du robot par joystick            |
| ![](media/3ab61154b4ae730a3757f40171846825.png) | Contrôler les mouvements du robot par gravité             |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) | Envoie "F" lorsqu'appuyé et "S" lorsque relâché<br />La voiture avance lorsqu'on appuie et s'arrête lorsqu'on relâche |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) | Envoie "L" lorsqu'appuyé et "S" lorsque relâché <br />La voiture tourne à gauche lorsqu'on appuie et s'arrête lorsqu'on relâche |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) | Envoie "R" lorsqu'appuyé et "S" lorsque relâché<br />La voiture tourne à droite lorsqu'on appuie et s'arrête lorsqu'on relâche |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) | Envoie "B" lorsqu'appuyé et "S" lorsque relâché<br />La voiture recule lorsqu'on appuie et s'arrête lorsqu'on relâche |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) | Envoie "u"+chiffre+"\#" lorsqu'on fait glisser<br />Faire glisser pour modifier la vitesse du moteur gauche |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) | Envoie "v"+chiffre+"\#" lorsqu'on fait glisser<br />Faire glisser pour modifier la vitesse du moteur droit |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) | Sélectionner pour accéder à la page des fonctions                                |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Envoie "G" lorsqu'appuyé et "S" lorsqu'appuyé à nouveau<br />Entrer en mode évitement d'obstacles lorsqu'appuyé et quitter lorsqu'appuyé à nouveau |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Envoie "h" lorsqu'appuyé et "S" lorsqu'appuyé à nouveau<br />Entrer en mode de suivi lorsqu'appuyé et quitter lorsqu'appuyé à nouveau |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Envoie "e" lorsqu'appuyé et "S" lorsqu'appuyé à nouveau<br />Entrer en mode suivi de ligne lorsqu'appuyé et quitter lorsqu'appuyé à nouveau |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Envoie "f" lorsqu'appuyé et "S" lorsqu'appuyé à nouveau<br />Entrer en mode déplacement en espace confiné lorsqu'appuyé et quitter lorsqu'appuyé à nouveau |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Envoie "i" lorsqu'appuyé et "S" lorsqu'appuyé à nouveau<br />Entrer en mode suivi de lumière lorsqu'appuyé et quitter lorsqu'appuyé à nouveau |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Envoie "j" lorsqu'appuyé et "S" lorsqu'appuyé à nouveau<br />Entrer en mode extinction d'incendie lorsqu'appuyé et quitter lorsqu'appuyé à nouveau |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Sélectionner pour accéder au mode d'affichage d'expressions faciales               |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Envoie "k" lorsqu'appuyé et "z" lorsqu'appuyé à nouveau<br />Affiche un motif souriant lorsqu'on clique et efface l'expression lorsqu'on clique à nouveau |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Envoie "l" lorsqu'appuyé et "z" lorsqu'appuyé à nouveau<br />Affiche un motif de dégoût lorsqu'on clique et efface l'expression lorsqu'on clique à nouveau |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Envoie "m" lorsqu'appuyé et "z" lorsqu'appuyé à nouveau<br />Affiche un visage heureux lorsqu'on clique et efface l'expression lorsqu'on clique à nouveau |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Envoie "n" lorsqu'appuyé et "z" lorsqu'appuyé à nouveau<br />Affiche un motif triste lorsqu'on clique et efface l'expression lorsqu'on clique à nouveau |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Envoie "o" lorsqu'appuyé et "z" lorsqu'appuyé à nouveau<br />Affiche un motif dédaigneux lorsqu'on clique et efface l'expression lorsqu'on clique à nouveau |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Envoie "p" lorsqu'appuyé et "z" lorsqu'appuyé à nouveau<br />Affiche un motif en forme de cœur lorsqu'on clique et efface l'expression lorsqu'on clique à nouveau |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) | Choisir pour accéder à l'interface de fonctions personnalisées ; il y a six touches 1,2,3,4,5,6 ; avec ces touches, vous pouvez développer certaines fonctions par vous-même |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) | Cliquer pour envoyer "w"<br />Cliquer pour afficher la valeur analogique détectée par la photorésistance gauche |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) | Cliquer pour envoyer "y"<br />Cliquer pour afficher la valeur analogique détectée par la photorésistance droite |
| ![](media/a76df707b84409e57a1167889c3510d9.png) | Cliquer pour envoyer "x" <br />Cliquer pour afficher la distance détectée par le capteur à ultrasons (unité : cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Cliquer pour envoyer "c", cliquer à nouveau pour envoyer "d"<br />Appuyer pour allumer le ventilateur et appuyer à nouveau pour l'éteindre |

#### **(3)Organigramme :**

![](media/image-20230427101759352.png)

#### **(4)Schéma de câblage :**

![](media/930a8024364e07505e845624a94c27bd.png)

Les broches GND, VCC, SDA et SCL de la matrice de points LED 8x16 sont respectivement connectées à -(GND), +(VCC), SDA, SCL de la carte d'extension ;

Les broches STATE et BRK du module Bluetooth n'ont pas besoin d'être connectées.

#### **(5)Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Lors du téléversement du code, le module Bluetooth doit être débranché, et le Bluetooth peut être reconnecté après le processus de téléversement. Sinon, le code pourrait ne pas être téléversé avec succès.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 17.
  bluetooth Control tank
  http://www.keyestudio.com
*/

// Tableau, utilisé pour sauvegarder les données des images, peut être calculé manuellement ou obtenu via un outil de modulation
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  // Définir la broche d'horloge comme A5
#define SDA_Pin  A4  // Définir la broche de données comme A4

#define ML_Ctrl 4  // Définir la broche de contrôle de direction du moteur gauche
#define ML_PWM 6   // Définir la broche de contrôle PWM du moteur gauche
#define MR_Ctrl 2  // Définir la broche de contrôle de direction du moteur droit
#define MR_PWM 5   // Définir la broche de contrôle PWM du moteur droit
char ble_val;      // Utilisé pour stocker la valeur obtenue par Bluetooth

void setup() 
{
  Serial.begin(9600);

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // Effacer l'écran
  matrix_display(start01);  // Afficher l'image de démarrage
}

void loop() 
{
  if (Serial.available())
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
  }
  switch (ble_val)
  {
    case 'F':  // Commande pour avancer
      Car_front();
      break;
    case 'B':  // Commande pour reculer
      Car_back();
      break;
    case 'L':  // Commande pour tourner à gauche
      Car_left();
      break;
    case 'R':  // Commande pour tourner à droite
      Car_right();
      break;
    case 'S':  // Commande pour s'arrêter
      Car_Stop();
      break;
  }
}

/***************Fonction pour faire fonctionner le moteur***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  // Reculer
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(front);  // Afficher l'image pour avancer
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  // Afficher l'image pour tourner à gauche
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  // Afficher l'image pour tourner à droite
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // Afficher l'image d'arrêt
}

// Cette fonction est utilisée pour l'affichage sur l'écran à matrice de points
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Fonction pour appeler la condition de démarrage du transfert de données
  IIC_send(0xc0);  // Choisir une adresse
  for (int i = 0; i < 16; i++) // Les données de motif ont 16 octets
  {
    IIC_send(matrix_value[i]); // Transférer les données du motif
  }
  IIC_end();   // Terminer le transfert des données du motif
  IIC_start();
  IIC_send(0x8A);  // Contrôle d'affichage, sélectionner la largeur d'impulsion à 4/16
  IIC_end();
}

// Conditions pour le début du transfert de données
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// Signe de fin de transmission de données
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

// Transférer des données
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // Chaque caractère a 8 chiffres, détectés un par un
  {
    if (send_data & mask)  // Définir des niveaux hauts ou bas en fonction de chaque bit (0 ou 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Mettre la broche d'horloge SCL_Pin à l'état haut pour arrêter la transmission de données
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // Mettre la broche d'horloge SCL_Pin à l'état bas pour changer les signaux de SDA
  }
}
```

#### **(6)Résultat du test :**

Après avoir téléversé le code, connectez le robot au module Bluetooth et associez l'application Bluetooth. Allumez l'interrupteur d'alimentation du bouclier de commande de moteur. Placez le robot sur le sol, vous pouvez utiliser ces boutons de l'application Bluetooth pour contrôler le robot.

![](media/4655aeffe0d2081fa2b9fd254113c392.jpeg)

1. Les flèches haut, bas, gauche et droite contrôlent respectivement le robot pour avancer, reculer, aller à gauche et aller à droite.


![](./media/img-20240117095345.png)

2. Cliquez sur le bouton joystick et tirez la direction du point noir dans le cercle blanc pour contrôler la direction de déplacement du robot.

![](./media/img-20240117095401.png)

3. Cliquez sur le bouton Gravité et inclinez le téléphone dans les directions avant, arrière, gauche et droite, et le robot se déplacera dans la direction dans laquelle le téléphone est incliné.

![](./media/img-20240117095419.png)