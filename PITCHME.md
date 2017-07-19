<!-- $theme: default -->

### 久々のLT
- お久しぶりです
- 最近は割とandroidの開発でjavaを書いていました
- 久しぶりにめちゃくちゃswift書きたくなっています
- 研究でpython使ってるとめちゃくちゃswift書きたくなってきます
- swift安心します
- React nativeに負けるな!

---
### 今日の話題
<div style="text-align: center">
<font size = "15">OOP</font><br>
↓ <br>
<font size = "15">POP</font>
</div>

---
### OOPってなんだっけ?
OOP(Object Oriented Programing)
オブジェクト指向プログラミング
- クラス
- 継承
- ポリモーフィズム
やらなんやらを前回紹介しました#generalの"11月8日"ってpdfに前回のLTありました.
データと処理をひとまとめにして共通部分を括りだして実装できるのがいいよねー

---
### POPってなに?
POP(Protocol Oriented Programing)
プロトコル指向プログラミング
プロトコルの詳細はまたのちほど

---

### OOPは概念的にすばらしい!
って前回熱く語りました.
すばらしい,大変素晴らしい.でもappleはPOPを推奨している.
![](/img/protocol.png)

こんな風に標準ライブラリでもprotocolで書かれてるところが多く見られる.(そしてこれはPOPを用いる際良いお手本とされている)

---

### protocolって何?
プロトコルとは「型のインターフェースを定義するもの」
はい,でましたよくわからない説明
噛み砕いて言うと「型が持つべきプロパティとメソッドを定義するもの」
百聞は一見にしかず
一度実装してあるものを見てみる

---
``` swift
protocol SomeProtocol{
	var id: Int{get}
    func someMethod() -> Void
}

struct SomeStruct1: SomeProtocol{
	var id: Int
    func someMethod() -> Void{
    //メソッドの実装
    }
}


```
