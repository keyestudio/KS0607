### Projet 23 : Robot Extincteur - Fonctions Multiples


#### **(1) Description :**

La voiture intelligente a exécuté une seule fonction dans chaque projet précédent.

Peut-elle afficher plusieurs fonctions à la fois ? Absolument.

Dans ce dernier grand projet, nous avons l'intention d'utiliser un code complet pour contrôler la voiture intelligente afin de présenter toutes les fonctions mentionnées dans les projets précédents. Nous utilisons les touches de l'application Bluetooth pour basculer automatiquement entre les différentes fonctions, ce qui est très simple et pratique.



#### **(2) Diagramme de flux :**

<span style="color: rgb(255, 76, 65);">**Veuillez vous référer au Projet 16 pour installer et configurer l'application Bluetooth**</span>

![](media/image-20230427102547633.png)

#### **(3) Schéma de connexion :**

![](media/e7ac834ba04aa2e8862995d2d33ce9356.jpg)

1\. GND, VCC, SDA et SCL de la carte 8x16 sont connectés à G (GND), + (VCC), A4 et A5 de la carte d'extension.

2\. VCC, IN+, IN- et Gnd du module ventilateur sont connectés à 5V (V), 12 (S), 13 (S) et Gnd (G).

3\. Le fil marron, le fil rouge et le fil orange du servomoteur sont connectés à Gnd (G), 5v (V) et D10.

4\. RXD, TXD, GND et VCC du module BT sont connectés à TX, RX, G (GND) et 5V (VCC). STATE et BRK n'ont pas besoin d'être connectés.

5\. Les broches « G », « V » et A du capteur de flamme gauche sont connectées respectivement à G (GND), V (VCC) et A1 ; le capteur de flamme droit est connecté à G (GND), V (VCC) et A2, respectivement.

6\. Les ports distaux du capteur de suivi de ligne sont 11, 7 et 8.

#### **(4) Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 23
  Fire Extinguishing Robot Multiple Functions
  http://www.keyestudio.com
*/
#include <IRremote.h>
IRrecv irrecv(3);  //
decode_results results;
long ir_rec;  // utilisé pour sauvegarder la valeur IR

/***********/
#define USE_FAN_FUNCTION   1

// Tableau, utilisé pour sauvegarder les données des images, peut être calculé manuellement ou obtenu via un outil de modulation
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

unsigned char Smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};
unsigned char Disgust[] = {0x00, 0x00, 0x02, 0x02, 0x02, 0x12, 0x08, 0x04, 0x08, 0x12, 0x22, 0x02, 0x02, 0x00, 0x00, 0x00};
unsigned char Happy[] = {0x02, 0x02, 0x02, 0x02, 0x08, 0x18, 0x28, 0x48, 0x28, 0x18, 0x08, 0x02, 0x02, 0x02, 0x02, 0x00};
unsigned char Squint[] = {0x00, 0x00, 0x00, 0x41, 0x22, 0x14, 0x48, 0x40, 0x40, 0x48, 0x14, 0x22, 0x41, 0x00, 0x00, 0x00};
unsigned char Despise[] = {0x00, 0x00, 0x06, 0x04, 0x04, 0x04, 0x24, 0x20, 0x20, 0x26, 0x04, 0x04, 0x04, 0x04, 0x00, 0x00};
unsigned char Heart[] = {0x00, 0x00, 0x0C, 0x1E, 0x3F, 0x7F, 0xFE, 0xFC, 0xFE, 0x7F, 0x3F, 0x1E, 0x0C, 0x00, 0x00, 0x00};

unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  // définir la broche d'horloge sur A5
#define SDA_Pin  A4  // définir la broche de données sur A4

#define ML_Ctrl 4  // définir la broche de contrôle de direction du moteur gauche sur 4
#define ML_PWM 6   // définir la broche de contrôle PWM du moteur gauche
#define MR_Ctrl 2  // définir la broche de contrôle de direction du capteur droit
#define MR_PWM 5   // définir la broche de contrôle PWM du moteur droit
char ble_val;      // utilisé pour sauvegarder la valeur Bluetooth
byte speeds_L = 200; // la vitesse initiale du moteur gauche est 200
byte speeds_R = 200; // la vitesse initiale du moteur droit est 200
String speeds_l, speeds_r; // recevoir les caractères PWM et les convertir en valeur PWM

// câblage du capteur de suivi de ligne
#define L_pin  11  // gauche
#define M_pin  7  // milieu
#define R_pin  8  // droite
int L_val, M_val, R_val;

#if USE_FAN_FUNCTION  /****utiliser le ventilateur*******/
int flame_L = A1; // définir le port analogique du capteur de flamme gauche sur A1
int flame_R = A2; // définir le port analogique du capteur de flamme droit sur A2
int flame_valL, flame_valR;

// la broche du moteur 130
int INA = 12;
int INB = 13;

#else /****utiliser le capteur ultrasonique*******/
#define servoPin    10  // broche du servomoteur
#define light_L_Pin A1   // définir la broche de la photorésistance gauche
#define light_R_Pin A2   // définir la broche de la photorésistance droite
int left_light;
int right_light;

#define Trig 12
#define Echo 13
float distance;// Stocker les valeurs de distance détectées par l'ultrason pour le suivi

// Stocker les valeurs de distance détectées par l'ultrason pour l'évitement d'obstacles
int a;
int a1;
int a2;

#endif

bool flag;  // variable flag, utilisée pour entrer et sortir d'un mode

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  // Initialiser la bibliothèque de la télécommande IR

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(L_pin, INPUT); // définir les broches des capteurs en INPUT
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);

  matrix_display(clear);    // effacer l'écran
  matrix_display(start01);  // afficher le démarrage

#if USE_FAN_FUNCTION/****utiliser le ventilateur*******/
  pinMode(INA, OUTPUT);// définir INA en OUTPUT
  pinMode(INB, OUTPUT);// définir INB en OUTPUT

  // définir les entrées du capteur de flamme
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
#else/****utiliser le capteur ultrasonique*******/
  pinMode(servoPin, OUTPUT);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);

  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  procedure(90); // régler l'angle du servomoteur à 90°
#endif
}

void loop() 
{
  if (Serial.available()) // s'il y a des données dans le tampon série
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
    switch (ble_val) 
    {
      case 'F': Car_front(); break; // la commande pour aller en avant

      case 'B': Car_back(); break;  // la commande pour reculer

      case 'L': Car_left(); break;  // la commande pour tourner à gauche

      case 'R': Car_right(); break; // la commande pour tourner à droite

      case 'S': Car_Stop();  break; // arrêt

      case 'e': Tracking();  break; // entrer en mode suivi de ligne

      case 'f': Confinement(); break;  // entrer en mode confinement

#if USE_FAN_FUNCTION/****utiliser le ventilateur*******/
      case 'j': Fire(); break;  // activer le mode extinction d'incendie

      case 'c': fan_begin(); break;  // activer le ventilateur

      case 'd': fan_stop();  break;  // éteindre le ventilateur

#else/****utiliser le capteur ultrasonique*******/
      case 'g': Avoid(); break;  // entrer en mode évitement d'obstacles

      case 'h': Follow(); break;  // entrer en mode suivi

      case 'i': Light_following();  break;  // entrer en mode suivi de lumière
#endif
      case 'u': 
        speeds_l = Serial.readStringUntil('#'); 
        speeds_L = String(speeds_l).toInt(); 
        break; // commencer par recevoir u, terminer par recevoir le caractère # et convertir en entier

      case 'v': 
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt(); 
        break; // commencer par recevoir u, terminer par recevoir le caractère # et convertir en entier

      case 'k': matrix_display(Smile);    break;  // afficher le visage "souriant"
      case 'l': matrix_display(Disgust);  break;  // afficher le visage "dégoûté"
      case 'm': matrix_display(Happy);    break;  // afficher le visage "heureux"
      case 'n': matrix_display(Squint);   break;  // afficher le visage "triste"
      case 'o': matrix_display(Despise);  break;  // afficher le visage "mépris"
      case 'p': matrix_display(Heart);    break;  // afficher l'image du cœur
      case 'z': matrix_display(clear);    break;  // effacer les images

      default: break;
    }
  }

#if (USE_FAN_FUNCTION != 1)/****la fonction sans utilisation du ventilateur*******/
  // Les trois signaux suivants sont principalement utilisés pour l'impression cyclique
  if (ble_val == 'x') 
  {
    distance = checkdistance(); Serial.println(distance);
    delay(50);
  } 
  else if (ble_val == 'w') 
  {
    left_light = analogRead(light_L_Pin);
    Serial.println(left_light);
    delay(50);
  } 
  else if (ble_val == 'y') 
  {
    right_light = analogRead(light_R_Pin);
    Serial.println(right_light);
    delay(50);
  }
#endif

  if (irrecv.decode(&results))  // Recevoir la valeur de la télécommande infrarouge
  {
    ir_rec = results.value;
    Serial.println(ir_rec, HEX);
    switch (ir_rec) 
    {
      case 0xFF629D: Car_front();   break;   // aller en avant
      case 0xFFA857: Car_back();    break;   // reculer
      case 0xFF22DD: Car_left();    break;   // tourner à gauche
      case 0xFFC23D: Car_right();   break;   // tourner à droite
      case 0xFF02FD: Car_Stop();    break;   // arrêt
      default: break;
    }
    irrecv.resume();
  }
}

#if (USE_FAN_FUNCTION != 1)/****utiliser le capteur ultrasonique*******/

// Contrôler le capteur ultrasonique
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //
  delay(10);
  return distance;
}


// la fonction pour contrôler le servomoteur
void procedure(int myangle) 
{
  int pulsewidth;
  pulsewidth = map(myangle, 0, 180, 500, 2000);  // Calculer la valeur de largeur d'impulsion, qui doit être la valeur de correspondance de 500 à 2500. En tenant compte de l'influence de la bibliothèque infrarouge, 500~2000 est utilisé ici.
  for (int i = 0; i < 5; i++) 
  {
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   // La durée du niveau haut est la largeur d'impulsion
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  // La période est de 20ms, donc le niveau bas dure le reste du temps
  }
}

/*****************évitement d'obstacles******************/
void Avoid()
{
  flag = 0;
  while (flag == 0)
  {
    a = checkdistance();  // la distance frontale est définie sur a
    if (a < 20) // Lorsque la distance en avant est inférieure à 20cm
    {
      Car_Stop();  // arrêt
      delay(500); // délai de 500ms
      procedure(180);  // le servomoteur tourne à gauche
      delay(500); // délai de 500ms
      a1 = checkdistance();  // la distance gauche est définie sur a1
      delay(100); // lire la valeur

      procedure(0); // le servomoteur tourne à droite
      delay(500); // délai de 500ms
      a2 = checkdistance(); // la distance droite est définie sur a2
      delay(100); // lire la valeur

      procedure(90);  // retour à 90°
      delay(500);
      if (a1 > a2)  // Lorsque la distance à gauche est supérieure à la distance à droite
      {
        Car_left();  // le robot tourne à gauche
        delay(700);  // tourner à gauche pendant 700ms
      } 
      else 
      {
        Car_right(); // tourner à droite
        delay(700);
      }
    }
    else  // si la distance frontale ≥20cm, le robot avance
    {
      Car_front(); // aller en avant
    }
    // recevoir la valeur Bluetooth pour sortir de la boucle
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S')  // recevoir S
      {
        flag = 1;  // définir flag à 1 pour sortir de la boucle
        Car_Stop();
      }
    }
  }
}

/*******************suivi***************/
void Follow() 
{
  flag = 0;
  while (flag == 0) 
  {
    distance = checkdistance();  // définir la valeur de distance sur distance
    if (distance >= 20 && distance <= 60) // aller en avant
    {
      Car_front();
    }
    else if (distance > 10 && distance < 20)  // arrêt
    {
      Car_Stop();
    }
    else if (distance <= 10)  // reculer
    {
      Car_back();
    }
    else  // arrêt
    {
      Car_Stop();
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S')
      {
        flag = 1;  // sortir de la boucle
        Car_Stop();
      }
    }
  }
}

/****************suivi de lumière******************/
void Light_following() 
{
  flag = 0;
  while (flag == 0) 
  {
    left_light = analogRead(light_L_Pin);
    right_light = analogRead(light_R_Pin);
    if (left_light > 650 && right_light > 650) // avancer
    {
      Car_front();
    }
    else if (left_light > 650 && right_light <= 650)  // tourner à gauche
    {
      Car_left();
    }
    else if (left_light <= 650 && right_light > 650) // tourner à droite
    {
      Car_right();
    }
    else  // sinon, arrêt
    {
      Car_Stop();
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

#else/****utiliser le ventilateur*******/
/***************activer le ventilateur*****************/
void fan_begin() 
{
  digitalWrite(INA, LOW);
  digitalWrite(INB, HIGH);
}

/***************arrêter le ventilateur*****************/
void fan_stop() 
{
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

/***************éteindre l'incendie****************/
void Fire() 
{
  flag = 0;
  while (flag == 0) 
  {
    // Lire la valeur analogique du capteur de flamme
    flame_valL = analogRead(flame_L);
    flame_valR = analogRead(flame_R);
    if (flame_valL <= 700 || flame_valR <= 700) 
    {
      Car_Stop();
      fan_begin();
    } 
    else 
    {
      fan_stop();
      L_val = digitalRead(L_pin); // Lire la valeur du capteur gauche
      M_val = digitalRead(M_pin); // Lire la valeur du capteur gauche
      R_val = digitalRead(R_pin); // Lire la valeur du capteur droit
```

```
      if (M_val == 1)  //le capteur du milieu détecte des lignes noires
      {
        if (L_val == 1 && R_val == 0)  //Si une ligne noire est détectée à gauche, mais pas à droite, tourner à gauche
        {
          Car_left();
        }
        else if (L_val == 0 && R_val == 1)  //Si une ligne noire est détectée à droite, pas à gauche, tourner à droite
        {
          Car_right();
        }
        else //aller tout droit
        { 
          Car_front();
        }
      }
      else //le capteur du milieu ne détecte pas de lignes noires
      { 
        if (L_val == 1 && R_val == 0) //Si une ligne noire est détectée à gauche, mais pas à droite, tourner à gauche
        { 
          Car_left();
        }
        else if (L_val == 0 && R_val == 1) //Si une ligne noire est détectée à droite, pas à gauche, tourner à droite
        { 
          Car_right();
        }
        else //sinon s'arrêter
        { 
          Car_Stop();
        }
      }
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

#endif

/***************suivi de ligne*****************/
void Tracking() 
{
  flag = 0;
  while (flag == 0) 
  {
    L_val = digitalRead(L_pin); //Lire la valeur du capteur gauche
    M_val = digitalRead(M_pin); //Lire la valeur du capteur intermédiaire
    R_val = digitalRead(R_pin); //Lire la valeur du capteur de droite
    if (M_val == 1)  //le capteur du milieu détecte des lignes noires
    {
      if (L_val == 1 && R_val == 0) //Si une ligne noire est détectée à gauche, mais pas à droite, tourner à gauche
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1) //Si une ligne noire est détectée à droite, pas à gauche, tourner à droite
      { 
        Car_right();
      }
      else //aller tout droit
      { 
        Car_front();
      }
    }
    else //le capteur du milieu ne détecte pas de lignes noires
    { 
      if (L_val == 1 && R_val == 0) //Si une ligne noire est détectée à gauche, mais pas à droite, tourner à gauche
      { 
        Car_left();
      }
      else if (L_val == 0 && R_val == 1) //Si une ligne noire est détectée à droite, pas à gauche, tourner à droite
      { 
        Car_right();
      }
      else //sinon s'arrêter
      { 
        Car_Stop();
      }
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

/***************Confinement*****************/
void Confinement() 
{
  flag = 0;
  while (flag == 0) 
  {
    L_val = digitalRead(L_pin); //Lire la valeur du capteur gauche
    M_val = digitalRead(M_pin); //Lire la valeur du capteur intermédiaire
    R_val = digitalRead(R_pin); //Lire la valeur du capteur de droite
    if ( L_val == 0 && M_val == 0 && R_val == 0 ) //Avancer quand aucune ligne noire n'est détectée   
    {    
        Car_front();
    }
    else 
    { 
      Car_back();
      delay(700);
      Car_left();
      delay(800);
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}


/***************matrice de points******************/
//cette fonction est utilisée pour l'affichage de la matrice de points 
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  //utiliser la fonction pour commencer la transmission de données
  IIC_send(0xc0);  //sélectionner une adresse
  for (int i = 0; i < 16; i++) //les données d'image ont 16 caractères
  {
    IIC_send(matrix_value[i]); //données pour transmettre les images
  }
  IIC_end();   //terminer la transmission de données des images
  IIC_start();
  IIC_send(0x8A);  //afficher le contrôle et sélectionner la largeur d'impulsion 4/16
  IIC_end();
}

//la condition de début de transmission de données
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

//transmettre des données
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) //chaque caractère a 8 chiffres, détectés un par un
  {
    if (send_data & mask)  //définir des niveaux hauts ou bas en fonction de chaque bit (0 ou 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); //tirer vers le haut la broche d'horloge SCL_Pin pour terminer la transmission de données
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); //tirer vers le bas la broche d'horloge SCL_Pin pour changer les signaux de SDA 
  }
}

//le signe que la transmission de données est terminée
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

/***************fonctionnement du moteur****************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  //afficher l'image du recul
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  //afficher l'image d'avance
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  //afficher l'image du virage à gauche
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(right);  //afficher l'image du virage à droite
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  //afficher l'image d'arrêt
}
```

#### (5) Résultat du test

Avant de téléverser le code du programme, le module Bluetooth doit être retiré ; sinon, le téléversement du code échouera.

Après avoir téléversé le code avec succès, activez les services de localisation sur votre appareil, puis connectez le module Bluetooth.

Une fois le module Bluetooth branché et alimenté, et l'application mobile connectée avec succès au Bluetooth, nous pouvons utiliser l'application mobile pour contrôler le robot char.

Vous pouvez également contrôler le robot avec la télécommande.

![](media/13656cfee75dc5acbeba18a90a084e159.jpg)