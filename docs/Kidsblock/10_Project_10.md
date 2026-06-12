### Projet 10 : Char Suiveur de Lumière


#### **(1) Description :**

Dans les projets précédents, nous avons présenté en détail l'utilisation de divers capteurs, modules et cartes d'extension sur le char intelligent. Passons maintenant aux projets du char intelligent. Les chars intelligents suiveurs de lumière, comme leur nom l'indique, sont des chars intelligents capables de suivre la lumière.

Nous pouvons combiner les connaissances des projets sur la photorésistance et la commande moteur pour fabriquer un char intelligent chercheur de lumière. Dans ce projet, nous utilisons deux modules photorésistors pour détecter l'intensité lumineuse sur les côtés gauche et droit du char intelligent, lire les valeurs analogiques correspondantes, puis contrôler la rotation des deux moteurs en fonction de ces deux données afin de contrôler les mouvements du char intelligent.

La logique spécifique du char intelligent suiveur de lumière est présentée ci-dessous.

![image-20230525113331422](media/image-20230525113331422.png)

#### **(2) Organigramme :**

![](media/wps117.png)

#### **(3) Schéma de connexion :**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Remarque : </span>Les broches "G", "V" et S du module photorésistor gauche sont connectées respectivement à G (GND), V (VCC), A1 ;

Les broches "G", "V" et S du module photorésistor droit sont connectées respectivement à G (GND), V (VCC) et A2.

Le câble à 4 broches est marqué A, A1, B1 et B. Le moteur arrière droit est connecté au port B de la carte d'extension pilote de moteur 8833 et le moteur avant gauche est connecté au port A de la carte d'extension pilote de moteur 8833.

#### **(4) Code de test :**


Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.

（1）![](media/9352e6447f9648efddc7d5a748618332.png)

（2）![](media/1d99d71f5fe52dd2145cb11d75cabb21.png)

（3）![](media/5004e509325dffb32c05afe25abedfc9.png)

（4）![](media/6c6f0492f657c4c78a0497bb86519561.png)

（5）![](media/b8fc70fa8b3f335dcdf0c8ad9ed998c6.png)

（6）![](media/9eb0e93fbd43aa24f2ce656191f7cd79.png)

(7) ![](media/9f023e6f571e597e661a8d71a7f803cb.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">Remarque :</span> Le seuil 650 dans le code peut être ajusté de manière appropriée en fonction de l'intensité lumineuse spécifique.

Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série du Bluetooth, ce qui peut entraîner l'échec du téléversement du code.)

![](media/6300174b85f63c05dbdcb3b77188f9dc.png)


#### **(5) Résultats du test :**

Après avoir téléversé le code de test avec succès, effectuez le câblage, basculez le commutateur DIP sur la position ON et mettez sous tension ; le char intelligent se déplace en suivant la lumière.

![](./media/img-20240117093758.png)