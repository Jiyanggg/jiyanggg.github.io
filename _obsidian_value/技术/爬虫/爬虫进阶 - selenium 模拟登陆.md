# Selenium 模拟登陆

[TOC]

`概述：`
Selenium 是一个自动化测试工具，利用它我们可以驱动浏览器执行特定的动作，如点击、下拉等操作。对于一些 JavaScript 渲染的页面来说，这种抓取方式非常有效。


## 1. 环境准备

(1) 安装 selenium 库
```
pip3 install selenium
```
(2) Chrome 浏览器及 ChromeDriver 驱动的配置

```
点击 Chrome 菜单 “帮助”→“关于 Google Chrome”，即可查看 Chrome 的版本号，并在官方网站上下载对应的 chromedriver.exe 驱动
https://sites.google.com/a/chromium.org/chromedriver/
```
(3) 将下载的 ChromeDriver 驱动放置在 Python 的 Scripts 目录中（在命令行中输入 chromedriver 有正确响应即代表配置成功）

## 2. 简单样例
```python
import time

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

browser = webdriver.Chrome()  # 声明浏览器
browser.get('https://www.baidu.com')  # 访问网页
search_input = WebDriverWait(browser, 10).until(    # 获取搜索框
    EC.presence_of_element_located((By.ID, "kw"))
)
search_input.send_keys('sincobd')  # 将文字填充到搜索框
time.sleep(1)

search_input.clear()  # 清空搜索框
search_input.send_keys('火狐')
submit = browser.find_element_by_id('su')  # 获取提交按钮
submit.click()  # 点击提交按钮
time.sleep(1)
browser.close()  # 关闭浏览器
```

## 3. 常用操作

### (1) 打开页面
```
driver.get("http://www.google.com")
```

### (2) 获取页面元素
```
element = driver.find_element_by_id("passwd-id")
element = driver.find_element_by_name("passwd")
element = driver.find_element_by_xpath("//input[@id='passwd-id']")
element = driver.find_element_by_link_text("")
element = driver.find_elements_by_class_name()
element = driver.find_element_by_css_selector("")
all_options = element.find_elements_by_tag_name("option")
```

### (3) 操作页面元素
```
 # 输入值
element.send_keys("some text")  

# 点击
driver.find_element_by_id("submit").click()  

# 拖放元素
element = driver.find_element_by_name("source")
target = driver.find_element_by_name("target")

from selenium.webdriver import ActionChains
action_chains = ActionChains(driver)
action_chains.drag_and_drop(element, target).perform()
```

### (4) 页面操作
```
# 切换窗口
driver.switch_to_window("windowName")
driver.switch_to_frame("frameName")
driver.switch_to_default_content()

# 浏览纪录中前进和后退
driver.forward()
driver.back()
```

### (5) 等待页面加载
```python
# 显示等待
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Firefox()
driver.get("http://somedomain/url_that_delays_loading")
try:
    element = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.ID, "myDynamicElement"))
    )
finally:
    driver.quit()


#隐式等待
from selenium import webdriver

driver = webdriver.Firefox()
driver.implicitly_wait(10) # seconds
driver.get("http://somedomain/url_that_delays_loading")
myDynamicElement = driver.find_element_by_id("myDynamicElement")
```

### (6) 操作动作链
```
driver = webdriver.Firefox()
menu = driver.find_element_by_css_selector(".nav")
hidden_submenu = driver.find_element_by_css_selector(".nav #submenu1")

actions = ActionChains(driver)
actions.move_to_element(menu)
actions.click(hidden_submenu)
actions.perform()
```

### (7) 实战样例
```python
# TODO

```

## 参考链接

https://selenium-python-zh.readthedocs.io/en/latest/index.html

https://cuiqingcai.com/2599.html
