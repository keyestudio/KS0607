### プロジェクト 23: 消火ロボット 複合機能


#### **(1)説明:**

スマートカーはこれまでのプロジェクトで毎回単一の機能を実行してきました。

複数の機能を同時に実行できるでしょうか？もちろんできます。

この最後の大きなプロジェクトでは、完全なコードを使用してスマートカーを制御し、これまでのプロジェクトで紹介したすべての機能を披露するつもりです。Bluetooth APPのキーを使って各種機能を自動的に切り替えます。非常にシンプルで便利です。



#### **(2)フロー図:**

<span style="color: rgb(255, 76, 65);">**Bluetooth APPのインストールと設定については、プロジェクト16を参照してください**</span>

![](media/image-20230427102547633.png)

#### **(3)接続図:**

![](media/e7ac834ba04aa2e8862995d2d33ce9356.jpg)

1\. 8x16ボードのGND、VCC、SDA、SCLは、拡張ボードのG（GND）、+（VCC）、A4、A5に接続します。

2\. ファンモジュールのVCC、IN+、IN-、Gndは、5V（V）、12（S）、13（S）、Gnd（G）に接続します。

3\. サーボのブラウン線、レッド線、オレンジ線は、Gnd（G）、5v（V）、D10に接続します。

4\. BTモジュールのRXD、TXD、GND、VCCは、TX、RX、G（GND）、5V（VCC）に接続します。STATEとBRKは接続不要です。

5\. 左炎センサーのピン「G」、「V」、Aはそれぞれ G（GND）、V（VCC）、A1に接続します。右炎センサーはG（GND）、V（VCC）、A2にそれぞれ接続します。

6\. ライントラッキングセンサーの遠端ポートは11、7、8です。

#### **(4)テストコード:**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードにもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 23
  Fire Extinguishing Robot Multiple Functions
  http://www.keyestudio.com
*/
#include <IRremote.h>
IRrecv irrecv(3);  //
decode_results results;
long ir_rec;  // IR値を保存するために使用

/***********/
#define USE_FAN_FUNCTION   1

// 配列、画像データを保存するために使用。自分で計算するかモジュラスツールから取得できます
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

unsigned char Smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};
unsigned char Disgust[] = {0x00, 0x00, 0x02, 0x02, 0x02, 0x12, 0x08, 0x04, 0x08, 0x12, 0x22, 0x02, 0x02, 0x00, 0x00, 0x00};
unsigned char Happy[] = {0x02, 0x02, 0x02, 0x02, 0x08, 0x18, 0x28, 0x48, 0x28, 0x18, 0x08, 0x02, 0x02, 0x02, 0x02, 0x00};
unsigned char Squint[] = {0x00, 0x00, 0x00, 0x41, 0x22, 0x14, 0x48, 0x40, 0x40, 0x48, 0x14, 0x22, 0x41, 0x00, 0x00, 0x00};
unsigned char Despise[] = {0x00, 0x00, 0x06, 0x04, 0x04, 0x04, 0x24, 0x20, 0x20, 0x26, 0x04, 0x04, 0x04, 0x04, 0x00, 0x00};
unsigned char Heart[] = {0x00, 0x00, 0x0C, 0x1E, 0x3F, 0x7F, 0xFE, 0xFC, 0xFE, 0x7F, 0x3F, 0x1E, 0x0C, 0x00, 0x00, 0x00};

unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  // クロックのピンをA5に設定
#define SDA_Pin  A4  // データピンをA4に設定

#define ML_Ctrl 4  // 左モーターの方向制御ピンを4に定義
#define ML_PWM 6   // 左モーターのPWM制御ピンを定義
#define MR_Ctrl 2  // 右センサーの方向制御ピンを定義
#define MR_PWM 5   // 右モーターのPWM制御ピンを定義
char ble_val;      // Bluetooth値を保存するために使用
byte speeds_L = 200; // 左モーターの初期速度は200
byte speeds_R = 200; // 右モーターの初期速度は200
String speeds_l, speeds_r; // PWM文字を受信してPWM値に変換

// ライントラッキングセンサーの配線
#define L_pin  11  // 左
#define M_pin  7  // 中央
#define R_pin  8  // 右
int L_val, M_val, R_val;

#if USE_FAN_FUNCTION  /****ファンを使用*******/
int flame_L = A1; // 左炎センサーのアナログポートをA1に定義
int flame_R = A2; // 右炎センサーのアナログポートをA2に定義
int flame_valL, flame_valR;

// 130モーターのピン
int INA = 12;
int INB = 13;

#else /****超音波センサーを使用*******/
#define servoPin    10  // サーボのピン
#define light_L_Pin A1   // 左フォトレジスタのピンを定義
#define light_R_Pin A2   // 右フォトレジスタのピンを定義
int left_light;
int right_light;

#define Trig 12
#define Echo 13
float distance; // 追従のために超音波で検出した距離値を保存

// 障害物回避のために超音波で検出した距離値を保存
int a;
int a1;
int a2;

#endif

bool flag;  // フラグ変数、モードへの入退出に使用

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  // IRリモートのライブラリを初期化

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(L_pin, INPUT); // センサーのピンをINPUTに定義
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);

  matrix_display(clear);    // 画面をクリア
  matrix_display(start01);  // スタートを表示

#if USE_FAN_FUNCTION/****ファンを使用*******/
  pinMode(INA, OUTPUT); // INAをOUTPUTに設定
  pinMode(INB, OUTPUT); // INBをOUTPUTに設定

  // 炎センサーの入力を定義
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
#else/****超音波センサーを使用*******/
  pinMode(servoPin, OUTPUT);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);

  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  procedure(90); // サーボの角度を90°に設定
#endif
}

void loop() 
{
  if (Serial.available()) // シリアルバッファにデータがある場合
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
    switch (ble_val) 
    {
      case 'F': Car_front(); break; // 前進コマンド

      case 'B': Car_back(); break;  // 後退コマンド

      case 'L': Car_left(); break;  // 左折コマンド

      case 'R': Car_right(); break; // 右折コマンド

      case 'S': Car_Stop();  break; // 停止

      case 'e': Tracking();  break; // ライントラッキングモードに入る

      case 'f': Confinement(); break;  // 閉じ込めモードに入る

#if USE_FAN_FUNCTION/****ファンを使用*******/
      case 'j': Fire(); break;  // 消火モードを有効にする

      case 'c': fan_begin(); break;  // ファンを有効にする

      case 'd': fan_stop();  break;  // ファンをオフにする

#else/****超音波センサーを使用*******/
      case 'g': Avoid(); break;  // 障害物回避モードに入る

      case 'h': Follow(); break;  // 追従モードに入る

      case 'i': Light_following();  break;  // 光追従モードに入る
#endif
      case 'u': 
        speeds_l = Serial.readStringUntil('#'); 
        speeds_L = String(speeds_l).toInt(); 
        break; // uの受信で開始し、文字#の受信で終了して整数に変換

      case 'v': 
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt(); 
        break; // uの受信で開始し、文字#の受信で終了して整数に変換

      case 'k': matrix_display(Smile);    break;  // 「smile（笑顔）」の表情を表示
      case 'l': matrix_display(Disgust);  break;  // 「disgust（嫌悪）」の表情を表示
      case 'm': matrix_display(Happy);    break;  // 「happy（喜び）」の表情を表示
      case 'n': matrix_display(Squint);   break;  // 「Sad（悲しみ）」の表情を表示
      case 'o': matrix_display(Despise);  break;  // 「despise（軽蔑）」の表情を表示
      case 'p': matrix_display(Heart);    break;  // ハートビート画像を表示
      case 'z': matrix_display(clear);    break;  // 画像をクリア

      default: break;
    }
  }

#if (USE_FAN_FUNCTION != 1)/****ファンを使用しない機能*******/
  // 以下の3つの信号は主に循環印刷に使用
  if (ble_val == 'x') 
  {
    distance = checkdistance(); Serial.println(distance);
    delay(50);
  } 
  else if (ble_val == 'w') 
  {
    left_light = analogRead(light_L_Pin);
    Serial.println(left_light);
    delay(50);
  } 
  else if (ble_val == 'y') 
  {
    right_light = analogRead(light_R_Pin);
    Serial.println(right_light);
    delay(50);
  }
#endif

  if (irrecv.decode(&results))  // 赤外線リモコン値を受信
  {
    ir_rec = results.value;
    Serial.println(ir_rec, HEX);
    switch (ir_rec) 
    {
      case 0xFF629D: Car_front();   break;   // 前進
      case 0xFFA857: Car_back();    break;   // 後退
      case 0xFF22DD: Car_left();    break;   // 左回転
      case 0xFFC23D: Car_right();   break;   // 右回転
      case 0xFF02FD: Car_Stop();    break;   // 停止
      default: break;
    }
    irrecv.resume();
  }
}

#if (USE_FAN_FUNCTION != 1)/****超音波センサーを使用*******/

// 超音波センサーを制御
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //
  delay(10);
  return distance;
}


// サーボを制御する関数
void procedure(int myangle) 
{
  int pulsewidth;
  pulsewidth = map(myangle, 0, 180, 500, 2000);  // パルス幅の値を計算。500から2500へのマッピング値にすべきだが、赤外線ライブラリの影響を考慮して500〜2000を使用。
  for (int i = 0; i < 5; i++) 
  {
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   // ハイレベルの持続時間がパルス幅
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  // 周期は20msなので、ローレベルは残りの時間持続
  }
}

/*****************障害物回避******************/
void Avoid()
{
  flag = 0;
  while (flag == 0)
  {
    a = checkdistance();  // 前方距離をaに設定
    if (a < 20) // 前方の距離が20cm未満の場合
    {
      Car_Stop();  // 停止
      delay(500); // 500msの遅延
      procedure(180);  // サーボが左に回転
      delay(500); // 500msの遅延
      a1 = checkdistance();  // 左距離をa1に設定
      delay(100); // 値を読み取る

      procedure(0); // サーボが右に回転
      delay(500); // 500msの遅延
      a2 = checkdistance(); // 右距離をa2に設定
      delay(100); // 値を読み取る

      procedure(90);  // 90°に戻る
      delay(500);
      if (a1 > a2)  // 左の距離が右の距離より大きい場合
      {
        Car_left();  // ロボットが左に回転
        delay(700);  // 700ms左折
      } 
      else 
      {
        Car_right(); // 右折
        delay(700);
      }
    }
    else  // 前方距離が20cm以上の場合、ロボットは前進
    {
      Car_front(); // 前進
    }
    // Bluetooth値を受信してループを終了
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S')  // Sを受信
      {
        flag = 1;  // flagを1に設定してループを終了
        Car_Stop();
      }
    }
  }
}

/*******************追従***************/
void Follow() 
{
  flag = 0;
  while (flag == 0) 
  {
    distance = checkdistance();  // 距離値をdistanceに設定
    if (distance >= 20 && distance <= 60) // 前進
    {
      Car_front();
    }
    else if (distance > 10 && distance < 20)  // 停止
    {
      Car_Stop();
    }
    else if (distance <= 10)  // 後退
    {
      Car_back();
    }
    else  // 停止
    {
      Car_Stop();
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S')
      {
        flag = 1;  // ループを終了
        Car_Stop();
      }
    }
  }
}

/****************光追従******************/
void Light_following() 
{
  flag = 0;
  while (flag == 0) 
  {
    left_light = analogRead(light_L_Pin);
    right_light = analogRead(light_R_Pin);
    if (left_light > 650 && right_light > 650) // 前進
    {
      Car_front();
    }
    else if (left_light > 650 && right_light <= 650)  // 左折
    {
      Car_left();
    }
    else if (left_light <= 650 && right_light > 650) // 右折
    {
      Car_right();
    }
    else  // それ以外は停止
    {
      Car_Stop();
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

#else/****ファンを使用*******/
/***************ファンを有効にする*****************/
void fan_begin() 
{
  digitalWrite(INA, LOW);
  digitalWrite(INB, HIGH);
}

/***************ファンを停止する*****************/
void fan_stop() 
{
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

/***************消火****************/
void Fire() 
{
  flag = 0;
  while (flag == 0) 
  {
    // 炎センサーのアナログ値を読み取る
    flame_valL = analogRead(flame_L);
    flame_valR = analogRead(flame_R);
    if (flame_valL <= 700 || flame_valR <= 700) 
    {
      Car_Stop();
      fan_begin();
    } 
    else 
    {
      fan_stop();
      L_val = digitalRead(L_pin); // 左センサーの値を読み取る
      M_val = digitalRead(M_pin); // 左センサーの値を読み取る
      R_val = digitalRead(R_pin); // 右センサーの値を読み取る
```

```      if (M_val == 1)  //真ん中のセンサーが黒線を検出した場合
      {
        if (L_val == 1 && R_val == 0)  //左側で黒線を検出し、右側では検出しない場合、左折する
        {
          Car_left();
        }
        else if (L_val == 0 && R_val == 1)  //右側で黒線を検出し、左側では検出しない場合、右折する
        {
          Car_right();
        }
        else //直進する
        { 
          Car_front();
        }
      }
      else //真ん中のセンサーが黒線を検出しない場合
      { 
        if (L_val == 1 && R_val == 0) //左側で黒線を検出し、右側では検出しない場合、左折する
        { 
          Car_left();
        }
        else if (L_val == 0 && R_val == 1) //右側で黒線を検出し、左側では検出しない場合、右折する
        { 
          Car_right();
        }
        else //それ以外は停止する
        { 
          Car_Stop();
        }
      }
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

#endif

/***************ライントレース*****************/
void Tracking() 
{
  flag = 0;
  while (flag == 0) 
  {
    L_val = digitalRead(L_pin); //左センサーの値を読み取る
    M_val = digitalRead(M_pin); //中央センサーの値を読み取る
    R_val = digitalRead(R_pin); //右センサーの値を読み取る
    if (M_val == 1)  //真ん中のセンサーが黒線を検出した場合
    {
      if (L_val == 1 && R_val == 0) //左側で黒線を検出し、右側では検出しない場合、左折する
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1) //右側で黒線を検出し、左側では検出しない場合、右折する
      { 
        Car_right();
      }
      else //直進する
      { 
        Car_front();
      }
    }
    else //真ん中のセンサーが黒線を検出しない場合
    { 
      if (L_val == 1 && R_val == 0) //左側で黒線を検出し、右側では検出しない場合、左折する
      { 
        Car_left();
      }
      else if (L_val == 0 && R_val == 1) //右側で黒線を検出し、左側では検出しない場合、右折する
      { 
        Car_right();
      }
      else //それ以外は停止する
      { 
        Car_Stop();
      }
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

/***************エリア制限*****************/
void Confinement() 
{
  flag = 0;
  while (flag == 0) 
  {
    L_val = digitalRead(L_pin); //左センサーの値を読み取る
    M_val = digitalRead(M_pin); //中央センサーの値を読み取る
    R_val = digitalRead(R_pin); //右センサーの値を読み取る
    if ( L_val == 0 && M_val == 0 && R_val == 0 ) //黒線が検出されない場合は直進する   
    {    
        Car_front();
    }
    else 
    { 
      Car_back();
      delay(700);
      Car_left();
      delay(800);
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}


/***************ドットマトリクス******************/
//この関数はドットマトリクスの表示に使用される
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  //データ送信を開始する関数を使用する
  IIC_send(0xc0);  //アドレスを選択する
  for (int i = 0; i < 16; i++) //画像データは16文字ある
  {
    IIC_send(matrix_value[i]); //画像を送信するデータ
  }
  IIC_end();   //画像のデータ送信を終了する
  IIC_start();
  IIC_send(0x8A);  //表示制御とパルス幅4/16の選択
  IIC_end();
}

//データ送信開始の条件
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

//データを送信する
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) //各文字は8桁あり、1つずつ検出される
  {
    if (send_data & mask)  //各ビット（0または1）に応じてハイレベルまたはローレベルを設定する
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); //クロックピンSCL_Pinをプルアップしてデータ送信を終了する
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); //クロックピンSCL_PinをプルダウンしてSDAの信号を変化させる
  }
}

//データ送信終了のサイン
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

/***************モーター動作****************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  //後退の画像を表示する
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  //前進の画像を表示する
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  //左折の画像を表示する
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(right);  //右折の画像を表示する
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  //停止の画像を表示する
}
```

#### (5)テスト結果

プログラムコードをアップロードする前に、Bluetoothモジュールを取り外す必要があります。そうしないと、コードのアップロードが失敗します。

コードのアップロードが完了したら、デバイスの位置情報サービスをオンにして、Bluetoothモジュールに接続します。

Bluetoothモジュールを接続して電源を入れ、モバイルAPPがBluetoothへの接続に成功したら、モバイルAPPを使用してタンクロボットを操作することができます。

リモコンでロボットを操作することもできます。

![](media/13656cfee75dc5acbeba18a90a084e159.jpg)