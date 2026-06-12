### プロジェクト15：IRリモコンタンク

![](./media/image-20250709113214889.png)


#### **(1)説明：**

赤外線リモコンは、電気モーター、電気ファン、その他多くの家電製品に最もよく使われるリモコンの一つです。このプロジェクトでは、これまでに学んだ知識を活用して、赤外線リモコンスマートカーを作成します。

第9レッスンでは、赤外線リモコンの各キーに対応するキー値をテストしました。このプロジェクトでは、コード（キー値）を設定して、対応するボタンでスマートカーの動きを制御し、8X16 LEDドットマトリクスに動作パターンを表示させることができます。

ライントラッキングスマートカーの具体的なロジックを以下の表に示します：

|                        超音波キー                        | キー値 |                    キーからの指示                    |
| :----------------------------------------------------------: | :-------: | :----------------------------------------------------------: |
| ![image-20230427094710725](media/image-20230427094710725.png) |  FF629D   | 前進（PWMを200に設定）<br />前進パターンを表示 |
| ![image-20230427094716639](media/image-20230427094716639.png) |  FFA857   | 後退（PWMを200に設定）<br />後退パターンを表示 |
| ![image-20230427094720417](media/image-20230427094720417.png) |  FF22DD   |           左折<br />「STOP」パターンを表示           |
| ![image-20230427094725151](media/image-20230427094725151.png) |  FFC23D   |     右折<br />左折パターンを表示      |
| ![image-20230427094729839](media/image-20230427094729839.png) |  FF02FD   |             停止<br />「STOP」パターンを表示              |

**初期設定**：8X16 LEDドットマトリクスに「![](media/wps20.jpg)」のパターンを表示します。



#### **(2)フローチャート：**

![](media/wps21.png)

#### **(3)接続図：**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">注意：</span>

8x16 LEDパネルのGND、VCC、SDA、SCLは、拡張ボードのG（GND）、V（VCC）、SDA、SCLに接続されています。

8833ボードにはIR受信機が内蔵されているため、配線する必要はありません。IR受信機のピンはG（GND）、V（VCC）、D3です。

#### (4)**テストコード：**

（<span style="color: rgb(255, 76, 65);">**注意：**</span>コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用しており、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。）

```C
/*
 Keyestudio Mini Tank Robot V3 (Popular Edition)
 lesson 15
 IRremote Control Tank
 http://www.keyestudio.com
*/
#include <IRremote.h>
IRrecv irrecv(3);  //
decode_results results;
long ir_rec;  //受信した赤外線値を格納するために使用

//配列、画像データを保存するために使用。自分で計算するかモジュールツールから取得できます
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  //クロックピンをA5に設定
#define SDA_Pin  A4  //データピンをA4に設定

#define ML_Ctrl 4  //左モーターの方向制御ピンを定義
#define ML_PWM 6   //左モーターのPWM制御ピンを定義
#define MR_Ctrl 2  //右モーターの方向制御ピンを定義
#define MR_PWM 5    //右モーターのPWM制御ピンを定義

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  //赤外線受信ライブラリを初期化

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); //画面をクリア
  matrix_display(start01);  //開始時の画像を表示
}

void loop() 
{
  if (irrecv.decode(&results))  //赤外線リモコン値を受信
  {
    ir_rec = results.value;
    String type = "UNKNOWN";
    String typelist[14] = {"UNKNOWN", "NEC", "SONY", "RC5", "RC6", "DISH", "SHARP", "PANASONIC", "JVC", "SANYO", "MITSUBISHI", "SAMSUNG", "LG", "WHYNTER"};
    if (results.decode_type >= 1 && results.decode_type <= 13) 
    {
      type = typelist[results.decode_type];
    }
    Serial.print("IR TYPE:" + type + "  ");
    Serial.println(ir_rec, HEX);
    irrecv.resume();
  }

  switch (ir_rec) 
  {
    case 0xFF629D: Car_front();     break;   //前進コマンド
    case 0xFFA857: Car_back();      break;   //後退コマンド
    case 0xFF22DD: Car_T_left();    break;   //左折コマンド
    case 0xFFC23D: Car_T_right();   break;   //右折コマンド
    case 0xFF02FD: Car_Stop();      break;   //停止コマンド
    case 0xFF30CF: Car_left();      break;   //左回転コマンド
    case 0xFF7A85: Car_right();     break;   //右回転コマンド
    default: break;
  }
}

/***************モーターを動かす関数***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  //後退
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(front);  //前進画像を表示
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  //左折画像を表示
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  //右折画像を表示
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  //停止画像を表示
}

void Car_T_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
  matrix_display(left);  //左折画像を表示
}

void Car_T_right() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 0);
  matrix_display(right);  //右折画像を表示
}

//この関数はドットマトリクス画面の表示に使用
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  //データ転送開始条件の関数を呼び出す
  IIC_send(0xc0);  //アドレスを選択
  for (int i = 0; i < 16; i++) //パターンデータは16バイト
  {
    IIC_send(matrix_value[i]); //パターンデータを転送
  }
  IIC_end();   //パターンデータ転送を終了
  IIC_start();
  IIC_send(0x8A);  //表示制御、パルス幅を4/16に選択
  IIC_end();
}

//データ転送開始の条件
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
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

//データを転送
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) //各文字は8桁あり、1つずつ検出される
  {
    if (send_data & mask)  //各ビット（0または1）に応じてHIGHまたはLOWレベルを設定
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); //クロックピンSCL_PinをHIGHに引き上げてデータ送信を停止
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); //クロックピンSCL_Pinを引き下げてSDAの信号を変更
  }
}
```

#### **(5)テスト結果：**

コードをアップロードした後、モータードライブシールドの電源スイッチをオンにします。ロボットを床に置き、上の表を参照して異なるボタンを押すと、ロボットは対応するプリセットの方向に動きます。

![](./media/img-20240117090114.png)