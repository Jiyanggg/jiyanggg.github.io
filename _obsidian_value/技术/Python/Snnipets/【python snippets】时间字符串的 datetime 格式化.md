```
import datetime
import re


def transformtime(date_str: str) -> datetime:
    date_str = date_str.strip()
    try:
        if '天' in date_str:
            result = re.search(re.compile(r'(.*?)天'), date_str)
            days = int(result.groups()[0])
            date = datetime.datetime.now() - datetime.timedelta(days=days)
        elif '小时' in date_str:
            result = re.search(re.compile(r'(.*?)小时'), date_str)
            hours = int(result.groups()[0])
            date = datetime.datetime.now() - datetime.timedelta(hours=hours)
        elif '分钟' in date_str:
            result = re.search(re.compile(r'(.*?)分钟'), date_str)
            minutes = int(result.groups()[0])
            date = datetime.datetime.now() - datetime.timedelta(minutes=minutes)
        else:
            date_str = date_str.replace('年', '-').replace('月', '-').replace('日', '')
            return date_str

        date = date.strftime('%Y-%m-%d')
        return date
    except Exception as e:
        return str(e)
        
if __name__ == '__main__':
    transformtime('5分钟前')
```