
#### GIL 定义

Python 常用的解释器 CPython 存在 Global Interperter Lock 全局解释器锁， 即使是多线程执行，同一时刻只有一个线程在运行。

#### CPython 引入 GIL 的原因

1. python 使用引用计数原则进行内存管理，GIL 保证多线程时的内存安全
2. CPython 大量使用 C 语言库，但 C 语言库都不是原生线程安全的



#### 注意

GIL 的设计，主要是为了方便 CPython 解释器层的编写者，而不是 Python 应用层面的程序员，所以在编写多线程应用程序时还是需要使用 lock 等工具保持线程安全。


#### 避开 GIL

1. 绕过 CPython 使用 JPython 解释器
2. 把关键性能代码，使用其他语言中实现，然后提供 Python 调用的接口
