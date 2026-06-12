### プロジェクト14：ライントラッキングタンク


#### **(1)概要：**

前のプロジェクトでは、スマートカーを特定のスペース内で移動させる方法を紹介しました。このプロジェクトでは、これまでに学んだ知識を活用して、ライントラッキングスマートカーを作成します。実験では、ライントラッキングセンサーを使用してスマートカーの周囲に黒線があるかどうかを検出し、その検出結果に基づいて2つのモーターの回転を制御することで、スマートカーが黒線に沿って移動できるようにします。

ライントラッキングスマートカーの具体的なロジックを以下の表に示します：

|               センサー               |                          検出内容                           |
| :--------------------------------: | :----------------------------------------------------------: |
| 中央のライントラッキングセンサー | 黒線を検出：ハイレベル<br />白線を検出：ローレベル |
|  左のライントラッキングセンサー  | 黒線を検出：ハイレベル<br />白線を検出：ローレベル |
| 右のライントラッキングセンサー  | 黒線を検出：ハイレベル<br />白線を検出：ローレベル |

|                         条件1                          |                         条件2                          |             動作             |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :------------------------------: |
| 中央のライントラッキングセンサーが<br />黒線を検出 | 左のライントラッキングセンサーが黒線を検出<br />かつ<br />右のセンサーが白線を検出 | 左回転<br />PWMを200に設定  |
| 中央のライントラッキングセンサーが<br />黒線を検出 | 左のライントラッキングセンサーが白線を検出<br />かつ<br />右のセンサーが黒線を検出 | 右回転<br />PWMを200に設定 |
| 中央のライントラッキングセンサーが<br />黒線を検出 | 左右両方のライントラッキングセンサーが白線を検出<br />または<br />左右両方が黒線を検出 |           前進           |
| 中央のライントラッキングセンサーが<br />白線を検出  | 左のライントラッキングセンサーが黒線を検出<br />かつ<br />右のセンサーが白線を検出 | 左回転<br />PWMを200に設定  |
| 中央のライントラッキングセンサーが<br />白線を検出  | 左のライントラッキングセンサーが白線を検出<br />かつ<br />右のセンサーが黒線を検出 | 右回転<br />PWMを200に設定 |
| 中央のライントラッキングセンサーが<br />白線を検出  | 左右両方のライントラッキングセンサーが白線を検出<br />または<br />左右両方のライントラッキングセンサーが黒線を検出 |               停止               |

#### **(2)フローチャート：**

![](media/wps11.png)

#### **(3)配線図：**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)テストコード：**

（<span style="color: rgb(255, 76, 65);">**注意：**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。）

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 14
  Line track tank
  http://www.keyestudio.com
*/

//ライントラッキングセンサーの配線
#define L_pin  11  //左
#define M_pin  7  //中央
#define R_pin  8  //右
#define ML_Ctrl 4  //左モーターの方向制御ピンを定義
#define ML_PWM 6   //左モーターのPWM制御ピンを定義
#define MR_Ctrl 2  //右モーターの方向制御ピンを定義
#define MR_PWM 5   //右モーターのPWM制御ピンを定義
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); //ボーレートを9600に設定
  pinMode(L_pin, INPUT); //ライントラッキングセンサーの全ピンを入力モードに設定
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); //左センサーの値を読み取る
  M_val = digitalRead(M_pin); //中央センサーの値を読み取る
  R_val = digitalRead(R_pin); //右センサーの値を読み取る
  if (M_val == 1) { //中央センサーが黒線を検出
    if (L_val == 1 && R_val == 0)  //左で黒線を検出し、右では検出しない場合、左折
    {
      Car_left();
    }
    else if (L_val == 0 && R_val == 1)  //右で黒線を検出し、左では検出しない場合、右折
    {
      Car_right();
    }
    else  //それ以外の場合、前進
    {
      Car_front();
    }
  }
  else  //中央センサーが黒線を検出しない
  {
    if (L_val == 1 && R_val == 0)  //左で黒線を検出し、右では検出しない場合、左折
    {
      Car_left();
    }
    else if (L_val == 0 && R_val == 1)  //右で黒線を検出し、左では検出しない場合、右折
    {
      Car_right();
    }
    else  //それ以外の場合、停止
    {
      Car_Stop();
    }
  }
}

//前進
void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

//後退
void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

//左折
void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

//右折
void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

//停止
void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)テスト結果：**

テストコードのアップロードが成功し、電源を入れると、スマートカーは黒線に沿って移動します。

![](./media/img-20240117085916.png)