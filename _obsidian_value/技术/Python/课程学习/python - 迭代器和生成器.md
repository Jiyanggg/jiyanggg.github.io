在 Python 中一切皆对象，对象的抽象就是类，而对象的集合就是容器。


#### 容器(Container)

对象的集合

#### 可迭代对象(Iterable)

实现了 \__iter__(), 可以作用于 for 语句进行遍历

#### 迭代器(Iterator)

实现 \__iter__() 和 \__next__() 方法， 可以进行延迟计算

\__iter__() ： 返回 self 迭代器自身

 \__next__()： 返回下一个元素，当没有下一个元素时抛出 StopIteration



#### 生成器(Generator)

生成器是特殊的迭代器 （generator function \ generator expression）


参考：https://segmentfault.com/a/1190000021070739