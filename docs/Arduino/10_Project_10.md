### Projet 10 : Char Suiveur de Lumière


#### **(1)Description :**

Dans les projets précédents, nous avons présenté en détail l'utilisation de divers capteurs, modules et cartes d'extension sur le robot. Passons maintenant aux projets du robot. Le robot suiveur de lumière, comme son nom l'indique, est un robot capable de suivre la lumière.

Nous pouvons combiner les connaissances des projets sur la photorésistance et la commande des moteurs pour fabriquer un robot chercheur de lumière. Dans ce projet, nous utilisons deux modules photorésistors pour détecter l'intensité lumineuse des côtés gauche et droit du robot, lire les valeurs analogiques correspondantes, puis contrôler la rotation des deux moteurs en fonction de ces deux données, afin de contrôler les mouvements du robot.

La logique spécifique du robot suiveur de lumière est présentée ci-dessous.

![](./media/image-20250709111733042.png)

#### **(2)Organigramme :**

![](media/wps8.png)

#### **(3)Schéma de connexion :**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Remarque :</span> Les broches "G", "V" et S du module photorésistor gauche sont connectées respectivement à G (GND), V (VCC) et A1 ;

Les broches "G", "V" et S du module photorésistor droit sont connectées respectivement à G (GND), V (VCC) et A2.

Le câble 4 broches est marqué A, A1, B1 et B. Le moteur arrière droit est connecté au port B de la carte d'extension moteur 8833 et le moteur avant gauche est connecté au port A de la carte d'extension moteur 8833.

#### **(4)Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, ce qui peut provoquer des conflits avec la communication série Bluetooth et faire échouer le téléversement.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 10
  light follow tank
  http://www.keyestudio.com
*/
#define light_L_Pin A1   // Définir la broche du capteur photosensible gauche
#define light_R_Pin A2   // Définir la broche du capteur photosensible droit
#define ML_Ctrl 4  // Définir la broche de contrôle de direction du moteur gauche
#define ML_PWM 6   // Définir la broche de contrôle PWM du moteur gauche
#define MR_Ctrl 2  // Définir la broche de contrôle de direction du moteur droit
#define MR_PWM 5   // Définir la broche de contrôle PWM du moteur droit
int left_light;
int right_light;
void setup() 
{
  Serial.begin(9600);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop() 
{
  left_light = analogRead(light_L_Pin);
  right_light = analogRead(light_R_Pin);
  Serial.print("left_light_value = ");
  Serial.println(left_light);
  Serial.print("right_light_value = ");
  Serial.println(right_light);
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
  else  // sinon, s'arrêter
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
```

#### **(5)Résultat du test**

Après avoir téléversé le code de test avec succès, effectué les connexions conformément au schéma de câblage, basculé le commutateur DIP vers la droite et mis sous tension, le robot se déplace en suivant la lumière.

![Img](./media/img-20240117090537.png)