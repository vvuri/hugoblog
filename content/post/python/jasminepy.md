+++
categories = ["Python","Programming"]
description = ""

tags = ["jasmine", "unit-test"]
date = "2017-04-16T14:19:23+03:00"
title = "Jasmine in Python"

+++

**Jasmine** — фреймворк для описания тестов на JavaScript, обладающий простым BDD-синтаксисом и широкими возможностями. Jasmine самодостаточен, тесты, написанные при помощи этого фреймворка можно запустить под Node без каких-либо дополнительных ухищрений.

<!--more-->
in Python:  
Jasmine projects for Python-based web projects 
(Django, Flask, etc.)
== jasmine.github.io/edge/python_egg.html
== github.com/jasmine/jasmine-py
{{< highlight bash >}}
$ pip install jasmine
Использование - инициализация 
$ jasmine-install
создает в глубинах папок файл jasmine.yml
в данном файле заносим где у нас что будет

$ jasmine -p 1337
запускает сервер на порту 1337, по-умолчанию на 8888

$ jasmine-ci
Запуск системы Continuous Integration environments

$ jasmine-ci --browser firefox

или
$ export JASMINE_BROWSER=chrome
$ jasmine-ci

или
$ jasmine-ci --seed 4321
$ jasmine-ci --browser phantomjs
описание команд используемых в проектах
{{< /highlight >}}
== jasmine.github.io/api/edge/global.html#describe
