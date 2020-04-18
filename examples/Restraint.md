<!-- NeosVR Techbook-->

# 拘束具

## 概要

![pic](https://pbs.twimg.com/media/EV0KgIiVcAMNqLM?format=jpg&name=small "pic")

このトーラスに腕を通すと、そのユーザーは腕を動かすことができなくなってしまいます。どのようにしてこの機能を実現しているのでしょうか？

## 解説

### 全体

![pic](https://pbs.twimg.com/media/EV0KixgU8Ac1TGg?format=jpg&name=large "pic")

これが全体のLogiXの様子です。左はトーラスから来ています。そして最後は[Set Slot Active Self](https://neosvrjp.memo.wiki/d/Set%20Slot%20Active%20Self)が働いています。上のSet Slot Active SelfではTrueが入り、下ではFalseが入っています。Falseが入ると、腕が動かなくなるという仕組みです。


### Slotの中身

最初に右下のSlot変数に何が入るか見てみましょう。左の[Get Active User](https://neosvrjp.memo.wiki/d/Get%20Active%20User)によりトーラスを握っているUserを得ます。そして[Body Node Slot](https://neosvrjp.memo.wiki/d/Body%20Node%20Slot)、[Find Child By Name](https://neosvrjp.memo.wiki/d/Find%20Child%20By%20Name)を通じてRight Hand ProxyのSlotを得ます。これが右下のSlot変数に入る内容です。

### トーラスをつかんでいるとき

最初はトーラスをつかんでいて、これを拘束したい別のユーザーに近づけます。このときには動かなくなったら困りますので、動けるようにする必要があります。これを上の部分で行っています。[Is Grabbable Grabbed](https://neosvrjp.memo.wiki/d/Is%20Grabbable%20Grabbed)により、このトーラスが握られているかどうかを判定します。これがTrueの時には[Fire On True](https://neosvrjp.memo.wiki/d/Fire%20On%20True)でImpulseをSet Slot Active Selfにだします。ここではTrueが入力されており、動けます。

### トーラスから手を離すと

そしてトーラスから手を離すと下のSet Slot Active SelfでRight Hand ProxyのSlotがFalseにされます。つまり動けなくなります。

## おわりに

この拘束具はSet Slot Active Selfを使って、Activeかそうでないかを設定することによりアバターの動きを決めていました。実際に動けなくなると、かなりおかしなことが起きます。自分一人の時には助けが誰もいませんから、緊急リスポーンが必要になるかもしれませんね。

## 関連するノード

Set Slot Active Self, Is Grabbable Grabbed, Get Active User, Body Node Slot, Fire On True, Write

<!-- ## 追記 -->