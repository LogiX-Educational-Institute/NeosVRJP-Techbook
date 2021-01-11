<!-- NeosVR Techbook-->
- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/) 
- [ユーザーリスト](#ユーザーリスト)
  - [はじめに](#はじめに)
  - [解説](#解説)
    - [全体図](#全体図)
    - [Timer](#timer)
    - [RootSlot](#rootslot)
    - [ForとWriteによるStringの初期化](#forとwriteによるstringの初期化)
    - [コア部分](#コア部分)
    - [出力部分](#出力部分)
    - [改変版のコア部分](#改変版のコア部分)
  - [終わりに](#終わりに)
  - [関連しているノード](#関連しているノード)
  
  
# ユーザーリスト

## はじめに

ここではセッションにいるユーザーリスト（メンバーリスト）を作るLogiXを使って実例の紹介をします。
このLogiXは@Aetoriz_in_VRさんの作品です。本当に10分くらいで作られました。

## 解説

### 全体図
全体のLogiXは次の図のようになっています。左がLogiX、真ん中右のリストがセッションにいるユーザーのリスト、ユーザーリストです。右はTextrendererのインタフェースノードが表示されています。
![pic](https://pbs.twimg.com/media/ETZimUfUcAE1Qot?format=jpg&name=large "pic")


### Timer

最初に左上のところから解説します。

ここでは[Timer](https://neosvrjp.memo.wiki/d/Timer)を使って、一定間隔でImpulseを発生させています。ここでは5秒に一度発火します。これでFor文をたたいています。ここでHost Userは特に必要は無いです。

![pic](https://pbs.twimg.com/media/ETeVCl_UUAQBHXn?format=png&name=small "pic")


### RootSlot
すべての情報は[Root Slot](https://neosvrjp.memo.wiki/d/Root%20Slot)から来ます。
[Root Slot](https://neosvrjp.memo.wiki/d/Root%20Slot)からスロット全体の情報を得て、[For](https://neosvrjp.memo.wiki/d/For)文のループ回数には[Children Count](https://neosvrjp.memo.wiki/d/Children%20Count)を使っています。セッションにあるChildスロットなのでかなりの数が出てくることになります。[Get Child](https://neosvrjp.memo.wiki/d/Get%20Child)でRoot Slotからn番目のChild Slotを取り出します。

![pic](https://pbs.twimg.com/media/ETgl0IXUcAAGxut?format=png&name=small "pic")


### ForとWriteによるStringの初期化
右に[String](https://neosvrjp.memo.wiki/d/String)があります。これにForにつながっている[Write](https://neosvrjp.memo.wiki/d/Write)の出力が薄いピンク色でつながっています。先が矢印になっています。Forの一番上は、Impulseを受けたときに一回だけ実行されます。Writeへの入力はないので、nullがStringに書き込まれて初期化されます。

![pic](https://pbs.twimg.com/media/ETicSooUwAAmjqL?format=png&name=small "pic")


### コア部分
まず、下のGet ChildからWriteのところまでをみてみましょう。[Get Active User](https://neosvrjp.memo.wiki/d/Get%20Active%20User)では「オブジェクトを保持しているユーザーを取得する」をします。Root Slotには多数のSlotがあり、Get Active Userをしてもほとんどはnullになります。これがnullでないときに、ImpulseをWriteにつなぎます。

Writeでは、ユーザー名前を再びStringに書き込んでいきます。これが上の部分で作られます。ここではStringがnullのときとそうでないときで[?:](https://neosvrjp.memo.wiki/d/%3f%3a)を使って切り替えています。つまりnullの時にはUser Usernameからの出力をそのまま、そうで無いときには+からの出力をWriteに入れています。なぜこのようにしているかというと、null+改行を避けるためです。この?:がないと、最初に改行されて、そして1番目のユーザーの名前が現れます。余計な改行はTextの設定次第で見た目を悪くする原因になりえます。

+の最初の入力は[User Username](https://neosvrjp.memo.wiki/d/User%20Username)を使ってユーザー名を文字列にしたものです。これに改行(New Line)加え、さらにこれまでの記録をしているStringを加えています。こうしてStringの上に次々にRoot Slotから得たユーザーの名前が付け加わっていきます。

![pic](https://pbs.twimg.com/media/ETimUgqUEAIa-KL?format=png&name=900x900 "pic")

### 出力部分
最後にStringの内容をRelay(入力に繋がれたものを出力する)を使って、TextRendererに書き込んでいます。これはインタフェースノードを表示させてそのTextという項目に接続すればOKです。

出力をみると分かりますが、このセッションを立てたVEXさんが一番下にあり、そこに新しいメンバーが上に順番に書き込まれています。

![pic](https://pbs.twimg.com/media/ETixb_AUcAEVk_x?format=jpg&name=medium "pic")

### 改変版のコア部分

まず一番上がセッションを立てたユーザー名にして、下に順番に入ってきたユーザー名とするには、+における文字列の接続順番を変えればできます。つまり最初にStringにして改行して次のユーザー名を入れます。

また、最初の改行を許すのであれば、?:の部分を取り除くことができます。そうすると図のようになります。

+への入力順番をさらに変更してString, User Username, New Lineにすれば、null+改行が入らなくなります。

![pic](https://pbs.twimg.com/media/ETirMXvVAAIu2H3?format=jpg&name=large "pic")

## 終わりに
Root Slotからの情報を切り分けて最後はユーザー名の文字列にしてそれをStringに次々に書き込んで行っています。

何かの役に立てば幸いです。

## 関連しているノード
Root Slot, Children Count, For, Get Child, Get Active User, Write, User Username, New Line, String, IsNull, NotNull, If, ?:, Relay
  
  
- [トップページ](https://logix-educational-institute.github.io/NeosVRJP-Techbook/)  
- [LogiX](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/logix.html)  
- [ノード一覧(公式Wiki)](https://wiki.neos.com/LogiX/ja)  
- [型一覧](https://logix-educational-institute.github.io/NeosVRJP-Techbook/tutorial/datatype.html)  
