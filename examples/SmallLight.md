<!-- NeosVR Techbook-->

# スモールライト

## 概要

ドラえもんの世界にある、スモールライトです。トリガーを引くとビームがでて、そのビームが当たったオブジェクト(図のレイでは牛乳パック)はだんだん小さくなります。

![pic](https://pbs.twimg.com/media/EVAI9umVAAUJXZf?format=jpg&name=thumb "pic")
![pic](https://pbs.twimg.com/media/EVAI9u_U0AU0LQ2?format=jpg&name=thumb "pic")


## 解説

### 全体
![pic](https://pbs.twimg.com/media/EVAJgS0U8AMD5AX?format=jpg&name=small "pic")

左に[Raycater](https://neosvrjp.memo.wiki/d/Raycaster)があります。これが「コライダーにぶつかるまでまっすぐ飛ぶ不可視の測定レーザー(レイ)を飛ばし続ける」を行い、前方に物体があることを見つけます。

真ん中に[Standard Controller](https://neosvrjp.memo.wiki/d/Standard%20Controller)があります。これでトリガーを引いていることを検出します。

右に[Global Transform](https://neosvrjp.memo.wiki/d/Global%20Transform)と[Set Global Scale](https://neosvrjp.memo.wiki/d/Set%20Global%20Scale)があり、物体のスケールを小さくしていきます。

### 物体の検出

スモールライトの前方にある物体の検出を[Raycater](https://neosvrjp.memo.wiki/d/Raycaster)で行っています。これには向きをベクトルで与えたり、Userでないことを示したり、どのくらいの距離までレーザ－（レイ）を飛ばすのかなどを入力します。そして出力としては"HitCollider(ICollider)"がでてきます。これを[Get Slot](https://neosvrjp.memo.wiki/d/Get%20Slot)と[Get Object Root](https://neosvrjp.memo.wiki/d/Get%20Object%20Root)を使って、その物体のRoot Slotを手に入れます。

### トリガーを引いていることの検出

スモールライトはトリガーを引いているときだけ、働きます。そこで[Standard Controller](https://neosvrjp.memo.wiki/d/Standard%20Controller)を用いて右手のトリガーが引かれているときだけTrueが出力されるようにします。このときにスモールライトのスロットを入力にして[Get Active User](https://neosvrjp.memo.wiki/d/Get%20Active%20User)スモールライトを持っているユーザーを得てStandard Controllerに入力しています。

またトリガーを引いているときだけビームがでます。ビームにはInventory→Neos Essentials→Examples にある[Green Laser](http://wiki.neosvr.com/subdom/wiki/index.php?title=Green_Laser/ja)を利用しています。そのインタフェースノードが中央に表示されていますが、そのActiveにトリガーの結果を接続しています。これによりトリガーが引かれているときだけ、ビームが表示されます。

またトリガーを引いているときだけ、0.25秒ごとに、スケールの縮小操作（ここでは0.97倍)をするようにします。そのために、[Fire While True](https://neosvrjp.memo.wiki/d/Fire%20While%20True)によりTrueが入力されているときにはパルスが出ているようにします。そして[Impulse Timeout](https://neosvrjp.memo.wiki/d/Impulse%20Timeout)を用いて0.25秒間はパルスの出力を行わないようにします。逆に言うと0.25秒ごとにImpulseの出力が行われます。

### 物体のスケールを小さくする

[Global Transform](https://neosvrjp.memo.wiki/d/Global%20Transform)と[Set Global Scale](https://neosvrjp.memo.wiki/d/Set%20Global%20Scale)があり、ここでは0.25秒ごとのImpulseを受けると元のスケールから0.97倍されたスケールをセットしていきます。これによって徐々に物体のスケールが小さくなっていく様子が再現できます。

### グリーンレーザーの処理

このスモールライトでは[Green Laser](http://wiki.neosvr.com/subdom/wiki/index.php?title=Green_Laser/ja)を利用していますが、これが検出されて小さくなっては意味がありません。

![pic](https://pbs.twimg.com/media/EVARXSlU8AAuUnv?format=jpg&name=small "pic")

![pic](https://pbs.twimg.com/media/EVARXSjU0AEnuIz?format=jpg&name=small "pic")

この図のようにConeColliderとGrabbableのEnabledのチェックを外して、衝突判定がされず、つかむこともできない、つまり一体となっているように設定します。

## おわりに

NeosVRはドラえもんの世界を再現できます。独自の物理(LogiX)があり、物理法則を利用してワールドのオブジェクトに影響を与えることができます。ここではスモールライトを紹介しました。

## 関連するノード
Raycater, Standard Controller, Global Transform, Set Global Scale, Get Slot Get Object Root, Get Active user, Fire While True, Impulse Timeout, Global Transform, Set Global Scale


<!-- ## 追記 -->
