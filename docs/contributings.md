NeosVRJP-Techbook

# 編集について  

- リポジトリは[NeosVRJP-Techbook](https://github.com/LogiX-Educational-Institute/NeosVRJP-Techbook)を使用します。
- 画像は外部サイトにアップして、それのリンクを貼ってください。  
- 動画はYoutubeなどにアップして、それのリンクを貼ってください。 
- よくつかうMarkdownの書き方は[こちら](../docs/cheatsheet.md)
- index.mdにある見出しについて（暫定）;
  
|大見出し(#)|中見出し(##)|小見出し(###)|
|:---|:---|:---|
|チュートリアルか作例|作品名|中見出しの解説|

  
# 編集の手順
  
前提:  
元の[リポジトリ](https://github.com/LogiX-Educational-Institute/NeosVRJP-Techbook)を上流  
あなたがforkしたリポジトリを支流と表現します。  
  
また、各エディタ、ツールによって使用方法は異なるので、必要な部分だけ記述します。  
  
- [NeosVRJP-Techbook](https://github.com/LogiX-Educational-Institute/NeosVRJP-Techbook)をforkします。
- 自分の名前のリポジトリになったことを確認します。(支流内での作業"～～")  
- 任意であなたの開発環境などへクローンを行ってください。  
- 二回目以降のためにCode>Cloneから上流のURL(末尾git)をコピーしUpstreamなど分かるように登録しておいてください。
- 上流のURLから念のためにプルを行います。（更新が来てないかみるため）  
～～  
- examples(実例)かtutorial(チュートリアル)のフォルダにsample（記事の名前を英語で書く）.mdと作成し、Markdownで記事を書く。
- indexを編集する。パスは（フォルダ/記事名.md）タイポ注意。
- docsにあるcontributings.mdに自分の名前を書く。
- ここまで行ったら支流へコミットを行います。（任意で内容分を記載してください）
- 支流のページの「Pull requests」からプルリクエストを作成、上流に申請してください。  
～～  
- 管理者はプルリクエストを受け次第適用します。(マージを行う)  
  - この段階では張られたURLが機能しているかや、競合が起きていないかを確認しています。  
  
----
  
## 二回目以降
  
- 上流からプルを行い更新を反映します。  
～～  
- 作業を行う。
- contributings.mdに記事のURLを貼る。パスは（フォルダ/記事名.md）タイポ注意。
- 同様にプルリクエストを行う  
～～  
  

## 競合等不具合が起きている場合
次のことを確認してください;  
- forkをしたあと自分の名前のリポジトリで作業しているかどうか　
- 上流からプルしているかどうか
- Markdownの[書き方](../docs/cheatsheet.md)にあっているかどうか
- コミットしたあとプッシュされているかどうか
  
  
# メンバー
  
- melnus  
  - 管理  
  -   
  -   
  
  
- litalita
  - [Particle Systemを使って桜の花びらをはらはらと散らそう](https://melnus.github.io/NeosVRJP-Techbook/tutorial/particlesystem.html)  
  - [ユーザーリスト](https://logix-educational-institute.github.io/NeosVRJP-Techbook/examples/UserList.html)  
  - [くっつくハート](https://logix-educational-institute.github.io/NeosVRJP-Techbook/examples/GluedHeart.html)  
  - [色の変わるリボン](https://logix-educational-institute.github.io/NeosVRJP-Techbook/examples/ColorChangingRibbon.html)
  - [スロットをアクティブにしてセッションに現れさせる](../examples/SetSlotActiveSelf.md)
  - [ダブルクリックを判定する](../examples/DoubleClick.md)
  - [Ez Cameraのアバターへのインストールとアンインストール](../examples/EzCameraInstallUninstall.md) 
  - [自分の声が聞こえる音符](../examples/VoiceRef.md)
  - [スモールライト](../examples/SmallLight.md)
  - [ブースター](../examples/Booster.md)
  - [拘束具](../examples/Restraint.md)
  - [どこでもドア](../examples/AnywayDoor.md)
  - [アバターにハンドサインから表情をつける](../examples/AvatarEmotion.md)
  - [発券機](../examples/TicketingMachine.md)BoxWithSound
  - [音の鳴る箱](../examples/BoxWithSound.md)
  - [ストップウォッチゲーム](../examples/StopWatchGame.md)
  　
  - 作成中 
  
  
- kurotori
  - [仮想しっぽ触覚デバイス](https://logix-educational-institute.github.io/NeosVRJP-Techbook/examples/VirtualTailSystem.html)
  
  
- [NeosVR日本語Wikiメンバー](https://neosvrjp.memo.wiki/members/)
  - チュートリアルなど