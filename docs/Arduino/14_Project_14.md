### Projet 14 : Tank Suiveur de Ligne


#### **(1) Description :**

Le projet précédent a expliqué comment confiner la voiture intelligente pour qu'elle se déplace dans un certain espace. Dans ce projet, nous pouvons utiliser les connaissances acquises précédemment pour en faire une voiture intelligente suiveur de ligne. Dans l'expérience, nous utilisons le capteur de suivi de ligne pour détecter s'il y a une ligne noire autour de la voiture intelligente, puis nous contrôlons la rotation des deux moteurs en fonction des résultats de détection, afin de faire se déplacer la voiture intelligente le long de la ligne noire.

La logique spécifique de la voiture intelligente suiveur de ligne est présentée dans le tableau ci-dessous :

|               Capteur               |                          Détection                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Capteur de suivi de ligne central | Ligne noire détectée : niveau haut<br />Ligne blanche détectée : niveau bas |
|  Capteur de suivi de ligne gauche  | Ligne noire détectée : niveau haut<br />Ligne blanche détectée : niveau bas |
| Capteur de suivi de ligne droit  | Ligne noire détectée : niveau haut<br />Ligne blanche détectée : niveau bas |

|                         Condition 1                          |                         Condition 2                          |             Mouvement             |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :------------------------------: |
| Le capteur de suivi de ligne central <br />détecte la ligne noire | Le capteur de suivi de ligne gauche détecte la ligne noire <br />et <br />celui de droite détecte la ligne blanche | Rotation à gauche<br />régler PWM à 200  |
| Le capteur de suivi de ligne central <br />détecte la ligne noire | Le capteur de suivi de ligne gauche détecte la ligne blanche <br />et <br />celui de droite détecte la ligne noire | Rotation à droite<br />régler PWM à 200 |
| Le capteur de suivi de ligne central <br />détecte la ligne noire | Les capteurs gauche et droit détectent tous deux la ligne blanche<br />ou<br />les deux détectent la ligne noire |           Avancer           |
| Le capteur de suivi de ligne central <br />détecte la ligne blanche  | Le capteur de suivi de ligne gauche détecte la ligne noire <br />et <br />celui de droite détecte la ligne blanche | Rotation à gauche<br />régler PWM à 200  |
| Le capteur de suivi de ligne central <br />détecte la ligne blanche  | Le capteur de suivi de ligne gauche détecte la ligne blanche<br />et <br />celui de droite détecte la ligne noire | Rotation à droite<br />régler PWM à 200 |
| Le capteur de suivi de ligne central <br />détecte la ligne blanche  | Les capteurs gauche et droit détectent tous deux la ligne blanche<br />ou<br />les deux capteurs de suivi de ligne gauche et droit détectent la ligne noire |               Arrêt               |

#### **(2) Organigramme :**

![](media/wps11.png)

#### **(3) Schéma de câblage :**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4) Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 14
  Line track tank
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
  pinMode(L_pin, INPUT); // Définir toutes les broches du capteur de suivi de ligne en mode entrée
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
  if (M_val == 1) { // le capteur central détecte une ligne noire
    if (L_val == 1 && R_val == 0)  // Si une ligne noire est détectée à gauche, mais pas à droite, tourner à gauche
    {
      Car_left();
    }
    else if (L_val == 0 && R_val == 1)  // Si une ligne noire est détectée à droite, pas à gauche, tourner à droite
    {
      Car_right();
    }
    else  // sinon, avancer
    {
      Car_front();
    }
  }
  else  // Le capteur central ne détecte pas de ligne noire
  {
    if (L_val == 1 && R_val == 0)  // Si une ligne noire est détectée à gauche, mais pas à droite, tourner à gauche
    {
      Car_left();
    }
    else if (L_val == 0 && R_val == 1)  // Si une ligne noire est détectée à droite, pas à gauche, tourner à droite
    {
      Car_right();
    }
    else  // sinon, s'arrêter
    {
      Car_Stop();
    }
  }
}

// avancer
void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

// reculer
void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

// tourner à gauche
void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

// tourner à droite
void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

// s'arrêter
void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5) Résultat du test :**

Après avoir téléversé le code de test avec succès et mis le système sous tension, la voiture intelligente se déplace le long de la ligne noire.

![](./media/img-20240117085916.png)