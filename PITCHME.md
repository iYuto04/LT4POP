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
### 参照型がもたらすバグ
```swift
class Temperature{
	var celsius: Double = 0
}
class Country{
	var temperature: Temparature
	init(temperature: Temparature){
		self.temperature = temperature
	}
}
let temperature = Temperature()
temperature.celsius = 25
let Japan = Country(temperature: temperature)
temperature.celsius = 40
let Egypt = Country(temperature: temperature)
Japan.temperature.celsius // 40
Egypt.temperature.celsius // 40
```

---
### 値型の構造体がもたらす安全性
```swift
struct Temperature{
	var celsius: Double = 0
}
struct Country{
	var temperature: Temperature
}
var temperature = Temperature()
temperature.celsius = 25
let Japan = Country(temperature: temperature)
temperature.celsius = 40
let Egypt = Country(temperature: temperature)
Japan.temperature.celsius // 25
Egypt.temperature.celsius // 40
```

---
swiftでは構造体を積極的に利用することを推奨していて,その上で要求を満たせないときはクラスを利用するように勧めている.
##クラスを利用するべきとき
- 参照を共有する必要がある時
- インスタンスのライフサイクルに合わせて処理を実行するとき

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
---
###クラスの継承に対するプロトコルの優位性
値型である構造体には継承に相当する概念はない.swiftにはプロトコルという抽象概念を表すもう一つの方法があり,構造体はプロトコルに準拠するという形で抽象的な概念を具象化できる.

---
###クラスの継承がもたらす期待しない挙動
```swift
class Animal{
	var owner: String?
	func sleep(){print("Sleeping.")}
	func move(){}
}
class Dog: Animal{
	override func move(){
		print("Running")
	}
}
class Cat: Animal{
	override func move(){
		print("Prancing")
	}
}
class WildEagle: Animal{
	override func move(){
		print("Flying")
	}
}
```

- moveメソッドの多態性が実現されている
- それぞれのサブクラスで実装しなくてもsleep()メソッドを利用できる
しかし次のような予期せぬ挙動も招く
- Animalクラスは特定の動物を表さない抽象的な概念だけどインスタンス化できてしまう
- 野生であるためプロパティが不要なWildEagleクラスにも継承によってownerプロパテティが追加されている.

---
### プロトコルによるクラスの継承の問題点の克服
```swift
protocol Ownable{
	var owner: String{get set}
}
protocol Animal{
	func sleep()
	func move()
}
extension Animal {
	func sleep(){print("Sleeping")}
}
struct Dog: Ownable, Animal{
    var owner: String
		func move(){print("Running")}
}
struct Cat: Ownable, Animal{
    var owner: String
		func move(){print("Prancing")}
}
struct WildEagle: Animal{
    func move(){print("Flying")}
}
```

---
プロトコルと構造体を用いてswiftらいくなコードを書こう
