# LogiX

[日本語WikiのLogiXの紹介記事](https://neosvrjp.memo.wiki/d/LogiX)

## Tips

### Impulseは分岐できない

Impulseは順番に実行するという特性から同時に二つにつなぐことはできないです。分岐したいときには[Sequence](https://neosvrjp.memo.wiki/d/Sequence)を使います。そのときには、上から順番にImpulseが出て行きます。同時ではないです。

### 変数の初期化

変数を初期化するのには、[Write](https://neosvrjp.memo.wiki/d/Write)を使います。Impulseを受けて書き込みます。たとえばグラブされたとかFor文が最初に動き始めたとかいうImpulseをWriteが受けることで初期化されます。

### スロットの位置

スロットの位置は親スロットの位置からの相対位置で表されています。もしPositionもRotationも(0,0,0)であるならば、親スロットの位置と同じ位置になります。
