来源：https://github.com/piglei/one-python-craftsman

### 建议

```
- 更多的使用 yield 关键字，返回生成器对象
- 尽量使用生成器表达式替代列表推导表达式
    生成器表达式：(i for i in range(100)) 👍
    列表推导表达式：[i for i in range(100)]
- 尽量使用模块提供的懒惰对象：
    使用 re.finditer 替代 re.findall
    直接使用可迭代的文件对象： for line in fp，而不是 for line in fp.readlines()
```

根据场景选择对应的容器类型

### 使用生成器代替放回生成列表的函数

Before
```
def add_ellipsis(comments: typing.List[str], max_length: int = 12):
    """如果评论列表里的内容超过 max_length，剩下的字符用省略号代替
    """
    index = 0
    for comment in comments:
        comment = comment.strip()
        if len(comment) > max_length:
            comments[index] = comment[:max_length] + '...'
        index += 1
    return comments


comments = [
    "Implementation note",
    "Changed",
    "ABC for generator",
]
print("\n".join(add_ellipsis(comments)))
```

Better
```
def add_ellipsis_gen(comments: typing.Iterable[str], max_length: int = 12):
    """如果可迭代评论里的内容超过 max_length，剩下的字符用省略号代替
    """
    for comment in comments:
        comment = comment.strip()
        if len(comment) > max_length:
            yield comment[:max_length] + '...'
        else:
            yield comment


print("\n".join(add_ellipsis_gen(comments)))
```

### 优雅的使用各种数据结构和算法模块
```
import bisect


# BREAKPOINTS 必须是已经排好序的，不然无法进行二分查找
BREAKPOINTS = (1, 60, 3600, 3600 * 24)
TMPLS = (
    # unit, template
    (1, "less than 1 second ago"),
    (1, "{units} seconds ago"),
    (60, "{units} minutes ago"),
    (3600, "{units} hours ago"),
    (3600 * 24, "{units} days ago"),
)


def from_now(ts):
    """接收一个过去的时间戳，返回距离当前时间的相对时间文字描述
    """
    seconds_delta = int(time.time() - ts)
    unit, tmpl = TMPLS[bisect.bisect(BREAKPOINTS, seconds_delta)]
    return tmpl.format(units=seconds_delta // unit)

now = time.time()
print(from_now(now))
print(from_now(now - 24))
print(from_now(now - 600))
print(from_now(now - 7500))
print(from_now(now - 87500))
# OUTPUT:
# less than 1 second ago
# 24 seconds ago
# 10 minutes ago
# 2 hours ago
# 1 days ago
```

### 使用动态解包

动态解包操作是指使用 * 或 ** 运算符将可迭代对象“解开”的行为

```
user = {**{"name": "piglei"}, **{"movies": ["Fight Club"]}}
```

### 避免“获取许可”和“要求原谅”
```
# AF: Ask for Forgiveness
# 要做就做，如果抛出异常了，再处理异常
def counter_af(l):
    result = {}
    for key in l:
        try:
            result[key] += 1
        except KeyError:
            result[key] = 1
    return result


# AP: Ask for Permission
# 做之前，先问问能不能做，可以做再做
def counter_ap(l):
    result = {}
    for key in l:
        if key in result:
            result[key] += 1
        else:
            result[key] = 1
    return result
```

Better
```
from collections import defaultdict

def counter_by_collections(l):
    result = defaultdict(int)
    for key in l:
        result[key] += 1
    return result
```

还有这些语法糖
```
dict[key] = dict.setdefault(key, 0) + 1
dict.pop(key, None)
dict.get(key, default_value)
```

### 当心消费完成的迭代器
```
numbers = [1, 2, 3]
numbers = (i * 2 for i in numbers)

# 第一次循环会输出 2, 4, 6
for number in numbers:
    print(number)

# 这次循环什么都不会输出，因为迭代器已经枯竭了
for number in numbers:
    print(number)
```

### 不要在循环体类修改被循环对象
```
def remove_even(numbers):
    """去掉列表里所有的偶数
    """
    for i, number in enumerate(numbers):
        if number % 2 == 0:
            # 有问题的代码
            del numbers[i]


numbers = [1, 2, 7, 4, 8, 11]
remove_even(numbers)
```
使用空列表或生成器


### 快去看 collections、itertools 模块~~

