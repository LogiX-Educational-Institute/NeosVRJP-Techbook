<!-- NeosVR Technote-->

# ダブルクリックを判定する

## 概要

[スロットをアクティブにしてセッションに現れさせる](SetSlotActiveSelf.md)ではメニューボタンのダブルクリックを判定するLogiXがありました。ここではれにうむ(@rhenium_vrc)さんが提案したよりシンプルなLogiXを紹介します。

## 解説

Pulseは[If](https://neosvrjp.memo.wiki/d/If)から引き出したノードで、ここをクリックします。[Standard Controller](https://neosvrjp.memo.wiki/d/Standard%20Controller)の出力をImpulseに変換してつなげばメニューボタンのクリックを読み取れます。(「[スロットをアクティブにしてセッションに現れさせる](SetSlotActiveSelf.md)」参照)

最初のImpulseがIfにたどり着く時には、[Elapsed Time](https://neosvrjp.memo.wiki/d/Elapsed%20Time)はとても大きい数字なっています。したがって、IfはFalseとなって、下のノードにImpulseを流します。

すると、[Elapsed Time](https://neosvrjp.memo.wiki/d/Elapsed%20Time)は0にリセットされます。その結果[<](https://neosvrjp.memo.wiki/d/%3c)はTureを出します。

その後、0.3秒以内に次のImpulseがIfに届けば、上のノードにImpulseが出力されます。

![pic](https://pbs.twimg.com/media/ETv-d4BUEAAdwzB?format=jpg&name=large "pic")

## おわりに
れにうむさんによれば、前のLogiXでは三回つづけてクリックするとかすると誤動作するとかで、このシンプルな形になったそうです。

ちなみにRelayを使っているのは、直接つなぐと、平面にLogiXが展開できないので、わかりやすさのために入れています。

また背景もワールドのごちゃごちゃした背景を消すために、ボードをセッション内にスポーンさせてくださいました。　