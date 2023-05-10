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

## os

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
# with 会在执行完 read_data = f.read()后自动关闭文件对象
# 相当于执行f.close()
print(read_data)
```

按行遍历文件

``` python
for line in f:
    print(line,end = '')
```





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







