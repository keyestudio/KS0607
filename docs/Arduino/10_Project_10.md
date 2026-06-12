### プロジェクト10：ライトフォロータンク


#### **(1)概要：**

前回のプロジェクトでは、スマートカーに搭載されている各種センサー、モジュール、拡張ボードの使い方について詳しく説明しました。ここからはスマートカーを使ったプロジェクトに移ります。ライトフォロースマートカーとは、その名の通り光を追いかけることができるスマートカーです。

フォトレジスターとモータードライブのプロジェクトで学んだ知識を組み合わせて、光追尾スマートカーを作ることができます。このプロジェクトでは、2つのフォトレジスターモジュールを使用してスマートカーの左右の光の強度を検出し、対応するアナログ値を読み取り、その2つのデータに基づいて2つのモーターの回転を制御することで、スマートカーの動きを制御します。

ライトフォロースマートカーの具体的なロジックは以下の通りです。

![](./media/image-20250709111733042.png)

#### **(2)フローチャート：**

![](media/wps8.png)

#### **(3)接続図：**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">注意：</span> 左フォトレジスターモジュールのピン「G」、「V」、Sはそれぞれ G (GND)、V (VCC)、A1 に接続されています；

右フォトレジスターモジュールのピン「G」、「V」、Sはそれぞれ G (GND)、V (VCC)、A2 に接続されています。

4ピンケーブルにはA、A1、B1、Bの表示があります。右後方モーターは8833モータードライバー拡張ボードのBポートに接続し、左前方モーターはAポートに接続します。

#### **(4)テストコード：**

(<span style="color: rgb(255, 76, 65);">**注意：**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 10
  light follow tank
  http://www.keyestudio.com
*/
#define light_L_Pin A1   //左側の光センサーのピンを定義する
#define light_R_Pin A2   //右側の光センサーのピンを定義する
#define ML_Ctrl 4  //左モーターの方向制御ピンを定義する
#define ML_PWM 6   //左モーターのPWM制御ピンを定義する
#define MR_Ctrl 2  //右モーターの方向制御ピンを定義する
#define MR_PWM 5   //右モーターのPWM制御ピンを定義する
int left_light;
int right_light;
void setup() 
{
  Serial.begin(9600);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop() 
{
  left_light = analogRead(light_L_Pin);
  right_light = analogRead(light_R_Pin);
  Serial.print("left_light_value = ");
  Serial.println(left_light);
  Serial.print("right_light_value = ");
  Serial.println(right_light);
  if (left_light > 650 && right_light > 650) //前進
  {
    Car_front();
  }
  else if (left_light > 650 && right_light <= 650)  //左折
  {
    Car_left();
  }
  else if (left_light <= 650 && right_light > 650) //右折
  {
    Car_right();
  }
  else  //それ以外は停止
  {
    Car_Stop();
  }
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)テスト結果**

テストコードのアップロードが完了し、配線図通りに接続し、DIPスイッチを右端に切り替えて電源を入れると、スマートカーは光を追いかけて動きます。

![Img](./media/img-20240117090537.png)