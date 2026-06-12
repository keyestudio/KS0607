### Projet 9 : Matrice de points LED 8*16 pour expressions faciales

#### **(1) Description :**

Ne serait-ce pas amusant d'ajouter un panneau d'expression au robot ? Et la matrice de points LED 8*16 de Keyestudio peut faire l'affaire. Grâce à elle, vous pouvez concevoir vous-mêmes des expressions faciales, des images, des motifs et d'autres affichages.

Le panneau LED 8*16 est équipé de 128 LEDs. Les données du microprocesseur (Arduino) communiquent avec l'AiP1640 via une interface de bus à deux fils. Par conséquent, il peut contrôler l'allumage et l'extinction des 128 LEDs du module, afin de faire afficher à la matrice de points du module le motif dont vous avez besoin. Un câble HX-2.54 4 broches est fourni pour faciliter le câblage.

#### **(2) Paramètres :**

-   Tension de fonctionnement : DC 3,3-5V

-   Perte de puissance : 400mW

-   Fréquence d'oscillation : 450KHz

-   Courant de commande : 200mA

-   Température de fonctionnement : -40\~80℃

-   Mode de communication : bus à deux fils

#### **(3) Connaissances :**

**Circuit de la matrice de points LED 8\*16**

![](media/edf6c77d05904eebbaa89d557e9e9c1a.png)

**Principe de la matrice de points LED 8\*16**

Comment contrôler chaque LED de la matrice de points 8\*16 ? On sait que chaque octet comporte 8 bits et que chaque bit vaut 0 ou 1. Quand il vaut 0, la LED est éteinte, et quand il vaut 1, la LED est allumée. Un octet peut contrôler une colonne de LEDs, et naturellement 16 octets peuvent contrôler 16 colonnes de LEDs, ce qui constitue la matrice de points 8\*16.

**Description des broches et protocole de communication**

Les données du microprocesseur (Arduino) communiquent avec l'AiP1640 via un câble de bus à deux fils.

Le schéma du protocole de communication est le suivant : (SCLK) est SCL, (DIN) est SDA.

![](media/ea2bab37f23c09453c680590b84653d6.png)

① La condition de départ pour l'entrée de données : SCL est au niveau haut et SDA passe du niveau haut au niveau bas.

② Pour le réglage de la commande de données, il existe des méthodes comme indiqué dans la figure ci-dessous.

Dans notre exemple de programme, on sélectionne la méthode d'**incrémentation automatique de l'adresse**, la valeur binaire est 0100 0000 et la valeur hexadécimale correspondante est 0x40.

![](media/image-20230907161100692.png)

③ Pour le réglage de la commande d'adresse, l'adresse peut être sélectionnée comme indiqué ci-dessous.

Le premier 00H est sélectionné dans notre exemple de programme, et le nombre binaire 1100 0000 correspond à l'hexadécimal 0xc0.

![](media/image-20230907161152467.png)

④ La condition pour l'entrée de données est que lorsque SCL est au niveau haut lors de la saisie des données, le signal sur SDA doit rester inchangé. Ce n'est que lorsque le signal d'horloge sur SCL est au niveau bas que le signal sur SDA peut être modifié. La saisie des données se fait d'abord par le bit de poids faible, puis par le bit de poids fort.

⑤ La condition de fin de transmission des données est que lorsque SCL est au niveau bas, SDA au niveau bas et SCL au niveau haut, le niveau de SDA devient haut.

⑥ Contrôle d'affichage, réglage de différentes largeurs d'impulsion ; la largeur d'impulsion peut être sélectionnée comme indiqué dans la figure ci-dessous.

Dans l'exemple, la largeur d'impulsion est de 4/16, et l'hexadécimal correspondant à 1000 1010 est 0x8A.

![](media/image-20230907161220995.png)

**Instructions pour l'utilisation de l'outil de modulation**

L'outil de matrice de points utilise la version en ligne, et le lien est : <http://dotmatrixtool.com/#>

① Entrez le lien et la page apparaît comme indiqué ci-dessous

![](media/354693b5679a2615c62e99b7025d6355.png)

② La matrice de points est 8\*16, donc ajustez la hauteur à 8 et la largeur à 16, comme indiqué dans la figure ci-dessous.

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③ Générer des données hexadécimales à partir du motif.

Comme indiqué dans la figure ci-dessous, appuyez sur le bouton gauche de la souris pour sélectionner, cliquez droit pour annuler ; dessinez le motif souhaité, cliquez sur Générer, et les données hexadécimales dont nous avons besoin seront générées.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4) Schéma de connexion :**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

Les broches GND, VCC, SDA et SCL du panneau lumineux LED 8x16 sont respectivement connectées aux broches G(GND), V (VCC), A4 et A5 de la carte d'extension pour la communication série à deux fils.

(<span style="color: rgb(255, 76, 65);">Remarque :</span> bien qu'il soit connecté à la broche IIC d'Arduino, ce module n'est pas destiné à la communication IIC. Le port IO ici simule la communication I2C et peut être connecté à deux broches quelconques)

#### **(5) Code de test :**

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous

![](media/e346413e7f38f5f6368dd8262f173514.png)

![](media/8ecfff600093779602b37d2202493057.png)

![](media/0f0df06e3ed2adbbe3ffaa20dd3fa0a5.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/75e6f65c9a299868d37544ac42c54f66.png)

#### **(6) Résultats du test :**

Après avoir téléversé le code de test avec succès, effectuez le câblage, mettez l'interrupteur DIP sur la position ON et mettez sous tension ; un motif en forme de sourire s'affiche sur la matrice de points.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7) Pratique d'extension :**

Nous utilisons l'outil de modulation que nous venons d'apprendre, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), pour faire afficher à la matrice de points les motifs : démarrer, avancer et s'arrêter, puis effacer le motif. L'intervalle de temps est de 2000 ms.

![](media/31ab1346c58438ca95c990e4ff963c0d.png)

Bloc pour afficher un visage souriant![](media/1702a82ce685e3e7da7b136cbc51e718.png)

Code pour afficher une expression![](media/bae6801afc8fbcc0e7a70c243559c266.png)

Bloc pour afficher un cœur![](media/dcaa414f16d10068d2c3627959141da6.png)

Code pour avancer![](media/8fc218e6b35826aa31f5e00f61414651.png)

Bloc pour reculer![](media/043abae4540c578f93772ed9b6648e60.png)

Bloc pour tourner à gauche![](media/7b3d80a76228ee5b23555af17269a02d.png)

Bloc pour tourner à droite![](media/5a84b3538a62367a8f35cc59071c0bda.png)

Bloc pour s'arrêter![](media/733bd1f96e1c9d116033a317cb507fac.png)

Bloc pour effacer![](media/06d37680acd61c9c5c4113c78c985eca.png)

Vous pouvez également faire glisser des blocs pour modifier votre code, comme indiqué ci-dessous.

（1）![](media/e346413e7f38f5f6368dd8262f173514.png)

（2）![](media/840217b5879f1fce9e36566dc76914a4.png)

（3）![](media/e72e75122897b0ef930196f762080623.png)

**Code de test complet**

(<span style="color: rgb(255, 76, 65);">**Remarque :**</span> Ne connectez pas le module Bluetooth avant de téléverser le code, car le téléversement du code utilise également la communication série, et il peut y avoir des conflits avec la communication série Bluetooth, ce qui peut entraîner l'échec du téléversement.)

![](media/dee30ed46775feb634d4e8e4ec0a189a.png)

Téléversez le code sur la carte de développement ; le panneau 8\*16 affichera les motifs suivants.

![](./media/image-20250709134319784.png)

![](./media/image-20250709134332835.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)