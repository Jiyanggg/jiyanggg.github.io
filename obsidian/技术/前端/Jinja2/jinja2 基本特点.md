## Jina2 使用基本特点

### 1. 支持`if` `for in`控制语句

### 2. 拥有`app` `session` `config`上下文变量和函数, 也可以自定义
```python
from flask import current_app
 
@app.context_processor
def appinfo():
    return dict(appname=current_app.name)
```

### 3. 过滤器和测试器
```html
<h1>Hello {{ name | upper }}!</h1>
<p>{{ [1,2,3,4,5] | sum }}</p>
<p>{{ users | map(attribute='name') | join(', ') }}</p>

{% if name is string %}
  <h2>{{ name }} is a string.</h2>
{% endif %}
```
自定义过滤器
```python
@app.template_filter('sub')
def sub(l, start, end):
    return l[start:end]

@app.template_test('end_with')
def end_with(str, suffix):
    return str.lower().endswith(suffix.lower())

<p>{{ [1,2,3,4,5] | sub }}</p>
{% if name is end_with "me" %}
```

### 4. 支持模板继承复用
base.jinja2
```html
<html>
    <head>
    {% block head %}
    Base -
    {% endblock %}
    </head>
    
    <body>
    {% block body %}
    {% endblock %}
    </body>
</html>
```

layout.jinja2
```html
{% extends "base.jinja2" %}

{% block head %}
{{ super() }}
Title 
{% endblock %}

{% block body %}
<h1>This is content</h1>
{% endblock %}
```