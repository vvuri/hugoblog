---
categories: []
tags: ["DevOps","GIT","GITLAB"]
description: ""
menu: 
    main:
        parent: "DevOps"
date: "2017-11-20T23:27:56+03:00"
title: "Работа с репозиторием"
---

#### GIT GITLAB 
- [Git Flow](https://ericdouglas.github.io/2016/04/01/Git-Useful-Tips/)
- [На русском часть команд](http://eax.me/git-commands/)
<!--more-->
	
#### Install Debian:
~~~
$ sudo apt-get install git
$ git --version
  git version 1.7.10.4
~~~

#### Термины
- помещение (push) 
- получение (pull) 

#### Основной процесс работы с репозиторием
1. GitHub - добавляем SSH key
2. находясь в основной папке клонируем весь образ - получаем отдельную папку
	
	~~~ 
	$ git clone git@git.XXXXXXXXX.git 
	~~~
3. все команды работают внутри
	~~~ 	
	$ cd partners-installation 
	~~~
4. Изменения в репозитории
   ~~~
   $ git status => master  
   ~~~
5. Создаем новую ветку:
   ~~~
   $ git checkout -b devdcm 
   ~~~
6. Внесение изменение и добавление или удаление
   ~~~
   $ git add doc.yml 
   $ git rm text.txt 
   ~~~
7. Локальный коммит
   ~~~
   $ git commit -m 'Add file ...' 
   ~~~
8. Откатится с перезаписью файлов но без удаления новых файлов					
   ~~~
   $ git reset --hard devdcm 
   ~~~
9. Посмотреть что менялось
   ~~~
   $ git diff 
   ~~~
10. Залить на сервер		
   ~~~
   S git push origin devdcm 
   ~~~
11. Объединение с основной веткой
   ~~~
   $ git checkout master
   $ git pull origin master
   $ git checkout dev
   $ git pull origin dev
   $ git merge master
   $ git push origin dev 
   ~~~


#### Дополнение:
- Создать новый репозиторий:
~~~
$ git init project-name 
~~~

- Если вы планируете клонировать его по ssh с удаленной машины, также скажите:
~~~
$ git config --bool core.bare true 
~~~

- Переключиться на другую ветку (из тех, с которыми уже работаем):
~~~
$ git checkout some_branch 
~~~

- Просмотреть все существующие ветви:
~~~
$ git branch -a # | grep something 
~~~

- Удалить бранч (после мерджа):
~~~
$ git branch -d some_branch 
~~~

- Просто удалить бранч (тупиковая ветвь):
~~~
$ git branch -D some_branch 
~~~

- История изменений:
~~~
$ git log 
~~~

- История изменений в обратном порядке:
~~~
$ git log --reverse 
~~~

- История конкретного файла:
~~~
$ git log file.txt
~~~

- Аналогично предыдущему, но с просмотром сделанных изменений:
~~~
$ git log -p file.txt
~~~

- История с именами файлов и псевдографическим изображением бранчей:
~~~
$ git log --stat --graph
~~~

- Изменения, сделанные в заданном коммите:
~~~
$ git show d1234edf8458ce06...
~~~

- Посмотреть, кем в последний раз правилась каждая строка файла:
~~~
$ git blame file.txt
~~~

- Удалить бранч из репозитория на сервере:
~~~
$ git push origin :branch-name
~~~

- Откатиться к конкретному коммиту (хэш смотрим в «git log»):
~~~
$ git reset --hard d1234edf8458ce06...
~~~

#### Error и их решения		
~~~
$ git checkout .gitignore
$ git reset
~~~