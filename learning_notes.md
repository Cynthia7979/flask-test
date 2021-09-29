# Learning Notes
## Custom Components in Jinja2
via Macros:
> Jinja2 uses macros. Once a Macro is defined, it can be called on to render elements.
>
> So if you define a macro in a template like:
> ```
> {% macro newComponent(text) -%}
>   <div class='container'><p>{{text}}</p></div>
> {%- endmacro %}
> ```
> Then it can be called on in any file with
>
> `{{ newComponent('Insert Text') }}`
>
> Here is a link to the [documentation](http://jinja.pocoo.org/docs/2.10/templates/#macros)
>
> Also Stack Overflow post on macros [Parameterized reusable blocks with Jinja2 (Flask) templating engine](https://stackoverflow.com/questions/15106741/parameterized-reusable-blocks-with-jinja2-flask-templating-engine)
>
~ AlexG on [StackOverflow](https://stackoverflow.com/a/55841718)

## Form Handling
* [Flask-WTF](https://flask-wtf.readthedocs.io/en/0.15.x/) (Integration of [WTForms](https://wtforms.readthedocs.io/en/2.3.x/))

## 提示/错误窗口 (Alert)
需要使用[闪现消息](https://flask.net.cn/api.html#flask.flash)，使用方法见`minified_tutorial.md`

下面是例子
* https://www.codegrepper.com/code-examples/python/flask+alert+popup
* https://stackoverflow.com/questions/40949746/how-to-display-flashing-message-without-reloading-the-page-in-flask

## 会话弹窗 (Dialog/Modal)
可以使用`data-toggle`和`data-target`参数实现。  
（它们不是标准HTML的参数，而是由Bootstrap库自定义的，因此找不到太多文档）

参考：
* [Modal Window in Jinja2 template. Flask](https://stackoverflow.com/questions/44606429/modal-window-in-jinja2-template-flask)
* [Data-toggle with Flask & Jinja template](https://stackoverflow.com/questions/23549807/data-toggle-with-flask-jinja-template)
```html
<div class="tabbable">
<!-- Only required for left/right tabs -->
<ul class="nav nav-tabs">
    <li class="active"><a href="#tab1" data-toggle="tab">Pick Colors</a>
    </li>
    <li><a href="#tab2" data-toggle="tab2">Add Text</a>
    </li>
    <li><a href="#tab3" data-toggle="tab3">Add Logos</a>
    </li>
</ul>
<div class="tab-content">
    <div class="tab-pane active" id="tab1">
        <div class="well">
            <ul class="nav">
                <li class="color-preview" title="White" style="background-color:#ffffff;"></li>
            </ul>
        </div>
    </div>
    <div class="tab-pane" id="tab2">
        <div class="well">
            <div class="input-append">
                <input class="span2" id="text-string" type="text" placeholder="add text here...">
                <button id="add-text" class="btn" title="Add text"><i class="icon-share-alt"></i>
                </button>
                <hr>
            </div>
        </div>
    </div>
    <div class="tab-pane" id="tab3">
        <div id="avatarlist">
            <img style="cursor:pointer;" class="img-polaroid" src="static/img/img1.png">
        </div>
    </div>
</div>
```

## 用来~~copy~~参考学习的repo
* [lufficc/flask_ishuhui](https://github.com/lufficc/flask_ishuhui)
* [tag:flask-application](https://github.com/topics/flask-application)