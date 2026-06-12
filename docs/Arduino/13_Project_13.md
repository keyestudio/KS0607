### Projet 13 : Char d'assaut se déplaçant dans un espace confiné


#### **(1) Description :**

Les fonctions de suivi de son ultrasonique et d'évitement d'obstacles du véhicule intelligent ont été présentées dans les projets précédents. Nous avons ici l'intention de combiner les connaissances des cours précédents pour confiner le véhicule intelligent à se déplacer dans un certain espace.

Dans l'expérience, nous utilisons le capteur de suivi de ligne pour détecter s'il y a une ligne noire autour du véhicule intelligent, puis nous contrôlons la rotation des deux moteurs en fonction des résultats de détection, afin de bloquer le véhicule intelligent dans un cercle tracé en ligne noire.

La logique spécifique du véhicule intelligent à suivi de ligne est présentée dans le tableau ci-dessous :

![](./media/image-20250709112523897.png)

|                         Condition                         |                         Mouvement                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Si l'un des trois capteurs de suivi de ligne détecte des lignes noires | Reculer（régler le PWM à 150）Puis tourner à gauche（régler le PWM à 150） |
|             Aucun d'eux ne détecte de lignes noires              |               Avancer（régler le PWM à 100）                |

#### **(2) Organigramme :**

![](media/image-20230427092708208.png)

#### **(3) Schéma de connexion :**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4) Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 13
  draw a circle for tank
  http://www.keyestudio.com
*/

// Câblage du capteur de suivi de ligne
#define L_pin  11  // gauche
#define M_pin  7  // milieu
#define R_pin  8  // droite

#define ML_Ctrl 4  // Définir la broche de contrôle de direction du moteur gauche
#define ML_PWM 6   // Définir la broche de contrôle PWM du moteur gauche
#define MR_Ctrl 2  // Définir la broche de contrôle de direction du moteur droit
#define MR_PWM 5   // Définir la broche de contrôle PWM du moteur droit
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); // Régler le débit en bauds à 9600
  pinMode(L_pin, INPUT); // Régler toutes les broches du capteur de suivi de ligne en mode entrée
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); // Lire la valeur du capteur gauche
  M_val = digitalRead(M_pin); // Lire la valeur du capteur central
  R_val = digitalRead(R_pin); // Lire la valeur du capteur droit
  if ( L_val == 0 && M_val == 0 && R_val == 0 )  // quand aucune ligne noire n'est détectée, avancer
  {
    Car_front();
  }
  else  // des lignes noires sont détectées, reculer puis tourner à gauche
  {
    Car_back();
    delay(700);
    Car_left();
    delay(800);
  }
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5) Résultats du test :**

Après avoir téléversé le code de test avec succès et mis le système sous tension, le véhicule intelligent se déplace dans un espace confiné, le cercle tracé en ligne noire.

![](./media/img-20240117090340.png)