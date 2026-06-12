### プロジェクト 17: Bluetoothコントロールタンク


#### **(1)概要:**

前のプロジェクトでBluetoothの基本知識を学びました。このレッスンでは、Bluetoothを使用してスマートカーを制御します。Bluetoothが関係するため、送信側と受信側が必要です。このプロジェクトでは、携帯電話を送信側（マスター）として使用し、HM-10 Bluetoothモジュールを接続したスマートカー（スレーブ）を受信側として使用します。

以前、ビットを送信してLEDを制御できることを学びました。このロボットカーを制御する原理も同じです。

まずAPP上の各ボタンの機能を理解し、次にAPP上のボタンを使ってタンクを制御します。

#### **(2)APP上のキー機能**

以下の表は対応するキーの機能を示しています：

|                      キー                       | 機能                                                         |
| :---------------------------------------------: | ------------------------------------------------------------ |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) | HM-10 Bluetoothモジュールとペアリングして接続する；もう一度クリックすると切断 |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) | 操作するロボットを選択する                                   |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) | ボタンでロボットの動きを制御する                             |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) | ジョイスティックでロボットの動きを制御する                   |
| ![](media/3ab61154b4ae730a3757f40171846825.png) | 重力でロボットの動きを制御する                               |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) | 押すと"F"を送信し、離すと"S"を送信<br />押している間は前進し、離すと停止 |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) | 押すと"L"を送信し、離すと"S"を送信<br />押している間は左折し、離すと停止 |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) | 押すと"R"を送信し、離すと"S"を送信<br />押している間は右折し、離すと停止 |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) | 押すと"B"を送信し、離すと"S"を送信<br />押している間は後退し、離すと停止 |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) | ドラッグすると"u"+数字+"\#"を送信<br />ドラッグして左モーターの速度を変更 |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) | ドラッグすると"v"+数字+"\#"を送信<br />ドラッグして右モーターの速度を変更 |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) | 機能ページへ進むを選択                                       |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | 押すと"G"を送信し、もう一度押すと"S"を送信<br />押すと障害物回避モードに入り、もう一度押すと終了 |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | 押すと"h"を送信し、もう一度押すと"S"を送信<br />押すと追従モードに入り、もう一度押すと終了 |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | 押すと"e"を送信し、もう一度押すと"S"を送信<br />押すとライントレースモードに入り、もう一度押すと終了 |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | 押すと"f"を送信し、もう一度押すと"S"を送信<br />押すと限られたスペース内移動モードに入り、もう一度押すと終了 |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | 押すと"i"を送信し、もう一度押すと"S"を送信<br />押すと光追従モードに入り、もう一度押すと終了 |
| ![](media/4250a152c647cc59f72bf51328943371.png) | 押すと"j"を送信し、もう一度押すと"S"を送信<br />押すと消火モードに入り、もう一度押すと終了 |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | 顔の表情表示モードに入るを選択                               |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | 押すと"k"を送信し、もう一度押すと"z"を送信<br />クリックすると笑顔パターンを表示し、もう一度クリックすると表情をクリア |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | 押すと"l"を送信し、もう一度押すと"z"を送信<br />クリックすると嫌悪パターンを表示し、もう一度クリックすると表情をクリア |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | 押すと"m"を送信し、もう一度押すと"z"を送信<br />クリックすると喜び顔を表示し、もう一度クリックすると表情をクリア |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | 押すと"n"を送信し、もう一度押すと"z"を送信<br />クリックすると悲しいパターンを表示し、もう一度クリックすると表情をクリア |
| ![](media/5e84087020b919a85495831b231efa5a.png) | 押すと"o"を送信し、もう一度押すと"z"を送信<br />クリックすると軽蔑パターンを表示し、もう一度クリックすると表情をクリア |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | 押すと"p"を送信し、もう一度押すと"z"を送信<br />クリックするとハート型パターンを表示し、もう一度クリックすると表情をクリア |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) | カスタム機能インターフェースに入るを選択；1,2,3,4,5,6の6つのキーがあり、これらのキーで機能を自分で拡張できる |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) | クリックすると"w"を送信<br />クリックすると左側の光センサーで検出されたアナログ値を表示 |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) | クリックすると"y"を送信<br />クリックすると右側の光センサーで検出されたアナログ値を表示 |
| ![](media/a76df707b84409e57a1167889c3510d9.png) | クリックすると"x"を送信<br />クリックすると超音波センサーで検出された距離を表示（単位：cm） |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | クリックすると"c"を送信し、もう一度クリックすると"d"を送信<br />押すとファンをオンにし、もう一度押すとオフにする |

#### **(3)フローチャート:**

![](media/image-20230427101759352.png)

#### **(4)配線図:**

![](media/930a8024364e07505e845624a94c27bd.png)

8x16 LEDドットマトリクスのGND、VCC、SDA、SCLは、それぞれ拡張ボードの-（GND）、+（VCC）、SDA、SCLに接続されています；

BluetoothモジュールのSTATEピンとBRKピンは接続する必要がありません。

#### **(5)テストコード:**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする際、Bluetoothモジュールを必ず取り外してください。アップロード完了後にBluetoothを再接続できます。そうしないと、コードのアップロードが失敗する可能性があります。)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 17.
  bluetooth Control tank
  http://www.keyestudio.com
*/

// 配列、画像データの保存に使用。自分で計算するかモジュールツールから取得できる
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  // クロックピンをA5に設定
#define SDA_Pin  A4  // データピンをA4に設定

#define ML_Ctrl 4  // 左モーターの方向制御ピンを定義
#define ML_PWM 6   // 左モーターのPWM制御ピンを定義
#define MR_Ctrl 2  // 右モーターの方向制御ピンを定義
#define MR_PWM 5   // 右モーターのPWM制御ピンを定義
char ble_val;      // Bluetoothで取得した値を保存するために使用

void setup() 
{
  Serial.begin(9600);

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // 画面をクリア
  matrix_display(start01);  // 開始画像を表示
}

void loop() 
{
  if (Serial.available())
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
  }
  switch (ble_val)
  {
    case 'F':  // 前進コマンド
      Car_front();
      break;
    case 'B':  // 後退コマンド
      Car_back();
      break;
    case 'L':  // 左折コマンド
      Car_left();
      break;
    case 'R':  // 右折コマンド
      Car_right();
      break;
    case 'S':  // 停止コマンド
      Car_Stop();
      break;
  }
}

/***************モーターを動かす関数***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  // 後退画像を表示
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(front);  // 前進画像を表示
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  // 左折画像を表示
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  // 右折画像を表示
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // 停止画像を表示
}

// この関数はドットマトリクス画面の表示に使用される
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // データ転送開始条件の関数を呼び出す
  IIC_send(0xc0);  // アドレスを選択
  for (int i = 0; i < 16; i++) // パターンデータは16バイト
  {
    IIC_send(matrix_value[i]); // パターンデータを転送
  }
  IIC_end();   // パターンデータ転送を終了
  IIC_start();
  IIC_send(0x8A);  // 表示制御、パルス幅を4/16として選択
  IIC_end();
}

// データ転送開始の条件
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// データ転送終了のサイン
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

// データを転送する
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // 各文字は8桁あり、1つずつ検出される
  {
    if (send_data & mask)  // 各ビット（0または1）に応じてHIGHまたはLOWレベルを設定
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // クロックピンSCL_PinをHIGHにしてデータ転送を停止
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // クロックピンSCL_PinをLOWにしてSDAの信号を変更
  }
}
```

#### **(6)テスト結果:**

コードをアップロードした後、ロボットをBluetoothモジュールに接続し、Bluetooth APPとペアリングします。モータードライブシールドの電源スイッチをオンにします。ロボットを床に置き、Bluetooth APPのボタンを使用してロボットを制御できます。

![](media/4655aeffe0d2081fa2b9fd254113c392.jpeg)

1. 上下左右の矢印は、それぞれロボットを前進、後退、左折、右折させます。


![](./media/img-20240117095345.png)

2. ジョイスティックボタンをクリックし、白い円の中の黒い点の方向を引っ張ってロボットの移動方向を制御します。

![](./media/img-20240117095401.png)

3. 重力ボタンをクリックし、前後左右の方向に携帯電話を傾けると、ロボットは携帯電話が傾いた方向に移動します。

![](./media/img-20240117095419.png)