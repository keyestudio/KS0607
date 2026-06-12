### プロジェクト12：超音波障害物回避タンク

![](./media/image-20250709112200577.png)


#### **(1)概要：**

前のプロジェクトでは、超音波を使った追跡スマートカーを作りました。実際には、同じコンポーネントと同じ配線方法を使い、テストコードを変更するだけで、超音波障害物回避スマートカーに変えることができます。このスマートカーは人の手の動きに合わせて動くことができます。

超音波センサーを使って、スマートカーと前方の障害物との距離を検出し、そのデータに基づいて2つのモーターの回転を制御することで、スマートカーの動きを制御します。

|                          検出                           |        |
| :----------------------------------------------------------: | :----: |
| 超音波センサーで測定したカーと前方の障害物との距離 <br />（サーボの角度を90°に設定） | a(cm)  |
| 超音波センサーで測定したカーと右側の障害物との距離 <br />（サーボの角度を20°に設定） | a2(cm) |
| 超音波センサーで測定したカーと左側の障害物との距離 <br />（サーボの角度を160°に設定） | a1(cm) |
|   **設定：** サーボの開始角度を90°に設定する    |        |

|   条件1   |        条件2         | 条件3 | 動作                                                     |
| :-------------: | :------------------------: | ----------- | ------------------------------------------------------------ |
|      a＜20      |                            |             | 500ms停止；<br />サーボの角度を180°に設定し、a1を読み取り、100msの遅延；<br />サーボの角度を0°に設定し、a2を読み取り、0.1sの遅延。 |
|                 | a1＜50<br />または<br />a2＜50 |             | a1とa2を比較する                                           |
|                 |                            | a1＞a2      | サーボの角度を90°に設定し、700ms左回転（PWMを255に設定）<br />前進（PWMを200に設定）。 |
|                 |                            | a1＜a2      | サーボの角度を90°に設定し、700ms右回転（PWMを255に設定）<br />前進（PWMを200に設定）。 |
| **条件1** |      **条件2**       |             | **動作**                                                 |
|      a＜20      | a1≥50<br />かつ<br />a2≥50  | ランダム      | サーボの角度を90°に設定し、500ms左回転（PWMを255に設定）<br />前進（PWMを200に設定）<br /><br />サーボの角度を90°に設定し、500ms右回転（PWMを255に設定）<br />前進（PWMを200に設定） |
|  **条件**  |                            |             | **動作**                                                 |
|      a≥20       |                            |             | 前進（PWMを100に設定）                                 |



#### **(2)フローチャート：**

![](media/wps10.png)

#### **(3)接続図：**

![](media/72a10097d286bc5f9589df031b60484a.png)

(<span style="color: rgb(255, 76, 65);">注意：</span> サーボの茶色、赤色、オレンジ色のワイヤーはそれぞれ拡張ボードのG（GND）、V（5V）、D10に接続します；超音波センサーについては、VCCピンを5v（V）に、Trigピンをデジタル12（S）に、Echoピンをデジタル13（S）に、GndピンをGnd（G）に接続します；前のプロジェクトと同様です。）

#### **(4)テストコード：**

(<span style="color: rgb(255, 76, 65);">**注意：**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合し、アップロードが失敗する可能性があります。)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 12
  Ultrasonic avoid tank
  http://www.keyestudio.com
*/
#define servoPin 10  //サーボのピン
int a, a1, a2;
#define ML_Ctrl 4  //左モーターの方向制御ピンを定義する
#define ML_PWM 6   //左モーターのPWM制御ピンを定義する
#define MR_Ctrl 2  //右モーターの方向制御ピンを定義する
#define MR_PWM 5   //右モーターのPWM制御ピンを定義する
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  Serial.begin(9600);
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //サーボの角度を90°に設定する
  delay(500); //500ms遅延する
}

void loop() 
{
  a = checkdistance();  //超音波センサーで検出した前方への距離を変数aに代入する

  if (a < 20) //前方への距離が20cm未満の場合
  {
    Car_Stop();  //ロボットが停止する
    delay(500); //500ms遅延する
    procedure(180);  //超音波パンチルトが左を向く
    delay(500); //500ms遅延する
    a1 = checkdistance();  //超音波センサーで検出した左側への距離を変数a1に代入する
    delay(100); //値を読み取る
    procedure(0); //超音波パンチルトが右を向く
    delay(500); //500ms遅延する
    a2 = checkdistance(); //超音波センサーで検出した右側への距離を変数a2に代入する
    delay(100); //値を読み取る
    
    procedure(90);  //90°に戻る
    delay(500);
    if (a1 > a2) 
    { //左側への距離が右側より大きい場合
      Car_left();  //ロボットが左折する
      delay(700);  //700ms左折する
    } 
    else 
    {
      Car_right(); //700ms右折する
      delay(700);
    }
  } 
  else//前方への距離が20cm以上の場合、ロボットは前進する
  {    
    Car_front(); //前進する
  }

}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
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

//サーボを制御する関数
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //パルス幅の値を計算する
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //ハイレベルの時間がパルス幅を表す
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //サイクルは20msなので、残りの時間はローレベルになる
  }
}

//超音波を制御する関数
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //ここでの58.20は2*29.1=58.2から来ている
  delay(10);
  return distance;
}
```

#### **(5)テスト結果：**

テストコードを正常にアップロードし、配線を行い、DIPスイッチをON側に切り替えて電源を入れると、スマートカーは前進しながら自動的に障害物を回避します。

![](./media/img-20240117090420.png)