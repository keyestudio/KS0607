### プロジェクト21：ファン

#### **(1)概要：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

このファンモジュールはHR1124Sモーター制御チップを使用しており、低導電抵抗のPMOSおよびNMOSパワートランジスタを含む単チャンネルHブリッジドライバチップです。低導電抵抗により消費電力を抑えることができ、チップを長時間安全に動作させることができます。

また、低スタンバイ電流および低静的動作電流により、玩具への応用に適しています。IN+およびIN-信号とPWM信号を出力することで、ファンの回転方向と速度を制御できます。

#### **(2)仕様：**

動作電圧：5V

電流：200MA

最大電力：2W

動作温度：-10℃～+50℃

サイズ：47.6MM \*23.8MM

#### **(3)接続図：**

ファンモジュールは大電流による駆動が必要なため、バッテリーホルダーを取り付けます。

![](media/2bd9aa5cc21e274458328958561f1915.png)

ファンモジュールのGND、VCC、IN+、IN-ピンは、シールドのG、V、D12、D13ピンに接続されます。

#### **(4)テストコード：**

(<span style="color: rgb(255, 76, 65);">**注意：**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合し、アップロードに失敗する可能性があります。)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.1
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;

void setup()
{
    pinMode(INA, OUTPUT);//デジタルポートINAを出力に設定
    pinMode(INB, OUTPUT);//デジタルポートINBを出力に設定
}

void loop() 
{
    //ファンを3秒間反時計回りに回転させる
    digitalWrite(INA, LOW);
    digitalWrite(INB, HIGH);
    delay(3000);
    //ファンを1秒間停止させる
    digitalWrite(INA, LOW);
    digitalWrite(INB, LOW);
    delay(1000);
    //ファンを3秒間時計回りに回転させる
    digitalWrite(INA, HIGH);
    digitalWrite(INB, LOW);
    delay(3000);
}
```

#### **(5)テスト結果：**

コードをアップロードし、部品を配線して電源を接続します。小型ファンは3000ms間反時計回りに回転し、1000ms間停止し、300ms間時計回りに回転します。

![](./media/img-20240117085032.png)

#### **(6)応用練習：**

炎センサーの動作原理を理解しました。次に、以下に示すように炎センサーを回路に接続し、炎センサーを使用してファンで火を消す制御を行います。

![](media/67463007499fe6b3f077b4bfbdce6cad.png)

(<span style="color: rgb(255, 76, 65);">**注意：**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合し、アップロードに失敗する可能性があります。)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.2
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;
int flame = A1; //炎ピンをアナログピンA1として定義
int val = 0; //デジタル変数を定義

void setup() 
{
    pinMode(INA, OUTPUT);//デジタルポートINAを出力に設定
    pinMode(INB, OUTPUT);//デジタルポートINBを出力に設定
    pinMode(flame, INPUT); //炎センサーを入力として定義
}

void loop() 
{
    val = analogRead(flame); //炎センサーのアナログ値を読み取る
    if (val <= 700)  //アナログ値が700以下のとき、ファンをオンにする
    {
        //炎が検出されたときにファンをオンにする
        digitalWrite(INA, LOW);
        digitalWrite(INB, HIGH);
    } 
    else 
    {
        //それ以外の場合は動作を停止する
        digitalWrite(INA, LOW);
        digitalWrite(INB, LOW);
    }
}
```

コードをアップロードした後、モータードライブシールドの電源スイッチをオンにすると、ロボットの左側の炎センサーが炎を検知したときにファンをオンにすることができます。

![](./media/image-20250709115926832.png)