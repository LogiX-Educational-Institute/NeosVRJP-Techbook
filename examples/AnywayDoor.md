<!-- NeosVR Techbook-->
- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/) 
- [どこでもドア](#どこでもドア)
  - [概要](#概要)
  - [解説](#解説)
    - [全体](#全体)
    - [どこでもドアに入ると原点に移動する](#どこでもドアに入ると原点に移動する)
    - [サウンドエフェクトをならす](#サウンドエフェクトをならす)
    - [どこでもドアの高さと回転角度を戻す。](#どこでもドアの高さと回転角度を戻す)
  - [おわりに](#おわりに)
  - [関連するノード](#関連するノード)
  - [関連するコンポーネント](#関連するコンポーネント)
  - [謝辞](#謝辞)

# どこでもドア

## 概要

![pic](https://pbs.twimg.com/media/EWIc1KrUYAIA3WI?format=jpg&name=thumb "pic")

ドラえもんの道具で一番有名って言ってもいい、どこでもドアを作ってみました。ただ、どこでもいけるわけじゃなくて、ここではリスポーンされた後にアバターが現れるワールドの原点(0,0,0)に戻るようになっています。

## 解説

### 全体
![pic](https://pbs.twimg.com/media/EWNSdwxUwAENeIo?format=jpg&name=large "pic")

全体は3つに分かれています。真ん中上部が、最後[Set Global Position](https://neosvrjp.memo.wiki/d/Set%20Global%20Position)になっており、これでどこでもドアにぶつかってきたユーザーの位置を(0,0,0)にします。次に、右上部の[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)を使って、サウンドエフェクトをならします。最後に[Write](https://neosvrjp.memo.wiki/d/Write)が2つありますが、ここではどこでもドアの高さと角度を元通りにします。これはどこでもドアがグラブされてどこかに置かれて位置が変わったときに、斜めになったり、高さが変なところにならないようにするためです。

### どこでもドアに入ると原点に移動する

![pic](https://pbs.twimg.com/media/EWNTz7UUwAIl4ki?format=jpg&name=900x900 "pic")

左は、どこでもドアの本体のスロットの中の、Box Colliderコンポーネントにつながっています。そして[On Collision Start](https://neosvrjp.memo.wiki/d/On%20Collision%20Start)によりこのスロットに衝突したときにImpulseが発生し、さらにぶつかった情報がIColliderで出力されます。ここから[Get Slot](https://neosvrjp.memo.wiki/d/Get%20Slot)でスロットを得て、[Get Active User](https://neosvrjp.memo.wiki/d/Get%20Active%20User)と[User Root Slot](https://neosvrjp.memo.wiki/d/User%20Root%20Slot)を使って、ぶつかったユーザーのRootスロットの情報を得ます。これを[Set Global Position](https://neosvrjp.memo.wiki/d/Set%20Global%20Position)に入れることにより、ユーザーのグローバル座標をセットします。座標のFloat3に入力がありませんが、これは省略記法で(0,0,0)が入力されていることになっていて、原点にユーザーは戻ります。

### サウンドエフェクトをならす

![pic](https://pbs.twimg.com/media/EWNTz7tU4AYhL94?format=jpg&name=small "pic")

前項のImpulseは次に[Play One Shot](https://neosvrjp.memo.wiki/d/Play%20One%20Shot)ノードの一番目の入力につながっています。これによりぶつかったときにサウンドエフェクトをならすことができます。次の入力はStaticAudioClipProviderコンポーネントに接続されていて、音源を指定しています。このコンポーネントは次の図のようになっています。

![pic](https://pbs.twimg.com/media/EWNSjJiU8AADREn?format=jpg&name=large "pic")

URL:のところに必要なサウンドエフェクトのURLを入力します。具体的には別なところからグラブしてドロップする、あるいは、仮想キーボードを表示させてから、PCの画面でNeosVRを表示させてそこにコピペで貼り付けるなどします。

最後の3番目の入力は音量で、1は最大の音量です。


### どこでもドアの高さと回転角度を戻す。

どこでもドアをグラブしてどこかに置くと、高さがずれたり角度がずれて曲がったりしてドアらしくなくなるので、常に高さは床にくっついているようにして、角度はまっすぐに立っているようにします。

![pic](https://pbs.twimg.com/media/EWNTz67U0AA3YrN?format=jpg&name=large "pic")

左にあるインタフェースノードは全体を示しているグローバル座標を記録しているスロットです。ここからまずPositionについてはいったん[Unpack xyz](https://neosvrjp.memo.wiki/d/Unpack%20xyz)を使って(x,y,z)にばらしておいて、yの情報だけを1.1にして[Pack xyz](https://neosvrjp.memo.wiki/d/Pack%20xyz)でふたたびFLoat3にしてこれをWriteを使って書き出します。書き出す先はもとのPositionです。Neosではyは高さ方向の位置座標です。ここでWriteはImpulseを入力に必要なので、TimerとSequenceを使って、常にImpulseを出してWriteに接続して、座標を書き出しています。

次に角度の方ですが、これもインタフェースノードからRotationの情報(x,y,z,w)を取り出して、[Euler Angles](https://neosvrjp.memo.wiki/d/Euler%20Angles)の(α,β,γ)のFloat3に変換します。これを再びUnpack xyzで3つに分けてこのうちの二つを0度にします。つまりy軸周りの回転は許すが他の回転はさせません。そしてPack xyzでFloat3にもどし、[From Euler](https://neosvrjp.memo.wiki/d/From%20Euler)を使って(x,y,z,w)に変換します。これをWriteを使って、もとのRotationに書き出します。これも常に書き出しています。これでどこでもドアは常に直立しています。

## おわりに

衝突したときに場所を移動するコンポーネントがあります。[CharacterTeleporter](https://neosvrjp.memo.wiki/d/CharacterTeleporter)というものです。これをどこでもドアに使うと、LocomotionがWalkの時にはきちんと動作するのですが、LocomotionがFlyになっていると衝突判定ができずに、動作しません。そこでここでは[On Collision Start](https://neosvrjp.memo.wiki/d/On%20Collision%20Start)ノードを使って衝突の判定をしています。

## 関連するノード

On Collision Start, Get Slot, Get Active User, User Root Slot, Set Global Position, Play One Shot, Timer, Sequence, Write, Unpack xyz, Pack xyz, Eular Angles, From Euler

## 関連するコンポーネント

CharacterTeleporter, StaticAudioClipProvider

## 謝辞

制作はlitalitaが行いましたが、[CharacterTeleporter](https://neosvrjp.memo.wiki/d/CharacterTeleporter)コンポーネント他についてはVEX(0_VEX_0)さんに、[On Collision Start](https://neosvrjp.memo.wiki/d/On%20Collision%20Start)ノードについてはオレンジ(@mikan3134)さんに教えていただきました。感謝申し上げます。

<!-- ## 追記 -->


  

- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/)  
- [LogiX](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/logix.html)  
- [ノード一覧(公式Wiki)](https://wiki.neos.com/LogiX/ja)  
- [型一覧](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/datatype.html)  
  
