
ObjC 是在运行时动态绑定，也就是说编译时，方法声明和实现是分开的，方法根本调用不了，只有运行时，动态绑定，才能运行方法调用；

那么 swift 运行时是否和 ObjC 一致；

和 ObjC 不同，swift 方法的调用有3种情况；

第一种，类似 C，静态绑定，例如 private methods、 final class methods，效率高；

第二种，类似 ObjC， 例如 @objc 修饰的方法，或者继承 NSObject 的类的方法； 

第三种，类似 C++，使用虚函数表；

除掉前2中情况，swift 默认都是使用第三种，也就是说对于纯 swift 类中的方法调用都是需要查询虚函数表的；


相关介绍见：[减少动态分发提高性能](https://github.com/FR15/KG/blob/master/Swift/swift_%E5%87%8F%E5%B0%91%E5%8A%A8%E6%80%81%E5%88%86%E5%8F%91%E6%8F%90%E9%AB%98%E6%80%A7%E8%83%BD.md)


原文：
https://stackoverflow.com/questions/37315295/how-does-ios-swift-runtime-work

c++ 虚函数
https://www.zhihu.com/question/23971699


