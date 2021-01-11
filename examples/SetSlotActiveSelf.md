<!-- NeosVR Techbook-->
- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/) 
- [スロットをアクティブにしてセッションに現れさせる](#スロットをアクティブにしてセッションに現れさせる)
  - [概要](#概要)
  - [解説](#解説)
    - [インストール時にカメラを表示し続ける](#インストール時にカメラを表示し続ける)
    - [Init Pointスロットからカメラの位置を初期化する](#init-pointスロットからカメラの位置を初期化する)
    - [メニューボタンのダブルクリックで表示する](#メニューボタンのダブルクリックで表示する)
  - [おわりに](#おわりに)
  - [関連しているノード](#関連しているノード)
  - [追記](#追記)
  
  
# スロットをアクティブにしてセッションに現れさせる

## 概要

レニウム(@rhenium_vrc)さんが作ったEZ Cameraはインストールすると、メニューボタンのダブルクリックで、左手にカメラが現れます。これは[Set Slot Active Self](https://neosvrjp.memo.wiki/d/Set%20Slot%20Active%20Self)を使って、スロットをアクティブにしてカメラをセッションに現れさせています。このLogiXについて解説をしてみましょう。

全体を見渡すと、左の方が入力になっていて、結果は右になっています。左の入力は緑色の矢印が3つあります。緑色はスロットを表しています。上からCamera, Init Point, Ez Cameraとなっています。Cameraは標準のカメラがこのEz Cameraに取り込まれています。Init Pointはインストールしたときの左手との距離、角度、スケールが記録されています。最後にこのLogiXがあるEz Cameraです。それらが分かるようにスロットの中身が表示されています。

右の結果は、大きく3つあります。一番上に[Set Slot Active Self](https://neosvrjp.memo.wiki/d/Set%20Slot%20Active%20Self)があり、これを使ってCameraのスロットにActiveを送って、カメラをセッションに表示させることをします。次に真ん中はInit Pointスロットに書かれていることを[Set Local Position](https://neosvrjp.memo.wiki/d/Set%20Local%20Position)と[Set Local Rotation](https://neosvrjp.memo.wiki/d/SetLocalRotation)と[Set Local Scale](https://neosvrjp.memo.wiki/d/SetLocalRotation)を使って設定します。最後に一番下の[Set Slot Active Self](https://neosvrjp.memo.wiki/d/Set%20Slot%20Active%20Self)はメニューボタンのダブルクリックがあったときに、カメラを表示したり、逆に消したりすることをします。

![pic](https://pbs.twimg.com/media/ETtPwh7U0AA69s4?format=jpg&name=large "pic")

## 解説

### インストール時にカメラを表示し続ける

一番上の[Set Slot Active Self](https://neosvrjp.memo.wiki/d/Set%20Slot%20Active%20Self)への入力を考えると常にTrueが送られるのでActiveにする、つまりCameraをセッションに表示することをします。その条件は2つあって、1つはEz cameraのスロットの親スロットの名前に"pref"があることと、そして2つめがEz cameraのスロットのユーザーが存在していることです。この"pref"というのはプレハブ(prefab)ということで、まだインストールが完了していないときに残っているスロットです。インストールが完了するとEZ Cameraから"pref"というスロットは消えています。

1つめはEz cameraスロットから[Get Parent Slot](https://neosvrjp.memo.wiki/d/Get%20Parent%20Slot)を使って親のスロットを取り出し、さらに[Get Slot Name](https://neosvrjp.memo.wiki/d/Get%20Slot%20Name)を使って親の名前を取り出し、これを"pref"が入っているかどうかを検査します。

2つめは[Get Active User](https://neosvrjp.memo.wiki/d/Get%20Active%20User)を使ってEz cameraスロットを所持しているユーザーをとりだし、[Is User Present](https://neosvrjp.memo.wiki/d/Is%20User%20Present)でユーザーがいるか検査します。

これらはインストールする際に、カメラを表示し続けるためにあります。

なお[Update](https://neosvrjp.memo.wiki/d/Update)により毎フレーム処理が実行されているので、この処理が毎フレームごとに行われます。

### Init Pointスロットからカメラの位置を初期化する

下の図は最終のインストールが終わったときのEz Cameraスロットの様子をインスペクターで見たところです。Ez cameraスロットの下に、Init Pointがあり、そこにはPosition: Rotation: Scale:についてそれぞれインストールの時の値が保存されています。NeosVRでは、子スロットの位置は親スロットの位置からの相対位置になっています。ですからCameraの位置は親のInit Pointの位置から相対的に決まります。

![pic](https://pbs.twimg.com/media/ETtPyQ7UUAA5Xnn?format=jpg&name=large "pic")

まず、[Set Parent](https://neosvrjp.memo.wiki/d/Set%20Parent)を使って、Init Pointスロットの親をEz Cameraスロットにします。そして、[Set Local Position](https://neosvrjp.memo.wiki/d/Set%20Local%20Position)と[Set Local Rotation](https://neosvrjp.memo.wiki/d/SetLocalRotation)と[Set Local Scale](https://neosvrjp.memo.wiki/d/SetLocalRotation)を使ってCameraスロットの位置、回転角度、スケールを設定します。ここでSet Local PositionとSet Local Rotationの左の入力値がないのですが、これらは(0,0,0)が設定されます。そうするとInit PointスロットがCameraの親なので、Init Pointスロットの位置に設定されます。Init Pointスロットは左手スロットの子供であり、そこからの相対位置を持っています。これによりカメラの位置を初期化します。

![pic](https://pbs.twimg.com/media/ETtPxcQU0AEQ9AS?format=jpg&name=large "pic")


### メニューボタンのダブルクリックで表示する

[Standard Controller](https://neosvrjp.memo.wiki/d/Standard%20Controller)を使ってメニューボタンが押されたかどうかを判定します。そして、[Fire On True](https://neosvrjp.memo.wiki/d/Fire%20On%20True)を使ってこのTureの信号をImpulseに変換します。

次に、[Sequence](https://neosvrjp.memo.wiki/d/Sequence)を使って、このImpulseを2つに分けます。しかし同時に2つのImpulseがでるわけではなくて、まず1つめのImpulseは[If](https://neosvrjp.memo.wiki/d/If)をたたきます。そしてIf文は成り立ちません。なぜかというと[Elapsed Time](https://neosvrjp.memo.wiki/d/Elapsed%20Time)では凄く大きな秒数が出力されているからです。
そしてIf文の判定が終わってから次のImpulseがSequenceから出てきて、
[Elapsed Time](https://neosvrjp.memo.wiki/d/Elapsed%20Time)にとどき、経過時間が0にセットされて0が出力されます。このときに[<](https://neosvrjp.memo.wiki/d/%3c)はTureを出力します。

ここで続いてダブルクリックをしているので、0.3秒以内に再びメニューボタンが押されると、SequenceにImpulseが流れ、Ifがたたかれます。このときに[Elapsed Time](https://neosvrjp.memo.wiki/d/Elapsed%20Time)では、前回のインパルスからの経過時間を計っています。これが0.3秒以内であればIf文が成立してImpulseが[Set Local Position](https://neosvrjp.memo.wiki/d/Set%20Local%20Position)に流れます。

このようなやり方でダブルクリックを判定しています。SequenceはImpulseを複数個に分けますが、上から順にImpulseを出していくことに注意が必要です。

[Standard Controller](https://neosvrjp.memo.wiki/d/Standard%20Controller)の3つめの入力は[Get Slot Active Self](https://neosvrjp.memo.wiki/d/Get%20Slot%20Active%20Self)の否定の結果がつながっています。これにより現在CameraがActiveでなければ、Get Slot Active SelfはFalseを返すので、Trueを送り込むことになり、CameraがActiveとなって、セッションに表示されます。逆にCameraが表示されていればGet Slot Active SelfはTrueを返すので、Falseを送り込むことになり、CameraのActiveが外れて、セッションからCameraが表示されなくなります。このようにしてCameraのトグル表示が実現されています。

![pic](https://pbs.twimg.com/media/ETtPxcQU0AEQ9AS?format=jpg&name=large "pic")

## おわりに
Cameraをセッションに表示させるのには、スロットをActiveにすればいいということが分かります。また初期値の設定の仕方が書かれていました。さらにメニューボタンのダブルクリックによりImpulseを出す方法がありました。

## 関連しているノード
Host User, Update, Get Active User, Get Parent Slot, Get Slot Name, Containing, Standard Controller, Fire On True, Sequence, Set Slot Active Self, Elapsed Time, Get Slot Active Self, Set Local Position, SEt Local Rotation, Set Local Scale

## 追記
れにうむ(@rhenium_vrc)さんがよりシンプルなLogiXを提案しています。下記で紹介します。

[ダブルクリックを判定する](DoubleClick.md)

- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/)  
- [LogiX](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/logix.html)  
- [ノード一覧(公式Wiki)](https://wiki.neos.com/LogiX/ja)  
- [型一覧](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/datatype.html)  
