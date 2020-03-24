<!-- NeosVR Techbook-->

# Submitボタンを押してインストールを完了する

## 概要

 [Ez Cameraのアバターへのインストールとアンインストール](EzCameraInstallUninstall.md)を行うと次のような球と箱と「Submit」というボタンが左手に現れます。

 ![pic](https://pbs.twimg.com/media/ETzF-7eUwAEmclO?format=jpg&name=small "pic")

ユーザーはこの箱や球をグラブして位置や角度、大きさを調整します。そして「Submit」ボタンをレーザーでクリックすると、この箱や球が消えて、Ez Cameraのインストール作業が完了します。

## 解説

### 全体

 ![pic](https://pbs.twimg.com/media/ETzGQKcU0AEFEaH?format=jpg&name=large "pic")
全体を見ると上の緑色の帯は箱や球が入っているスロットであるuiスロットにつながっています。Button Eventsには「Submit」ボタンがつながっています。下の緑色の帯はEZ Cameraスロットがつながっています。

スロットの初期の様子は以下の図のようになっています。
 [Ez Cameraのアバターへのインストールとアンインストール](EzCameraInstallUninstall.md)で解説した「Install」を行うとこの"pref"以下のEZ Cameraスロットが左手のスロットの子スロットとなっています。
![pic](https://pbs.twimg.com/media/ETzF-7xU4AAWxz6?format=jpg&name=large "pic")

さらに「Submit」を押すとuiスロットが消されて、最終的に下記だけが左手のスロットの子スロットとなってインストールが完全に終わります。
![pic](https://pbs.twimg.com/media/ETzF-8NUYAE-hDD?format=jpg&name=small "pic")



### 「Submit」が押されたらuiスロットを壊す
![pic](https://pbs.twimg.com/media/ETzGQKcU0AEFEaH?format=jpg&name=large "pic")

動作は単純で下から見てみましょう。EZ Cameraスロットの親スロットを[Get Parent Slot](https://neosvrjp.memo.wiki/d/Get%20Parent%20Slot)を使って取り出し、その名前を[Get Slot Name](https://neosvrjp.memo.wiki/d/Get%20Slot%20Name)を使って得ます。そのstring型の結果を"pref"と[Contains](https://neosvrjp.memo.wiki/d/Contains)を使って判定して名前に"pref"が入っているかどうかを判定します。"pref"はプレハブ(prefab)で、最初のインストール作業中にはEZ Cameraの親スロットにあるのですが、インストールが終わると無くなります。ここでは"pref"がない時に、[Destroy Slot](https://neosvrjp.memo.wiki/d/Destroy%20Slot)にImpulseが伝わります。これで間違ってインストール作業中に不要な動作が起きないようにしています。

[Destroy Slot](https://neosvrjp.memo.wiki/d/Destroy%20Slot)で壊されるスロットはuiスロットで、箱や球、「Submit」ボタンなど入っています。

## おわりに

