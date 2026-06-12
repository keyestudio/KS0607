### プロジェクト 9: 8*16 表情 LED ドットマトリクス

![](./media/image-20250709110751263.png)

#### **(1)概要:**

ロボットに表情ボードを追加したら楽しいと思いませんか？Keyestudio の 8*16 LED ドットマトリクスがその役割を果たします。これを使えば、表情・画像・パターンなど様々なディスプレイを自分でデザインすることができます。

8*16 LED ボードには 128 個の LED が搭載されています。マイクロプロセッサ（Arduino）のデータは、2線式バスインターフェースを介して AiP1640 と通信します。これにより、モジュール上の 128 個の LED のオン・オフを制御し、モジュール上のドットマトリクスに必要なパターンを表示することができます。配線の便宜のために HX-2.54 4Pin ケーブルが付属しています。

#### **(2)仕様:**

- 動作電圧: DC 3.3-5V
- 消費電力: 400mW
- 発振周波数: 450KHz
- 駆動電流: 200mA
- 動作温度: -40\~80℃
- 通信方式: 2線式バス

#### **(3)知識:**

**8\*16 LED ドットマトリクスの原理**

8*16 ドットマトリクスの各 LED をどのように制御するのでしょうか？1バイトは 8ビットで構成され、各ビットは 0 または 1 です。0 のとき LED は消灯し、1 のとき LED は点灯します。1バイトで LED の1列を制御でき、自然に 16バイトで 16列の LED を制御できます。これが 8*16 ドットマトリクスの仕組みです。

![](media/image-20230427082712905.png)

**ピンの説明と通信プロトコル**

マイクロプロセッサ（Arduino）のデータは、2線式バスケーブルを介して AiP1640 と通信します。

通信プロトコルの図は以下の通りです（SCLK）は SCL、（DIN）は SDA です。

![](media/ea2bab37f23c09453c680590b84653d6.png)

①データ入力の開始条件: SCL がハイレベルで SDA がハイからローに変化する。

②データコマンドの設定については、以下の図に示す方法があります。

サンプルプログラムでは**アドレスに自動的に1を加算する**方式を選択しており、2進数値は 0100 0000 で対応する16進数値は 0x40 です。

![](media/image-20230427083500152.png)

③アドレスコマンドの設定については、以下のようにアドレスを選択できます。

サンプルプログラムでは最初の 00H を選択しており、2進数 1100 0000 は16進数 0xc0 に対応します。

![](media/image-20230427083716284.png)


④データ入力の要件として、SCL がハイレベルのときにデータを入力する場合、SDA の信号は変化してはなりません。SCL のクロック信号がローレベルのときのみ、SDA の信号を変化させることができます。データの入力は下位ビットが先で、上位ビットが後になります。

⑤データ送信終了の条件は、SCL がローレベル、SDA がローレベルで SCL がハイレベルになったとき、SDA のレベルがハイになることです。

⑥表示制御として、異なるパルス幅を設定します。パルス幅は以下の図のように選択できます。サンプルでは、パルス幅は 4/16 で、1000 1010 に対応する16進数は 0x8A です。

![](media/image-20230427084941994.png)



**モジュールツールの使用手順**

ドットマトリクスツールはオンライン版を使用し、リンクは次の通りです: [http://dotmatrixtool.com/#]( http://dotmatrixtool.com/#)

①リンクにアクセスすると、以下のようなページが表示されます。

![](media/354693b5679a2615c62e99b7025d6355.png)

②ドットマトリクスは 8\*16 なので、高さを 8、幅を 16 に調整します（下図参照）。

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③パターンから16進数データを生成する

以下の図に示すように、マウスの左ボタンを押して選択し、右クリックでキャンセルします。希望のパターンを描き、Generate をクリックすると、必要な16進数データが生成されます。

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4)接続図:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

8x16 LED ライトボードの GND、VCC、SDA、SCL は、それぞれ Keyestudio センサー拡張ボードの -(GND)、+(VCC)、A4、A5 に接続し、2線式シリアル通信を行います。

(<span style="color: rgb(255, 76, 65);">注意:</span> Arduino の IIC ピンに接続されていますが、このモジュールは IIC 通信用ではありません。ここでの IO ポートは I2C 通信をシミュレートするためのもので、任意の2つのピンに接続することができます。)

#### **(5)テストコード:**

笑顔を表示するコード

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前に Bluetooth モジュールを接続しないでください。コードのアップロードにもシリアル通信を使用するため、Bluetooth シリアル通信と競合し、アップロードが失敗する可能性があります。)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.1
  Matrix face
  http://www.keyestudio.com
*/
// モジュールツールから笑顔画像のデータを取得する
unsigned char smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};

#define SCL_Pin  A5  // クロックのピンを A5 に設定する
#define SDA_Pin  A4  // データピンを A4 に設定する

void setup() {
  // ピンを OUTPUT に設定する
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // 画面をクリアする
  //matrix_display(clear);
}
void loop() {
  matrix_display(smile);  // 笑顔画像を表示する
}
// この関数はドットマトリクスの表示に使用される
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // データ送信を開始する関数を使用する
  IIC_send(0xc0);  // アドレスを選択する

  for (int i = 0; i < 16; i++) // 画像データは16文字ある
  {
    IIC_send(matrix_value[i]); // 画像を送信するデータ
  }

  IIC_end();   // 画像のデータ送信を終了する

  IIC_start();
  IIC_send(0x8A);  // 表示制御でパルス幅 4/16 を選択する
  IIC_end();
}

// データ送信開始の条件
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// データ送信終了のサイン
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

// データを送信する
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // 各文字は8桁あり、1つずつ検出される
  {
    if (send_data & mask) { // 各ビット（0 または 1）に応じてハイまたはローレベルを設定する
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // クロックピン SCL_Pin をプルアップしてデータ送信を終了する
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // クロックピン SCL_Pin をプルダウンして SDA の信号を変化させる
  }
}
```

#### **(6)テスト結果:**

テストコードのアップロードに成功し、配線図に従って接続し、DIP スイッチを右端に切り替えて電源を入れると、ドットマトリクスに笑顔のパターンが表示されます。

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7)応用プロジェクト:**

先ほど学んだモジュールツール [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#) を使って、ドットマトリクスにスタート、前進、停止のパターンを順番に表示させ、その後パターンをクリアします。時間間隔は 2000 ms です。

![](media/9866c73416df7466b5fe8be3712e6eb3.png)

![](media/1c7ab4b08636c2fe61deaf6c784da7d8.png)

![](media/b0a961f27eb5f0b66603abe23d6bb56a.png)


**モジュールツールから取得したコード：**

**スタートパターンのコード:**

0x01,0x02,0x04,0x08,0x10,0x20,0x40,0x80,0x80,0x40,0x20,0x10,0x08,0x04,0x02,0x01

**前進パターンのコード:**

0x00,0x00,0x00,0x00,0x00,0x24,0x12,0x09,0x12,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**後退パターンのコード:**

0x00,0x00,0x00,0x00,0x00,0x24,0x48,0x90,0x48,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**左折パターンのコード:**

0x00,0x00,0x00,0x00,0x00,0x00,0x44,0x28,0x10,0x44,0x28,0x10,0x44,0x28,0x10,0x00

**右折パターンのコード:**

0x00,0x10,0x28,0x44,0x10,0x28,0x44,0x10,0x28,0x44,0x00,0x00,0x00,0x00,0x00,0x00

**停止パターンのコード:**

0x2E,0x2A,0x3A,0x00,0x02,0x3E,0x02,0x00,0x3E,0x22,0x3E,0x00,0x3E,0x0A,0x0E,0x00

**画面クリアのコード:**

0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00

**テストコード**


(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前に Bluetooth モジュールを接続しないでください。コードのアップロードにもシリアル通信を使用するため、Bluetooth シリアル通信と競合し、アップロードが失敗する可能性があります。)

```C
/*
  keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.2
  Matrix face
  http://www.keyestudio.com
*/

// 配列：画像のデータを保存するために使用。自分で計算するかモジュールツールから取得できる
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  // クロックのピンを A5 に設定する
#define SDA_Pin  A4  // データピンを A4 に設定する

void setup() {
  // ピンを OUTPUT に設定する
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // 画面をクリアする
  matrix_display(clear);
}
void loop() {
  matrix_display(start01);  // "Start" 画像を表示する
  delay(2000);
  matrix_display(front);    // "front" 画像を表示する
  delay(2000);
  matrix_display(STOP01);   // "STOP01" 画像を表示する
  delay(2000);
  matrix_display(clear);    // "clear" 画像を表示する
  delay(2000);
}
// この関数はドットマトリクスの表示に使用される
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // データ送信を開始する関数を使用する
  IIC_send(0xc0);  // アドレスを選択する

  for (int i = 0; i < 16; i++) // 画像データは16文字ある
  {
    IIC_send(matrix_value[i]); // 画像を送信するデータ
  }

  IIC_end();   // 画像のデータ送信を終了する

  IIC_start();
  IIC_send(0x8A);  // 表示制御でパルス幅 4/16 を選択する
  IIC_end();
}

// データ送信開始の条件
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// データ送信終了のサイン
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

// データを送信する
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // 各文字は8桁あり、1つずつ検出される
  {
    if (send_data & mask) { // 各ビット（0 または 1）に応じてハイまたはローレベルを設定する
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // クロックピン SCL_Pin をプルアップしてデータ送信を終了する
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // クロックピン SCL_Pin をプルダウンして SDA の信号を変化させる
  }
}
```

テストコードのアップロード後、表情ボードにはこれらのパターンが順番に表示され、このシーケンスが繰り返されます。

![](media/e7ba47508826acc25d348182a0530c05.png)

![](media/831b7e0e07250cbc7bdc4fa509c5a0a3.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)