<!-- NeosVR Techbook-->

# 自分の声が聞こえる音符

## はじめに

ProbablePrimeさんの作った(?)不思議な作品を紹介します。

![pic](https://pbs.twimg.com/media/EUWwVTdUMAEc-lV?format=jpg&name=thumb "pic")

外見は上の図のような音符になっていて、これをグラブして声を出すと、なんとこの音符が自分の声でしゃべります。VoiceRefという作品名です。自分の声はなんとも奇妙な声に聞こえます。


## 解説

### 全体図
全体のLogiXは次の図のようになっています。左は音符とかつかんだユーザーの入力になっています。真ん中にEquip Avaterが二つあります。これがとても面白い動作をさせます。そして出力はWriteRefを使っていて音声出力のコンポーネントにつながっています。
![pic](https://pbs.twimg.com/media/EUWwVTgUMAAgn1T?format=jpg&name=large "pic")


### User変数とSlot変数の初期化

最初に左のところから解説します。
[On Grabbable Grabbed](https://neosvrjp.memo.wiki/d/On%20Grabbable%20Grabbed)ではこの音符がグラブされたときにImpulseが発生されて2つのWriteでUser変数にはグラブしたユーザーの情報を記録し、Slot変数にはグラブしたユーザーのアバターのスロットの情報を記録させます。

### dummy avatarに着替える

次に真ん中の[Equip Avater](https://neosvrjp.memo.wiki/d/Equip%20Avatar)が二つあります。このノードではUserにスロットのアバターを装備（着替え）させます。上のEquip Avaterでは何を着替えさせるかというと、なんと音符です。

図にあるようにこの音符にはdummy avatarというのが含まれています。これに着替えさせるわけです。
![pic](https://pbs.twimg.com/media/EUWwVTeUcAIj582?format=jpg&name=large "pic")

さらにもう一つの下のEquip Avaterでは自分自身のアバターに着替えさせます。これが一瞬で行われます。

### WriteRefで音に接続

->では音源を取り出しています。そしてWriteRefではdummy avatarのSoundに接続しています。これにより、自分のアバターからは声がまったく出なくて、音符の中に隠れているdummy avatarから音がでます。その結果、自分の声が、ちょっと遠くから聞こえているようになります。これはとても不思議な感覚です。テープレコーダーで自分の声を聞くとこういう感覚を味わえますが、リアルタイムで聞くことができます。

## 終わりに

アバターを音符に着替えたら視点とかどうなるのでしょう？このLogiXの処理は1フレームごとに行われます。音符をグラブしていると1フレームごとに一瞬アバターを切り替えてもとに戻しています。そして切り替えている瞬間だけ声をdummy avatarから出しています。その結果、ユーザーはアバターが切り替わっているのを気づけません。

とてもおもしろいLogiXでした。

## 関連しているノード
Grabbable Grabber, On Grabbable Grabbed, On Grabbable Released, Get Slot, Get Object Root, Write, Grabbed, On Grabbable Released, Get Slot, Get Object Root, Write, Get Active User, Equip Avatar, WriteRef, On Grabbable Released, ->, User, Slot
