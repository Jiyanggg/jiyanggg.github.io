## 官方文档

https://pyppeteer.github.io/pyppeteer/

## 基本使用

```
# encoding='utf-8'

import asyncio
import time

from bs4 import BeautifulSoup
from pyppeteer import launch

source = "https://kns.cnki.net/kns8/defaultresult/index"
headers = {
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;"
              "q=0.8,application/signed-exchange;v=b3",
    "Accept-Language": "zh,en-US;q=0.9,en;q=0.8,zh-CN;q=0.7,und;q=0.6",
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 "
                  "(KHTML, like Gecko) Chrome/74.0.3729.131 Safari/537.36",
}


async def main():
    browser = await launch(headless=False)
    page = await browser.newPage()
    await page.goto(source, headers=headers)
    await page.type('input#txt_search', '航空')
    await page.click('input.search-btn')

    time.sleep(2)
    html = await page.content()
    soup = BeautifulSoup(html, 'lxml')
    tags = soup.select("table.result-table-list tr")
    print(len(tags))
    for tag in tags:
        print(tag.text)

    await browser.close()


asyncio.get_event_loop().run_until_complete(main())

```

### 常见的操作

```
await page.goto(source, headers=headers) # 进入页面

await page.type('input#txt_search', '航空') # 文本键入

await page.click('input.search-btn') # 点击

html = await page.content() # 获取 HTML

await page.evaluate('window.scrollBy(0, document.body.scrollHeight)') # 滚动屏幕

await page.screenshot({'path': 'example.png'})  # 屏幕截图

dimensions = await page.evaluate('''() => {
    return {
        width: document.documentElement.clientWidth,
        height: document.documentElement.clientHeight,
        deviceScaleFactor: window.devicePixelRatio,
    }
}''')  # 执行 JS 

```

