---
title: "Hugo on GitHub"
date: 2018-12-10
tags: ["github", "JavaScript", "Golang" ]
description: "Разработка"
category: "Developmen"
menu: 
    main:
        parent: "Golang"
---

Разнесение кода и статических страниц в двух репозиториях
<!--more-->
1. Создаем репозиторий и клонируем его 
```bash
$ git clone https://github.com/vvuri/hugoblog.git
```
2. Ставим hugo
3. Создаем новый сайт
```bash    
$ hugo new site hugoblog
```
4. Создаем первый пост
```bash
$ cd vvuri
$ hugo new post/start-new-blog.md
```
5. Правим контекст в /content/post/*.md

6. Добаляем .gitignore

7. Добавляем тему оформления
```bash
$ cd themes 
$ git clone https://github.com/azmelanar/hugo-theme-pixyll.git
```
правим файл config.toml
8. Смотрим локально, что получилось localhosyt:8000
```bash
$ hugo server --buildDrafts --port=8000
```
после запуска чистим public
```bash
$ rm -rf public
```
9. Заливаем на Git
```bash
$ git add .
$ git commit -m "Initial commit"
$ git push -u origin master
```
10. Создаем отдельную ветку внутри основного репозитория
```bash
$ git submodule add -b master https://github.com/vvuri/vvuri.github.io.git public
```
11. Создаем статические страницы из всего набора
```bash
$ hugo
```
в итоге весь статический сайт в public
меняем в config.toml http на https
```bash
baseURL = "https://vvuri.github.io"
```
12. Заливаем все на vvuri.github.io
```bash
$ cd public
$ git add .
$ git commit -m "New Public"
$ git push https://github.com/vvuri/vvuri.github.io.git
```
13. Если надо удалить субмодуль 
```
git submodule deinit <path_to_submodule>
git rm <path_to_submodule>
git commit-m "Removed submodule "
rm -rf .git/modules/<path_to_submodule>
```
14. В дальнейшем
```
$ hugo
$ cd public
$ git add .
$ git commit -m "New Public"
$ git push -u origin master
```
15. Другая тема - так же в темах
```
$ cd themes
$ git clone https://github.com/spech66/bootstrap-bp-hugo-theme.git

```
16. Переновсим и редактируем из темы файлы в layouts

17. Особенности формления:
- созадем каталоги 000-название-статьи
- статья называется index.md 
- разделитель теста в списке `<!--more-->`
- картинки:
  - *feature* небольшая в общем оглавлении
  - *motivation* в основном блоке
- меню через 
  ```
  menu: 
      main:
          parent: "QA testing"
  ```

18. Menu:
- DevOps
- Python and ML
- QA testing
- Golang
- JavaScript
- Hobby