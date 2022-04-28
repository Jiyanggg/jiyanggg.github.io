
> 概要：CPU 密集型使用多进程，I/O 密集型任务使用多线程，I/O 任务数量多时可以使用协程


## 进程

是系统中正在运行的一个应用程序，是资源（CPU/内存）分配的最小单位

## 线程

是进程中负责程序执行、运算的执行单元

## 协程

### 定义

协程是一种并发编程模型，本质可以进行函数执行切换的轻量级的线程


### 关键概念


### 使用要点

使用 async 关键字声明协程对象，使用 await 关键词调度执行协程任务

```python
async def func():
    pass
    
await func()
```

### 使用示例

```

import asyncio

async def crawl_page(url):
    print('crawling {}'.format(url))
    sleep_time = int(url.split('_')[-1])
    await asyncio.sleep(sleep_time)
    print('OK {}'.format(url))

async def main(urls):
    tasks = [asyncio.create_task(crawl_page(url)) for url in urls]
    await asyncio.gather(*tasks)

asyncio.run(main(['url_1', 'url_2', 'url_3', 'url_4']))
```

```

import asyncio

async def crawl_page(url):
    print('crawling {}'.format(url))
    sleep_time = int(url.split('_')[-1])
    await asyncio.sleep(sleep_time)
    print('OK {}'.format(url))

async def main(urls):
    tasks = [asyncio.create_task(crawl_page(url)) for url in urls]
    for task in tasks:
        await task

asyncio.run(main(['url_1', 'url_2', 'url_3', 'url_4']))
```


```
import asyncio

async def crawl_page(url):
    print('crawling {}'.format(url))
    sleep_time = int(url.split('_')[-1])
    await asyncio.sleep(sleep_time)
    return 'OK {}'.format(url)
    

async def main(urls):
    tasks = [asyncio.create_task(crawl_page(url)) for url in urls]
    for task in tasks:
        task.add_done_callback(lambda future: print('result: ', future.result()))
    await asyncio.gather(*tasks)
    
asyncio.run(main(['url_1', 'url_2', 'url_3', 'url_4']))
```

协程池