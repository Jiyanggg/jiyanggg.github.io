## 1. 关于 ORM

ORM（对象关系映射): 将 Python 操作映射到 SQL 间接操作 DataBase

## 2. 创建模型对象

### 2.1 模型字段 fields

```
# 常见类型
- IntegerField：整型
- FloatField: 浮点型
- BooleanField: 布尔型
- CharField: 字符型
- TextField: 文本型
- DateField: 日期类型 （datetime.date）
- DateTimeField: 日期时间类型 （datetime.datetime）
- FileField: 文件类型 （文件路径：MEDIA_ROOT / upload_to / 中）
- AutoField： 自增整型
- UUIDField: uuid 字段
```

### 2.2 模型方法 methods

## 3. 同步模型至数据库

```
python manage.py makemigrations  # 创建修改记录

python manage.py mirgrate    # 数据迁移同步
```

