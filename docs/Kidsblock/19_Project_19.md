### Projet 19 : Capteur de flamme

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1) Description :**

Le capteur de flamme utilise un tube récepteur infrarouge pour détecter les flammes. Il convertit la luminosité de la flamme en signaux de niveau haut et bas et les transmet au processeur central pour le traitement du programme correspondant. La valeur de tension du port analogique varie selon qu'une flamme est proche ou qu'il n'y en a pas du tout.

S'il n'y a pas de flamme, le port analogique lit environ 0,3V ; lorsqu'il y a une flamme, le port analogique lit environ 1,0V. Plus la flamme est proche, plus la valeur de tension est élevée. Il peut être utilisé pour détecter une source de feu ou pour construire un robot intelligent.

Notez que la sonde du capteur de flamme ne peut supporter que des températures comprises entre -25℃ et 85℃.

Lors de l'utilisation, assurez-vous de maintenir le capteur de flamme à une distance de sécurité du feu pour éviter de l'endommager.

#### **(2) Paramètres :**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Tension de fonctionnement : 3,3V-5V (DC)

- Courant : 100mA

- Puissance maximale : 0,5W

- Température de fonctionnement : -10°C à +50 degrés Celsius

- Dimensions du capteur : 31,6mm x 23,7mm

- Interface : interface 4 broches vers 3 broches

- Signal de sortie : signaux analogiques A0, A1

#### **(3) Schéma de connexion :**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

La broche A de deux photorésistances est connectée à A1 et A2. Nous connectons le capteur de flamme à A1 et A2. En remplaçant deux photorésistances et le capteur ultrasonique par deux capteurs de flamme et un ventilateur, une voiture d'extinction est créée.

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
1) Cette expérience nécessite l'utilisation d'une source de feu. Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer que vous êtes en sécurité, veuillez abandonner l'expérience.
2) **Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.**

#### **(4) Code de test :**

Vous pouvez également faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/4bc6c8a4d6e964fd078a6aeb0dd51ff4.png)

#### **(5) Résultats du test :**

Câblez les composants, gravez le code, ouvrez le moniteur série et réglez le débit en bauds à 9600.

Vous pouvez visualiser la valeur de simulation du capteur de flamme.

Plus la flamme est proche, plus la valeur de simulation est faible.

Ajustez le potentiomètre sur le module pour maintenir la LED au point critique. Lorsque le capteur ne détecte pas de flamme, la LED sera éteinte, mais si le capteur détecte une flamme, la LED sera allumée.

![](./media/img-20240117100139.png)

![](media/60d0ce2044a504135af3b1113a1a4c7d.png)

#### **(6) Pratique d'extension :**

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
1) Cette expérience nécessite l'utilisation d'une source de feu. Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer que vous êtes en sécurité, veuillez abandonner l'expérience.
2) Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.
Nous pouvons contrôler une LED externe avec le capteur de flamme. La LED est toujours connectée à D9. Lorsqu'un feu est détecté, la LED s'allumera.

![](media/814c315d3bb44278b476a754d3681227.png)

Vous pouvez faire glisser des blocs pour éditer votre code, comme indiqué ci-dessous

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/9d2f5915e4a6991ed4549b39ec853fa5.png)

Vous pouvez utiliser la flamme d'un briquet près du capteur de flamme gauche. Lorsque le capteur de flamme détecte une flamme, le module LED s'allumera comme alarme.

![](./media/img-20240117100333.png)

<span style="color: rgb(255, 76, 65);">**Remarque :**</span>
Veuillez l'éloigner des matières inflammables pour prévenir tout incendie. Les enfants doivent expérimenter sous la supervision d'un adulte. Si vous ne pouvez pas confirmer que vous êtes en sécurité, veuillez abandonner l'expérience. Le capteur de flamme n'est pas ignifuge, veuillez ne pas le brûler directement avec une flamme.