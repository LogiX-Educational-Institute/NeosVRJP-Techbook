# LogiX

[日本語WikiのLogiXの紹介記事](https://neosvrjp.memo.wiki/d/LogiX)

## Tips

### Impulseは分岐できない

Impulseは順番に実行するという特性から同時に二つにつなぐことはできないです。分岐したいときには[Sequence](https://neosvrjp.memo.wiki/d/Sequence)を使います。そのときには、上から順番にImpulseが出て行きます。同時ではないです。

([Ez Cameraのアバターへのインストールとアンインストール](EzCameraInstallUninstall.md)参照)

### 変数の初期化

変数を初期化するのには、[Write](https://neosvrjp.memo.wiki/d/Write)を使います。Impulseを受けて書き込みます。たとえばグラブされたとかFor文が最初に動き始めたとかいうImpulseをWriteが受けることで初期化されます。

( [ユーザーリスト](UserList.md)参照)

### スロットの位置

スロットの位置は親スロットの位置からの相対位置で表されています。もしPositionもRotationも(0,0,0)であるならば、親スロットの位置と同じ位置になります。

([Ez Cameraのアバターへのインストールとアンインストール](EzCameraInstallUninstall.md)参照)

### 入力が無いときのノードの動作

[Set Local Position](https://neosvrjp.memo.wiki/d/Set%20Local%20Position)を使うときに左側の入力が無いときには、LogixToolを使ってノードを引き出してみるとわかるように、(0,0,0)が入力されています。明示しないことで見た目がすっきりします。

([Ez Cameraのアバターへのインストールとアンインストール](EzCameraInstallUninstall.md)参照)

