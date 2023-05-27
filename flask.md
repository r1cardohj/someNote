

# flask

[TOC]



## Jinja2

> Jinja2太tm牛了

### 上下文

注册模板上下文比变量

``` python
@app.context_processor
def xxx():
    n = '我是模板上下文变量'
    return dict(n = n)
```

注册模板上下文函数

``` python
@app.template_global()
def xx():
    #do something
    return xxxx
```

注册模板全局对象

``` python
def xx():
    return xxx

def my_filter(s):
    return s + '11'

xxx = 'xxx'

def my_test(s):
    if s == 1:
        return True
    return False


app.jinjia_env.globals['xx'] = xx
app.jinjia_env.globals['foo'] = foo
app.jinjia_env.filters['my_filter'] = my_filter
app.jinjia_env.tests['my_test'] = my_test
```



内置上下文变量

| 变量    | 说明                   |
| ------- | ---------------------- |
| config  | 配置当前对象           |
| request | 当前请求对象           |
| session | 当前的会话对象         |
| g       | 全局变量，内置在进程中 |

内置全局函数

| 函数                                 | 说明         |
| ------------------------------------ | ------------ |
| range()                              | 同python     |
| lipsum(n=5,html=True,min=20,max=100) | 随机生成文本 |
| dict()                               | 同python     |
| url_for()                            | 懂的都懂     |
| get_flashed_messages()               | 获取闪现信息 |

### 过滤器

内置过滤器

| name           | 说明           |
| -------------- | -------------- |
| default(value) | 默认值         |
| escape(s)      | 转义HTML文本   |
| first(seq)     | 第一个元素     |
| last(seq)      | 最后一个元素   |
| length(object) | 长度           |
| trim           | 清除前后的空格 |

> 安全性考虑，可以把变量渲染前转换flask中的Markup类的对象

自定义过滤器

``` python
from flask import Markup

@app.template_filter()
def my_filter(s):
    return s + Markup('xxx')

#模板中
{{ name | my_filter }}
```

### 测试器

> 相当于比较运算语句吧...

内置测试器

| name          | 说明                   |
| ------------- | ---------------------- |
| callable      | 是否可调用             |
| defined       | 是否已定义             |
| undefined     | 不解释                 |
| none          |                        |
| number        |                        |
| string        |                        |
| squence       | 序列                   |
| iterable      | 是否可迭代             |
| mapping       | 字典                   |
| sameas(other) | 是否指向相同的内存地址 |

自定义测试器

``` python
@app.template_test()
def is_me(n):
    if n =='me':
        return True
    return False
```

### 局部模板

html模板文件:_banner.html

> 局部模板文件请加下划线

引入写法:` {% include '_banner.html'%} `

### 宏

创建html文件:macros.html

``` jinja2
{% macro my_macro(a=1) %}
    {% if a == 1 %}
        i am gl
    {% else %}
        i am not gl
    {% endif %}
{% endmacro %}
```

引入

``` jinja2
{% from 'macros.html' import my_macro%}
{{ my_macro(1) }}
```

### 模板继承

不展开写了 感觉很好记

1. 写个base.html

   ```jinja2
   <html>
   ....
   {% block head %}
   ...
   {% endblock head%}
   
   {% block context %}
   {% endblock context %}
   
   {% block footer %}
   {% endblock footer %}
   
   ```

2. 子模板

   ``` jinja2
   {% extend 'base.html' %}
   ...
   {% block head %}
   ... {# 重写 #}
   {% endblock head%}
   
   {% block head %}
   {{ super() }}
   ... {# 追加 #}
   {% block head %}

### 闪现消息

视图

```python
from flask import flash

...
flash('i am a freash ')

```

模板

``` jinja2
{% for message in get_flashed_message() %}
	<div class="alert">{{ message }}</div>
{% endfor %}
```

