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



