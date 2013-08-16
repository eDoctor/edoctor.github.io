---
layout: default
date: 2013-08-09 10:45:35 +0800
title: Javascript Styleguide
---

>  Push 至 Git 库前，必须先通过 [JSHint](http://jshint.com/install/) 检查！

## 命名规范

- 文件和目录名必须匹配`/^_?[a-z0-9-]+$/`，否则将被构建工具忽略。
- 尚在开发阶段、不宜部署上线的文件，可加上`-dev`后缀，便于构建工具排除。
- 首选合适的英文单词，严禁拼音首字母缩写，做到「见名识意」。
- 命名约定：
  - 常量全大写`UPPERCASE_WORD`
  - 变量小驼峰`camelName`
  - 类名大驼峰`CamelName`

## 编码规范

- 缩进使用 2 个空格，禁用 tab。

  Sublime Text 可以设置：

  ```js
  {
      "tab_size": 2,
      "translate_tabs_to_spaces": true
  }
  ```

- 对于单 var 模式和多 var 模式，不做强行约定，但同一个文件里，风格必须一致。

  推荐有赋值的分开写，没赋值的写一块：

  ```js
  var foo = 'foofoo'
  var bar = 'barbar'
  var baz, len, i
  ```

- 不允许一行判断。

  <p class="good">Good:</p>

  ```
  if (true) {
      return
  }
  ```

  <p class="bad">Bad:</p>

  ```
  if (true) return;
  ```

- 操作符之间需要有 1 个空格。

  <p class="good">Good:</p>

  ```js
  var x = y + z
  ```

  <p class="bad">Bad:</p>

  ```js
  var x=y+z
  ```

- 不要为了对齐冒号，而增加多余空格。

  <p class="good">Good:</p>

  ```js
  {
      foo: 'foo',
      barbar: 'barbar'
  }
  ```

  <p class="bad">Bad:</p>

  ```js
  {
      foo   : 'foo',
      barbar: 'barbar'
  }
  ```

- 在行末使用逗号，而非行首。

  <p class="good">Good:</p>

  ```js
  {
      foo: 'foo',
      barbar: 'barbar'
  }
  ```

  <p class="bad">Bad:</p>

  ```js
  {
      foo: 'foo'
    , barbar: 'barbar'
  }
  ```

- 缓存 jQuery 对象，能复用的绝不新建。

  <p class="good">Good:</p>

  ```js
  var body = $(document.body)
  body.find('.foo').text('foo')
  body.find('.bar').text('bar')
  ```

  <p class="bad">Bad:</p>

  ```js
  $('body').find('.foo').text('foo')
  $('body').find('.bar').text('bar')
  ```
