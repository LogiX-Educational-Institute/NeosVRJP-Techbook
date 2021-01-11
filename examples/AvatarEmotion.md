<!-- NeosVR Techbook-->
- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/) 
- [アバターにハンドサインから表情をつける](#アバターにハンドサインから表情をつける)
  - [概要](#概要)
  - [解説](#解説)
    - [Oculus](#oculus)
    - [VIVE](#vive)
  - [おわりに](#おわりに)
  - [関連するノード](#関連するノード)

# アバターにハンドサインから表情をつける

## 概要

ハンドサインでグーや指さしなどのジェスチャーを作ることができます。これをさらにアバターの表情につなぐことができるLogiXを解説します。

## 解説

### Oculus
![pic](https://pbs.twimg.com/media/EYIetEeU4AAbVsK?format=jpg&name=large "pic")

オレンジさんによるとてもいいビデオがあります。
[https://twitter.com/mikan3134/status/1212216322668412928](https://twitter.com/mikan3134/status/1212216322668412928)

これを観るとコンパクトでとてもわかりやすいです。ただ、DevToolTip, LogixTipの使い方が分からないとだめです。詳しくは、NeosVR日本語Wikiの記事を参照してください。

DevToolTip: [https://neosvrjp.memo.wiki/d/DevToolTip](https://neosvrjp.memo.wiki/d/DevToolTip)

LogixTip: [https://neosvrjp.memo.wiki/d/LogixTip](https://neosvrjp.memo.wiki/d/LogixTip)

<br>

それではこのビデオにあるように手順を紹介および解説しましょう。

(1) DevToolTipを装備して、表情をつけたいアバターに向けてセカンダリーアクションを押して、選択します。

(2) リングメニューからOpen Inspectorでインスペクターパネルを開きます。

(3) インスペクターでアバターの一番上のスロットまで移動します。

(4) LogixTipを装備して、インスペクターからアバターのスロットをグリップして、何もない空間でセカンダリーアクションを押して、インターフェースノードを表示させます。

(5) このインタフェースノードの一番上のSLOTにLogixTipの先端を当てて、帯を引き出して、今回紹介しているBlueprintの一番左端の[Get Active User](https://neosvrjp.memo.wiki/d/Get%20Active%20User)ノードに接続します。これでこのアバターを着た人のコントローラー入力がとれるようになりました。

(6) ここでこのBlueprintでは"Left"となっているので、左手のコントローラーから入力をとっています。たとえば、一番右にある"Fist"(グー)で表情につなげることを考えましょう。左手のコントローラーを操作してグーがでるようにします。これはプライマリーアクションとグリップを同時に握っているときです。確かめるのには、"Fist"と書かれているノードから帯を引き出してfloatの数字を眺めてみるといいです。グーをすると数字が0から1に変わっていきます。逆に離すと1から0に戻っていきます。

(7) [Smooth Leap](https://neosvrjp.memo.wiki/d/Smooth%20Lerp)は数値を時間とともに徐々に変えていくことができます。ここでは0と1のあいだを徐々に変えていきます。つまりグーが入力されると0から1に徐々に変えていき、入力が解かれると1から0に向かって変えていきます。

(8) この数字をシェープキーの入っているプロパティに流し込みます。インスペクターでシェープキーのあるスロットを選択して、右から必要なプロパティを見つけます。

(9) LogixTipを装備して、リングメニューからExtract:を選択してExtract: Drive Nodeになるようにします。

(10) この状態でシェープキーのあるプロパティの名前をグリップして、何もない空間でセカンダリーアクションを押して、Drive Nodeをスポーンさせます。

(11) LogixTipを使ってさきほどの"Fist"から帯を引き出して、このDrive Nodeの青い矢印の根元に接続します。

(12) 鏡とか使って、ハンドサインのグーをするときちんと表情が変わったことを確認できるはずです。

(13) 最後にLogiXをアバターに格納する必要があります。アバターの親スロットを選択して、インスペクターの星マークをクリックすると、子スロットを作ることができます。この子スロットの名前をemoteとでも変えておきます。

(14) この子スロットの名前をグリップして、リングメニューから"Set Packing Root"を選びます。これでこのLogixToolにこのスロットがセットされました。

(15) この状態でノードにレーザーを当てながら、セカンダリーアクションを押します。LogixToolで青のリングが一周すれば、ノードが消えて、このスロットの中にLogiXが入りました。

(16) この状態でアバターをインベントリにセーブしましょう。


### VIVE

![pic](https://pbs.twimg.com/media/EYIetleU0AAiSVj?format=jpg&name=large "pic")

これがAetorizさんが作ったVIVEのバージョンです。

ここでは[Unpack xy](https://neosvrjp.memo.wiki/d/Unpack%20xy)により、VIVEのタッチパネルのどの位置が触られているのかを得て、(x,y)に変換します。これをAtan(アークタンジェント)ではy/xを入力し、Acos(アークコサイン)ではx/&#124;V&#124;から角度(ラジアン)に変換しています。Atanは時々、無限大とかを出すことがあるので、Acosが使いやすいかもしれません。ここで&#124;V&#124;=sqrt(x^2+y^2)です。そして[Rad -> Deg](https://neosvrjp.memo.wiki/d/Rad-%a1%e4Deg)で180/3.14を与えて、度数に変換します。この角度の位置により表情をつけるようにしています。


## おわりに

実際にやるとシェープキーを探すのが大変かもしれません。あるいは複数のシェープキーに接続する必要があるかもしれません。いずれにしろNeosVRではすべての作業をVR内でできるところがとても面白いです。

## 関連するノード
Get Active User, Smooth Leap, Unpack xy, Rad -> Deg

<!-- ## 追記 -->

  

- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/)  
- [LogiX](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/logix.html)  
- [ノード一覧(公式Wiki)](https://wiki.neos.com/LogiX/ja)  
- [型一覧](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/datatype.html)  

