### プロジェクト 1: LED点滅

#### **(1)概要:**

![](media/64b0b431d58473408ac46b39d2dc2ad0.jpeg)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

初心者や愛好家にとって、LED点滅は基本的なプログラムです。LEDは発光ダイオードの略称で、Ga、As、P、Nなどの化学化合物で構成されています。テストコードのディレイ時間を変更することで、LEDはさまざまな色で点滅することができます。制御時は、GNDとVCCに電源を供給します。S端がハイレベルの場合、LEDが点灯し、ローレベルの場合は消灯します。

#### **(2)パラメータ:**

![](./media/image-20250709104606457.png)

- 制御インターフェース: デジタルポート
- 動作電圧: DC 3.3-5V
- ピン間隔: 2.54mm
- LED表示色: 黄色

#### **(3)必要なコンポーネント:**

![](media/img-20240117081416.png)


#### **(4)8833モータードライバー拡張ボード:**

Keyestudio 8833モータードライバー拡張ボードは、Arduino UNO開発ボードと互換性があります。使用する際は、開発ボードの上に重ねて装着してください。

![](./media/image-20250709104749140.png)

#### **(5)接続図:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](media/d68e6475a7c9ed55bb057b75d1b11689.png)

<span style="color: rgb(255, 76, 65);">**注意:**</span> LEDはD9ポートに接続されています。シールドにジャンパーキャップを取り付けることを忘れないでください。

#### **(6)テストコード:**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードに失敗する可能性があります。)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.1

Blink

http://www.keyestudio.com

*/

int LED = 9; //LEDのピンをデジタルポート9に定義する

void setup()
{
	pinMode(LED, OUTPUT); //LEDピンを出力モードに初期化する
}

void loop() //無限ループ
{
	digitalWrite(LED, HIGH); //ハイレベルを出力し、LEDを点灯する
	delay(1000); //1秒待つ
	digitalWrite(LED, LOW); //ローレベルを出力し、LEDを消灯する
	delay(1000); //1秒待つ
}
```

#### **(7)テスト結果:**

プログラムをアップロードすると、LEDが1秒間隔で点滅します。

#### **(8)コードの説明:**

**pinMode(LED，OUTPUT) -** この関数はピンがINPUTかOUTPUTかを指定します。

**digitalWrite(LED，HIGH) -** ピンがOUTPUTの場合、HIGH（5V出力）またはLOW（0V出力）に設定できます。

#### **(9)応用練習:**

LEDの点滅に成功しました。次に、ピンとディレイ時間を変更するとLEDがどうなるか観察してみましょう。

**テストコード**

(<span style="color: rgb(255, 76, 65);">**注意:**</span> コードをアップロードする前にBluetoothモジュールを接続しないでください。コードのアップロードもシリアル通信を使用するため、Bluetoothシリアル通信と競合が発生し、アップロードに失敗する可能性があります。)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.2

Blink

http://www.keyestudio.com

*/

int LED = 9; //LEDのピンを9として定義する

void setup()
{
	pinMode(LED, OUTPUT); //LEDのピンをOUTPUTに設定する
}

void loop() //無限ループ
{
    digitalWrite(LED, HIGH); //ハイレベルを出力し、LEDを点灯する
	delay(100); //0.1秒待つ
	digitalWrite(LED, LOW); //ローレベルを出力し、LEDを消灯する
	delay(100); //0.1秒待つ

}
```

テスト結果より、LEDがより速く点滅することが確認できます。したがって、ピンとディレイ時間が点滅の周波数に影響を与えるという結論を導くことができます。