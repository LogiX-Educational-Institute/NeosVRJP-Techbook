# ユーザーリスト

## はじめに

ここではセッションにいるユーザーリスト（メンバーリスト）を作るLogiXを使って実例の紹介をします。
このLogiXは@Aetoriz_in_VRさんの作品です。本当に10分くらいで作られました。

## 解説

### 全体図
全体のLogiXは次の図のようになっています。
![pic](https://pbs.twimg.com/media/ETZimUfUcAE1Qot?format=jpg&name=large "pic")


### Timer

最初に左上のところから解説します。

ここでは[Timer](https://neosvrjp.memo.wiki/d/Timer)を使って、一定間隔でImpulseを発生させています。ここでは5秒に一度発火します。これでFor文をたたいています。ここでHost Userは特に必要は無いです。
![pic](https://pbs.twimg.com/media/ETeVCl_UUAQBHXn?format=png&name=small "pic")


### RootSlot
すべての情報は[Root Slot](https://neosvrjp.memo.wiki/d/Root%20Slot)から来ます。
[Root Slot](https://neosvrjp.memo.wiki/d/Root%20Slot)からスロット全体の情報を得て、[For](https://neosvrjp.memo.wiki/d/For)文のループ回数には[Children Count](https://neosvrjp.memo.wiki/d/Children%20Count)を使っています。セッションにあるChildスロットなのでかなりの数が出てくることになります。[Get Child](https://neosvrjp.memo.wiki/d/Get%20Child)でRoot Slotからn番目のChildを取り出します。
![pic](https://pbs.twimg.com/media/ETgl0IXUcAAGxut?format=png&name=small "pic")


### ForとWriteによるStringの初期化
右に[String](https://neosvrjp.memo.wiki/d/String)があります。これにForにつながっている[Write](https://neosvrjp.memo.wiki/d/Write)の出力が薄いピンク色でつながっています。先が矢印になっています。Forの一番上は、Impulseを受けたときに一回だけ実行されます。Writeの入力はないので、nullがStringに書き込まれて初期化されます。
![pic](https://pbs.twimg.com/media/ETicSooUwAAmjqL?format=png&name=small "pic")


### コア部分
まず、下のGet ChildからWriteのところまでをみてみましょう。[Get Active User](https://neosvrjp.memo.wiki/d/Get%20Active%20User)では「オブジェクトを保持しているユーザーを取得する」をします。Root Slotには多数のSlotがあり、Get Active Userをしてもほとんどはnullになります。これがnullでないときに、ImpulseをWriteにつなぎます。

Writeでは、ユーザー名前をStringに書き込んでいきます。これが上の部分で作られます。ここではStringがnullのときとそうでないときで[?:](https://neosvrjp.memo.wiki/d/%3f%3a)を使って切り替えています。つまりnullの時にはnullをそうで無いときには+からの出力をWriteに入れています。

+では[User Username](https://neosvrjp.memo.wiki/d/User%20Username)を使ってユーザー名を文字列で得ています。これに改行(New Line)加え、さらにこれまでの記録をしているStringを加えています。こうしてStringの上に次々にRoot Slotから得たユーザーの名前が付け加わっていきます。
![pic](https://pbs.twimg.com/media/ETimUgqUEAIa-KL?format=png&name=900x900 "pic")

### 改良版のコア部分
![pic](https://pbs.twimg.com/media/ETirMXvVAAIu2H3?format=jpg&name=large "pic")


