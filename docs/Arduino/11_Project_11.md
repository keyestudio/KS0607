### Projet 11 : Char Suiveur à Ultrasons


#### **(1) Description :**

Dans la leçon précédente, nous avons appris à fabriquer une voiture intelligente suivant la lumière. Dans cette leçon, nous pouvons combiner les connaissances acquises pour réaliser une voiture suivant le son ultrasonique.

Dans ce projet, nous utilisons des capteurs ultrasoniques pour détecter la distance entre la voiture et l'obstacle en face, puis nous contrôlons la rotation des deux moteurs en fonction de ces données afin de contrôler les mouvements de la voiture intelligente.

La logique spécifique de la voiture intelligente suivant le son ultrasonique est présentée dans le tableau ci-dessous :

|                        Détection                        |              Paramètre              |
| :-----------------------------------------------------: | :-------------------------------: |
| La distance (cm) entre la voiture et l'obstacle en face | Régler l'angle du servo à 90° |
|                      **Condition**                      |           **Mouvement**            |
|               distance≥20 et distance≤50               |             Avancer              |
|            10＜distance＜20<br/>distance＞50            |               Arrêt                |
|                       distance≤10                       |              Reculer              |

#### **(2) Organigramme :**

![](media/wps9.png)

#### **(3) Schéma de connexion :**

![](media/72a10097d286bc5f9589df031b60484a.png)

#### **(4) Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut provoquer des conflits avec la communication série Bluetooth et entraîner l'échec du téléversement.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 11
  Ultrasonic follow tank
  http://www.keyestudio.com
*/
#define servoPin 10  //La broche du servo

#define ML_Ctrl 4  //Définir la broche de contrôle de direction du moteur gauche
#define ML_PWM 6   //Définir la broche de contrôle PWM du moteur gauche
#define MR_Ctrl 2  //Définir la broche de contrôle de direction du moteur droit
#define MR_PWM 5   //Définir la broche de contrôle PWM du moteur droit
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //Régler l'angle du servo à 90°
  delay(500); //délai de 500ms
}

void loop() 
{
  distance = checkdistance();  //Assigner la distance mesurée par ultrason à distance
  if (distance >= 20 && distance <= 50) //avancer
  {
    Car_front();
  }
  else if (distance > 10 && distance < 20)  //arrêt
  {
    Car_Stop();
  }
  else if (distance <= 10)  //reculer
  {
    Car_back();
  }
  else  //Dans les autres conditions, la voiture s'arrête
  {
    Car_Stop();
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

//La fonction pour contrôler les servos
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //Calculer la valeur de la largeur d'impulsion    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //Le temps en niveau haut représente la largeur d'impulsion
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //Comme le cycle est de 20ms, le temps restant est en niveau bas
  }
}
//La fonction pour contrôler le son ultrasonique
float checkdistance() 
{
  static float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //Le 58.20 ici provient de 2*29.1=58.2
  delay(10);
  return distance;
}
```

#### **(5) Résultats du test :**

Après avoir téléversé le code de test avec succès, effectué le câblage, basculé le commutateur DIP vers la droite, mis sous tension et réglé le servo à 90°, la voiture intelligente suit l'obstacle et se déplace.

![](./media/img-20240117090457.png)