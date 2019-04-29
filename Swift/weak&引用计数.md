

内存管理方案

1.1 针对不同场景提供不同内存管理方案；

TaggedPointer

NONPOINTER_ISA

散列表

1.2 散列表

SideTables 是一个64个元素长度的 hash数组；

SideTables 的 hash 键值是 一个对象的地址对应一个 SideTable，即 [obj.address : SideTable]；

也就是说 一个对象对应一个 SideTable，但是一个 SideTable 对应多个对象，因为 SideTable 的数量是有限的，多个对象会共用一个 SideTable；

SideTable 中有2个成员： 

```c
spinlock_t slock;        // 自旋锁
RefcountMap refcnts;     // 引用计数表
weak_table_t weak_table; // 弱引用计数表
```
refcnts 是一个 hash map，key 是对象的地址，value 是对象的引用计数；

weak_table 是一个 hash 表， key 是对象的地址，value 是一个该对象的弱引用；








arm64 架构下， isa 指针是 64位的，这意味着，有些位数是用不到的，为了提高使用率，这些位数用来存储

散列表

SideTables 



1.1 引用计数管理



引用计数表

弱引用计数表