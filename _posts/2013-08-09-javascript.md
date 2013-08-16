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
