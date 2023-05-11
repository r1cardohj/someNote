# Python笔记

[TOC]



## Pipenv

_python的虚拟环境以及包依赖管理工具_

### 包引入

`pip install pipenv`

### 虚拟环境创建或复制

`pipenv install`

> 复制Pipfile文件和Pipfile.lock文件到需即为环境迁移

## 爬虫相关

| BaiduSpider | 百度      | www.baidu.com     |
| ----------- | --------- | ----------------- |
| Googlebot   | 谷歌      | www.google.com    |
| 360Spider   | 360 搜索  | www.so.com        |
| YodaoBot    | 有道      | www.youdao.com    |
| ia_archiver | Alexa     | www.alexa.cn      |
| Scooter     | altavista | www.altavista.com |
| Bingbot     | 必应      | www.bing.com      |

### request

#### 避免ssl认证

```python
import requests

#关掉警告
requests.packages.urllib3.disable_warnings()

requests.get(url,verify=False)
```

或捕获到日志

``` py
import logging
import requests

logging.captureWarnings(True)
response = requests.get('https://ssr2.scrape.center/', verify=False)
print(response.status_code)
```

或指定本地证书(key必须是解密状态)

``` python
import requests

response = requests.get('https://ssr2.scrape.center/', cert=('/path/server.crt', '/path/server.key'))
print(response.status_code)
```

## 各种标准库

### os

> os模块提供了与操作系统交互的函数
>
> tips:官方建议`import os`而不是`from os import *`避免内建的open()给os.open隐式替换

如果不存在则生成文件夹

``` python
from os import makedir
from os.path import exists

MYDIR = 'xxx'
os.path.exists(MYDIR) or makedirs
```

打开并读取文件

``` python
with open('bibi.txt',encoding="utf-8") as f:
    read_data = f.read()
# with 会在执行完 代码块 后自动关闭文件对象
# 相当于执行f.close()
print(read_data)
```

按行遍历文件

``` python
for line in f:
    print(line,end = '')
```

命令行相关

```python
import os
os.getcwd() #获取当前工作目录
os.chdir("/xxx/xxx") #改变工作目录
os.system("") #执行bash命令
```

### shutil

> 对于日常文件和目录管理任务， [`shutil`](https://docs.python.org/zh-cn/3.10/library/shutil.html#module-shutil) 模块提供了更易于使用的更高级别的接口:

```python
import shutil
shutil.copyfile('xxx.xx','xxx.xx') #复制
shutil.move('/xxx/xx','xxxx')
```

### glob

> 在目录中使用通配符搜索创建文件列表的函数

``` python
import glob
glob.glob('*.py') #当前目录下返回.py后缀的列表 
```

### random

> 随鸡库

``` python
import random
random.choice('6556456') #参数为可迭代数据类型
random.sample(range(100),10) #依旧是可迭代数据类型 加 需要的数量 返回一个list len(list) = 10
```

### statistics

> 计算数值的基本统计属性

```python
import statistics
data = [1,2,3] 
statistics.mean(data) #求平均值
statistics.median(data) #中位数
```

### 正则请用re

> 正则表达式专用

``` python
import re
re.finall(r'\bf[a-z]*','which foot or hand full fauck') # 返回由匹配结果组成的list
```

### datetime

> 時間庫

``` python
from datetime import date
now = date.today() 
#output:datetime.date(2023,05,11)
now.strftime("%d %y %m %B %b %A %Y")
'''
%d : 11
%y : 23
%m : 05
%B : May
%A : 星期的單詞我不知道怎麽拼
%Y : 2023
'''
```

### unittest

> 单元测试
>
> 挖个坑 有空专门研究...

## 数据结构

### *号的使用

​	在python中*号可以获取任意数量的值，并以此创建一个数组，哪怕没有值，也会返回一个空的数组

```bash
>>> record = ('Dave', 'dave@example.com', '773-555-1212', '847-555-1212')
>>> name, email, *phone_numbers = record
>>> name
'Dave'
>>> email
'dave@example.com'
>>> phone_numbers
['773-555-1212', '847-555-1212']
>>>
```

​	如果在可迭代对象中使用，则会对该数据结构进行解包。







