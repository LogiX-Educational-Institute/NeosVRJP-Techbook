<!-- NeosVR Techbook-->

# 仮想しっぽ触覚デバイス

## 概要

仮想しっぽ触覚デバイスはVR空間で、プレイヤーの死角にあるアバターのしっぽが触れられたことをプレイヤーが認知できるようにしっぽを触れらた感覚を疑似的に再現する触覚デバイスです。

VRChatのアバターなどに多くついているしっぽですが、基本的にプレイヤーの死角に存在するため鏡やカメラを使って見たりしないと誰かが触っているということに気づくことはできません。このデバイスはアバターのしっぽを誰かが触った時にプレイヤーが装着した振動モーターを動作させることでしっぽの感覚を獲得することができます。
現在はNeosVRのみ対応です。

仕組みはNeosVRで尻尾のコライダーに触れたり、ダイナミックボーンを掴むと、Webサーバーとして稼働しているM5StackにHTTP通信を行い、M5Stackに接続された振動モーターが振動するというものです。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330214546_704c61383664696d4a6a.png "pic")

![pic](https://f.easyuploader.app/eu-prd/upload/20200330215351_373141366f6f7a6b5264.png "pic")

### 機材構成

#### 仮想しっぽ触覚デバイス

振動モーターがついている尻尾デバイス本体です。

#### 無線LANルーター

仮想しっぽ触覚デバイスはローカルネットワーク内で動作するWebサーバーなのでNeosVRが動作しているPCと接続するためにルーターが必要です。さらに無線LANで繋げるので無線LAN機能がついている必要がありますが、家庭にあるルーターのほとんどは無線LAN機能がついていると思うので、パソコンが接続しているルーターがあればOKです。

#### NeosVRが動作しているPC

NeosVRが動作しているPCです。

## 仮想しっぽ触覚デバイスの作り方

### 必要なパーツ

本体

- M5Stack
- 振動モーター（CL-0614-13103-3）
- 振動モーター用ケース
- 電池ボックス　単３×１本　リード線
- ASB樹脂ケース
- ウレタンクッションテープ
- NPNトランジスタ
- ミニブレッドボード
- ピンソケット
- 線材

消耗品

- はんだ
- 両面テープ
- 単3電池

### M5Stack

今回の製作では、手持ちのM5Stack Grayを使いましたが、より安価なM5Stack BasicでOKです。
M5Stack Basicなら4000円以下で購入することができます。

### 振動モーター

振動モーターには千石電商さんの、CL-0614-13103-3を使用しました。221円で買えます。   
[https://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=EEHD-0F4B](https://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=EEHD-0F4B)

### 振動モーター用ケース

振動モーターをカバーするためのケースです。千石電商でたまたま見つけたこのケースを使用しました。
1つ120円です。

[https://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=EEHD-0ACA](https://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=EEHD-0ACA)

### 電池ボックス

単3電池が1本入る電池ボックスです。秋月電子で30円で購入しました。  
[http://akizukidenshi.com/catalog/g/gP-00221/](http://akizukidenshi.com/catalog/g/gP-00221/)

### プラスチックケース

パーツを納めるケースです。パーツにアクセスしやすいようにパカっと開くケースを選択しました。
秋月電子で120円で売っている112-TSを使用しました。  
[http://akizukidenshi.com/catalog/g/gP-00277/](http://akizukidenshi.com/catalog/g/gP-00277/)

### ウレタンクッションテープ

![pic](https://f.easyuploader.app/eu-prd/upload/20200330215619_4c5747327a57386e596f.png "pic")


ホームセンターで売っているウレタンクッションテープです。M5Stackがケース内で動いて傷がつかないように保護するためのクッションとして使用します。価格は忘れてしまいました・・・。



### NPNトランジスタ

モーターの電子制御に必要なトランジスタです。秋月電子の2SC1815-GR-T92-Kを使いました。
1つしか使わないのですが、最低でも20個入りでしか買えませんでした。100円です。  
[http://akizukidenshi.com/catalog/g/gI-06477/](http://akizukidenshi.com/catalog/g/gI-06477/)


### ミニブレッドボード

パーツの配線に使用する基板代わりです。耐久度を上げるならユニバーサル基板に半田づけするのがよいのですが、配線を失敗すると結構面倒なのでブレッドボードにしました。秋月で150円です。クリスタルカラーもあってそちらは170円です。

[http://akizukidenshi.com/catalog/g/gP-05158/](http://akizukidenshi.com/catalog/g/gP-05158/)

### 線材

配線に使用する線材です。

耐熱電子ワイヤー  
[http://akizukidenshi.com/catalog/g/gP-10672/](http://akizukidenshi.com/catalog/g/gP-10672/)

ブレッドボード・ジャンパーワイヤ 14種類×10本  
[http://akizukidenshi.com/catalog/g/gP-10672/](http://akizukidenshi.com/catalog/g/gP-00288/)

ブレッドボード・ジャンパーワイヤ（オス－オス）　10cmセット  
[http://akizukidenshi.com/catalog/g/gC-05371/](http://akizukidenshi.com/catalog/g/gC-05371/)

いっぱいありますが、実際にパーツとして使用するのはこの中からそれぞれ1~2本程度しか使いませんでした。頑張れば一番上の耐熱電子ワイヤーだけで配線出来ます。

### ピンソケット

ケースの都合上、M5Stackに繋がるジャンパーワイヤーをブレッドボードに刺すと高さが足りなかったのでこれをL字にまげて使いました。

ピンソケット 1×5 リード長10mm  
[http://akizukidenshi.com/catalog/g/gC-06360/](http://akizukidenshi.com/catalog/g/gC-06360/)

## 必要な道具

### ニッパー

線材を切るのに必要です。

### はんだごて

モーターを配線するのにはんだ付けします。

### ドリル

ケースに穴あけするのに必要です。手動のドリルとかでも大丈夫だと思いますが、自分は電動ドリルを使用しました。

### やすり

ケースの穴を整えるのに使います。

### グルーガン

振動モーターをケースに固定するのに使いました。

## M5Stackの開発環境を整える

以下のサイトを参考に開発環境を整えましょう。  
[https://raspberrypi.mongonta.com/howto-start-m5stack-arduinoide/#M5Stack-2](https://raspberrypi.mongonta.com/howto-start-m5stack-arduinoide/#M5Stack-2)

HelloWorldの動作チェックまで通ればOKです。

Windows 10 64Bit版でのM5Stackの環境構築方法を説明します。

## M5StackにWebサーバープログラムを書き込む

以下のソースコードをダウンロードします。

[https://drive.google.com/file/d/1g_XdzOZg5AvtQRb9Ccc8C3ou3NuTo3cF/view?usp=sharing](https://drive.google.com/file/d/1g_XdzOZg5AvtQRb9Ccc8C3ou3NuTo3cF/view?usp=sharing)

AruduinoIDEから「ファイル」→「開く...」を選択し、「VirtualTailsSystem.ino」を開きます。

9行目と、10行目のssidとpasswordをPCが繋がっている無線LANルーターのものに書き換えます。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330215902_373835445967695a7775.png "pic")

書き換えたら、「マイコンボードに書き込む」ボタンを押してM5Stackにプログラムを書き込みます。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330220225_694a7179733364653656.png "pic")

書き込みが完了するとM5Stackが再起動して、以下の画像のようになるはずです。「* Virtual Tail System *」以降「...」しか表示されていない場合は無線LAN接続がうまくいっていないので、SSIDとパスワードの確認、またはルーターの設定の確認を行ってください。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330220102_413776566a49577a6a79.png "pic")

### Webサーバーの動作確認

M5Stackに表示されているIPアドレスにPCのブラウザからアクセスできるか試してみましょう。

画像ではIPアドレスが、192.168.3.11なので、以下のURLでアクセスします。

http://192.168.3.11/?LENGTH=30000&POWER=255

そして

![pic](https://f.easyuploader.app/eu-prd/upload/20200330220656_50373342385a5a506279.PNG "pic")

とブラウザで表示されれば問題ありません。


## デバイスの組立

本当は製作工程ごとに写真で解説出来ればよかったのですが、写真を撮るのを忘れていました・・・。なので完成品を見ながら解説になります。

### ケースの加工

ケースにモーターの線を通すための穴と、M5Stackの外部電源ようにUSB3.0用の穴を空けます。M5Stackをいったんケースに入れて、穴を空ける場所をペンなどで印を付けてからドリルで穴あけし、やすりで整えます。
モーターを格納するケースにも穴を空けます。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330220947_67397454355057476e75.png "pic")

### モーターのはんだ付け

購入したモーターの線はかなり短いので被膜ワイヤーをはんだ付けして繋げます。ただ、このままだとはんだした部分の長さが同じで、その部分でショートする可能性があるため、自分はグルーガンで絶縁処理しました。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330221105_3475585a715346545352.png "pic")

ワイヤーはより線なので、反対側はブレッドボードに刺しやすいようにはんだを流してコーティングするとよいです。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330221151_436f576358686b5a6d61.png "pic")

### 配線

下図のようにパーツを配線します。トランジスタには向きがあるので注意しましょう。平べったい方を外側に向ければOKです。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330221232_55585575556e706a3436.png "pic")
![pic](https://f.easyuploader.app/eu-prd/upload/20200330221118_387835723549736a3963.png "pic")
![pic](https://f.easyuploader.app/eu-prd/upload/20200330221228_474a3939596e63786568.png "pic")


### 動作チェック

パーツをすべて配線し終わったら再度上記のURLで動作チェックをします。
アクセスした際にモーターが一定時間振動すればOKです。

### ケースへのセット

動作チェックできたら、それぞれのパーツをケースに納めます。電池ボックスとブレッドボードは両面テープで固定してしまいます。最後にウレタンクッションテープでM5Stackを保護するようにケースに貼れば完成です。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330221312_5054494152505a5a446b.jpg "pic")

### 装着の仕方

自分の場合はこのようなベルトに付けるタイプのポシェットにモバイルバッテリーと繋げた仮想しっぽデバイスをいれて、フルトラ時の腰トラッカーのベルトに付けています。振動モーターはズボンで挟んで尾てい骨あたりに当たるようにします。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330221512_4e37716b395a6b74614c.png "pic")

## NeosVR側での準備

### 付け尻尾方式

導入が簡単になるように、設定済み付け尻尾バージョンを作りました。ちょっとしたセットアップ機能付きです。

セットアップツールはNeosVRで「virtual tail system」というワールドを開き、そこにあるフォルダをインベントリに保存して使うことが出来ます。
「World Browser」から検索窓で「virtual」まで入力して検索すると出てきます。

フォルダの中にある「VTS Spawner」を取り出し、テキストフィールドに自分の仮想しっぽデバイスのIPアドレスを入れます。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330221616_655441426f69754b4a6f.jpg "pic")

そして「Create」を押すと尻尾が生成されます。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330221616_4b4b713875367a725039.jpg "pic")

生成された尻尾をDevToolTipを使って、アバターの導入したいボーン以下に設置すれば完了です。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330221730_6f6d57415a48574f4f32.jpg "pic")
![pic](https://f.easyuploader.app/eu-prd/upload/20200330221917_6a4c554a367768497642.jpg "pic")
![pic](https://f.easyuploader.app/eu-prd/upload/20200330221917_46724d71393231374754.jpg "pic")
![pic](https://f.easyuploader.app/eu-prd/upload/20200330221917_6b684438776d62393165.jpg "pic")

アバターを着ると、このURLに接続してよいかの許可画面が出ます。「Allow」を押します。

![pic](https://f.easyuploader.app/eu-prd/upload/20200330233012_5035746a755735335666.png "pic")

この尻尾は人またはオブジェクトに触れると振動し、また尻尾の先端ほど振動が弱くなります。自分で触った場合は反応しないようになっています（コライダーのマスキングのため）。ただし、尻尾を掴む場合は自分でも反応します。尻尾を掴んだ場合は引っ張った時の長さで振動が強まります。

### オリジナルモデルに導入する場合

LogiXを含めた詳細な解説が必要になるため後日公開します！



