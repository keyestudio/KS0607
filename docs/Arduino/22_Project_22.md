### Projet 22 : Char Extincteur


#### **(1)Description :**

La fonction de suivi de ligne du char intelligent a été expliquée dans le projet précédent. Dans ce projet, nous utilisons le capteur de flamme pour fabriquer un robot extincteur.

Lorsque le véhicule rencontre des flammes, le moteur du ventilateur tourne pour souffler le feu. Bien entendu, nous devons d'abord remplacer le capteur ultrasonique et les deux photorésistances par un module ventilateur et des capteurs de flamme.

La logique spécifique du char intelligent suiveur de ligne est présentée dans le tableau ci-dessous :

| Capteur de flamme gauche | Capteur de flamme droit | État                                                      |
| :----------------------: | :---------------------: | :-------------------------------------------------------- |
|          ≤700            |          ≤700           | Le char s'arrête, le ventilateur commence à tourner pour éteindre la flamme |
|          ≥700            |          ≥700           | Le char s'arrête, le ventilateur commence à tourner pour éteindre la flamme |
|          ≥700            |          ≥700           | Le char s'arrête, le ventilateur commence à tourner pour éteindre la flamme |
|          ＞700           |          ＞700          | Le ventilateur s'arrête, le char avance                   |

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
1）Cette expérience nécessite l'utilisation d'une source de feu. Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer votre sécurité, veuillez abandonner l'expérience.
2）Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.
Nous pouvons contrôler une LED externe avec le capteur de flamme. La LED est toujours connectée à D9. Lorsqu'un feu est détecté, la LED s'allume.

#### **(2)Organigramme :**

![](media/wps12.png)

#### **(3)Schéma de connexion :**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

#### **(4)Code de test :**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 22
  Fire extinguishing tank
  http://www.keyestudio.com
*/

int flame_L = A1; //Définir l'interface de flamme gauche comme broche analogique A1
int flame_R = A2; //Définir l'interface de flamme droite comme broche analogique A2
//Le câblage du capteur de suivi de ligne
#define L_pin  11  //gauche
#define M_pin  7  //milieu
#define R_pin  8  //droite
//La broche du servo 130
int INA = 12;
int INB = 13;
#define ML_Ctrl 4  //Définir la broche de contrôle de direction du moteur gauche
#define ML_PWM 6   //Définir la broche de contrôle PWM du moteur gauche
#define MR_Ctrl 2  //Définir la broche de contrôle de direction du moteur droit
#define MR_PWM 5   //Définir la broche de contrôle PWM du moteur droit
int L_val, M_val, R_val, flame_valL, flame_valR;

void setup()
{
  Serial.begin(9600);
  //Définir toutes les broches du capteur de suivi de ligne en mode entrée
  pinMode(L_pin, INPUT);
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  //Définir la flamme comme ENTRÉE
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
  //Définir le moteur comme SORTIE
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  pinMode(INA, OUTPUT);//Définir le port numérique INA comme SORTIE
  pinMode(INB, OUTPUT);//Définir le port numérique INB comme SORTIE
}

void loop () 
{
  //Lire la valeur analogique des capteurs de flamme
  flame_valL = analogRead(flame_L);
  flame_valR = analogRead(flame_R);
  Serial.print(flame_valL);
  Serial.print("  ");
  Serial.print(flame_valR);
  Serial.println("  ");
//  delay(500);
  if (flame_valL <= 700 || flame_valR <= 700) 
  {
    Car_Stop();
    fan_begin();
  } 
  else 
  {
    fan_stop();
    L_val = digitalRead(L_pin); //Lire la valeur du capteur gauche
    M_val = digitalRead(M_pin); //Lire la valeur du capteur du milieu
    R_val = digitalRead(R_pin); //Lire la valeur du capteur droit
    
    if (M_val == 1)  //le capteur du milieu détecte une ligne noire
    {
      if (L_val == 1 && R_val == 0)  //Si une ligne noire est détectée à gauche, mais pas à droite, tourner à gauche
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  //Si une ligne noire est détectée à droite, mais pas à gauche, tourner à droite
      {
        Car_right();
      }
      else  //sinon, avancer
      {
        Car_front();
      }
    }
    else  //Le capteur du milieu ne détecte pas de ligne noire
    {
      if (L_val == 1 && R_val == 0)  //Si une ligne noire est détectée à gauche, mais pas à droite, tourner à gauche
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  //Si une ligne noire est détectée à droite, mais pas à gauche, tourner à droite
      {
        Car_right();
      }
      else  //sinon, s'arrêter
      {
        Car_Stop();
      }
    }
  }
}

void fan_stop() 
{
  //arrêter la rotation
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

void fan_begin() 
{
  //le ventilateur tourne
  digitalWrite(INA, LOW);
  digitalWrite(INB, HIGH);
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 150);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 150);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
  
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Résultat du test :**

Après avoir téléversé le code de test avec succès et mis sous tension, le char intelligent éteint le feu lorsqu'il détecte une flamme et continue de se déplacer le long de la ligne noire.

![](media/694677ab33053846ec588667dc40ecfa.jpeg)

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer votre sécurité, veuillez abandonner l'expérience. Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.