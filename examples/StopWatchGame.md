<!-- NeosVR Techbook-->

# ストップウォッチゲーム

## 概要

2020年7月24日19時からNeosVRで『LogiX講習会No.2』がありました。そこではストップウォッチゲームを扱いました。
Aetoriz博士とオレンジ先生による丁寧な解説で10名ほどの生徒は無事に最後まで作ることができました。
ここではそのストップウォッチゲームがこの記事を読んで制作できるようにしてみます。
![pic](https://pbs.twimg.com/media/EdvFtIyUMAAtIuG?format=jpg&name=4096x4096 "pic")

## 解説

### 全体
![pic](https://pbs.twimg.com/media/Eds2M-dUYAAQfx-?format=jpg&name=large "pic")

中央にあるのが、今回のストップウォッチゲームで、「sippai」と書かれていてその下に「Start」と「Stop」のボタンがあります。「Start」ボタンを押すと表示は「???」に変わります。10秒と思ったところで「Stop」ボタンを押します。成功すると表示は「seikou」になります。このゲームを作ります。

LogiXは次のようになっています。

![pic](https://pbs.twimg.com/media/EdwK9iMU4AEKIuH?format=jpg&name=large "pic")

ボタンが押されたことを検知して、左に「Pulse」が3つ並んでいるStopwatchがスタートします。これで時間を計ります。そして9.5秒以上10.5秒以下であれば「succeeded」を表示し、それ以外は「failed」を表示します。

### インターフェース部分

テキストは、DevToolチップからコンテキストメニュー（リングメニュー）を使ってCreate NewでText → Basic Textを選び作り出すことができます。

ボタンは、DevToolチップからコンテキストメニュー（リングメニュー）を使ってCreate NewでObject → NeosUI → ButtonButton　によって作ることができます。

これらを並べ置きます。ここで、インスペクターパネルにあるReset Position, Reset Rotation Reset Scaleをうまく使い、ギズモや数値入力を利用すると、綺麗に配置することができます。

またBasic Text, ButtonからはGrabbableコンポーネントのEnabled:のチェックを外しておきます。そうすることにより不用意にグラブしても動かないので安全です。

逆に、Stop watchにはGrabbableコンポーネントを追加します。Transform → Interaction の下にあります。そしてEnebled:にチェックしておきます。これで掴むことができるようになり、インベントリに保存することができるようになります。

同じようにコンポーネントがどこの下にあるのか分からないときには[日本語Wikiのコンポーネント一覧](https://neosvrjp.memo.wiki/d/%a5%b3%a5%f3%a5%dd%a1%bc%a5%cd%a5%f3%a5%c8%b0%ec%cd%f7)をご覧ください。


### スロットの構成

![pic](https://pbs.twimg.com/media/EdwEZ0AVAAMyfZE?format=jpg&name=large "pic")

インスペクターパネルでこのStop watchをみると、上のようになっています。Basicの上に、黄色い上矢印を押して、親スロットを作り、それを「Stop watch」としています。そこにStopButtonとStartButtonを入れています。またlogixを格納する子スロットを、黄色い星を押して、作っています。

### LogiXの構成

LogiXのノードがどこの下にあるのか分からないときには[日本語Wikiのノード一覧](https://neosvrjp.memo.wiki/d/%a5%ce%a1%bc%a5%c9%b0%ec%cd%f7)をご覧ください。

![pic](https://pbs.twimg.com/media/EdwK9iMU4AEKIuH?format=jpg&name=large "pic")

[ButtonEvents](https://neosvrjp.memo.wiki/d/Button%20Events)ノードはNode PanelではInteractionの下にあります。出力の一番上はボタンが押されたときにインパルスを発生します。これが[Stopwatch](https://neosvrjp.memo.wiki/d/Stopwatch)ノードのそれぞれStartとStopに接続されています。[Stopwatch](https://neosvrjp.memo.wiki/d/Stopwatch)ノードからPulseが引き出されているのは、デバッグのためです。StopwatchはInputの下にあります。

[Stopwatch](https://neosvrjp.memo.wiki/d/Stopwatch)ノードの4番目の出力はTime(float)です。これが経過時間を出力します。これを不等号と[&](https://neosvrjp.memo.wiki/d/%26)を使って9.5秒よりも大きく、10.5秒よりも小さい時にTrueを出すようにします。

Operatorの下にある[?:](https://neosvrjp.memo.wiki/d/%3f%3a)ノードは三項演算子とか条件演算子と呼ばれます。3番目の入力がTrueであれば、1番目の入力を出力します。Falseであれば、2番目の入力を出力します。そこにはInputの下にある[String](https://neosvrjp.memo.wiki/d/string)ノードが2つあり、ここでは「succeeded(seikou)」と、「failed(sippai)」が書いてあります。

さて、これらの文字列とスタートボタンが押された時に書かれる「???」はActionsの下にある[Write](https://neosvrjp.memo.wiki/d/Write)ノードを使って、Basic Textに書き込まれます。この[Write](https://neosvrjp.memo.wiki/d/Write)ノードが重要です。LogiXではインパルスを受けてこの[Write](https://neosvrjp.memo.wiki/d/Write)ノードが値を次に渡す重要な役割をします。

[?:](https://neosvrjp.memo.wiki/d/%3f%3a)ノードからの出力はWriteノードに行きます。Writeノードは、Stopwatchノードの2番目の出力、つまり止まったときに発生するインパルスによって動くことになります。そして書き終わるとWriteノードの2番目の出力のインパルスが発生し、Stopwatchノードの3番目の入力につながり、ストップウォッチのリセットを行います。

「???」はWriteノードに行きます。Writeノードは、Stopwatchノードの1番目の出力、つまり動き出したときに発生するインパルスによって動くことになります。

### インタフェースノードの接続

Buttonをインスペクターパネルで開いて、LogixTipを装備して、NeosButtonコンポーネントをグラブして、インタフェースノードを表示させます。この一番上のNeoxButtonをそれぞれのButtonEventsノードの入力に接続します。

またBasic Textのインスペクターパネルを開いて、LogixTipを装備して、TextRendererコンポーネントをグラブして、インタフェースノードを表示させます。この中のTextをWriteノードの出力に接続します。2カ所あります。これで文字列が書き込まれます。

## おわりに

簡単なゲームですが、Buttonなどのオブジェクト、LogiX、コンポーネント、インターフェースノードがきちんと使われていてできているので、この記事からきちんと再現できるようになると、かなりLogiXプログラミングはできるようになっているはずです。ぜひ試してみてください。

また2020年7月に発表になったNoesVR内で動くスマホEvolverのアプリに簡単に変換することもできます。一番上の図ではAetoriz博士のスマホに生徒のアプリを入れて動かしてみました。

なお、この講座はビデオを撮っているので、公開される予定です。そこではこの記事の順番では無くて、どのように考えるのかということがとても丁寧に説明されています。それも参照されてください。

## 関連するノード

Button Events, Stopwatch, ?:, Write, String

## 関連するコンポーネント

Grabbable, TextRenderer, NeosButton
<!-- ## 追記 -->