# はじめに

これはNeosVR日本語Wiki [https://neosvrjp.memo.wiki/](https://neosvrjp.memo.wiki/)　の応用編である「複数の項目にまたがる」＆「初心者で扱うものよりは難しい」項目に限って、専門にまとめる用の技術ノートです。

LogiXのノードやToolTipsなど、各項目について詳しく知りたい方は日本語Wikiをご利用ください。
  
# チュートリアル (LogiXやDevToolTipのチュートリアル) 
## [DevToolTip](tutorial/devtool.md)
  
  
## [LogiX](tutorial/logix.md)  
  
  
## [Particle System](tutorial/particlesystem.md)  
  
  
## [工事中]

<br>
<br>

# メイキング・作例（外部リンクなど解説をまとめたもの）
## [色の変わるリボン](examples/ColorChangingRibbon.md)  
<details><summary>関連しているノード</summary><div>
(FromHSV, T/10, Sin)
</div></details>
  

  
## [ユーザーリスト](examples/UserList.md)  
<details><summary>関連しているノード</summary><div>
(Root Slot, Children Count, For, Get Child, Get Active User, Write, User Username, New Line, String, IsNull, NotNull, If, ?:, Relay)
</div></details>
  
  
## [くっつくハート](examples/GluedHeart.md)  
<details><summary>関連しているノード</summary><div>
(On Grabbable Grabbed, Local User, Write, User, Nearest User Head, NotNull, Body Node Slot, Global Transform, Distance, On Grabbable Released, Root Slot, Set Parent)
</div></details>
  
  

## [スロットをアクティブにしてセッションに現れさせる](examples/SetSlotActiveSelf.md)  
<details><summary>関連しているノード</summary><div>
(Host User, Update, Get Active User, Get Parent Slot, Get Slot Name, Containing, Standard Controller, Fire On True, Sequence, Set Slot Active Self, Elapsed Time, Get Slot Active Self, Set Local Position, SEt Local Rotation, Set Local Scale)
</div></details> 
  
  
## [ダブルクリックを判定する](examples/DoubleClick.md)  
<details><summary>関連しているノード</summary><div>
(If, Elapsed Time, Relay)
</div></details>
  
  

## [Ez Cameraのアバターへのインストールとアンインストール](examples/EzCameraInstallUninstall.md)  
<details><summary>関連しているノード</summary><div>
(Button Events, Write, Sequence, Local User, Body Node Slot, Duplicate Slot, Set Parent, Set Local Position, Set Local Rotation, Set Local Scale, NotNull, Find Child By Tag, Destroy Slot, Relay)
</div></details>
  

## [Submitボタンを押してインストールを完了する](examples/EzCameraSubmit.md)  
<details><summary>関連しているノード</summary><div>
(Button Events, Relay, Get Parent Slot, Get Slot Name, Contains, If Write, Destroy Slot)
</div></details>


## [工事中]
<details><summary>関連しているノード</summary><div>
...
</div></details>
  
  
----
[編集規則.メンバーなど](docs/contributings.md)



