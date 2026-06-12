### プロジェクト16：Bluetoothリモートコントロール

![](./media/img-20240111140012.png)

#### **(1)概要：**

ここ数十年、Bluetoothは使いやすさからバッテリー駆動のほとんどのデバイスに広く利用されており、最も人気のあるワイヤレス通信モジュールとなっています。

時代やユーザーのニーズに対応するため、Bluetoothは何度もアップグレードされてきました。近年では、データ転送速度、ウェアラブルデバイスやIoTデバイスの消費電力、セキュリティシステムなど多くの面で変革を遂げています。ここでは、ArduinoボードとDX-BT24について学習します。

#### **(2)仕様：**

- Bluetoothプロトコル：Bluetooth Specification V5.1 BLE

- シリアルポートの送受信バイト数制限なし

- 通信距離：40m（開放環境）

- 動作周波数：2.4GHz ISMバンド

- 変調方式：GFSK（ガウス周波数偏移変調）

- セキュリティ機能：認証および暗号化

- サポートサービス：Central および Peripheral UUIDs FFE0、FFE1、FFE2

- 消費電力：自動スリープモード、スタンバイ電流 400uA〜800uA、送信中 8.5mA

- 電源：5V

- 動作温度：–10〜+65℃

#### **(3)接続図：**

1.STATEはステータステストピンで、内部発光ダイオードに接続されており、通常は未接続のままにします。

2.RXDは受信端子のシリアルポートインターフェースです。

3.TXDは送信端子のシリアルポートインターフェースです。

4.GNDはグランドです。

5.VCCはプラス極です。

6.EN/BRK：これを切断するとBluetoothが切断され、通常は未接続のままにします。

（注：ここではBluetoothをV2シールドに直接接続します。**方向に注意してください**）

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)


#### **(4)アプリのダウンロードとインストール：**

##### **iOSシステムの場合**

1\. App Storeを開きます。

2\. Apple Storeで <span style="color: rgb(61, 167, 66);">KeyesRobot</span> を検索し、ダウンロードをクリックします。

![](./media/img-20240111141301.png)

3\. アプリがインストールされると、スマートフォンのデスクトップに以下のアイコンが表示されます。

![](./media/img-20240111141412.png)

**iOSスマートフォンをBluetoothモジュールに接続する方法：**

1\. 設定からスマートフォンのBluetoothと位置情報サービスをオンにします。

![](./media/img-20240111141943.png)

2\. 設定からKeyesRobot APPがBluetoothにアクセスすることを許可します。

![](./media/img-20240111142052.png)

3\. KeyesRobot Appをタップして開きます。

![](./media/img-20240111142140.png)

4\. KeyesRobot Appは複数のkeyestudioロボットに対応したユニバーサルAPPです。インターフェースに「TANK ROBOT」が表示されていない場合は、左右のボタンをクリックして「TANK ROBOT」を見つけてください。

5\. 右上隅の <span style="color: rgb(61, 167, 66);">Bluetooth</span> ボタン ![](./media/img-20240111142336.png) をクリックしてBluetoothをスキャンします。

![](./media/img-20240111142415.png)

6\. <span style="color: rgb(0, 209, 0);">**BT24**</span> という名前のBluetoothが表示されます。<span style="color: rgb(255, 169, 0);">Connect</span> ボタンをクリックします。

![](./media/img-20240111142536.png)

7\. BluetoothモジュールのオンボードLEDが点滅をやめて点灯し続ければ、スマートフォンがBluetoothモジュールへの接続に成功したことを意味します。

![](./media/img-20240111142702.png)


##### **Androidシステムの場合**

1\. Google Playで <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> を検索するか、以下のリンクを開いてアプリをダウンロードしてインストールします。

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. スマートフォンのBluetoothと位置情報サービスをオンにします。

![](./media/img-20240111143354.png)

3\. 設定からKeyesRobot Bluetooth appを見つけ、アプリの権限オプションをクリックして、位置情報と近くのデバイスの権限を有効にします。（<span style="color: rgb(255, 76, 65);">注：</span>一部のスマートフォンには近くのデバイスの権限機能がない場合があります。）

![](./media/img-20240111143451.png)

4\. KeyesRobot Appをタップして開きます。

![](./media/img-20240111143529.png)

5\. KeyesRobot Appは複数のkeyestudioロボットに対応したユニバーサルAPPです。インターフェースに「TANK ROBOT」が表示されていない場合は、左右のボタンをクリックして「TANK ROBOT」を見つけてください。

6\. 右上隅の <span style="color: rgb(61, 167, 66);">Bluetooth</span> ボタン ![](./media/img-20240111142336.png) をクリックしてBluetoothをスキャンします。

![](./media/img-20240111142415.png)

7\. <span style="color: rgb(0, 209, 0);">**BT24**</span> という名前のBluetoothが表示されます。<span style="color: rgb(255, 169, 0);">Connect</span> ボタンをクリックします。

![](./media/img-20240111143910.png)

8\. スマートフォンがBluetoothモジュールへの接続に成功すると、BluetoothモジュールのオンボードLEDが点滅をやめて点灯し続けます。

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(5)Bluetooth APPのテスト：**

（<span style="color: rgb(255, 76, 65);">**注：**</span>コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、BluetoothのシリアP通信と競合してアップロードが失敗する可能性があります。）

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.1
Bluetooth
http://www.keyestudio.com
*/

char ble_val; // 文字変数（Bluetoothで受信した値を格納するために使用）

void setup() 
{
	Serial.begin(9600);
}

void loop() 
{
    if (Serial.available() > 0) // シリアルポートバッファにデータがあるか確認
    {
        ble_val = Serial.read(); // シリアルポートバッファのデータを読み取る
        Serial.println(ble_val); // 出力する
    }
}
```

コードを開発ボードにアップロードし、Bluetoothモジュールを差し込み、スマートフォンをBluetoothモジュールに接続します。

スマートフォンがBluetoothモジュールへの接続に成功したら、Bluetooth APPを開き、<span style="color: rgb(0, 252, 255);">ホームページ</span>の <span style="color: rgb(0, 252, 255);">Select</span> ボタンをクリックします。

![](./media/img-20240111144744.png)

Bluetooth appのメインインターフェースは以下の図のとおりです。

![](./media/img-20240111144859.png)

上記のコードのアップロードが成功したら、Arduino IDEのシリアルモニターを開き、ボーレートを9600に設定します。APP画面のアイコンをクリックすると、シリアルモニターにボタンから送信されたコマンドが表示されます。

![](media/805f8ee5c8998a5d6cb8bcef9da09186.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**注：APPの接続方法は以下と同様です。**</span>
<br>
<b>

#### **(6)コードの説明：**

**Serial.available()** はシリアルポートバッファに現在残っている文字数を表します。

この関数は一般的にこの領域にデータがあるかどうかを判断するために使用されます。Serial.available()\>0 の場合、シリアルポートがデータを受信しており、読み取ることができることを意味します。

**Serial.read()** はシリアルポートバッファから1バイトのデータを取り出して読み取ることを指します。例えば、デバイスがシリアルポートを介してArduinoにデータを送信した場合、Serial.read()を使用して送信されたデータを読み取ることができます。

#### **(7)応用プロジェクト：**

ここでは、スマートフォンから送信されるコマンドを使用してLEDライトをオン・オフします。接続図を見ると、LEDはD9ピンに接続されています。

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)

**テストコード**

（<span style="color: rgb(255, 76, 65);">注：</span>コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、BluetoothのシリアP通信と競合してコードのアップロードが失敗する可能性があります。）

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.2
Bluetooth
http://www.keyestudio.com
*/

int LED = 9;
char ble_val; // Bluetoothで受信した値を格納するために使用する整数変数

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);
}

void loop() 
{

    if (Serial.available() > 0) // シリアルポートバッファにデータがあるか確認
    {
        ble_val = Serial.read(); // シリアルポートバッファからデータを読み取る
        Serial.print("DATA RECEIVED:");
        Serial.println(ble_val);
        if (ble_val == 'a') 
        {
            digitalWrite(LED, HIGH);
            Serial.println("led on");
        }
        if (ble_val == 'b') 
        {
            digitalWrite(LED, LOW);
            Serial.println("led off");
        }
    }
}
```

![](media/3577f17c526b1dc55d4f587ef95f2d08.png)

上記のコードのアップロードが成功したら、Arduino IDEのシリアルモニターを開き、ボーレートを9600に設定します。![](media/3fd6c998c0f665fb607a5827794b9bfe.png) をクリックしてLEDを制御します。クリックすると文字 a が送信され、LEDが点灯します。このボタンをもう一度押すと、LEDが消灯します。

![](./media/img-20240117094533.png)

![](media/b45c3c46391467218fe07003dbb2f3e3.png)

プロジェクトが終了したら、BTモジュールを取り外してください。