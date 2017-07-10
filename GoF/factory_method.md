# Factory Method

---

* Factory
  * 「オブジェクト生産工場」のことを言う

* **Factroy Method**
	* オブジェクトの生成手順をパターン化したもの
	* 「抽象的な工場」

---

## 役割

---

### 1. Creator 作成者
### 2. Product 製品
### 3. ConcreteCreator 具体的な作成者
### 4. ConcreteProduct 具体的な製品

<br><br>

抽象度 | 役割
-------|-----
High | Creator、Product
Low | ConcreteCreator、ConcreteProduct

---

Creator.java
```java
protocol abstract class Creator{

    // abstract キーワードが必要
    public abstract Product factoryMethod(); 

    // 抽象クラスの中にメソッドを定義することもできる
    public final Product create(){ 
	Product product = factoryMethod();
	return product;
    }
}
```

---

Product.java
```java
public abstract class Product{
    public abstract void method1();
    public abstract void method2();
}
```

---

ConcreteCreator.java
```java
public class ConcreteCreator extends Creator{
    public Product factoryMethod(){
	return new ConcreteProduct();
    }
}
```

---

ConcreteProduct.java
```java
public class ConcreteProduct extends Product{
    public void method1(){
	System.out.println("method1");
    }

    public void method2(){
	System.out.println("method2");
    }
}
```

---

Client.java
```java
public class Client{
    public static void main(String[] args){
	// Creator は抽象クラスなので, 
	//Creator() コンストラクタが使えない.
	Creator creator = new ConcreteCreator();
	Product product = creator.factoryMethod();

	product.method1();
	product.method2();
    }
}
```

---

* Swiftに移植してみたけど。。。
	- https://github.com/kNagadou/FactoryMethodSwift

---

* 参考
  * http://www.ie.u-ryukyu.ac.jp/~e085739/java.it.1.html