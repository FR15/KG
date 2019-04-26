
相关资料：
swift 5 官方文档： Automatic Reference Counting

1.1 iOS 使用自动引用计数来管理内存

1.2 循环强引用

2个对象相互强引用，导致任何一方都无法释放，造成内存无法释放；

1.3 解决方法

weak reference

unowned[注意发音] reference

用法区别： 从生命周期来判断；

假如2个对象 A、B 需要相互引用；

如果 A 的生命周期长于 B， 则 A 使用 weak 引用 B， B 释放后，A 引用 B 的指针会自动设置为 nil；

```swift
class A {
    // A的生命周期长于B
    // 所以B可能先释放
    // 所以使用可选类型
    weak var b: B?
}
class B {
    var a: A!
}
```

如果 A 的生命周期短于 B，或者差不多，则 A 使用 unowned 引用 B；使用 unowned 引用要求此引用永远是有值的，也就是说，A 的生命周期不长于 B，只要 A 不释放，则 A 指向 B 的引用永远有值；

```swift
class A {
    unowned var b: B
}

class B {
    // A的生命周期不长于B
    // 所以A可能先释放
    // 所以使用可选类型
    var a: A?
}
```

针对第二种情况，还有一种特殊的情况，就是 A 和 B 的生命周期一样；

```swift
class A {
    unowned var b: B
}

class B {
    // A的生命周期等于B
    // 所以a肯定一直有值
    // 所以使用 隐式展开可选类型 ，提高取值效率
    var a: A!
}
```


1.4 闭包强引用

道理是一样的，闭包是一个对象，对象内部引用了外部对象，导致循环强引用；

```swift
class HTMLElement {
    
    let text: String?
    
    // 闭包内对 self 弱引用
    lazy var asHTML:() -> String = { [unowned self] in
        if let text = self.text {
            return "<name>\(text)</name>"
        } else {
            return ""
        }
    }
    
    init(text: String? = nil) {
        self.text = text
    }
}
```

问题： 

自动引用计数 如何保存

弱引用如何保存







