```python
#汉字转url码，用于拼接url

class Urlchuli():                        
    def __init__(self,can,mazhi='utf-8'):
        self.can = can
        self.mazhi = mazhi

    def url_bm(self):
        quma = str(self.can).encode(self.mazhi)
        bianma = urllib.parse.quote(quma)
        return bianma

if __name__ == '__main__':
    Urlchuli("http://www.baidu.com?keywork=小星星", "gbk").url_bm()

```