### Projet 4 : Capteur de Suivi de Ligne

#### **(1)Description :**

![](media/d37c24e508361ab86b019135ab6950a9.png)

Le capteur de suivi est en réalité un capteur infrarouge. Le composant utilisé ici est le tube infrarouge TCRT5000.

Son principe de fonctionnement consiste à utiliser la différence de réflectivité de la lumière infrarouge selon les couleurs, puis à convertir l'intensité du signal réfléchi en signal de courant.

Lors du processus de détection, le noir est actif au niveau HAUT (HIGH) tandis que le blanc est actif au niveau BAS (LOW). La hauteur de détection est de 0 à 3 cm.

Le module de suivi de ligne 3 canaux Keyestudio intègre 3 ensembles de tubes infrarouges TCRT5000 sur une seule carte, ce qui facilite le câblage et le contrôle.

Si le capteur de suivi de ligne ne fonctionne pas comme prévu, vous devrez utiliser un tournevis pour ajuster son potentiomètre afin de le rendre plus sensible. Lorsque votre doigt est proche du capteur, la LED embarquée s'allume, et lorsque votre doigt s'éloigne, la LED embarquée s'éteint. À ce moment-là, sa sensibilité est relativement bonne.

![](./media/img-20240117091947.png)

#### **(2)Paramètres :**

- Tension de fonctionnement : 3,3-5V (DC)
- Interface : 5PIN
- Signal de sortie : Signal numérique
- Hauteur de détection : 0-3 cm

Remarque particulière : avant le test, tournez le potentiomètre sur le capteur pour régler la sensibilité de détection. Lorsque vous réglez la LED au seuil entre ALLUMÉ et ÉTEINT, la sensibilité est optimale.

<span style="color: rgb(255, 76, 65);">Remarque :</span> le capteur de suivi de ligne est installé sous le fond du robot.

#### **(3)Schéma de connexion :**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4)Code de test :**

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/700cb0ecc14cbccd6e367c5098360f08.png)

![](media/271423c55b5f147796beb344eed7e9cf.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut provoquer l'échec du téléversement.)

![](media/5298cdfb6fd7c71df155c969c80450cd.png)

#### **(5)Résultats du test :**

Téléversez le code sur la carte de développement, ouvrez le moniteur série à 9600 et vérifiez les capteurs de suivi de ligne. La valeur affichée est 1 (niveau haut) lorsqu'aucun signal n'est reçu. La valeur passe à 0 lorsque le capteur est recouvert de papier.

![](media/5630032421adf9446d51b770f0e7f8af.png)

#### **(6)Pratique d'extension :**

Nous pouvons contrôler une LED avec ce capteur. La LED est connectée à D9. Si nous la recouvrons, la LED s'allumera.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/574854f4d96c40a85e1db549d85f14f4.png)

![](media/9077c0d059f7a4d3277f10ccb4e962fb.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

![](media/80e9c514357c63f4791c72220829b673.png)

![](media/b10e1897e99af2c1ade6c09da6c30dba.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne pas connecter le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut provoquer l'échec du téléversement.)

![](media/b5a4b5a04cdee9f79d6e18a5c48cbe48.png)

Lorsqu'un objet (tel que du papier ou un doigt) s'approche du capteur de suivi de ligne, le capteur détecte le signal de retour qu'il a lui-même émis, et le module LED s'allume. Lorsque le capteur ne détecte aucun signal de retour, le module LED s'éteint.

![](./media/img-20240117092116.png)