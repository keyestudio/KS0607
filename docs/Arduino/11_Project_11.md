### プロジェクト 11: 超音波追従タンク


#### **(1)説明:**

前回のレッスンでは、光追従スマートカーについて学びました。このレッスンでは、その知識を組み合わせて超音波音追従カーを作ることができます。

このプロジェクトでは、超音波センサーを使用してカーと前方の障害物との距離を検出し、そのデータに基づいて2つのモーターの回転を制御し、スマートカーの動きを制御します。

超音波音追従スマートカーの具体的なロジックを以下の表に示します：

|                        検出                        |              設定              |
| :-----------------------------------------------------: | :-------------------------------: |
| カーと前方の障害物との距離(cm) | サーボの角度を90°に設定 |
|                      **条件**                      |           **動作**            |
|               distance≥20 かつ distance≤50               |             前進              |
|            10＜distance＜20<br/>distance＞50            |               停止                |
|                       distance≤10                       |              後退              |

#### **(2)フローチャート:**

![](media/wps9.png)

#### **(3)接続図:**

![](media/72a10097d286bc5f9589df031b60484a.png)

#### **(4)テストコード:**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードに失敗する可能性があります。)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 11
  Ultrasonic follow tank
  http://www.keyestudio.com
*/
#define servoPin 10  //サーボのピン

#define ML_Ctrl 4  //左モーターの方向制御ピンを定義
#define ML_PWM 6   //左モーターのPWM制御ピンを定義
#define MR_Ctrl 2  //右モーターの方向制御ピンを定義
#define MR_PWM 5   //右モーターのPWM制御ピンを定義
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //サーボの角度を90°に設定
  delay(500); //500msの遅延
}

void loop() 
{
  distance = checkdistance();  //超音波で測定した距離をdistanceに代入
  if (distance >= 20 && distance <= 50) //前進
  {
    Car_front();
  }
  else if (distance > 10 && distance < 20)  //停止
  {
    Car_Stop();
  }
  else if (distance <= 10)  //後退
  {
    Car_back();
  }
  else  //その他の条件では停止
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
    pulsewidth = myangle * 11 + 500;  //パルス幅の値を計算    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //ハイレベルの時間がパルス幅を表す
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //サイクルは20msなので、残りの時間はローレベル
  }
}
//超音波を制御する関数
float checkdistance() 
{
  static float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //58.20は2*29.1=58.2から来ている
  delay(10);
  return distance;
}
```

#### **(5)テスト結果:**

テストコードを正常にアップロードし、配線して、DIPスイッチを右端に切り替え、電源を入れてサーボを90°に設定すると、スマートカーは障害物に追従して移動します。

![](./media/img-20240117090457.png)