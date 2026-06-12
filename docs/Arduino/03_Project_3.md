### プロジェクト3：フォトレジスタ

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)概要：**

光感知抵抗（フォトレジスタ）は、硫化物やセレンなどの半導体材料で作られた特殊な抵抗で、光導電効果を持つ防湿樹脂でコーティングされています。光感知抵抗は周囲の光に最も敏感で、照明の強さが異なると、光感知抵抗の抵抗値も異なります。光感知抵抗を使用して光感知抵抗モジュールを設計します。

モジュールの信号はマイクロコントローラのアナログポートに接続されます。光の強度が強いほど、アナログポートの電圧が大きくなり、つまりマイクロコントローラのシミュレーション値も大きくなります。逆に、光の強度が弱いほど、アナログポートの電圧が小さくなり、つまりマイクロコントローラのシミュレーション値も小さくなります。

このようにして、光感知抵抗モジュールを使用して対応するアナログ値を読み取り、環境内の光の強度を検知することができます。

![](media/7784e14e15402644cdbe674d500327c4.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)パラメータ：**

光感知抵抗の抵抗値：5K Ou-0.5m

インターフェースタイプ：シミュレーションポート A0、A1

動作電圧：3.3V-5V

ピン間隔：2.54mm


#### **(3)接続図：**

次にテストするのはロボットの左側にある光感知抵抗モジュールです。

![](./media/img-20240117091559.png)

左側の光感知抵抗はモータードライブシールドの A1/P3 に接続されています。

![](media/484852a36f52bdbe44bec1b9a8941e44.png)

#### **(4)テストコード：**

（<span style="color: rgb(255, 76, 65);">**注意：**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードにもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する場合があります。）

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.1

photocell

http://www.keyestudio.com

*/

int sensorPin = A1; // A1はフォトレジスタの入力ピン

int sensorValue = 0; // フォトレジスタの値を保存する

void setup() 
{
	Serial.begin(9600); // シリアルポートモニターを開き、ボーレートを9600に設定する
}

void loop() 
{
	sensorValue = analogRead(sensorPin); // フォトレジスタセンサーからアナログ値を読み取る
	Serial.println(sensorValue); // シリアルポートにフォトレジスタの値を出力する
	delay(500); // 500msの遅延
}
```

#### **(5)テスト結果：**

![](media/54b92578e3210999e23f5fb8138f0fa0.png)

覆うと値が小さくなり、覆わない場合は値が大きくなります。

#### **(6)コードの説明：**

**analogRead(sensorPin)**：フォトレジスタのアナログ値を読み取る

**Serial.begin(9600)**：シリアルポートを初期化し、ボーレートを9600に設定する

**Serial.println**：シリアル出力

#### **(7)応用練習：**

上記のコードはフォトレジスタの値を読み取るだけです。光感知とLEDを組み合わせてLEDを変化させることができます。フォトレジスタでLEDの明るさを制御してみましょう。

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

LEDの明るさはPWMで制御されます。そのため、LEDをシールドのPMWピン（ピン9）に接続します。

**テストコード**

（<span style="color: rgb(255, 76, 65);">**注意：**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードにもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する場合があります。）

```c
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.2

photocell-analog output

http://www.keyestudio.com

*/

int analogInPin = A1; // A1はフォトレジスタの入力ピン

int analogOutPin = 9; // デジタルポート9がPMWの出力

int sensorValue = 0; // フォトレジスタの抵抗値の変数を保存する

int outputValue = 0; // PMWへの出力値

void setup() 
{
	Serial.begin(9600); // シリアルポートモニターを開き、ボーレートを9600に設定する
}

void loop() 
{
    sensorValue = analogRead(analogInPin); // フォトレジスタセンサーからアナログ値を読み取る
    // アナログ値0\~1023をPWM出力値255\~0にマッピングする
    outputValue = map(sensorValue, 0, 1023, 255, 0);
    // アナログ出力を変更する
    analogWrite(analogOutPin, outputValue);
    Serial.println(sensorValue); // シリアルポートにフォトレジスタの値を出力する
    delay(2);
}
```

開発ボードにコードをアップロードし、フォトレジスタを覆ってLEDの明るさの変化を観察してください。

![](./media/img-20240117091105.png)