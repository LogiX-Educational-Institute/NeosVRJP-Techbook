# くっつくハート

## はじめに

れにうむ(@rhenium_vrc)さんが作られたハートは、渡されてからアバターの頭の近辺に来るとそのユーザーの頭にくっつきます。このLogiXについて説明します。

![pic](https://pbs.twimg.com/media/ETjQGOeUYAATJQl?format=jpg&name=large "pic")

![pic](https://pbs.twimg.com/media/ETjQNcBUYAEvt7q?format=jpg&name=medium "pic")


## 解説

### 全体
全体を見渡すと、中央にHeadというのが出ています。これは左右の<<と>>を使うとBodyの他の部位、たとえば首とか手とかに変えることができます。また右には0.6とありますが、これは0.6 mの近さに近づいたときに、くっつくことになります。
![pic](https://pbs.twimg.com/media/ETjQGMvU8AIoBnP?format=jpg&name=large "pic")

<!-- Grabbable と　ハートのスロットはどうやって接続しているのか？ -->

### ハートを装備するユーザーの情報を得る
[On Grabbable Grabbed](https://neosvrjp.memo.wiki/d/On%20Grabbable%20Grabbed)を用いて、このハートが握られている(グラブしている)ときにImpulseを発生させます。Impulseは一瞬しかでないので、[Local User](https://neosvrjp.memo.wiki/d/Local%20User)からの情報はWriteを使ってUserという変数に書き込んでおきます。このときにはこのハートを握ったユーザーの情報がUserに書かれます。

次に上の[Nearest User Head](https://neosvrjp.memo.wiki/d/Nearest%20User%20Head)を使って入力Slot(この場合にはハート)から見て最も近いUser Headの情報を取得します。ただしUser(ここではハートを握ったユーザー)は除かれます。そうすると2つ可能性があります。つまりAさんがBさんにハートを与えているときには、ハートを与えられたユーザーBのUser型情報(紫帯)とハートとの距離(青帯)が出力されます。もう一つは、自分で自分に与えているときですが、そのときにはUser型情報(紫帯)は空です。そのときには下の[Nearest User Head](https://neosvrjp.memo.wiki/d/Nearest%20User%20Head)が働いて自分のUser型情報と距離を出力します。

AさんがBさんに与えるときには上のNearest User Headの値が小さくなり、自分で自分に与えているときには下のNearest User Headの値が小さくなります。結局ハートを装備するユーザ－が必ず選ばれるようになっています。

[?:](https://neosvrjp.memo.wiki/d/%3f%3a)の出力はハートを装備するユーザーの情報が渡されます。

<!-- NotNullの役割は？ -->


![pic](https://pbs.twimg.com/media/ETjQGM6UMAA2BKY?format=jpg&name=large "pic")

### ハートと頭の距離が近くなったらくっつける
[Global Transform](https://neosvrjp.memo.wiki/d/Global%20Transform)を使うとスロットのグローバルにおける座標を取り出すことができます。上のGlobal Transformではハートの座標を、下のではハートを装備するユーザーの頭の座標を取り出します。

[Distance](https://neosvrjp.memo.wiki/d/Distance)を使って二つの座標の距離を計算します。それが0.6 m以下であれば[If](https://neosvrjp.memo.wiki/d/If)を使って上の[Set Parent](https://neosvrjp.memo.wiki/d/Set%20Parent)によりSlotの親を設定します。つまりこのときにはハートを装備するユーザーの頭をParentにするので、頭にくっつきます。距離が遠いときにはRoot SlotつまりそのセッションをParentにするので、その位置にくっつくことになります。これも重要で、0.6 m以上離れると、ユーザーの頭から剥がれるということになります。下のSet Parentが無いと、ユーザーの頭から剥がすことができなくなります。

Ifは[On Grabbable Rleased](https://neosvrjp.memo.wiki/d/On%20Grabbable%20Released)によりグラブが解放されたとき、つまり手から離したときに動くようになっています。それまでは動きません。

これで解説は終了です。

![pic](https://pbs.twimg.com/media/ETjQGNlU0AAIdHc?format=jpg&name=large "pic")


## おわりに

ハートがくっつくのには、ハートの親をつけるユーザーの頭にすればいいのですが、そこに至るまでにどの頭なのかとか、距離だとかが関係してきます。それを行うLogiXが上手に組まれています。
