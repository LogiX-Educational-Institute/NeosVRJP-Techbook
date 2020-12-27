- [一覧](#一覧)
  - [組み込み型](#組み込み型)
  - [クラス](#クラス)
  - [インターフェイス](#インターフェイス)

# 一覧

##  組み込み型

|型名|概要|関連LogiX Node|
|:---|:---|:---|
|int|32bit整数|[[int]],[[Int]]|
|long|64bit整数|[[long]],[[Long]]|
|float|単精度浮動小数点数|[[float]],[[Float]]|
|double|倍精度浮動小数点数|[[double]],[[Double]]|
|bool|論理値|[[bool]],[[Bool]]|
|char|文字|[[char]],[[Char]]|
|string|文字列|[[string]],[[String]]|
|floatQ|X,Y,Z回転角度(オイラー角)とX, Y, Z, Wをまとめて7つのfloatで格納している | | |
|float3|X, Y, Z, Wをまとめて3つのfloatで格納している | | |
|...| | |

## クラス

| 型名                  | 概要                     | インターフェイス | 関連LogiX Node                  |
|:---|:---|:---|:---|
| Slot                | Neosにおけるオブジェクトそのものを表す型 |          |                               |
| User                | User(Player)自体を表す型     |          | [[Nearest User Hand]]         |
| CharacterController | ?                      |          | [[Character Ground Collider]] |
| UserRoot| Userのルートを表す型　　|          | |
| Space| 空間の情報を表す型                      |          ||
| HeadOutputDevice| ヘッドマウントディスプレイの情報を表す型 名前(RiftTouch)などが入っている                      |          ||
| ControllerNode| 	                      |          ||
|Chirality| | | |
|color|色情報を扱う型 | | |
|DateTime|日付と時刻を扱う型 | | |
|Grabber||||
|BodyNode||||
|TouchEventRelay||||
|EventState||||
|TextEditor||||
|TipJar||||
|LocomotionGrip||||
|PhysicalLocomotion||||
|Camera|||Renderingノード|
|RawDataTooltip|||Toolsノード|
|BoundingBox|||Transformの下のBoundsのノード|
|SyncType|||UIノード|
|Guid|||Utilityノード|
|TwitchInterface|||Networkの下のTwitchのノード|
|BadgeColor| ||Networkの下のTwitchのノード|
|SubscriptionPlan| ||Networkの下のTwitchのノード|
|...| | | |

##  インターフェイス

| インターフェイス名 | 概要 | 関連LogiX Node |
|:---|:---|:---|
| ICollider| ?    | [[Character Ground Collider]]             |
|IGrabbable||Grabbable|
|IButton||Button|
|ILocomotionModule|||
|IPlayable|||
|IWorldElement||Referenceノード|
|IToolTip||Toolsノード|
|IFocusable||UIノード|
|ISyncRef||UIノード|
|...| | |

