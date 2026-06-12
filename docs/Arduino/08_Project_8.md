### プロジェクト8: モーター駆動と速度制御

#### **(1)説明:**

モーターを駆動する方法はたくさんあります。このスマートカーは、L298Pと呼ばれる最も一般的なソリューションを使用しています。STMicroelectronicsが製造するL298Pは、高出力モーターを駆動するために特別に設計された優れた駆動チップです。

DCモーター、2相および4相モーターを直接駆動でき、駆動電流は2Aに達します。また、モーターの出力端子には保護として8つの高速ショットキーダイオードが採用されています。

L298P回路をベースにした拡張ボードを設計しており、積層設計によりUNO R3ボードに直接差し込んで使用することができ、ユーザーがモーターを使用・駆動する際の技術的な困難を軽減します。

拡張ボードをボードに重ね、BATに電源を入れ、DIPスイッチをON側に切り替えると、外部電源を介して拡張ボードとUNO R3ボードに同時に電源が供給されます。

配線を容易にするため、拡張ボードには逆接防止インターフェース（PH2.0 -2P -3P -4P -5P）が装備されており、モーター、電源、センサー/モジュールを直接接続することができます。

駆動拡張ボードのBluetoothインターフェースは、Keyestudio HM-10 Bluetoothモジュールと完全に互換性があります。そのため、接続時にHM-10 Bluetoothモジュールを対応するインターフェースに挿入するだけです。

同時に、駆動拡張ボードは2.54ピンヘッダーを使用して、利用可能なデジタルポートとアナログポートを拡張しているため、他のセンサーを追加して拡張実験を続けることができます。

拡張ボードには4つのDCモーターを接続できます。デフォルトのジャンパーキャップ接続モードでは、AとA1、BとB1インターフェースのモーターは並列接続されており、動作パターンは同じです。8つのジャンパーキャップを使用して、4つのモーターインターフェースの回転方向を制御できます。

例えば、モーターAインターフェース前面の2つのジャンパーキャップを横接続から縦接続に変更すると、モーターAの回転方向が元の方向と逆になります。

![](media/image-20230427081635216.png)

![](media/5381c98d3be6da099ce43e841b8f736b.png)

#### **(2)パラメーター：**

- ロジック部入力電圧: DC 5V

- 駆動部入力電圧: DC 7-12V

- ロジック部動作電流: ≤36mA

- 駆動部動作電流: ≤ 2A

- 最大消費電力: 25W (T=75℃)

- 制御信号入力レベル:
  
  ​	ハイレベル: 2.3V ≤ Vin ≤ 5V
  
  ​	ローレベル: 0V ≤ Vin ≤ 1.5V

- 動作温度: -25℃～＋130℃

#### **(3)ロボットを動かす**

モーターAの方向ピンはD2、速度制御ピンはD5です。モーターBの方向ピンはD4、速度制御ピンはD6です。

以下の表から、デジタルポートとPWMポートを通じて2つのモーターの回転を制御することにより、ロボットの動きを制御する方法がわかります。PWM値の範囲は0〜255で、値が大きいほどモーターの回転が速くなります。

|   機能   |  D4  | D6（PWM） | モーター（左）B |  D2  | D5（PWM） | モーター（右）A |
| :------: | :--: | :-------: | :-------------: | :--: | :-------: | :-------------: |
| 前進     | HIGH |  255-200  |   左回転        | HIGH |  255-200  |   左回転        |
| 後退     | LOW  |    200    |  右回転         | LOW  |    200    |  右回転         |
| 左折     | LOW  |    200    |  右回転         | HIGH |  255-200  |   左回転        |
| 右折     | HIGH |  255-200  |   左回転        | LOW  |    200    |  右回転         |
| 停止     | LOW  |     0     |      停止       | LOW  |     0     |      停止       |




#### **(4)接続図:**

![](media/3e53cf19ea5f85a931b955453b86304b.png)

<span style="color: rgb(255, 76, 65);">注意:</span>

4ピンコネクタにはA、A1、B1、Bと表示されています。右後部モーターは8833ボードのBに接続され、左前部モーターはAポートに接続されています。

#### **(5)テストコード:**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードにもシリアル通信を使用しており、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.1
motor driver
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // 左モーターの方向制御ピンを定義する
#define ML_PWM 6 // 左モーターのPWM制御ピンを定義する
#define MR_Ctrl 2 // 右モーターの方向制御ピンを定義する
#define MR_PWM 5 // 右モーターのPWM制御ピンを定義する

void setup()
{
    pinMode(ML_Ctrl, OUTPUT);// 左モーターの方向制御ピンをOUTPUTとして定義する
    pinMode(ML_PWM, OUTPUT);// 左モーターのPWM制御ピンをOUTPUTとして定義する
    pinMode(MR_Ctrl, OUTPUT);// 右モーターの方向制御ピンをOUTPUTとして定義する
    pinMode(MR_PWM, OUTPUT);// 右モーターのPWM制御ピンをOUTPUTとして定義する
}

void loop()
{
    // 前進
    digitalWrite(ML_Ctrl, HIGH); // 左モーターの方向制御速度をHIGHに設定する
    analogWrite(ML_PWM, 55); // 左モーターのPWM制御速度は55
    digitalWrite(MR_Ctrl, HIGH); // 右モーターの方向制御速度をHIGHに設定する
    analogWrite(MR_PWM, 55); // 右モーターのPWM制御速度は55
    delay(2000);// 2秒間待機

    // 後退
    digitalWrite(ML_Ctrl, LOW); // 左モーターの方向制御速度をLOWに設定する
    analogWrite(ML_PWM, 200); // 左モーターのPWM制御速度は200
    digitalWrite(MR_Ctrl, LOW); // 右モーターの方向制御速度をLOWに設定する
    analogWrite(MR_PWM, 200); // 右モーターのPWM制御速度は200
    delay(2000);// 2秒間待機

    // 左折
    digitalWrite(ML_Ctrl, LOW); // 左モーターの方向制御速度をLOWに設定する
    analogWrite(ML_PWM, 200); // 左モーターのPWM制御速度は200
    digitalWrite(MR_Ctrl, HIGH); // 右モーターの方向制御速度をHIGHに設定する
    analogWrite(MR_PWM, 55); // 右モーターのPWM制御速度は55
    delay(2000);// 2秒間待機

    // 右折
    digitalWrite(ML_Ctrl, HIGH); // 左モーターの方向制御速度をHIGHに設定する
    analogWrite(ML_PWM, 55); // 左モーターのPWM制御速度は55
    digitalWrite(MR_Ctrl, LOW); // 右モーターの方向制御速度をLOWに設定する
    analogWrite(MR_PWM, 200); // 右モーターのPWM制御速度は200
    delay(2000);// 2秒間待機

    // 停止
    digitalWrite(ML_Ctrl, LOW);
    analogWrite(ML_PWM, 0); // 左モーターのPWM制御速度は0
    digitalWrite(MR_Ctrl, LOW);
    analogWrite(MR_PWM, 0); // 右モーターのPWM制御速度は0
    delay(2000);// 2秒間待機
}
```

#### **(6)テスト結果:**

図に従って配線し、テストコードをアップロードして電源を入れると、

![](./media/img-20240117082646.png)

スマートカーは2秒間前進し、2秒間後退し、2秒間左折し、2秒間右折し、2秒間停止し、この動作を繰り返します。

#### **(7)コード説明:**

**digitalWrite(ML_Ctrl,LOW);**

ハイレベルとローレベルの切り替えにより、モーターを時計回りまたは反時計回りに回転させることができます。これらの動作を制御するには、一般的なデジタルピンを使用できます。

**analogWrite(ML_PWM,200);**

モーターの速度調整はPWMによって実現されており、モーターの速度を制御するピンはArduinoのPWMピンである必要があります。

#### **(8)応用プロジェクト:**

PWMを制御することでモーターの速度を調整します。配線は同じです。

**テストコード**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードにもシリアル通信を使用しており、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.2
motor driver pwm
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // 左モーターの方向制御ピンを定義する
#define ML_PWM 6 // 左モーターのPWM制御ピンを定義する
#define MR_Ctrl 2 // 右モーターの方向制御ピンを定義する
#define MR_PWM 5 // 右モーターのPWM制御ピンを定義する

void setup() 
{
    pinMode(ML_Ctrl, OUTPUT);// 左モーターの方向制御ピンをOUTPUTとして定義する
    pinMode(ML_PWM, OUTPUT);// 左モーターのPWM制御ピンをOUTPUTとして定義する
    pinMode(MR_Ctrl, OUTPUT);// 右モーターの方向制御ピンをOUTPUTとして定義する
    pinMode(MR_PWM, OUTPUT);// 右モーターのPWM制御ピンをOUTPUTとして定義する
}

void loop() 
{
    // 前進
    digitalWrite(ML_Ctrl, HIGH); // 左モーターの方向制御速度をHIGHに設定する
    analogWrite(ML_PWM, 155); // 左モーターのPWM制御速度は155
    digitalWrite(MR_Ctrl, HIGH); // 右モーターの方向制御速度をHIGHに設定する
    analogWrite(MR_PWM, 155); // 右モーターのPWM制御速度は155
    delay(2000);// 2秒間待機

    // 後退
    digitalWrite(ML_Ctrl, LOW); // 左モーターの方向制御速度をLOWに設定する
    analogWrite(ML_PWM, 100); // 左モーターのPWM制御速度は100
    digitalWrite(MR_Ctrl, LOW); // 右モーターの方向制御速度をLOWに設定する
    analogWrite(MR_PWM, 100); // 右モーターのPWM制御速度は100
    delay(2000);// 2秒間待機

    // 左折
    digitalWrite(ML_Ctrl, LOW); // 左モーターの方向制御速度をLOWに設定する
    analogWrite(ML_PWM, 100); // 左モーターのPWM制御速度は100
    digitalWrite(MR_Ctrl, HIGH); // 右モーターの方向制御速度をHIGHに設定する
    analogWrite(MR_PWM, 155); // 右モーターのPWM制御速度は155
    delay(2000);// 2秒間待機

    // 右折
    digitalWrite(ML_Ctrl, HIGH); // 左モーターの方向制御速度をHIGHに設定する
    analogWrite(ML_PWM, 155); // 左モーターのPWM制御速度は155
    digitalWrite(MR_Ctrl, LOW); // 右モーターの方向制御速度をLOWに設定する
    analogWrite(MR_PWM, 100); // 右モーターのPWM制御速度は100
    delay(2000);// 2秒間待機

    // 停止
    digitalWrite(ML_Ctrl, LOW); // 左モーターの方向制御速度をLOWに設定する
    analogWrite(ML_PWM, 0); // 左モーターのPWM制御速度は0
    digitalWrite(MR_Ctrl, LOW); // 右モーターの方向制御速度をLOWに設定する
    analogWrite(MR_PWM, 0); // 右モーターのPWM制御速度は0
    delay(2000);// 2秒間待機
}
```

コードをアップロードすると、モーターの速度が遅くなります。

電流が低いとモーターの回転が遅くなります。