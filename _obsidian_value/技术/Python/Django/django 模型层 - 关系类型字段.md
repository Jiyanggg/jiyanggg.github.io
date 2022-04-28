## 多对一

> 例如：一辆汽车对应一个生产厂商，一个生产厂商对应多辆汽车


### 定义外键

外键一般定义于'多'的一方，指向'一'的一方

```
user = models.ForeignKey(
    User,
    on_delete=models.SET_NULL,
    blank=True,
    null=True,
)
```

### 外键的参数


`to`: 外键指向的对象 (self 指向自己)

`on_delete`: 当外键关联的对象删除时的策略

```

- CASCADE: 定义有对应外键的模型对象同时删除
- PROTECT: 阻止删除操作，抛出异常
- SET_NULL: 将外键设置为 null, 只有当字段设置了 null=True 时
- SET_DEFAULT: 将外键设置为默认值， 只有当字段设置了default参数时
- DO_NOTHING: 什么都不做
- SET(): 设置一个传递 SET() 的值
```

`limit_choices_to`: 限制外键所能关联的对象的属性

`related_name`: 用于关联对象反向引用模型的名词 （默认是 模型的小写_set）

```
class Car(models.Model):
    manufacturer = models.ForeignKey(
        'production.Manufacturer',      
        on_delete=models.CASCADE,
        related_name='car_producted_by_this_manufacturer',  # 看这里！！
    )
```

`related_query_name`: 用于反向查询关联名


```
class Tag(models.Model):
    article = models.ForeignKey(
        Article,
        on_delete=models.CASCADE,
        related_name="tags",
        related_query_name="tag",       # 注意这一行
    )
    name = models.CharField(max_length=255)

# 现在可以使用‘tag’作为查询名了
Article.objects.filter(tag__name="important")
```





## 多对多

> 例如：一本书对应多个作者，一个多个对应有多本书


```
class ManyToManyField(to, **options)
```

### 参数说明

related_name: 同上

related_query_name: 同上

limit_choices_to：同上

symmetrical：是否为双向关系

through：多对多之间的中间表

```
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=50)

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(
        Person,
        through='Membership',       ## 自定义中间表
        through_fields=('group', 'person'),
    )

class Membership(models.Model):  # 这就是具体的中间表模型
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    inviter = models.ForeignKey(
        Person,
        on_delete=models.CASCADE,
        related_name="membership_invites",
    )
    invite_reason = models.CharField(max_length=64)
```

through_fields: 显式定义关联的主键（group, person）

## 一对一

> 例如：常用于一个模型需要从别的模型扩展而来的情况

```
class OneToOneField(to, on_delete, parent_link=False, **options)
```


```
from django.conf import settings
from django.db import models

# 两个字段都使用一对一关联到了Django内置的auth模块中的User模型
class MySpecialUser(models.Model):
    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
    )
    supervisor = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name='supervisor_of',
    )
```