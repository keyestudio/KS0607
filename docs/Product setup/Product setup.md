# 2. Installation du Produit

<span style="color: rgb(255, 76, 65);">**Attention**</span> : Réglez l'angle initial du servo et retirez les films protecteurs des cartes avant d'installer ce robot.

![](./media/image-20250709092645945.png)

 **Étape 1**

![KS0607_18](./media/KS0607_18.png)

![KS0607_19](./media/KS0607_19.png)

![KS0607_20](./media/KS0607_20.png)

Veuillez d'abord effectuer le câblage.

![](./media/image-20250709093344681.png)

![KS0607-099](./media/KS0607-099.jpg)

![KS0607_21](./media/KS0607_21.png)

![KS0607_22](./media/KS0607_22.png)

![KS0607_23](./media/KS0607_23.png)

**Étape 2**

![KS0607_24](./media/KS0607_24.png)

![KS0607_25](./media/KS0607_25.png)

![KS0607_26](./media/KS0607_26.png)

**Étape 3**

![KS0607_28](media\KS0607_28.png)

![KS0607_29](./media/KS0607_29-177909268352217.png)

![KS0607_30](./media/KS0607_30-177909269696918.png)

 **Étape 4**

![KS0607_31](./media/KS0607_31-17790915380363.png)

![KS0607_32](./media/KS0607_32-17790915471644.png)

![KS0607_33](./media/KS0607_33-17790915540415.png)

![KS0607_34](./media/KS0607_34-17790915654246.png)

![KS0607_35](./media/KS0607_35-17790915710247.png)



**Étape 5**

![KS0607_36](./media/KS0607_36-17790915806918.png)

<span style="color: rgb(255, 76, 65);">Notez la direction des cavaliers.</span>

![KS0607_37](./media/KS0607_37-17790915896649.png)

![KS0607_38](./media/KS0607_38-177909159600610.png)

 **Étape 6**

![KS0607_39](./media/KS0607_39.png)

![KS0607_40](./media/KS0607_40.png)

![KS0607_41](./media/KS0607_41.png)

**Étape 7**

![KS0607_42](./media/KS0607_42.png)

![KS0607_43](./media/KS0607_43.png)

![KS0607_44](./media/KS0607_44.png)

**Étape 8**

（Il est nécessaire de régler l'angle du servo）

![KS0607-098](./media/KS0607-098.jpg)

![KS0607-097](./media/KS0607-097.jpg)

**Régler l'angle du servo à 90°**

Pour ajuster le code du servo, veuillez le sélectionner selon le cours.

1.**Arduino :** Téléchargez le fichier de code : [Arduino](./Arduino.7z)

![](./media/image-20250710110650230.png)

2.**Kidsblock :** Téléchargez le fichier de code : [Kidsblock](./Kidsblock.7z)

![](./media/image-20250710110906515.png)

**Après avoir initialisé l'angle du servo, installez le module Bluetooth.**

Gardez le capteur ultrasonique parallèle à la carte.

![KS0607-096](./media/KS0607-096.jpg)

![](./media/image-20250709095307371.png)

 **Étape 9**

![KS0607_48](./media/KS0607_48-177909161769011.png)

![KS0607_49](./media/KS0607_49-177909162425112.png)

![KS0607_50](./media/KS0607_50-177909163131113.png)

**Étape 10**

![KS0607_51](./media/KS0607_51-177909163803814.png)

![KS0607_52](./media/KS0607_52-177909164311315.png)

![KS0607_53](./media/KS0607_53-177909164907716.png)

**Câblage**

Pour le panneau LED 8\*16, connectez les fils à A4 et A5.

![](./media/image-20250709095552072.png)

![](./media/image-20250709095606248.png)

![](./media/image-20250709095643567.png)

Connectez le moteur A au port A et le moteur B au port B.

![](./media/image-20250709095728739.png)

![](./media/image-20250709095740866.png)

Connectez le fil d'alimentation.

![](./media/image-20250709095759390.png)

![](./media/image-20250709095811580.png)

Capteur de suivi de ligne (voir l'image)

![](./media/image-20250709095830428.png)

![](./media/image-20250709095848550.png)

![](./media/image-20250709095901776.png)

![](./media/image-20250709095911639.png)

Câblage des photorésistances

![](./media/image-20250709095929779.png)

![](./media/image-20250709095939414.png)

| Photorésistance | Keyestudio 8833 Board |
| :-------------: | :-------------------: |
|        G        |           G           |
|        V        |           V           |
|        s        |          A1           |

![](./media/image-20250709100043670.png)

| Photorésistance | Keyestudio 8833 Board |
| :-------------: | :-------------------: |
|        G        |           G           |
|        V        |           V           |
|        S        |          V2           |

Câblage du capteur ultrasonique.

![](./media/image-20250709100317508.png)

![](./media/image-20250709100329430.png)

| Capteur Ultrasonique | Keyestudio 8833 Board |
| :------------------: | :-------------------: |
|         Vcc          |           V           |
|         Trig         |          D12          |
|         Echo         |          D13          |
|         Gnd          |           G           |

Câblage du servo (D10)

![](./media/image-20250709100626238.png)

| Servo  | Keyestudio 8833 Board |
| :----: | :-------------------: |
| Marron |           G           |
| Rouge  |         V(5V)         |
| Orange |          D10          |

<span style="color: rgb(255, 76, 65);">**Nous utilisons une batterie lithium 18650 avec un pôle positif pointu, dont la puissance et la capacité ne sont pas imposées.**</span>

![](./media/image-20250709100841625.png)