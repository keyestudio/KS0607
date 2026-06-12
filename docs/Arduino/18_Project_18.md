### プロジェクト 18: BT スピードコントロールロボット

#### (1)**説明:**

前のプロジェクトでは、Bluetooth を使用してスマートタンクを制御する方法を学びました。前で使用したモーターの PWM 値は 200 でした（速度は 200）。

このレッスンでは、Bluetooth を使用してスマートカーの速度を調整します。200 の固定速度に限定されません。左右のモーターの速度値をそれぞれ格納するために 2 つの変数を定義します。これまでの学習を通じて、この値の範囲は 0 から 255 までしか取れないことがわかっています。

#### **(2)フローチャート:**

![](media/image-20230427102042028.png)

#### **(3)接続図:**

![](media/930a8024364e07505e845624a94c27bd.png)

8x16 LED ドットマトリクスの GND、VCC、SDA、SCL はそれぞれ拡張ボードの -（GND）、+（VCC）、SDA、SCL に接続されています。

#### **(4)テストコード:**

(<span style="color: rgb(255, 76, 65);">注意:</span> コードをアップロードする際は、Bluetooth モジュールを必ず取り外してください。アップロード完了後に Bluetooth を再接続できます。そうしないとコードが書き込めない場合があります。)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 18
  bluetooth control speed tank
  http://www.keyestudio.com
*/

// 配列：画像データの保存に使用。自分で計算するかモジュールツールから取得できます
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char speed_a[] = {0x00, 0x00, 0x00, 0x20, 0x10, 0x08, 0x04, 0x02, 0xff, 0x02, 0x04, 0x08, 0x10, 0x20, 0x00, 0x00};
unsigned char speed_d[] = {0x00, 0x00, 0x00, 0x04, 0x08, 0x10, 0x20, 0x40, 0xff, 0x40, 0x20, 0x10, 0x08, 0x04, 0x00, 0x00};
#define SCL_Pin  A5  // クロックのピンを A5 に設定
#define SDA_Pin  A4  // データピンを A4 に設定

#define ML_Ctrl 4  // 左モーターの方向制御ピンを定義
#define ML_PWM 6   // 左モーターの PWM 制御ピンを定義
#define MR_Ctrl 2  // 右モーターの方向制御ピンを定義
#define MR_PWM 5   // 右モーターの PWM 制御ピンを定義
char ble_val;      // 右モーターの PWM 制御ピンを定義
byte speeds_L = 200; // 左モーターの初期速度は 200
byte speeds_R = 200; // 右モーターの初期速度は 200
String speeds_l, speeds_r; // PWM の文字列を受信して整数の PWM 値に変換する

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
  matrix_display(start01);  // スタート画像を表示
}

void loop() 
{
  if (Serial.available() > 0) 
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
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
      case 'u':  // u で始まり # で終わる文字列を受信し、整数値に変換する
        speeds_l = Serial.readStringUntil('#');
        speeds_L = String(speeds_l).toInt();
        break;
      case 'v':  // v で始まり # で終わる文字列を受信し、整数値に変換する
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt();
        break;
    }
  }
}

/***************モーターを動かす関数***************/

void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  // 後退
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  // 前進画像を表示
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  // 左折画像を表示
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
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

// ドットマトリクス画面表示に使用する関数
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // データ転送開始条件を呼び出す関数
  IIC_send(0xc0);  // アドレスを選択
  for (int i = 0; i < 16; i++) // パターンデータは 16 バイト
  {
    IIC_send(matrix_value[i]); // パターンデータを転送
  }
  IIC_end();   // パターンデータ転送を終了
  IIC_start();
  IIC_send(0x8A);  // 表示制御、パルス幅を 4/16 に選択
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
  for (byte mask = 0x01; mask != 0; mask <<= 1) // 各文字は 8 桁あり、1 つずつ検出される
  {
    if (send_data & mask)  // 各ビット（0 または 1）に応じてハイまたはローレベルを設定
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // クロックピン SCL_Pin をハイにしてデータ転送を停止
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // クロックピン SCL_Pin をローにして SDA の信号を変化させる
  }
}
```

#### **(5)テスト結果:**

テストコードのアップロードが完了したら、DIP スイッチを右端に切り替えて電源を入れ、APP と Bluetooth をペアリングすると、APP でスマートカーの動きを制御できます。また、左右のモーターのスピードダイヤルを引くことでカーの速度を調整できます。

![](media/b9c902b937801f829b9ce2fd254b1849.jpeg)

（プロジェクト 17 の機能一覧表を参照してください）