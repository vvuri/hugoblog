---
categories: ["DataBase"]
tags: ["InfluxDB", "Grafana"]
description: ""
menu: 
    main:
        parent: "DevOps"
date: "2019-01-20"
title: "Начало работы с InfluxDB"
---

InfluxData представляет собой набор приложений, написанных на языке Go:
<!--more-->
- Telegraf - утилита для сбора измерений временных рядов.
- InfluxDB - кластеризуемая база данных, специально разработанная для хранения временных рядов.
- Chronograf - инструмент для визуализации временных рядов. Web приложение для настройки графиков и dashboard'ов.
- Kapacitor - утилита для обработки значений временных рядов и контроля отклонений значений. 

Скачиваем последнюю версию InfluxDB с [сайта](https://influxdata.com/downloads), и устанавливаем.
```bash
$ wget https://s3.amazonaws.com/influxdb/influxdb_0.9.6.1_amd64.deb
$ sudo dpkg -i influxdb_0.9.6.1_amd64.deb
```
После установки запускаем сервис influxdb:
```bash
$ sudo service influxdb start
  Starting the process influxdb [ OK ]
  influxdb process was started [ OK ]
```

#### influx	
> show databases<br>
> create database mydb<br>
> use mydb

> insert cpu,host=serverA,region=Yekaterinburg value=0.35<br>
> insert cpu,host=serverA,region=Yekaterinburg value=0.26<br>
	Мы добавили 2 точки измерения с именем "cpu" со значениями "0.35" и "0.26" и с тегами "host" и "region".
> insert cpu,host=serverB,region=Yekaterinburg value=0.89<br>
	
> select * from cpu

#### HTTP 	
```
curl -i -XPOST 'http://localhost:8086/write?db=mydb' --data-binary 'cpu,host=serverA,region=Yekaterinburg value=0.11'
```
добавляем через HTTP API точки по пути /write. Имя базы данных передается URL параметром db, а строка данных передается в теле запроса. 
```
curl -G 'http://localhost:8086/query?pretty=true' --data-urlencode "db=mydb" --data-urlencode "q=select * from cpu where host='serverB'"
```
Получить данные


#### Теория: 
[Описание-influxdb](http://blog.egrik.ru/2016/01/influxdata-1-influxdb.html), [Описание-telegraf](http://blog.egrik.ru/2016/01/influxdata-2-telegraf.html), [Описание-chronograf](http://blog.egrik.ru/2016/01/influxdata-3-chronograf.html)

Данные в InfluxDB организованы в виде временного ряда, который содержит измеренные значения, например загрузка процессора - "cpu_load" или температура - "temperature". Временной ряд содержит 0 или несколько точек, по одной на каждое значение измерения метрики. Каждая точка содержит время (timestamp), имя измерения или метрики (measurement), не менее одного поля (fields) в формате ключ-значения (например value=0.5), и 0 или несколько тегов (tags) в формате ключ-значение, которые содержат метаинформацию о собранном значении (host="server01", region="Yekaterinburg").
		
Если провести аналогию с SQL базой данных, то измерение (measurement) - это таблица, в которой первичным ключом является колонка со временем (timestamp). Теги (tags) - это индексированные колонки, а поля (fields) - это не индексированные колонки. Только в отличие от SQL базы данных в InfluxDB, можно сохранить миллионы измерений (measurement), вы не обязаны заранее определять схему, и null значения не будут храниться.

В общем виде формат добавления новой точки измерения в БД выглядит так:
```
<measurement>[,<;tag-key>=<tag-value>...] <field-key>=<field-value>[,<field2-key>=<field2-value>...] [unix-nano-timestamp]
`

