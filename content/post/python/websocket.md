+++
tags = ["websocket"]
categories = ["Python","Programming"]
description = ""
draft = true
date = "2017-04-15T23:50:36+03:00"
title = "WebSocket in Python"

+++

Протокол предназначен для обмена сообщениями между браузером и веб-сервером
Соединение - используется протокол похожий на HTTP.
Клиент формирует особый HTTP-запрос, на который сервер отвечает определенным образом.
<!--more-->

Есть rfc6455
Поверх TCP, встоен в ключевые браузеры и доступен из JS
JS:  var ws = new WebSocket("ws://127.0.0.1:5678/"),

http://websockets.readthedocs.io/en/latest/
{{< highlight bash >}}
$ pip install asyncio.
$ pip install websockets
{{< /highlight >}}
требуется так же asyncio on Python 3.3+
Есть готовый пример http://websockets.readthedocs.io/en/latest/intro.html