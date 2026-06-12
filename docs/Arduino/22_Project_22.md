### プロジェクト22: 消火タンク


#### **(1)説明:**

スマートタンクのライントラッキング機能については前のプロジェクトで説明しました。このプロジェクトでは炎センサーを使用して消火ロボットを作成します。

車が炎を検知すると、ファンのモーターが回転して火を吹き消します。もちろん、まず超音波センサーと2つの光抵抗をファンモジュールと炎センサーに交換する必要があります。

ライントラッキングスマートカーの具体的なロジックを以下の表に示します：

| 左炎センサー | 右炎センサー | 状態                                          |
| :----------: | :----------: | :---------------------------------------------- |
|    ≤700      |    ≤700      | 車が停止、ファンが回転して炎を吹き消す |
|    ≥700      |    ≥700      | 車が停止、ファンが回転して炎を吹き消す |
|    ≥700      |    ≥700      | 車が停止、ファンが回転して炎を吹き消す |
|    ＞700     |    ＞700     | ファンが停止、車が移動                            |

<span style="color: rgb(255, 76, 65);">**注意:**</span>
1）この実験では火源を使用します。火災を防ぐために可燃物から遠ざけてください。子供は大人の監督のもとで実験してください。安全であることが確認できない場合は、実験を中断してください。
2）炎センサーは耐火性ではありません。炎で直接燃やさないでください。
炎センサーで外部LEDを制御することができます。LEDは引き続きD9に接続されています。火が検知されると、LEDが点灯します。

#### **(2)フローチャート:**

![](media/wps12.png)

#### **(3)接続図:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

#### **(4)テストコード:**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 22
  Fire extinguishing tank
  http://www.keyestudio.com
*/

int flame_L = A1; //左の炎インターフェースをアナログピンA1として定義
int flame_R = A2; //右の炎インターフェースをアナログピンA2として定義
//ライントラッキングセンサーの配線
#define L_pin  11  //左
#define M_pin  7  //中央
#define R_pin  8  //右
//サーボ130のピン
int INA = 12;
int INB = 13;
#define ML_Ctrl 4  //左モーターの方向制御ピンを定義
#define ML_PWM 6   //左モーターのPWM制御ピンを定義
#define MR_Ctrl 2  //右モーターの方向制御ピンを定義
#define MR_PWM 5   //右モーターのPWM制御ピンを定義
int L_val, M_val, R_val, flame_valL, flame_valR;

void setup()
{
  Serial.begin(9600);
  //ライントラッキングセンサーの全ピンを入力モードに設定
  pinMode(L_pin, INPUT);
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  //炎センサーをINPUTとして定義
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
  //モーターをOUTPUTとして定義
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  pinMode(INA, OUTPUT);//デジタルポートINAをOUTPUTに設定
  pinMode(INB, OUTPUT);//デジタルポートINBをOUTPUTに設定
}

void loop () 
{
  //炎センサーのアナログ値を読み取る
  flame_valL = analogRead(flame_L);
  flame_valR = analogRead(flame_R);
  Serial.print(flame_valL);
  Serial.print("  ");
  Serial.print(flame_valR);
  Serial.println("  ");
//  delay(500);
  if (flame_valL <= 700 || flame_valR <= 700) 
  {
    Car_Stop();
    fan_begin();
  } 
  else 
  {
    fan_stop();
    L_val = digitalRead(L_pin); //左センサーの値を読み取る
    M_val = digitalRead(M_pin); //中央センサーの値を読み取る
    R_val = digitalRead(R_pin); //右センサーの値を読み取る
    
    if (M_val == 1)  //中央が黒線を検知
    {
      if (L_val == 1 && R_val == 0)  //左に黒線を検知し、右に検知しない場合、左折
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  //右に黒線を検知し、左に検知しない場合、右折
      {
        Car_right();
      }
      else  //それ以外は前進
      {
        Car_front();
      }
    }
    else  //中央が黒線を検知しない
    {
      if (L_val == 1 && R_val == 0)  //左に黒線を検知し、右に検知しない場合、左折
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  //右に黒線を検知し、左に検知しない場合、右折
      {
        Car_right();
      }
      else  //それ以外は停止
      {
        Car_Stop();
      }
    }
  }
}

void fan_stop() 
{
  //回転停止
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

void fan_begin() 
{
  //ファン回転
  digitalWrite(INA, LOW);
  digitalWrite(INB, HIGH);
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 150);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 150);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
  
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)テスト結果:**

テストコードを正常にアップロードして電源を入れると、スマートカーは炎を検知したときに消火し、引き続き黒線に沿って移動します。

![](media/694677ab33053846ec588667dc40ecfa.jpeg)

<span style="color: rgb(255, 76, 65);">**注意:**</span>
火災を防ぐために可燃物から遠ざけてください。子供は大人の監督のもとで実験してください。安全であることが確認できない場合は、実験を中断してください。炎センサーは耐火性ではありません。炎で直接燃やさないでください。