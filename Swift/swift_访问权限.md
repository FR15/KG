访问权限

首先了解 模块 的概念：   
模块： 例如 framework，使用前需要 import ；

1.1 5种访问级别

open/public : 模块之间可以直接访问，最高权限；

internal : 限制在同一模块下可以直接访问；

file-private : 限制在同一文件下可以直接访问；

private : 限制实体只能在其定义的作用域，以及同一文件内的 extension 访问。


1.2 public 和 open ：   

open 只能修饰 类 和 类成员；   
public 修饰的类，只能在其模块内被继承；   
public 修饰的类成员，只能在其模块内被重写；   
open 修饰的类，不受限制，模块内外都可以被继承；   
open 修饰的类成员，不受限制，模块内部都可以被重写； 


1.3 规则： 

实体不能定义在访问权限比它低的实体中，例如 private class 中不能定义 public func；

子类的访问权限不得高于父类的访问权限，例如 父类是 private， 子类不能是 public；不过，子类可以通过重写修改 父类成员的 访问权限；

private\file-private class 其所有的成员的默认访问权限为 private\file-private;

__public class 其所有的成员的默认访问权限为 internal，需要手动指定为 public;__

元组的访问级别将由元组中访问级别最严格的类型来决定，例如 (private, public) 其访问权限为 private;

枚举成员的访问级别和该枚举类型相同，你不能为枚举成员单独指定不同的访问级别;