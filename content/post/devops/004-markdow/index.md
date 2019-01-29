---
title: "Markdown разметка"
categories: ["Designe"]
description: "Разметака текста"
date: "2017-04-16T14:24:08+03:00"
draft: false
tags: []
menu: 
    main:
        parent: "DevOps"
---

Достаточно подробно на [getgrav](https://learn.getgrav.org/content/media)
описана так же шапка - это линки на папки и маршрутизация
отличный 
редактор с двумя окнами под [win free](http://markdownpad.com/)
<!--more-->

# h1 Heading
## h2 Heading
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading
___

**rendered as bold text**    
_rendered as italicized text_

~~Strike through this text.~~

> **Fusion Drive** combines 

> text line 2

> text line 3

* valid bullet
* valid list
* list

  - [x] This is a complete item
  - [ ] This is an incomplete item
  - [x] This is a complete item
  - [ ] This is an incomplete item

 `<section>  code  </section>`

 ``` markup
 для подсветки кода требуется Grav Highlight Plugin
 Sample text here...      
 ```

| Option | Description |
| ------ | -----------: |
| data   | path to data files to supply . |
| engine | engine to be used. |

[Assemble link](http://assemble.io)

[Upstage link](https://github.com/upstage/ "Visit!")

[Chapter 1 - якорь](#chapter-1)


[link](../../02.green/01.grass/item.md)

[Big Button](../some-page?classes=button,big)
[Unique Button](../some-page?id=important-button)

<!-- more -->

Text after more

**TOML**
```toml
[params]
  disqusShortname = "spf13"
```

**YAML**
```yaml
params:
  disqusShortname: "spf13"
```