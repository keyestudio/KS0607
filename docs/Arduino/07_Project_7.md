### プロジェクト 7: IR受信

#### **(1)説明:**

![](media/8969111328604c5358f7c915ac94e474.png)

赤外線リモコンが日常生活において広く普及していることは言うまでもありません。テレビ、ステレオ、ビデオレコーダー、衛星信号受信機など、さまざまな家電製品の制御に使用されています。赤外線リモコンは、赤外線送信システムと赤外線受信システム、すなわち赤外線リモコンと赤外線受信モジュール、およびデコード可能なシングルチップマイコンで構成されています。

リモコンから送信される38Kの赤外線キャリア信号は、リモコン内のエンコーディングチップによってエンコードされます。パイロットコード、ユーザーコード、ユーザー逆コード、データコード、データ逆コードで構成されています。パルスの時間間隔を利用して0または1の信号を識別し、これらの0と1の信号によってエンコードが行われます。

同一リモコンのユーザーコードは変わらず、データコードによってキーを識別できます。

リモコンのボタンが押されると、リモコンは赤外線キャリア信号を送信します。IR受信機が信号を受信すると、プログラムはキャリア信号をデコードし、どのキーが押されたかを判断します。MCUは受信した01信号をデコードし、それによってリモコンでどのキーが押されたかを判断します。

![](media/image-20230426172824683.png)

赤外線受信機はモータードライブボードに取り付けられています。受信、増幅、復調を一体化しており、内部ICはすでに赤外線受信・出力を実現するよう調整されており、TTL信号互換で動作します。デジタル信号を出力し、赤外線リモコンと赤外線データ伝送に適しています。このモジュールにはシグナル、VCC、GNDの3ピンしかなく、arduinoなどのマイコンとの接続・通信が非常に便利です。

#### **(2)パラメータ:**

動作電圧: 3.3-5V（DC）

インターフェース: 3PIN

出力信号: デジタル信号

受信角度: 90度

周波数: 38khz

受信距離: 10m

モータードライブボードに統合された赤外線受信機：

![](./media/img-20240117082433.png)




#### **(3)テストコード:**

まずIRライブラリをインポートする必要があります。

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードのアップロード前にBluetoothモジュールを接続しないでください。コードのアップロードにもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 7.1

IRremote

http://www.keyestudio.com

*/

#include <IRremote.h> // IRremoteライブラリの宣言

int RECV_PIN = 3; //IR受信機のピンを3に定義
IRrecv irrecv(RECV_PIN);
decode_results results; //"decode results"の"result"にデコード結果が格納される

void setup() 
{
    Serial.begin(9600);
    irrecv.enableIRIn(); //受信機を有効化
}

void loop() 
{
    if (irrecv.decode(&results))//デコード成功、赤外線信号のセットを受信
    {
        Serial.println(results.value, HEX);//16進数HEXで改行して出力し受信コードを表示
        irrecv.resume(); //次の値を受信
    }
    delay(100);
}
```

#### **(4)テスト結果:**

テストコードをアップロードし、シリアルモニターを開いてボーレートを9600に設定し、リモコンをIR受信機に向けます。対応する値が表示されます。キーを長押しするとエラーコードが表示される場合があります。

![](media/a484b81d031c8d6e8addb169136fd45c.png)

以下にkeyestudioリモコンの各ボタン値を一覧表示しています。参考としてお使いください。

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

IR受信機はD3に接続されているため、配線は不要です。

#### **(5)コードの説明:**

**irrecv.enableIRIn():** IR デコードを有効化した後、IR信号が受信され、"decode()"関数がデコードの成否を継続的にチェックします。

**irrecv.decode(&results):** デコードが成功すると、この関数は"true"を返し、結果を"results"に保存します。IR信号をデコードした後、resume()関数を実行して次の信号を受信します。

#### **(6)応用実習:**

IRリモコンのキー値をデコードしました。測定した値でLEDを制御するにはどうすればよいでしょうか？実験を設計してみましょう。

D9にLEDを取り付け、リモコンのキーを押してLEDを点灯・消灯させます。

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)

**テストコード**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードのアップロード前にBluetoothモジュールを接続しないでください。コードのアップロードにもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードが失敗する可能性があります。)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 7.2
IRremote
http://www.keyestudio.com
*/

#include <IRremote.h> //IRremoteの宣言

int RECV_PIN = 3; //LEDのピンをピン3として定義
int LED = 9;
bool flag = 0;
IRrecv irrecv(RECV_PIN);
decode_results results; //"decode results"の"result"にデコード結果が格納される

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);//LEDを出力に設定
    irrecv.enableIRIn(); //受信機を有効化
}

void loop() 
{
    if (irrecv.decode(&results)) 
    {
        if (results.value == 0xFF02FD & flag == 0) //上記のキーコード、リモコンのOKボタンを使用、OKボタンを押した場合
        {
            digitalWrite(LED, HIGH); //LED点灯
            flag = 1;
        }

        else if (results.value == 0xFF02FD & flag == 1) //再度押した場合
        {
            digitalWrite(LED, LOW); //LED消灯
            flag = 0;
        }
        irrecv.resume(); // 次の値を受信
    }
}
```

コードを開発ボードにアップロードし、リモコンの「OK」キーを押してLEDを点灯・消灯させます。

![](./media/img-20240117090645.png)