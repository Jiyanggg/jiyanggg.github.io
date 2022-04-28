

### Pymysql 连接

```
pip install PyMySQL
```

简单例子：

```python
import pymysql
conn = pymysql.connect(host='127.0.0.1', user='root', passwd="xxx", db='mysql')
cur = conn.cursor()
cur.execute("SELECT Host,User FROM user")
for r in cur:
    print(r)
cur.close()
conn.close()
```
