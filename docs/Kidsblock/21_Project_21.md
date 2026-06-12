### Projet 21 : Char d'extinction d'incendie

#### **(1)Description :**

La fonction de suivi de ligne du char intelligent a été expliquée dans le projet précédent. Dans ce projet, nous utilisons le capteur de flamme pour fabriquer un robot d'extinction d'incendie.

Lorsque le véhicule rencontre des flammes, le moteur du ventilateur tourne pour souffler sur le feu. Bien entendu, nous devons d'abord remplacer le capteur ultrasonique et les deux photorésistances par un module ventilateur et des capteurs de flamme.

La logique spécifique du char intelligent est indiquée dans le tableau ci-dessous :

| Capteur de flamme gauche | Capteur de flamme droit | Statut                                                       |
| :----------------------: | :---------------------: | :----------------------------------------------------------- |
|          ≤700            |          ≤700           | Le char s'arrête, le ventilateur commence à tourner pour éteindre la flamme |
|          ≥700            |          ≥700           | Le char s'arrête, le ventilateur commence à tourner pour éteindre la flamme |
|          ≥700            |          ≥700           | Le char s'arrête, le ventilateur commence à tourner pour éteindre la flamme |
|          ＞700           |          ＞700          | Le ventilateur s'arrête, le char se déplace                  |

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
1）Cette expérience nécessite l'utilisation d'une source de feu. Veuillez vous éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer que vous êtes en sécurité, veuillez abandonner l'expérience.
2）Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.
Nous pouvons contrôler une LED externe avec le capteur de flamme. La LED est toujours connectée à D9. Lorsqu'un feu est détecté, la LED s'allume.


#### **(2)Organigramme :**

![](media/wps120.png)

#### **(3)Schéma de connexion :**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

<span style="color: rgb(255, 76, 65);">Remarque :</span>

GND, VCC, SDA et SCL du panneau LED 8x16 sont connectés à G（GND), V（VCC), A4 et A5.

G, V et A des deux capteurs de flamme sont reliés à G（GND), V（VCC), A1 et A2 de la carte d'extension.

#### **(4)Code de test :**


Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/2e3d4904d9605dfecb5736b4bf235ab2.png)

（4） ![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（5） ![](media/4b40151c7482ff9371570978b8ef9c77.png)

（6）![](media/c0365237fa7ec7de10e9fc465353fae1.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/c07c09e5533a37838722b8c2b513646d.png)

#### **(5)Résultats du test :**

Après avoir téléversé le code de test avec succès, mettez sous tension et basculez l'interrupteur DIP sur la position ON. Le char intelligent éteindra le feu lorsqu'il détecte une flamme.

![](media/2de5f1d832d40c0fc94274f1d87443c6.jpeg)

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
Veuillez vous éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer que vous êtes en sécurité, veuillez abandonner l'expérience. Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.