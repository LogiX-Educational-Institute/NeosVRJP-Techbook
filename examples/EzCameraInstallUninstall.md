<!-- NeosVR Techbook-->

# Ez Cameraのアバターへのインストールとアンインストール

## 概要

レニウム(@rhenium_vrc)さんが作ったEZ Cameraはインストーラーがあります。そこではCamera(NeosVR Essentialにある)をアバターの左手につけておくためのインストールと、左手につけていたCameraを外すアンインストールをするLogiXがあります。その解説をします。

![pic](https://pbs.twimg.com/media/ETzF-7dUMAE9tFU?format=jpg&name=medium "pic")

## 解説

### 全体

全体を見渡すと、
左に[Button Events](https://neosvrjp.memo.wiki/d/Button%20Events)が2つあり、これがそれぞれ上の図の「Install」と「Uninstall」のボタンに接続されています。また右ではインストールするときの[Set Parent](https://neosvrjp.memo.wiki/d/Set%20Parent)とアンインストールするときの[Destory Slot](https://neosvrjp.memo.wiki/d/Destroy%20Slot)があります。


![pic](https://pbs.twimg.com/media/ETzBehCUcAE1dNz?format=jpg&name=large "pic")

### インストール作業

インストールをすると、左手に次の図のような球と「Submit」が現れます。

![pic](https://pbs.twimg.com/media/ETzF-7eUwAEmclO?format=jpg&name=small "pic")

これは次のスロットの階層のEZ CCamera by rheniumが左手の子スロットになった状態です。"pref"はプレハブ(prefab)という意味で、インストール作業をしているときだけ親スロットにいます。そして間違った操作が行われないようにしています。つまり親スロットの名前に"pref"があると、インストール作業中であることが分かります。([スロットをアクティブにしてセッションに現れさせる](SetSlotActiveSelf.md)参照)

![pic](https://pbs.twimg.com/media/ETzF-7xU4AAWxz6?format=jpg&name=large "pic")

さらに「Submit」ボタンを押すとuiというスロットが消されて、位置がInit Pointに書き込まれていて、最終的にInit Pointとez camera logixのみが左手の子スロットとして残ります。uiスロットには球、カメラの形、「Submit」ボタンなどが入っています。([Submitボタンを押してインストールを完了する](EzCameraSubmit.md)参照)

![pic](https://pbs.twimg.com/media/ETzF-8NUYAE-hDD?format=jpg&name=small "pic")

Ez Cameraには2つのボタンがあり、「Install」ボタンを押すと[Button Events](https://neosvrjp.memo.wiki/d/Button%20Events)が一番の上の出力(Pressed)からImpulseを出します。

Impulseは分岐できないので、[Sequence](https://neosvrjp.memo.wiki/d/Sequence)を使ってImpulseを3つに分けています。

1つめのImpluseで現在のユーザーの情報を[Local User](https://neosvrjp.memo.wiki/d/Local%20User)と[Write](https://neosvrjp.memo.wiki/d/Write)を使って、変数Userに格納しています。

2つめのImpulseを使って、すでにインストールされているときには、現在のインストールされているEz Cameraを[Destory Slot](https://neosvrjp.memo.wiki/d/Destroy%20Slot)を使って消します。

3つめのImpulseを使って、インストール作業をします。まず[Duplicate Slot](https://neosvrjp.memo.wiki/d/Duplicate%20Slot)を使ってEZ Cameraスロットを複製します。緑色の帯の左端は切れていますが、中身を確認すればEZ Cameraスロットに接続していることを確認することができます。そして、複製されたEZ Cameraスロットをユーザーの左手のスロットが親になるように[Set Parent](https://neosvrjp.memo.wiki/d/Set%20Parent)を使って設定します。これにより"pref"から外れて、結果的に"pref"が消えます。これで左手にEZ Cameraが入りました。途中でユーザーの左手のスロットを取り出すために、[Body Node Slot](https://neosvrjp.memo.wiki/d/Body%20Node%20Slot)を使っています。

そして次に、[Set Local Position](https://neosvrjp.memo.wiki/d/Set%20Local%20Position)と[Set Local Rotation](https://neosvrjp.memo.wiki/d/SetLocalRotation)と[Set Local Scale](https://neosvrjp.memo.wiki/d/SetLocalRotation)を使ってCameraスロットの位置、回転角度、スケールを初期設定します。ここでSet Local PositionとSet Local Rotationの左の入力値がないのですが、(0,0,0)が入力されます。Cameraスロットの親スロットがInit Pointなので、Init Pointと同じ位置に初期化されます。

最後にNo Impulseと表示されているノードがありますが、これはデバッグ用で、最後までImpulseが届いていることを確認しています。


### アンインストール作業
Ez Cameraにあるもう一つのボタンである、「Uninstall」ボタンを押すと[Button Events](https://neosvrjp.memo.wiki/d/Button%20Events)が一番の上の出力(Pressed)からImpulseを出します。これをまた[Sequence](https://neosvrjp.memo.wiki/d/Sequence)で2つに分けます。

1つ目のImpulseにより、インストール作業と同じように変数Userにローカルユーザーを記録します。

2つめのImpulseにより、[Destory Slot](https://neosvrjp.memo.wiki/d/Destroy%20Slot)を使ってインストールされているEz Cameraスロットを消すのですが、その前にEz Cameraスロットがあるかどうかを確認しています。ここでは[Find Child By Tag](https://neosvrjp.memo.wiki/d/Find%20Child%20By%20Tag)を使って、ローカルユーザーの左手のスロットの下に"Ez Camera"を見つけています。

Destory Slotで消した後もSequenceでまたImpulseをIfに戻しています。これは複数Ez Cameraをインストールしているときに、無くなるまで消すことができる処理です。

<!--  Sequenceの2番目が上の記述であっているか確認する　-->

## おわりに
ここではEz CameraでCameraを左手にインストール、アンインストールするLogiXを説明しました。インストール後には球と「Submit」というボタンが現れます。左手との位置を決めてこのボタンを押すとインストールが完了します。その解説はまた別な記事で行います。([Submitボタンを押してインストールを完了する](EzCameraSubmit.md)参照)
