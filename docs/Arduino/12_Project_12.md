### Projet 12 : Char à Évitement d'Obstacles par Ultrasons

![](./media/image-20250709112200577.png)


#### **(1) Description :**

Dans le projet précédent, nous avons fabriqué une voiture intelligente de suivi par ultrasons. En réalité, en utilisant les mêmes composants et la même méthode de câblage, il suffit de modifier le code de test pour la transformer en une voiture intelligente à évitement d'obstacles par ultrasons. Cette voiture intelligente peut se déplacer en fonction du mouvement des mains humaines.

Nous utilisons des capteurs à ultrasons pour détecter la distance entre la voiture intelligente et l'obstacle devant elle, puis contrôlons la rotation des deux moteurs en fonction de ces données afin de contrôler les mouvements de la voiture intelligente.

|                          Détection                           |        |
| :----------------------------------------------------------: | :----: |
| Distance mesurée par le capteur à ultrasons entre la voiture et l'obstacle devant <br />（régler l'angle du servo à 90°） | a(cm)  |
| Distance mesurée par le capteur à ultrasons entre la voiture et l'obstacle à droite <br />（régler l'angle du servo à 20°） | a2(cm) |
| Distance mesurée par le capteur à ultrasons entre la voiture et l'obstacle à gauche <br />（régler l'angle du servo à 160°） | a1(cm) |
|   **Réglage :** régler l'angle de départ du servo à 90°    |        |

|   Condition 1   |        Condition 2         | Condition 3 | Mouvement                                                     |
| :-------------: | :------------------------: | ----------- | ------------------------------------------------------------ |
|      a＜20      |                            |             | Arrêt pendant 500ms ；<br />régler l'angle du servo à 180°, lire a1, délai de 100ms ；<br />régler l'angle du servo à 0°, lire a2, délai de 0,1s. |
|                 | a1＜50<br />ou<br />a2＜50 |             | Comparer a1 avec a2                                           |
|                 |                            | a1＞a2      | Régler l'angle du servo à 90°, tourner à gauche pendant 700ms (régler PWM à 255)<br />avancer（régler PWM à 200）. |
|                 |                            | a1＜a2      | Régler l'angle du servo à 90°, tourner à droite pendant 700ms (régler PWM à 255) <br />avancer（régler PWM à 200）. |
| **Condition 1** |      **Condition 2**       |             | **Mouvement**                                                 |
|      a＜20      | a1≥50<br />et<br />a2≥50  | Aléatoire      | Régler l'angle du servo à 90°, tourner à gauche pendant 500ms (régler PWM à 255)<br />avancer (régler PWM à 200)<br /><br />Régler l'angle du servo à 90°, tourner à droite pendant 500ms (régler PWM à 255) <br />avancer (régler PWM à 200) |
|  **Condition**  |                            |             | **Mouvement**                                                 |
|      a≥20       |                            |             | avancer (régler PWM à 100)                                 |



#### **(2) Organigramme :**

![](media/wps10.png)

#### **(3) Schéma de Connexion :**

![](media/72a10097d286bc5f9589df031b60484a.png)

(<span style="color: rgb(255, 76, 65);">Remarque :</span> les fils marron, rouge et orange du servo sont respectivement connectés à G (GND), V（5V）et D10 de la carte d'extension ; et pour le capteur à ultrasons, la broche VCC est connectée au 5v (V), la broche Trig au numérique 12 (S), la broche Echo au numérique 13 (S), et la broche Gnd à Gnd (G) ; identique au projet précédent.）

#### **(4) Code de Test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 12
  Ultrasonic avoid tank
  http://www.keyestudio.com
*/
#define servoPin 10  // La broche du servo
int a, a1, a2;
#define ML_Ctrl 4  // Définir la broche de contrôle de direction du moteur gauche
#define ML_PWM 6   // Définir la broche de contrôle PWM du moteur gauche
#define MR_Ctrl 2  // Définir la broche de contrôle de direction du moteur droit
#define MR_PWM 5   // Définir la broche de contrôle PWM du moteur droit
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  Serial.begin(9600);
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); // Régler l'angle du servo à 90°
  delay(500); // délai de 500ms
}

void loop() 
{
  a = checkdistance();  // Assigner la distance devant détectée par le capteur à ultrasons à la variable a

  if (a < 20) // Lorsque la distance devant est inférieure à 20cm
  {
    Car_Stop();  // Le robot s'arrête
    delay(500); // délai de 500ms
    procedure(180);  // La tourelle à ultrasons tourne à gauche
    delay(500); // délai de 500ms
    a1 = checkdistance();  // Assigner la distance à gauche détectée par le capteur à ultrasons à la variable a1
    delay(100); // lire la valeur
    procedure(0); // La tourelle à ultrasons tourne à droite
    delay(500); // délai de 500ms
    a2 = checkdistance(); // Assigner la distance à droite détectée par le capteur à ultrasons à la variable a2
    delay(100); // lire la valeur
    
    procedure(90);  // Retour à 90°
    delay(500);
    if (a1 > a2) 
    { // Lorsque la distance à gauche est supérieure à celle à droite
      Car_left();  // Le robot tourne à gauche
      delay(700);  // tourner à gauche pendant 700ms
    } 
    else 
    {
      Car_right(); // Il tourne à droite pendant 700ms
      delay(700);
    }
  } 
  else // Lorsque la distance devant est >=20cm, le robot avance
  {    
    Car_front(); // avancer
  }

}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}

// La fonction contrôle les servos
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  // Calculer la valeur de la largeur d'impulsion
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   // Le temps en niveau haut représente la largeur d'impulsion
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  // Comme le cycle est de 20ms, le temps restant est en niveau bas
  }
}

// La fonction contrôle les ultrasons
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  // Le 58.20 ici provient de 2*29.1=58.2
  delay(10);
  return distance;
}
```

#### **(5) Résultat du Test :**

Après avoir téléversé le code de test avec succès, câblé, basculé le commutateur DIP sur la position ON et mis sous tension, la voiture intelligente avance et évite automatiquement les obstacles.

![](./media/img-20240117090420.png)