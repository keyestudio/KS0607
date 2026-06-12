### Projet 18 : Robot à Contrôle de Vitesse BT

#### (1)**Description :**

Dans le projet précédent, nous avons appris à contrôler le tank intelligent avec Bluetooth. La valeur PWM du moteur que nous avons utilisée précédemment est de 200 (la vitesse est de 200).

Dans cette leçon, nous allons utiliser Bluetooth pour ajuster la vitesse de la voiture intelligente. Elle n'est pas limitée à une vitesse fixe de 200. Nous définissons deux variables pour stocker respectivement les valeurs de vitesse des moteurs gauche et droit. Grâce à l'étude précédente, nous savons que la plage de cette valeur ne peut prendre que de 0 à 255.

#### **(2)Organigramme :**

![](media/image-20230427102042028.png)

#### **(3)Schéma de Connexion :**

![](media/930a8024364e07505e845624a94c27bd.png)

Les broches GND, VCC, SDA et SCL de la matrice de points LED 8x16 sont respectivement connectées à -(GND), +(VCC), SDA, SCL de la carte d'extension ;

#### **(4)Code de Test :**

(<span style="color: rgb(255, 76, 65);">Remarque :</span> Lors du téléversement du code, le module Bluetooth doit être débranché, et le Bluetooth peut être reconnecté après le processus de téléversement. Sinon, le code pourrait ne pas être gravé.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 18
  bluetooth control speed tank
  http://www.keyestudio.com
*/

// Tableau, utilisé pour sauvegarder les données des images, peut être calculé manuellement ou obtenu depuis l'outil de modulation
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char speed_a[] = {0x00, 0x00, 0x00, 0x20, 0x10, 0x08, 0x04, 0x02, 0xff, 0x02, 0x04, 0x08, 0x10, 0x20, 0x00, 0x00};
unsigned char speed_d[] = {0x00, 0x00, 0x00, 0x04, 0x08, 0x10, 0x20, 0x40, 0xff, 0x40, 0x20, 0x10, 0x08, 0x04, 0x00, 0x00};
#define SCL_Pin  A5  // définir la broche d'horloge sur A5
#define SDA_Pin  A4  // définir la broche de données sur A4

#define ML_Ctrl 4  // définir la broche de contrôle de direction du moteur gauche
#define ML_PWM 6   // définir les broches de contrôle PWM du moteur gauche
#define MR_Ctrl 2  // définir la broche de contrôle de direction du moteur droit
#define MR_PWM 5   // définir la broche de contrôle PWM du moteur droit
char ble_val;      // définir la broche de contrôle PWM du moteur droit
byte speeds_L = 200; // La vitesse initiale du moteur gauche est 200
byte speeds_R = 200; // La vitesse initiale du moteur droit est 200
String speeds_l, speeds_r; // Recevoir une chaîne de PWM pour la convertir en valeur PWM entière

void setup() 
{
  Serial.begin(9600);

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // effacer l'écran
  matrix_display(start01);  // afficher l'image de démarrage
}

void loop() 
{
  if (Serial.available() > 0) 
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
    switch (ble_val) 
    {
      case 'F':  // la commande pour aller en avant
        Car_front();
        break;
      case 'B':  // la commande pour aller en arrière
        Car_back();
        break;
      case 'L':  // la commande pour tourner à gauche
        Car_left();
        break;
      case 'R':  // la commande pour tourner à droite
        Car_right();
        break;
      case 'S':  // la commande pour s'arrêter
        Car_Stop();
        break;
      case 'u':  // Recevoir une chaîne commençant par u et se terminant par #, et la convertir en valeur entière
        speeds_l = Serial.readStringUntil('#');
        speeds_L = String(speeds_l).toInt();
        break;
      case 'v':  // Recevoir une chaîne commençant par v et se terminant par #, et la convertir en valeur entière
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt();
        break;
    }
  }
}

/***************La fonction pour faire tourner le moteur***************/

void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  // Aller en arrière
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  // afficher l'image pour aller en avant
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  // afficher l'image pour tourner à gauche
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(right);  // afficher l'image pour tourner à droite
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // afficher l'image pour s'arrêter
}

// Cette fonction est utilisée pour l'affichage sur l'écran à matrice de points
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Fonction pour appeler la condition de début de transfert de données
  IIC_send(0xc0);  // Choisir une adresse
  for (int i = 0; i < 16; i++) // Les données de motif ont 16 octets
  {
    IIC_send(matrix_value[i]); // transférer les données de motif
  }
  IIC_end();   // Terminer le transfert des données de motif
  IIC_start();
  IIC_send(0x8A);  // contrôle d'affichage, sélectionner la largeur d'impulsion à 4/16
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

// le signe de fin de transmission de données
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

// transférer des données
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // chaque caractère a 8 chiffres, qui sont détectés un par un
  {
    if (send_data & mask)  // définir des niveaux hauts ou bas en fonction de chaque bit (0 ou 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Tirer la broche d'horloge SCL_Pin haut pour arrêter la transmission de données
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // tirer vers le bas la broche d'horloge SCL_Pin pour changer les signaux de SDA
  }
}
```

#### **(5)Résultats du Test :**

Après avoir téléversé avec succès le code de test, basculé le commutateur DIP vers la droite, mis sous tension et associé l'APP avec le Bluetooth, la voiture intelligente peut être contrôlée pour se déplacer via l'APP. La vitesse de la voiture peut être réglée en tirant les curseurs de vitesse des moteurs gauche et droit.

![](media/b9c902b937801f829b9ce2fd254b1849.jpeg)

(Vous pouvez vous référer au tableau des fonctions du projet 17)