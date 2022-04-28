
### 反射

JAVA 反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的方法的功能称为 java 语言的反射机制。

### 异常

异常和错误的区别：异常能被程序本身处理，错误是无法处理。

```
Throwable -> Exceptions 
Throwable -> Errors 
```

tip: 对资源的使用异常处理, 使用 try-with-resource 

```java
try (Scanner scanner = new Scanner(new File("test.txt"))) {
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException fnfe) {
    fnfe.printStackTrace();
}
```

### 多线程/多进程


程序: 是静态的代码

进程: 进程是资源分配的最小单位 

线程: 线程是CPU调度的最小单位


> 切换进程需要开辟新的上下文, 消耗资源, 而同类的多个线程共享一块内存空间和一组系统资源


### 文件与 I/O 流

- 按照流的流向分，可以分为输入流和输出流；
- 按照操作单元划分，可以划分为字节流和字符流；
- 按照流的角色划分为节点流和处理流。


BIO,NIO,AIO 有什么区别?

- BIO 同步阻塞 I/O 模式，数据的读取写入必须阻塞在一个线程内等待其完成。
- NIO 同步非阻塞的 I/O 模型: 它支持面向缓冲的，基于通道的 I/O 操作方法
- AIO 异步非阻塞的 IO 模型

> 同步/异步：程序之间的消息通信机制, 阻塞/非阻塞: 程序在等待调用结果时的状态