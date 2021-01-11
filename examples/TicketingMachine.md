<!-- NeosVR Techbook-->
- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/) 
- [発券機](#発券機)
  - [概要](#概要)
  - [解説](#解説)
  - [おわりに](#おわりに)
  - [関連するノード](#関連するノード)


# 発券機

## 概要

spoil(@tpmpt206)さんはサイン会ができるワールドを発案して、みんなの協力の下で完成させました。そのときに、オレンジ(@mikan3134)さんに制作していただいたのがこの発券機です。発券機は整理券を発券します。整理券には番号が1から順に印刷されています。発券機のボタンを押すごとに順番に整理券が発券されていきます。このLogiXの紹介をします。


## 解説

![pic](https://pbs.twimg.com/media/EaFAwgIUMAEJFAD?format=jpg&name=large "pic")

左にある「発券」というボタンを押すと、上にあるような「1」が書かれた整理券が発券されます。

真ん中ほどの[On Loaded](https://neosvrjp.memo.wiki/d/On%20loaded)はセッションが開始して、この発券機のスロットが読み込まれたときにインパルスを発生させます。ここでは[Write](https://neosvrjp.memo.wiki/d/Write)を使って0をInt変数に書き込んでいます。Writeの出力は薄いオレンジ色の帯でIntに繋がっています。これが整理券番号の初期化です。なお、上にPulseがありますが、これはデバッグ用に、強制的に0を書き込む為に入れています。

そして[Button Events](https://neosvrjp.memo.wiki/d/Button%20Events)によってボタンが押されたときにインパルスが発生するようにします。先ほどのInt変数の値を1つ増やして、[ToString](https://neosvrjp.memo.wiki/d/ToString)により二桁の文字列にしてこれを、整理券の番号として書き出しています。

さらにもう一つ先のWriteを使って、この数字は元のInt変数に書き込まれています。

次に、発券をする必要があります。[Duplicate Slot](https://neosvrjp.memo.wiki/d/Duplicate%20Slot)を使って、スロットを複製しています。複製するスロットはあらかじめ準備されています。この発券機のスロットの様子を次の図で示します。

![pic](https://pbs.twimg.com/media/EaJCCE-UwAAGFNa?format=jpg&name=large "pic")

Prefと書かれているのが整理券で、NumCardの下にはBasicという文字列を扱うスロットと、それが乗っているQuadという板があります。これをあらかじめ準備しています。先ほどの整理券の番号はここのBasicに書き込まれます。

最後に、複製された整理券を[Set Parent](https://neosvrjp.memo.wiki/d/Set%20Parent)を使って、[Root Slot](https://neosvrjp.memo.wiki/d/Root%20Slot)の直下においています。これでこのセッションにスポーンされます。

## おわりに

オレンジさんは900秒ほどで作られましたが、「意外と時間をかけてしまった」のようなことを言われていました。15分で、発券機のデザインからLogiXまで作られるのだから凄いものです！

## 関連するノード

On Loaded, Write, Button Events, ToStr, Duplicate Slot, Set Parent, Root Slot
  
  
- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/)  
- [LogiX](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/logix.html)  
- [ノード一覧(公式Wiki)](https://wiki.neos.com/LogiX/ja)  
- [型一覧](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/datatype.html)  
  