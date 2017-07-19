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

こんな風に標準ライブラリでもprotocolで書かれてるところが多く見られる.

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

---
POPとはこのように「プロトコル」と「構造体」を中心としたプログラミングの方法である.

いや,僕の印象としては構造体を中心としたプログラミングをするためにプロトコルを使うという印象である.

---

|クラス|構造体|
|--|--|
|参照型|値型|
|継承可|継承不可|

---

え?継承不可なら冗長なコード増えるくない?  
↓  
そうならないようにプロトコルを使うのです.

---

そもそもクラスでよくない?  
↓  
参照型を使うことによる予期しないバグが生まれる可能性があるので,できるだけ値型を使おうという指針.
参照型の方が適しているような場面においては参照型のクラスを使っていこうというように使い分ける.

---
### extensionを用いたプロトコルの実装
```swift
protocol Item {
	var name: String{ get }
	var category: String{ get}
}
extension Item {
  var description: String{
		return "商品名: \(name), カテゴリ: \(category)"
	}
}
struct Book: Item {
    let name: String
		var category: String{
			return "書籍"
		}
}

let book = Book(name: "Swift実践入門")
print(book.description) //商品名: Swift実践入門, カテゴリ: 書籍
```
