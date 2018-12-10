# hugoblog

Personal blog on Hugo and Static Pages github.io

Разнесение кода и статичкских страниц в двух репозиториях
1. Создаем репозиторий и клонируем его 
```
$ git clone https://github.com/vvuri/hugoblog.git
```
2. Ставим hugo
3. Создаем новый сайт
```    
$ hugo new site hugoblog
```
4. Создаем первый пост
```
$ cd vvuri
$ hugo new post/start-new-blog.md
```
5. Правим контекст в /content/post/*.md

6. Добаляем .gitignore

7. Добавляем тему оформления
```
$ cd themes 
$ git clone https://github.com/azmelanar/hugo-theme-pixyll.git
```
правим файл config.toml
8. Смотрим локально, что получилось localhosyt:8000
```
$ hugo server --buildDrafts --port=8000
```
после запуска чистим public
```
$ rm -rf public
```


Смотрим что же получилось