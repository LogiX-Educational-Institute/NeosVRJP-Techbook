<!-- NeosVR Techbook-->

# 音の鳴る箱

## 概要

2020年7月1日22時よりAetorizさんとオレンジさんによる『LogiX講習会』初級編がありました。そこではグラブすると「ぽん」って音の鳴る箱を教材にしました。音の鳴らし仕方は2つの方法を習いました。ここではその作品の解説をしましょう。


## 解説1

### 全体1

ここでは最初の方法について解説します。

![pic](https://pbs.twimg.com/media/Eb6a_MXVcAAU1l_?format=jpg&name=large "pic")

LogiXは[Play](https://neosvrjp.memo.wiki/d/Play)ノードを使う単純なものです。このPulseのところに、後半で説明するBoxのGrabableを使い[On Grabbalbe Grabbed](https://neosvrjp.memo.wiki/d/On%20Grabbable%20Grabbed)の出力をつなげば、箱を掴んだ（グラブした）ときに、インパルスが流れて音が出ます。


![pic](https://pbs.twimg.com/media/Eb6a-fPVcAM4tYp?format=jpg&name=large "pic")

この作品の大きな特徴は、音を出すのに、3つのコンポーネントを使っているということです。具体的には、"AudioClipPlayer", "AudioOutput", "StaticAudioClipProvider"です。

### audioスロットの準備

[DevToolTip](https://neosvrjp.memo.wiki/d/DevToolTip)を使います。基本的なことは[日本語Wiki](https://neosvrjp.memo.wiki/d/DevToolTip)をご覧ください。

DevToolTipを装備して、リングメニューから"Create new"を選び、さらに”3D Model”から"Box"を選んで、箱をスポーンさせます。

箱に向かってレーザーを当てて、セカンダリーアクションを押して選択します。

リングメニューから"Open Inspector"でインスペクターを表示させます。

Boxというスロットの下に子スロットをインスペクターパネルの上の「☆」を押すことにより作ります。

プロパティを変更して"audio"というスロット名にします。

### 3つのコンポーネント追加と設定

![pic](https://pbs.twimg.com/media/Eb6a-fPVcAM4tYp?format=jpg&name=large "pic")

audioスロットを選択して緑色にします。

インスペクターの右下にコンポーネントを追加するボタンがあります。これをクリックします。そして以下の3つのコンポーネントを追加します。

StaticAudioClipProviderはAssetsの下にあります。

AudioClipPlayerはAudioの下にあります。

AudioOutputはAudioの下にあります。

まず、StaticAudioClipProviderのURL:にオーディオがあるURLを入れます。この講習会では、URLをグラブしてドロップして入力しました。

次に、AudioClipPlayerのClip:には上のStaticAudioProviderを設定します。StaticAudioProviderにレーザーを当ててグラブし、そのままClip:のところにドロップします。

最後に、AudioOutputのSource:をAudioClipPlayerに設定します。同じように、AudioClipPlayerにレーザーを当ててグラブし、そのままSouce:にドロップします。

これで、コンポーネントの設定は完了です。

### Logixの配線

![pic](https://pbs.twimg.com/media/Eb6a_MXVcAAU1l_?format=jpg&name=large "pic")

[LogiXTip](https://neosvrjp.memo.wiki/d/LogixTip)を使います。基本的なことは[日本語Wiki](https://neosvrjp.memo.wiki/d/LogixTip)をご覧ください。

LogiXTipを装備して、リングメニューからNode Selecterを選び、表示させます。

[Play](https://neosvrjp.memo.wiki/d/Play)はPlaybackの下にあります。このノードの入力をLogiXTipの先端を当ててセカンダリーアクションを押しながら引き出して離すことにより、Pulseを取り出します。

さきほどのaudioスロットのインタフェースノードを表示させます。インスペクターパネルで左のスロット一覧からaudioの名前にレーザーをあてて、グラブしてから、空中でセカンダリーアクションをします。そうするとインタフェースノードが表示されます。

このインタフェースノードのPlayBackプロパティとPlayノードの出力をつなぎます。

これでPulseをレーザーでクリックすれば、音が鳴ります。

### 後始末

後始末として、最後にLogiXをパックしておきます。Boxスロットの下に「☆」を使って子スロットを作り、それをlogixという名前にしておきます。

できたlogixスロットにレーザー当ててドラッグしてから、そのままLogiXTipのリングメニューからSet Packing Rootを選びます。これでこのLogiXTipにlogixが納められるようになりました。Playノードでいいので、レーザーを当てて、セカンダリーアクションの長押しをします。LogiXTipを眺めていると青い輪が一周すれば離してOKです。これでパックされます。

インタフェースノードは消えないので、掴んで、リングメニューからDestoryを選び消しましょう。

## 解説2

### 全体2

続いてもう一つの方法について解説します。

![pic](https://pbs.twimg.com/media/Eb6bOrXUcAAihqj?format=jpg&name=large "pic")

今度のaudioスロットには1つのコンポーネント"StaticAudioClipProvider"しかありません。

![pic](https://pbs.twimg.com/media/Eb6bPdPVcAATvig?format=jpg&name=large "pic")

ちょっと複雑なのは、[Audio Clip Input](https://neosvrjp.memo.wiki/d/Audio%20Clip%20Input)ノードをインスペクターパネルで観ていることです。

![pic](https://pbs.twimg.com/media/Eb6bQIYUwAA7224?format=jpg&name=large "pic")

重要なノードに[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)があります。

###  audioスロットの準備

一つ前の作品と同じようにしてBoxを3D Modelから作り、audioスロットを作っておきます。

### コンポーネントの設定

この方法では一つのコンポーネントのみ必要です。それはStaticAudioClipProviderであり、上の方法と同じようにURL:を設定しておきます。

### Audio Clip Inputの設定

LogiXTipを装備して、[Audio Clip Input](https://neosvrjp.memo.wiki/d/Audio%20Clip%20Input)ノードをNode Selectorから選んで、スポーンさせましょう。

そして、DevToolTipを装備して、レーザーを当ててセカンダリーアクションを押して、このノードを選択します。そして、リングメニューからOpen Inspectorを選んで、インスペクターパネルを表示させます。最初はAudio Clip Inputのスロットが表示されないので、曲がった上矢印を何回かクリックして図のように表示させます。

![pic](https://pbs.twimg.com/media/Eb6bPdPVcAATvig?format=jpg&name=large "pic")

そして、このClip:のプロパティに、さきほどのStaticAudioClipProviderを設定します。具体的にはStaticAudioClipProviderにレーザーを当てて、グラブしてから、このClip:にドロップすると設定できます。

### Logixの配線

![pic](https://pbs.twimg.com/media/Eb6bQIYUwAA7224?format=jpg&name=large "pic")

[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)ノードをスポーンさせます。そして[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)ノードと[Audio Clip Input](https://neosvrjp.memo.wiki/d/Audio%20Clip%20Input)を接続します。

また、[On Grabbalbe Grabbed](https://neosvrjp.memo.wiki/d/On%20Grabbable%20Grabbed)を使って、この箱がグラブされたときにインパルスが発生するようにします。入力は箱のGrabbableプロパティです。Boxスロットを表示させると右側にこのGrabbableプロパティを見つけることができます。LogiXTipを装備して、このGrabbableプロパティの名前をグラブしたまま、空中でセカンダリーアクションをすると、インタフェースノードをスポーンさせることができます。この一番上の名前と[On Grabbalbe Grabbed](https://neosvrjp.memo.wiki/d/On%20Grabbable%20Grabbed)ノードの入力をつなぎます。またこのノードの出力を[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)ノードの一番上の入力と接続します。[On Grabbalbe Grabbed](https://neosvrjp.memo.wiki/d/On%20Grabbable%20Grabbed)ノードでは、特性のオブジェクトがグラブされたときに、インパルスが発生します。

実はこのままだと、音は箱からは聞こえません。そこで、Boxスロットと[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)ノードを接続します。Boxスロットをインスペクターパネルで表示させて、同じようにLogiXTipを使って、インタフェースノードを表示させます。一番上のSlotと[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)の薄い緑の入力を接続します。これで、音は箱から聞こえるようになります。

### 後始末

1番目の方法と同じようにlogixというLogiXを格納する子スロットを作り、ここにLogiXを格納しましょう。

## おわりに

ここでは箱をグラブすると音が鳴るという作品例を紹介しました。音を出すのに、コンポーネントやノードを駆使する必要があります。ここではその2つの方法を紹介しました。

## 関連するノード

Play, Play One Shot, Audio Clip Input, On Grabbalbe Grabbed, Puls

## 関連するコンポーネント

AudioClipPlayer, AudioOutput, StaticAudioClipProvider

## 追記

![pic](https://pbs.twimg.com/media/Eb9TlE0UEAAYOHN?format=jpg&name=large "pic")

[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)ノードを使用するとここの図にあるように、音を鳴らすたびにスロットに"OneShotAudio"が現れて、音が鳴り終わると消されます。したがって一時的に作っては消すので、資源的に有利だそうです。[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)ノードでは音量とかも細かく指定できるので、便利です。

音ファイルのURLはneosdbから始まります。これはNeosVRのクラウドサーバーにあるデータのアドレスとなっています。自分の作った音ファイルを載せたいときには、インベントリに保存します。すぐあとではlocalですが、しばらくしてsyncされるとneosdbとなります。