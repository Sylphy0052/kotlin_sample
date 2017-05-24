# kotlin_sample

## Kotlinとは…
- Kotlinは静的型付けのコンパイラ言語

## Hello World!

```
fun main(args: Array<String>) {
    println("Hello World!")
}
```
- 文末に`;`はいらない
- defaultでpublic
- printlnはクラスに属さない関数として実装されている

## Memo
### 変数宣言
```
var s: String = "abc"
val t: String = "def"
```

- 変数名の後ろに型を宣言する
- `var`は変数
- `val`はfinal変数
- 型推論があるため，型の省略ができる -> `var s = "abc"`

### プリミティブ型
```
JavaCode -> Kotlin
-------------------
int a = 42; -> var a: Int = 42
final boolean b = true; -> val b: Boolean = true
```

- この型はクラスとして振る舞うのでメソッドを呼ぶことができる

### 制御構文
#### if
- ifは式として使えるので，ifやelseのブロック中で最後に評価された式の値を直接代入できる
- まるで三項演算子
```
var foo = if(bar < 42) {
    "abc"
} else {
    "xyz"
}
```

#### for
- 拡張for文しかない

- pythonっぽい
```
for(number in numbers) {
    println(number)
}
```

```
for(i in 0 until 100) {
    println(i)
}
```

- このuntilはメソッドであり，`0 until 100`は`0.until(100)`と同じ -> 中置記法のメソッド

```
for(i in 99 downTo 0) // for(int i = 99; i >= 0; i--)
for(i in 0 until 100 step 2) // for(int i = 0; i < 100; i += 2)
for(i in 1..100) // for(int i = 1; i <= 100; i++)
```

#### switch -> when
- Javaの`switch`はKotlinでは`when`を使う
```
val s = when(a) {
    0 -> "abc"
    1, 2 -> "def"
    else -> "xyz"
}
```
- ん〜シンプルでこれ好き

#### new
- コンストラクタの呼び出しに`new`はいらない
```
val foo = Foo()
```

#### クラス
- アクセス修飾子は`public`,`private`,`protected`,`internal`

- `protected`は同じパッケージ内でもサブクラスからしかアクセスできない
- `internal`は同じモジュール内からアクセスできる

- Kotlinにはフィールドが存在しないため，変数はプロパティとなる(getter/setterをまとめたようなもの)

```
class Person {
    val firstName: String
    val lastName: String
    val age: Int

    constructor(firstName: String, lastName: String, age: Int) {
        this.firstName = firstName
        this.lastName = lastName
        this.age = age
    }

    fun getFullName(): String {
        return firstName + " " + lastName
    }
}
```

- プロパティの使い方
```
// Java
final int age = person.getAge();
person.setAge(age+1);

// Kotlin
val age = person.age
person.age = age + 1
```

- `person.fullName`で取得可能

```
val fullName: String
    get() {
        return firstName + " " + lastName
    }
```

- varで宣言するとsetterの実装も可能

- プロパティの実装が式1つで済む場合

```
val fullName: String
    get() = firstName + " " + lastName
```

- プロパティはメソッドと等価なので，サブクラスでオーバーライドやインタフェースにプロパティを宣言して，それをオーバーライドして実装もできる

#### コンストラクタ
- プロパティの宣言とコンストラクタの宣言をまとめることができる(プリまりコンストラクタ)

```
class Person(val firstName: String, val lastName: String, var age: Int) {

}
```

- これはプロパティを初期化する処理しか書けない

- `init`を使う

```
class Person(val firstName: String, val lastName: String) {
    var age: Int

    init {
        age = 0
    }
}
```

- `constructor`で作るコンストラクタ(セカンダリコンストラクタ) -> いくつでも作れる

```
class Person(val firstName: String, val lastName: String, var age: Int) {
    constructor(firstName: String, lastName: String) : this(firstName, lastName, 0) {
    }
}
```

- `age`を省略するだけのコンストラクタなら次のようにかける

```
class Person(var firstName: String, val lastName: String, var age: Int = 0) {
}
```

#### メソッド
