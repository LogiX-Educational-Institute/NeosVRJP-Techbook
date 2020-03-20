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
すべての情報はRootSlotから来ます。
RootSlotからスロット全体の情報を得て、For文のループ回数にはChildrenCountを使っています。GetChildでRootSlotからn番目のChildを取り出します。セッションにあるChildスロットなのでかなりの数が出てくることになります。
![pic](https://pbs.twimg.com/media/ETgl0IXUcAAGxut?format=png&name=small "pic")


