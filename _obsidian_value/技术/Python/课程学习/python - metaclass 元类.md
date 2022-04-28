

### 概况

类的实例化是对象，元类的实例化是类， type 是特殊的元类

### 特殊的元类 type

type 的参数

```
type(name, bases, dict):

1. class的名称；
2. 继承的父类集合，注意Python支持多重继承，如果只有一个父类，别忘了tuple的单元素写法；
3. class的方法名称与函数绑定，这里我们把函数fn绑定到方法名hello上。
```

示例：

```
class Foo(object):
    bar = True

    def echo_bar(self):
        print(self.bar)
```

等效于

```
def echo_bar(self):
    print(self.bar)

Foo = type('Foo', (), {'bar':True, 'echo_bar': echo_bar})
```

