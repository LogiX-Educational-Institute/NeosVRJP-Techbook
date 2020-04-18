<!-- NeosVR Techbook-->

# ブースター

## 概要

![pic](https://pbs.twimg.com/media/EV37rFCUwAA5OnY?format=jpg&name=medium "pic")

ブースターという作品はトーラスがあって、そこにユーザーが入り込むと、トランポリンのように垂直方向に弾かれるというものです。同時にパーティクルシステムで三角のキラキラしたものが飛び散り、いかにも加速しているというようなサウンドエフェクトの音もします。

## 解説

### 全体

ブースターのLogiXはすごく少ないです。ほとんどはコンポーネントにより構成されます。

### ユーザーを飛ばす仕組み

![pic](https://pbs.twimg.com/media/EV37liiVAAEFcIO?format=jpg&name=large "pic")

ユーザーがトーラスにはいると、トランポリンのように垂直方向にはじかれますが、それはこのCharacterForceFieldコンポーネントにより実現されています。ここではForce:というプロパティが(0,3,0)ですが、オリジナルでは(0,15,0)となっています。これだけで、このトーラスに垂直方向に”力”(ForceField)がかかることになり、入ったオブジェクトはこの影響を受けるようになります。つまり、トーラスをつくり、それにこのCharacterForceFieldを設定するだけで、ユーザーを飛ばす仕組みは実現できます。

### その他のコンポーネント

![pic](https://pbs.twimg.com/media/EV37lijVAAEy2e3?format=jpg&name=large "pic")

インスペクターをみるとBoosterの下にはTorusというトーラス作っているスロット、Particle Systemというパーティクルシステムを作っているスロットがあり、その下はすべてLogiXのノードです。ここではLogiXというスロットを作ってそこに格納することはせずに、Boosterに直接LogiXを格納しています。

そしてTorusアイテム(スロット)にはさきほどのCharacterForceFiledの他に興味深いコンポーネントが追加されています。

Spinnerによりトーラスは回転します。ここでは_speed:が(0,60,0)となって垂直軸の周りに回転します。

CylinderColliderはコライダーを設定します。ここでは半径0.5 mの円柱がトーラスの中心に設定されます。そしてType:にTriggerが設定されています。オブジェクトがこのコライダーに当たると、トリガーのイベントが発生します。

CharacterEventTriggerでは、上で設定したトリガーが発生したときに、TriggerEnterd(list):に書かれていることが実行されるように設定しています。ここではサウンドエフェクトが再生されるようになっています。

RandomAudioClipPlayerがそのサウンドエフェクトを再生します。Clips(list):に今回のサウンドエフェクトが格納されています。それは下図のようになっています。

![pic](https://pbs.twimg.com/media/EV37rFTVAAAKRCD?format=jpg&name=large "pic")

このように、この作品はほとんどがコンポーネントの機能で実現されています。

### パーティクルシステム

さきほどのインスペクターでわかるようにTorusの下にはParticle Systemが含まれています。パーティクルシステム([Particle System](../tutorial/particlesystem.md))はとても強力で、様々な効果を与えることができます。今回は最初の図で示したように、一つ一つは三角の形をした破片が円形に巻き散らかされている効果を与えます。

![pic](https://pbs.twimg.com/media/EV37lihUcAUAsh8?format=jpg&name=large "pic")

上図はそのParticle Systemの中のCircleEmitterコンポーネントの部分です。このように円形にパーティクルがとぶように設定されています。そのうちのEnabled:がピンク色になっています。これはLogiXからつながっていることを示しています。そのLogiXは次のようになっています。

![pic](https://pbs.twimg.com/media/EV0JvFOU0AAu2gx?format=jpg&name=large "pic")


[On Cllision Start](https://neosvrjp.memo.wiki/d/On%20Collision%20Start)はトーラスからつながっており、衝突（コリージョン）が起こったときにImpulseが発生します。そして[Sequence](https://neosvrjp.memo.wiki/d/Sequence)でImpulseを二つに分けます。最初はそのまま[Boolean Latch](https://neosvrjp.memo.wiki/d/Boolean%20Latch)に行き、その出力のTureは先ほどのParticle SystemのCircleEmitterコンポーネントのEnabled:につながっています。つまり、トーラスに何かがぶつかると、CircleEmitterが動き、パーティクルシステムにより三角が巻き散らかされます。そして、0.1秒後にふたたびBoolean LatchにImpulseが送られますが、ここはToggleとなっているので、FalseがEnabled:に送られます。これで次の衝突を待つ準備ができました。

このようにここでのLogiXはとてもシンプルで、トーラスに何かがぶつかったときにCircleEmitterコンポーネントのEnabled:をスイッチオンして、その後オフにしているだけでした。

## おわりに

このようにこの作品はほとんどコンポーネントだけで実現されています。CharacterForceFieldはコンポーネントのLocomotion →　Interactionにありますが、他にもCharacterTeleporterなどがあり、どこかにオブジェクトを飛ばすことができることができるでしょう。

## 関連するノード

On Collision Start, Delay, Boolean Ltach, Sequence

## 関連するコンポーネント

CharacterForceField, Spinner, CylinderCollider, CharacterEventTrigger, RandomAudioClipPlayer, CircleEmitter

<!-- ## 追記 -->