

1.1 类型检查

在编译的时候会进行类型检查；

1.2 类型推断

如果没有显示的指定类型，swift 会使用类型推断来选择合适的类型，原理很简单，只要检查变量的赋值就可以了；

1.3 可选类型

使用可选类型来处理 值可能缺失的情况；

1.4 可选类型的取值

可选绑定，通过临时变量来获取是否有值；

```swift
var optional: String?

if let value = optional {
    // do something
}
```


隐式展开可选类型(implicitly unwrapped optionals)，前提条件，如果每次取可选类型变量的值的时候总是能取到值，那么可以将变量声明为 隐式展开可选类型；

这样每次取值的时候，省去了检查和展开可选类型的值，提高取值效率；

```swift
var optional: String!
```

1.5 可选类型的探究

可选类型本质是一个枚举：

```swift
public enum Optional<Wrapped> : _Reflectable, NilLiteralConvertible {
    case None
    case Some(Wrapped)

    public init(_ some: Wrapped) { self = .some(some) }
}

let number: Int? = Optional.some(42)
let nonumber: Int? = Optional.none
```

1.6 面试题

```swift
var a: Int? = 3
var b: Int?? = a

var c: Int?? = 3
var d: Int? = c
```

上面的成立，下面的不成立；就是因为它有一个构造函数 `public init(_ some: Wrapped) { self = .some(some) }`;





