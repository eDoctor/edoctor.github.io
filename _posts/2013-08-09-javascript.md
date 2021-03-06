---
layout: default
date: 2013-08-09 10:45:35 +0800
title: Javascript Styleguide
category: styleguide
---

>  Push 至 Git 库前，必须先通过 [JSHint][] 检查！

## 命名规范

- 文件和目录名，必须匹配`/^_?[a-z0-9-]+$/`，否则将被构建工具忽略。
- 尚在开发阶段、不宜部署上线的文件，可加上`-dev`后缀，便于构建工具排除。
- 首选合适的英文单词，严禁拼音首字母缩写，做到「见名识意」。
- 命名约定：
  - 常量全大写`UPPERCASE_WORD`
  - 变量小驼峰`camelName`
  - 类名大驼峰`CamelName`

## 编码规范

- 使用`UTF-8`作为文件编码格式。
- 缩进使用 2 个空格，禁用 tab。

  [Sublime Text][] 可以设置：

  ```js
  {
      "tab_size": 2,
      "translate_tabs_to_spaces": true
  }
  ```

- 尽量不要让每行超过 120 个字符，在不影响阅读的前提下，适当换行。
- 利用（1~2个）空行分隔逻辑上相对独立的代码块，提高代码可读性与美感，同时照顾其他 review 你代码的同事的心情。
- 行末、空行不要有空格。

  [Sublime Text][] 可以设置：

  ```js
  {
      "ensure_newline_at_eof_on_save": true,
      "trim_trailing_white_space_on_save": true
  }
  ```

- 合理使用注释，写注释是为了「__提高代码的可读性，从而提高代码的可维护性__」，不要懒，也不要滥。Refer to [注释规范](https://github.com/aralejs/aralejs.org/wiki/JavaScript-注释规范)

- 对于单 var 模式和多 var 模式，不做强行约定，但同一个文件里，风格必须一致。

  推荐有赋值的分开写，没赋值的写一块：

  ```js
  var foo = 'foofoo'
  var bar = 'barbar'
  var baz, len, i
  ```

- 对于分号问题，也不做强行约定，但同一个文件里，风格必须一致。
- 尽量减少全局变量的使用。

  如果需要从 HTML 页面传入多个变量，给它们指派合适的命名空间：

  <p class="bad">Bad:</p>

  ```
  javascript:
      var userName = 'Steve Jobs'
      var userAge = 56
  ```

  <p class="good">Good:</p>

  ```
  javascript:
      var user = {
        name: 'Steve Jobs',
        age: 56
      }
  ```

  > 然后将上面的`user`写进「edr-assets」对应项目目录内的`.jshintrc`中。

- 使用 Array/Object 直接量，避免使用 Array/Object 构造器。

  <p class="bad">Bad:</p>

  ```js
  var arr = new Array()
  var obj = new Object()
  ```

  <p class="good">Good:</p>

  ```js
  var arr = []
  var obj = {}
  ```

- 语句块必须使用大括号`{}`。

  <p class="bad">Bad:</p>

  ```
  if (true) return;
  ```

  <p class="good">Good:</p>

  ```
  if (true) {
      return
  }
  ```

- 大括号不换行，并与前面的小括号之间空一格。

  <p class="bad">Bad:</p>

  ```
  if (true)
  {
      return
  }

  if(true){
      return
  }
  ```

  <p class="good">Good:</p>

  ```
  if (true) {
      return
  }

  function name(options) {
      options || (options = {})
  }
  ```

- 操作符之间需要有 1 个空格。

  <p class="bad">Bad:</p>

  ```js
  var x=y+z
  ```

  <p class="good">Good:</p>

  ```js
  var x = y + z
  ```

- 不要为了对齐冒号，而增加多余空格。

  <p class="bad">Bad:</p>

  ```js
  {
      foo   : 'foo',
      barbar: 'barbar'
  }
  ```

  <p class="good">Good:</p>

  ```js
  {
      foo: 'foo',
      barbar: 'barbar'
  }
  ```

- 在行末使用逗号，而非行首。

  <p class="bad">Bad:</p>

  ```js
  {
      foo: 'foo'
    , barbar: 'barbar'
  }
  ```

  <p class="good">Good:</p>

  ```js
  {
      foo: 'foo',
      barbar: 'barbar'
  }
  ```

- 缓存 jQuery 对象，能复用的绝不新建。

  <p class="bad">Bad:</p>

  ```js
  $('body').find('.foo').text('foo')
  $('body').find('.bar').text('bar')
  ```

  <p class="good">Good:</p>

  ```js
  var body = $(document.body)
  body.find('.foo').text('foo')
  body.find('.bar').text('bar')
  ```

- 优先使用 jQuery 最快的 ID 选择器。
  > 可以配合给 HTML 标签加上`js-`前缀的 id，提高 DOM 操作效率。此类 id 只用于 js，不应该出现在 css 文件中。

  <p class="bad">Bad:</p>

  ```js
  $('#js-based-id .class')
  ```

  <p class="good">Good:</p>

  ```js
  $('#js-based-id').find('.class')
  ```

- 事件绑定一律使用`.on()`。

  <p class="bad">Bad:</p>

  ```js
  $('#js-based-id').bind('click', function(e) {
      e.preventDefault()
  })

  $('#js-based-id').click(function(e) {
      e.preventDefault()
  })
  ```

  <p class="good">Good:</p>

  ```js
  $('#js-based-id').on('click', function(e) {
      e.preventDefault()
  })
  ```

- 同时给同一类 DOM 元素绑定事件时，利用冒泡机制，将事件绑定在公共父元素上。

  <p class="bad">Bad:</p>

  ```js
  $('ul > li').on('click', function() {})
  ```

  <p class="good">Good:</p>

  ```js
  $('ul').on('click', 'li', function() {})
  ```

- 避免频繁操作 DOM，减少重绘「Repaint」与重排「Reflow」。

  <p class="bad">Bad:</p>

  ```js
  var ul = $('ul')
  for (var i = 0; i < 100; i++) {
      ul.append('<li>...</li>')
  }
  ```

  <p class="good">Good:</p>

  ```js
  // 方法一
  var html = ''
  for (var i = 0; i < 100; i++) {
      html += '<li>...</li>'
  }
  $('ul').html(html)

  // 方法二
  var fragment = document.createDocumentFragment()
  var li
  for (var i = 0; i < 100; i++) {
      li = document.createElement('li')
      fragment.appendChild(li)
  }
  $('ul').html(fragment)
  fragment = li = null
  ```


[Sublime Text]: http://mrzhang.me/blog/after-reinstall-the-system.html#sm
[JSHint]: {% post_url 2013-08-22-jshint %}
