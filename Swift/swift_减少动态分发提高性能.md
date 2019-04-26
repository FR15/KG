
#### 减少动态分发提高性能

[原文](https://developer.apple.com/swift/blog/?id=27)

1.1 动态分发

swift 允许子类重写父类的方法和属性，这意味着程序需要在运行时才能确定一个对象的类型(到底是子类还是父类)及其关联的属性和方法，然后间接调用(这种技术称为 动态分发)；

swift 中，动态分发的实现原理是 在方法列表中查找对应的函数(见1.4)，然后再调用；

这种间接调用方式效率肯定低于直接调用，而且会防止编译器做一些优化，从而使 动态分发 的代价更加昂贵；

动态分发增加了运行时的开销，对于性能敏感的代码，应尽量避免；

1.2 final 

final 可以限制 class、method、property 不被重写，有效避免 动态分发；

1.3 访问权限

只要 属性、方法对外是不可见的，就无法重写，编译器就可以推断其具有 final 特性；

方式1：

private 可以限制 class、method、property 的可见性，private function 对子类不可见，无法重写，所以编译器视 private function 为 final function；

方式2：

```swift
public class ParticleModel {
    var point = ( x: 0.0, y: 0.0 )
    var velocity = 100.0

    func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
        point = newPoint
        velocity = newVelocity
    }

    public func update(newP: (Double, Double), newV: Double) {
        updatePoint(newP, newVelocity: newV)
    }
}
```

编译器可以推断出 属性 `point`、`velocity`，及函数 `updatePoint` 是可以具有 final 特性的，但是方法 `update` 不能，因为它是 public ;


1.4 C++ 多态虚函数表

动态分发说白了就是 多态；

首先了解 C++ 的多态；

C++ 虚函数表是支撑C++多态的重要技术；

一个类中如果有虚函数，那么该类就有一个虚函数表，这个虚函数表是属于类的，所有该类的实例化对象中都会有一个虚函数表指针去指向该类的虚函数表；

虚函数就像 抽象基类中定义的一个方法，是给子类去重写的；

例如：

```c
// A 是基类  B 是子类
// func 是A中虚函数，B中实现了 func
ClassA *a = new ClassB();
// a 其实是 ClassB 的实例
// 调用流程
// a -> 虚函数表指针 -> 虚函数表(查找函数指针) -> 调用函数 
a.func();
```

swift 的动态分发就应该是指 查询虚函数表；

[c++虚函数表](https://blog.csdn.net/qq_36359022/article/details/81870219)



