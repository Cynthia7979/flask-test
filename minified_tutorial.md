# Flask Tutorial
修改自[Flask中文文档](https://dormousehole.readthedocs.io/en/latest/quickstart.html)

## 安装
参见[《安装》](https://dormousehole.readthedocs.io/en/latest/installation.html)

## 创建一个Flask项目
1. 创建一个文件夹
2. 在文件夹中创建一个Python文件，文件名随意
3. 将`run.bat`移动到文件夹中，并将其中的`minimal_app`修改为文件名
（如果文件名是`app.py`就可以留空）
4. 运行`run.bat`
5. 用浏览器打开http://127.0.0.1:5000 查看应用

## 路由
一般来说，浏览器路径栏中的URL（如“https://dormousehole.readthedocs.io/en/latest/installation.html”）
并不指向任何一个页面。这个链接需要由**路由**进行处理，然后程序的某一个部分才能对其作出响应。

Flask的路由是通过装饰器实现的。装饰器就是函数、类或方法上面，以 **@** 开头的一个语句。

例子：  
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')  # 这是一个装饰器
def hello_world():
    return "<p>Hello, World!</p>"
```

这段代码中的`@app.route('/')`是一个路由，它为这个应用的主页（即http://127.0.0.1:5000/）绑定了一个函数，即`hello_world()`。

### 简单的URL
对于类似`/`，`/foo/`等简单的URL，直接将对应的路径作为字符串传给`@app.route()`即可

需要注意的是，如果URL没有尾部的斜杠（如`/foo`），那么用户访问`/foo/`的时候就会遇到404错误。相反地，如果URL有尾部的斜杠（`/foo/`），那么用户访问`/foo`的时候会被自动重定向至`/foo/`。

### 包含变量的URL
`app.route()`可以自动将URL的一部分作为参数传递给绑定的函数。比如说：

```python
@app.route('/post/<int:post_id>')
def show_post(post_id):
    return 'Post %d' % post_id
```

其中，`<` `>`表示这是一个变量，`post_id`为变量名，而`int:`表示需要将这个变量自动转换为哪个数据类型。可用的转换器有：

| string 	| （缺省值） 接受任何不包含斜杠的文本 	|
|--------	|-------------------------------------	|
| int    	| 接受正整数                          	|
| float  	| 接受正浮点数                        	|
| path   	| 类似 string ，但可以包含斜杠        	|
| uuid   	| 接受 UUID 字符串                    	|

可选变量应该用如下方法实现：
```python
from flask import render_template

@app.route('/hello/')
@app.route('/hello/<name>')
def hello(name=None):
    return render_template('hello.html', name=name)
```

### HTTP方法
一般情况下，`app.route()`只会处理GET请求（即，获取某个页面或数据的请求）。如果需要处理POST请求，需要加上`methods=['GET', 'POST']`参数。

## 获取指定的URL
**`url_for(endpoint, **values)`**（[文档](https://flask.net.cn/api.html#flask.url_for)）

这个函数会返回指定函数所对应的URL：
* `endpoint`为字符串形式的函数名称
* `values`为传递给该函数的参数。

需要获取`static/`目录下的静态文件时，应将`endpoint`设为`"static"`，同时传入`filename="<文件名>"`参数。

## 渲染静态页面
静态页面是在HTML文件中预先写好的页面。Flask搭载的Jinja库可以将这些文件作为页面渲染的模板。模板文件应该放在`templates/`目录下，具体写法请参考[Jinja2模板文档](http://jinja.pocoo.org/docs/templates/)。

使用**`render_template('<模板名>', 参数1=参数值)`**即可渲染任意模板。

Flask本身不支持Markdown渲染，但是可以通过第三方库（E.g. [Flask-FlatPages](https://github.com/Flask-FlatPages/Flask-FlatPages)）弥补这一点。

（完全没用过模板.jpg 回头再研究下）

## 处理请求

> 某些对象在 Flask 中是全局对象，但不是通常意义下的全局对象。这些对象实际上是特定环境下本地对象的代理。真拗口！但还是很容易理解的。

Flask用了一种神奇的方式实现了一个全局局部对象`request`。这个对象代表任意页面收到的请求，包括请求类型 `request.method`、表单数据 `request.form`、等等。完整的列表详见[文档](https://flask.net.cn/api.html#flask.Request)（TODO）。

处理请求前，需要先从flask导入该对象：`from flask import request`。随后只要在函数内直接使用`request`即可。

