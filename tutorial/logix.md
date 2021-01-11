- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/)  
- [LogiX](#logix)  
  - [動画でのチュートリアル](#動画でのチュートリアル)
  - [文章でのチュートリアル](#文章でのチュートリアル)
  - [Tips](#tips)
    - [Impulseは分岐できない](#impulseは分岐できない)
    - [変数の初期化](#変数の初期化)
    - [スロットの位置](#スロットの位置)
    - [入力が無いときのノードの動作](#入力が無いときのノードの動作)
    - [型変換(Cast)](#型変換cast)
    - [Neos UIのボタンを押した人のUSER NAMEを取得する方法がわかりません。](#neos-uiのボタンを押した人のuser-nameを取得する方法がわかりません)
  
  
# LogiX  
## 動画でのチュートリアル
- [【Neos VR】3分でできちゃうLogiXの作り方！(Youtube)](https://www.youtube.com/watch?v=Bhg2zbBQUoY)

- [【LogiX講習会】初級編その2『ゲーム制作』(Youtube)](https://www.youtube.com/watch?v=-dHo8T2J1WQ)
  
## 文章でのチュートリアル
  
- [NeosVRでのLogiX事始め（バーチャル空間でプログラミング）- @pet_sensei](https://qiita.com/pet_sensei/items/ea9bf12e07e04e803496)  
  
- [LogiXチュートリアル](https://LogiX-Educational-Institute.github.io/NeosVRJP-Techbook/tutorial/logixtutorial.html)  
  
そのほか[Qiita](https://qiita.com/tags/neosvr)にも解説などの記事があります。  
  
  
## Tips

### Impulseは分岐できない

Impulseは順番に実行するという特性から同時に二つにつなぐことはできないです。分岐したいときには[Sequence](https://neosvrjp.memo.wiki/d/Sequence)を使います。そのときには、上から順番にImpulseが出て行きます。同時ではないです。

([Ez Cameraのアバターへのインストールとアンインストール](https://LogiX-Educational-Institute.github.io/NeosVRJP-Techbook/examples/EzCameraInstallUninstall.html)参照)

### 変数の初期化

変数を初期化するのには、[Write](https://neosvrjp.memo.wiki/d/Write)を使います。Impulseを受けて書き込みます。たとえばグラブされたとかFor文が最初に動き始めたとかいうImpulseをWriteが受けることで初期化されます。

( [ユーザーリスト](https://LogiX-Educational-Institute.github.io/NeosVRJP-Techbook/examples/UserList.html)参照)

### スロットの位置

スロットの位置は親スロットの位置からの相対位置で表されています。もしPositionもRotationも(0,0,0)であるならば、親スロットの位置と同じ位置になります。

([Ez Cameraのアバターへのインストールとアンインストール](https://LogiX-Educational-Institute.github.io/NeosVRJP-Techbook/examples/EzCameraInstallUninstall.html)参照)

### 入力が無いときのノードの動作

[Set Local Position](https://neosvrjp.memo.wiki/d/Set%20Local%20Position)を使うときに左側の入力が無いときには、LogixTipを使ってノードを引き出してみるとわかるように、(0,0,0)が入力されています。明示しないことで見た目がすっきりします。

([Ez Cameraのアバターへのインストールとアンインストール](https://LogiX-Educational-Institute.github.io/NeosVRJP-Techbook/examples/EzCameraInstallUninstall.html)参照)

### 型変換(Cast)
Castは変換したい先のRelayを2つ作って、それに繋げることでできます。LogixTipを装備してRelayをセカンダリーアクションでセットすると、同じ型のRelayが複製できます。

int→floatを作るとき<br>
① floatのRelayを２つ繋げる<br>
Relay(float)-Relay(float)<br>
② 最初のRelayにintを入れる<br>
何か(int)-Relay(int)-Cast(int→float)→Relay(float)<br>

[引用元](https://discordapp.com/channels/673668075718967296/673745117923770387/693984427100995604)

### Neos UIのボタンを押した人のUSER NAMEを取得する方法がわかりません。
InteractionのButton EventsノードをNeosButtonコンポーネントに繋いでPressed(またはReleased)をWriteに繋げ、LocalUserをVariableのUserに書きこみでButtonを押したUserをとれます。  
  
またLocalUserは、ButtonEventsの出力するSource(Component)→GetSlot→GetActiveUserでも代用できます。  
(NeosVR JP discord 質問 2020/3/23)  
