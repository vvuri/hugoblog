---
title: "Jupyter in Hugo"
date: 2019-01-01   
tags: ["github", "python"]
description: "Hugo plugins"
category: "Developmen"
---

Добавляем возможность интеграции Jupyter файлов, как статических данных
<!--more-->
Попробовал следующий варинт:
```bash
$ pip install hugo_jupyter
```
досталяется достаточно много модулей
```
$ cd root_of_hugo_project
$ hugo_jupyter --init
```

- Запускаем Jupyter notebook
- Создаем новый файл
- название меняем на необходимое
- Edit - Edit Notebook Metadata
- Добавляем следующий заголовок
```
  "front-matter":{
  "date":"2019-01-03",
  "subtitle": "Add Jupyter print",
  "title": "Jupyter Hugo"
  },
  "hugo_jupyter": {
    "render-to": "/path/to/blog/content"
  }
```
- сохраняем 
- должен появится файл с расширением md

НО не выходит, не создается и что просходит пока не ясно

Другой способ менее элегантный:
- запускаем  Jupyter notebook
- выбираем нужный файл
- File -> Download as -> Markdown
- md файл редактируем, добавляя шапку
данный способ работает


["Полное описание" | https://github.com/knowsuchagency/hugo_jupyter]