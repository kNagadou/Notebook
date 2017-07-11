# Singleton

---

* 1つのクラスから、1つのオブジェクト/インスタンスしか生成しない
	* 余計なオブジェクト生成を減らしたい
	* わずかでも実行速度を改善したい
	* 本質的に1つのインスタンスで良い場合

---

## Singletonが使える条件

* 別のクラスを継承したり、インターフェースを実装したりする
	* もしくは、継承される
* 属性は ない
  * コンストラクタは引数が ない
  * Setterが1つも存在し ない
* staticなメソッドのみ ではない

http://qiita.com/ndxbn/items/c7a37ea950876176bb81#singleton%E3%81%8C%E4%BD%BF%E3%81%88%E3%82%8B%E3%81%A8%E3%81%8D

---

## Swift実装例

Singletonクラス
```swift
class SingletonPattern {
  static let instance: SingletonPattern = SingletonPattern()
  private init() {}
    
  func doing(success: 
             @escaping (_ response: String?) -> Void, 
             failure: 
             @escaping (_ error: NSError?) -> Void) {
    Stub_ServerConnection.get(success: { (response) in
      print(response)
      success(response.appending(
      "Singleton Pattern で実行しました"))
    }) { (error) in
      print(error)
      failure(error)
    }
  }
}
```

---

Singleton使う側
```swift
// MARK: - Singleton Pattern
  @IBAction func singletonPatternTUI(_ sender: UIButton) {
    inProgress()
    SingletonPattern.instance.doing(success:
    { [weak self] (response) in
      self?.progressSuccess(response: response!)
    }) { [weak self] (error) in
      self?.progressFailure(error: error!)
    }
  }
```