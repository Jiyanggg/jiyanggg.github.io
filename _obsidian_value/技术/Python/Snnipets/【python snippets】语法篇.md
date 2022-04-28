## Bash 调用 Python 脚本的参数传递

```
sys.argv
```

## Python 函数的参数类型 ?
```
必选参数，默认参数，可变参数，关键字参数
def func(fargs, *args, **kwargs)
    pass
    
函数注解：def f(ham: 42, eggs: int = 'spam') -> "Nothing to see here":
```

## 模块与包的使用

需要避免循环调用

```
__all__ = ["echo", "surround", "reverse"]
```

## 函数式编程 ?
```
map() 
filter() 
reduce()
```

## 常见的数据结构 ?
```
list: sort() reverse() 
set: intersection() differrence() 
dict: 
defaultdict: defaultdict(list)
counter: Counter(name for name, colour in colours)
deque: d.popleft()
namedtuple: namedtuple('Animal', 'name age type')
enum:
```
