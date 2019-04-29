
值捕获


三次握手和四次握手 详细介绍

TCP有哪些手段保证可靠交付


闭包是引用类型，闭包应该和OC的block原理是一样的，截获变量的值；

逃逸闭包: 将一个闭包作为参数传给一个函数，如果这个闭包在函数返回之后才被执行，称为 逃逸闭包；

逃逸闭包中 必须显示的使用 self; 


自动闭包：自动创建的闭包，不接受任何参数，自动闭包通常是一个表达式；

```swift

class Test {
    
    var arr: [Int] = []
    
    // 这就是一个自动闭包
    lazy var auto = {
        self.arr.append(1)
    }
    
    // 自动闭包作为参数
    func serve(customer customerProvider: @autoclosure () -> Void) {
        customerProvider()
    }
}

let t = Test()
t.serve(customer: t.arr.append(3))
t.auto()

```
 