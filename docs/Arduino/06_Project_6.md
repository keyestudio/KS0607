### プロジェクト6：超音波センサー

#### **(1) 説明:**

![](media/0180b169a1c3b228394b43df704fac32.png)

HC-SR04超音波センサーは、コウモリのようにソナーを使用して物体までの距離を測定します。使いやすいパッケージで、高精度かつ安定した読み取りによる優れた非接触距離検出を提供します。超音波送信モジュールと受信モジュールが一体となっています。

HC-SR04または超音波センサーは、障害物検知や距離測定アプリケーション、その他さまざまなアプリケーションを作成するための幅広い電子プロジェクトで使用されています。ここでは、Arduinoと超音波センサーで距離を測定するシンプルな方法と、Arduinoで超音波センサーを使用する方法を紹介します。

![](./media/image-20250709105712919.png)

#### **(2)パラメータ：**

- 電源：+5V DC

- 静止電流：\<2mA

- 動作電流：15mA

- 有効角度：\<15°

- 測定距離：2cm～400cm

- 分解能：0.3cm

- 測定角度：30度

- トリガー入力パルス幅：10uS


#### **(3) 超音波センサーの原理：**

上の図に示すように、2つの目のようなものです。一方が送信端、もう一方が受信端です。

超音波モジュールは信号をトリガーした後、超音波を放射します。超音波が物体に当たって反射されると、モジュールはエコー信号を出力します。これにより、トリガー信号とエコー信号の時間差から物体までの距離を計算できます。

tは、放射した信号が障害物に当たって返ってくるまでの時間です。空気中の音の伝播速度は約343m/sであり、距離 = 速度 × 時間です。ただし、超音波は放射されて戻ってくるため、距離の2倍になります。そのため2で割る必要があり、**超音波で測定した距離 = (速度 × 時間) / 2** となります。

1. 超音波モジュールの使用方法とタイミングチャート：

2. SR04のTrigピンの遅延時間を少なくとも10μSに設定することで、距離検出をトリガーできます。

3. トリガー後、モジュールは自動的に40KHzの超音波パルスを8回送信し、信号の返答があるかどうかを検出します。このステップはモジュールが自動的に実行します。

4. 信号が返ってきた場合、EchoピンはHighレベルを出力し、そのHighレベルの持続時間が超音波の送信から返却までの時間となります。

![](media/image-20230426172540424.png)

超音波センサーの回路図：

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4)接続図：**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">注意：</span>超音波センサーのVCC、Trig、Echo、Gndピンはそれぞれシールドの5v(V)、12(S)、13(S)、Gnd(G)に接続されています。

#### **(5)テストコード：**

(<span style="color: rgb(255, 76, 65);">**注意：**</span>コードのアップロードにもシリアル通信を使用するため、アップロード前にBluetoothモジュールを接続しないでください。BluetoothのシリアL通信と競合し、アップロードが失敗する場合があります。)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.1
Ultrasonic sensor
http://www.keyestudio.com
*/

int trigPin = 12; // Trigピンを12に接続
int echoPin = 13; // EchoピンをPin 13に接続
long duration, cm, inches;

void setup() 
{
    // シリアルポート開始
    Serial.begin(9600);// ボーレートを9600に設定
    // 入出力の定義
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
}

void loop() 
{
    // クリーンなHighパルスを確保するため、短いLowパルスを事前に与える
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// 少なくとも10usのHighレベルトリガーを与える
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // Highレベルの時間は超音波の送信と受信の時間差に等しい
    duration = pulseIn(echoPin, HIGH);
    // 距離に変換
    cm = (duration / 2) / 29.1; // センチメートルに変換
    inches = (duration / 2) / 74; // インチに変換
    // シリアルポートに出力
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    delay(50);
}
```

#### **(6)テスト結果：**

テストコードを開発ボードにアップロードし、シリアルモニターを開いてボーレートを9600に設定します。検出された距離がcmとインチで表示されます。手で超音波センサーを遮ると、表示される距離の値が小さくなります。

![](media/2ff018e5d9d631a32fce99eb9b4778be.png)

#### **(7)コードの説明：**

**int trigPin = 12;** このピンは超音波を送信するために定義されており、一般的に出力です。

**int echoPin = 13;** これは受信ピンとして定義されており、一般的に入力です。

**cm = (duration/2) / 29.1; inches = (duration/2) / 74; 0.0135で割る**

以下の計算式を使用して距離を計算できます：

distance = (traveltime/2) x speed of sound

音速は：343m/s = 0.0343 cm/uS = 1/29.1 cm/uS

またはインチで：13503.9in/s = 0.0135in/uS = 1/74in/uS

波が送信されて物体に当たり、センサーに戻ってくることを考慮する必要があるため、移動時間を2で割る必要があります。

#### **(8)応用練習：**


超音波で測定した距離を表示する方法を学びました。測定した距離でLEDを制御してみましょう。LEDライトモジュールをD9ピンに接続してみましょう。

![](media/291ac1db0f38418772d11bb1786b7314.png)

**テストコード**

(<span style="color: rgb(255, 76, 65);">**注意：**</span>コードのアップロードにもシリアル通信を使用するため、アップロード前にBluetoothモジュールを接続しないでください。BluetoothのシリアL通信と競合し、アップロードが失敗する場合があります。)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.2
Ultrasonic LED
http://www.keyestudio.com
*/

int trigPin = 12; // TrigをPin 12に接続
int echoPin = 13; // EchoをPin 13に接続
int LED = 9;
long duration, cm, inches;

void setup() 
{
    // シリアルポート開始
    Serial.begin (9600);// ボーレートを9600に設定
    // 入出力の定義
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(LED, OUTPUT);
}

void loop() 
{
    // クリーンなHighパルスを確保するため、短いLowパルスを事前に与える
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// 少なくとも10usのHighレベルトリガーを与える
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // Highレベルの持続時間は超音波の送信から返却までの時間
    duration = pulseIn(echoPin, HIGH);
    // 距離に変換
    cm = (duration / 2) / 29.1; // センチメートルに変換
    inches = (duration / 2) / 74; // インチに変換
    // シリアルポートに出力
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    if (cm >= 2 && cm <= 10) 
    {
    	digitalWrite(LED, HIGH);// LEDを点灯
    } 
    else 
    {
    	digitalWrite(LED, LOW); // LEDを消灯
    }
    delay(50);
}
```

テストコードを開発ボードにアップロードし、手で超音波センサーを遮って、LEDが点灯するか確認してください。

![](./media/img-20240117090734.png)