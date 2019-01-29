---
title: "Hugo описание структуры"
date: 2018-12-10
tags: ["github", "JavaScript", "Golang" ]
description: "Разработка"
category: "Developmen"
menu: 
    main:
        parent: "Golang"
draft: true        
---

## Структура Hugo.
Теги и категории - два метода структурирования данных	
Кактегории: разработка, тестирование, администрирование, обучение и наука, фотография  (о чем пойдет речь в статье) - сделать по каталогам и подкаталоги -> путь 
Теги - спечифика поста, как хеш-теги: Ubuntu, ESP8266, TensorFlow, TestLink, Allure, ... т.е. их много и они индивидуальны
SEO: теги должны быть закрыты от поисковиков. используйте категории для сео, теги - для юзабилити. 

<!--more-->
### Заголовок:
	+++
	date        = "2013-06-21T11:27:27-04:00"                    - дата создания
	draft 		= true 											 - не публиковать
	title       = "Nitro: A quick and simple profiler for Go"    - заголовок
	description = "Nitro is a simple profiler Golang app"
	tags        = [ "Development", "Go", "profiling" ]           - «теги» или «метки» - более детальное описание
	categories  = []                                             - «категории» или «рубрики» - основная канва, направление
	topics      = [ "Development", "Go" ]
	slug        = "nitro"                                        - что мы увидим в хвосте url, т.е. не имя файла а это
	project_url = "https://github.com/spf13/nitro"
	weight      = 4                                              - порядок показа вначале весь потом дата
	+++

	Создание нового поста по шаблону:

### Каталог:
    .
    |-- archetypes   - создаем файлов со своими шапками шаблонами musician.md -> new musician/first.md
    |-- config.toml  - configuration file
    |-- content 	 - весь контент в папках разделах
    |-- data 		 - ? конфигурационный файлы Hugo 
    |-- layouts 	 - как будет преобразовыватьс контент в web страницу
    |-- static		 - CSS, JavaScript, static content
    `-- themes		 - темы, как выглядит сам сайт

    archetypes	
        archetypes/default.md
            +++
            tags = ["x", "y"]
            categories = ["x", "y"]
            +++
        archetypes/musician.md
            +++
            name = ""
            bio = ""
            genre = ""
            +++
        и при создании $ hugo new musician/mozart.md

### themes
> theme.toml 		 - информация об авторе и темах
  screenshot.png 	 - image of the list view
  tn.png 			 - single post view
  single.html 	     - single piece of content. 
  list.html 		 - list of content items.
  static			 - jQuery or CSS styles or images

### Добавление комментариев
```
[Params]
  Author = "Shekhar Gulati"
  disqusShortname = <your disqus shortname>
```

### Команды: 
```
$ hugo new [path/to/my/content]  - создание нового поста, при этом шапка берется из папки archetypes
$ hugo new post/my-new-post.md

$ hugo server 			 - запуск локального сервера
$ hugo server --buildDrafts 	 - вместе с Draft публикациями

$ git clone https://github.com/dim0627/hugo_theme_robust.git  	 - добавление новой темы
$ hugo server --theme=hugo_theme_robust --buildDrafts 			 - запуск с новой темой
										robust позволяет перегружать контент по ходу
$ hugo undraft content/post/good.md		- снять со страницы пометку  draft=true, а можно и руками
```