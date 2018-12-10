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
9. Заливаем на Git
```
$ git add .
$ git commit -m "Initial commit"
$ git push -u origin master
```
10. Создаем отдельную ветку внутри основного репозитория
```
$ git submodule add -b master https://github.com/vvuri/vvuri.github.io.git public
```
11. Создаем статические страницы из всего набора
```
$ hugo
```
в итоге весь статический сайт в public
меняем в config.toml http на https
```
baseURL = "https://vvuri.github.io"
```
12. Заливаем все на vvuri.github.io
```
$ cd public
$ git add .
$ git commit -m "New Public"
$ git push https://github.com/vvuri/vvuri.github.io.git
```

Смотрим что же получилось