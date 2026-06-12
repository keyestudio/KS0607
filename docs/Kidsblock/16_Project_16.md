### プロジェクト16：Bluetoothリモートコントロール

![](./media/image-20250709134858245.png)

#### **(1)概要：**

ここ数十年で、Bluetoothは使いやすさから最も人気の高い無線通信モジュールとなり、バッテリー駆動のほとんどのデバイスで広く活用されています。

時代や現実のニーズ、顧客の要望に応えるため、Bluetoothは何度もアップグレードされてきました。近年では、データ転送速度、ウェアラブルデバイスやIoTデバイスの消費電力、セキュリティシステムなど、多くの面で大きな変革を遂げています。ここでは、ArduinoボードとDX-BT24について学びます。

#### **(2)仕様：**

- Bluetoothプロトコル：Bluetooth Specification V5.1 BLE
- 通信距離：開けた環境で最大40mの超長距離通信
- 動作周波数：2.4GHz ISMバンド
- 通信インターフェース：UART
- Bluetooth認証：FCC CE ROHS REACH認証基準に準拠
- シリアルポートパラメータ：9600、データビット8、ストップビット1、パリティなし、フロー制御なし
- 電源：5V DC
- 動作温度：–10〜+65℃


#### **(3)用途：**

DX-BT24モジュールはBT5.1 BLEプロトコルにも対応しており、BLE Bluetooth機能を持つiOSデバイスに直接接続でき、バックグラウンドプログラムの常駐起動をサポートします。主に短距離の無線データ通信分野で使用されます。煩わしいケーブル接続を回避でき、シリアルケーブルを直接置き換えることができます。BT24モジュールの主な応用分野：

※ Bluetooth無線データ通信；

※ 携帯電話・コンピュータ周辺機器；

※ ハンドヘルドPOS機器；

※ 医療機器の無線データ通信；

※ スマートホームコントロール；

※ Bluetoothプリンタ；

※ Bluetoothリモートコントロールトイ；

※ シェアサイクル；

#### **(4)ピン説明：**

![](media/cd97cf79ff5cdd5bbd78f4cc960d38e5.png)

①STATE：状態ピン

②RX：受信ピン

③TX：送信ピン

④GND：グラウンド

⑤VCC：電源ピン

⑥EN：イネーブルピン

Bluetoothを開発ボードに接続する

| Uno  | BT24 |
| :--: | :--: |
|  TX  |  RX  |
|  RX  |  TX  |
| VCC  |  5V  |
| GND  | GND  |

#### **(5)接続図：**

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)

#### **(6)アプリのダウンロード：**

##### **iOS システムの場合**

1\. App Storeを開きます。

2\. Apple Storeで<span style="color: rgb(61, 167, 66);">KeyesRobot</span>を検索し、ダウンロードをクリックします。

![](./media/img-20240111141301.png)

3\. アプリがインストールされると、スマートフォンのデスクトップに以下のアイコンが表示されます。

![](./media/img-20240111141412.png)

**iOSスマートフォンをBluetoothモジュールに接続する方法：**

1\. 設定からスマートフォンのBluetoothと位置情報サービスをオンにします。

![](./media/img-20240111141943.png)

2\. 設定からKeyesRobot APPのBluetooth使用を許可します。

![](./media/img-20240111142052.png)

3\. KeyesRobot Appをタップして開きます。

![](./media/img-20240111142140.png)

4\. KeyesRobot Appは複数のkeyestudioロボットに対応したユニバーサルAPPです。インターフェースに「TANK ROBOT」が表示されていない場合は、左右ボタンをクリックして「TANK ROBOT」を見つけてください。

5\. 右上角の<span style="color: rgb(61, 167, 66);">Bluetoothボタン</span>![](./media/img-20240111142336.png)をクリックしてBluetoothをスキャンします。

![](./media/img-20240111142415.png)

6\. <span style="color: rgb(0, 209, 0);">**BT24**</span>という名前のBluetoothが表示されたら、<span style="color: rgb(255, 169, 0);">Connect</span>ボタンをクリックします。

![](./media/img-20240111142536.png)

7\. BluetoothモジュールのオンボードLEDが点滅を止めて点灯し続けたら、スマートフォンがBluetoothモジュールへの接続に成功したことを意味します。

![](./media/img-20240111142702.png)


##### **Androidシステムの場合**

1\. Google Playで<span style="color: rgb(61, 167, 66);">**KeyesRobot**</span>を検索するか、以下のリンクを開いてアプリをダウンロード・インストールします。

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. スマートフォンのBluetoothと位置情報サービスをオンにします。

![](./media/img-20240111143354.png)

3\. 設定からKeyesRobot Bluetooth appを見つけ、アプリの権限オプションをクリックして、位置情報と近くのデバイスの権限を有効にします。（<span style="color: rgb(255, 76, 65);">注意：</span>一部のスマートフォンには近くのデバイスの権限機能がない場合があります。）

![](./media/img-20240111143451.png)

4\. KeyesRobot Appをタップして開きます。

![](./media/img-20240111143529.png)

5\. KeyesRobot Appは複数のkeyestudioロボットに対応したユニバーサルAPPです。インターフェースに「TANK ROBOT」が表示されていない場合は、左右ボタンをクリックして「TANK ROBOT」を見つけてください。

6\. 右上角の<span style="color: rgb(61, 167, 66);">Bluetoothボタン</span>![](./media/img-20240111142336.png)をクリックしてBluetoothをスキャンします。

![](./media/img-20240111142415.png)

7\. <span style="color: rgb(0, 209, 0);">**BT24**</span>という名前のBluetoothが表示されたら、<span style="color: rgb(255, 169, 0);">Connect</span>ボタンをクリックします。![](./media/img-20240111143910.png)

8\. スマートフォンがBluetoothモジュールへの接続に成功すると、BluetoothモジュールのオンボードLEDが点滅を止めて点灯し続けます。

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(7)BTテストコード：**

以下のようにブロックをドラッグしてコードを編集することもできます。

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/19a90ffb7565966f7d40462abed876a7.png)

（5）![](media/c8228c5040a43ae322612b312c995ac3.png)

**完全なテストコード**

（<span style="color: rgb(255, 76, 65);">**注意：**</span>コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードに失敗する可能性があります。）

![](media/4766ada3bf48bb35522f292d9352bb78.png)


コードを開発ボードにアップロードしたら、Bluetoothモジュールを接続し、スマートフォンをBluetoothモジュールに接続します。

スマートフォンのBluetoothモジュールへの接続が成功したら、Bluetooth APPを開き、<span style="color: rgb(0, 252, 255);">ホームページ</span>の<span style="color: rgb(0, 252, 255);">Select</span>ボタンをクリックします。

![](./media/img-20240111144744.png)

Bluetooth appのメインインターフェースは下図のとおりです。

![](./media/img-20240111144859.png)

![Img](./media/img-20240111171312.png)をクリックして、ボーレートを9600に設定します。APPインターフェース上のアイコンをクリックすると、シリアルモニタにボタンから送信されたコマンドが表示されます。

![](media/f5004f5334fb4885ac0096f99e4133f9.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**注意：APPの接続方法は以下と同様です。**</span>
<br>
<br>


#### **(8)応用練習：**

上記のプロジェクトでは、BluetoothがスマートフォンからのシグナルをDX-BT24モジュールで受信し、開発ボードのシリアルポートに表示しました。ここでは、スマートフォンから送信されたコマンドを使ってLEDのオン・オフを制御します。配線図を見ると、LEDがD9ピンに接続されています。

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)


以下のようにブロックをドラッグしてコードを編集することもできます。

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/aa78663af261ff1d9bc8ffa6ad7a65bc.png)

(5）![](media/c8228c5040a43ae322612b312c995ac3.png)

（6）![](media/4164bcf66d3d2415f43a0efcd1ce4243.png)

**完全なテストコード**

（<span style="color: rgb(255, 76, 65);">**注意：**</span>コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードに失敗する可能性があります。）

![](media/91fd9d6f85e291fe90a63e5095ed7f44.png)

上記のコードが正常にアップロードされたら、![](media/d5e59839bafc63f8b35c78c60573d1fc.png)をクリックしてLEDを制御します。

![](./media/img-20240117094418.png)


BTプロジェクトが終了したら、取り外してください。