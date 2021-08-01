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