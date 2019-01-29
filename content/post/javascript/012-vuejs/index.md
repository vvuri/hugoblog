---
title: "Кратко об основах Vue.js"
categories: ["Code"]
tags: ["JavaScript","Vuejs"]
description: ""
menu: 
    main:
        parent: "JavaScript"
date: "2018-12-20"
---

- Основной сайт - `vuejs.org`
- [короткий вводный курс](https://tproger.ru/video/vue-from-scratch/)
- достаточно подключить `vue.min.js`
<!--more-->
- далее `new Vue({el:"#app", data:{}})` 
  где 
  - `<div id="app">` контейнер в котором будет все исполнятся, 
  - data - данные экспортируемые в контейнер
  - к тегам добавляются свойсва v-xxx которые делают те или иные действия
- события `<button v-on:click="onClickfun">` и далее делаем обработчик в methods:`{onClickfun:function(){...}`
- есть возможность анимировать
- фильтры - js функции, есть набор встроенных `{{ 'фильтры' | uppercase}}`, `orderBy` - сортировка, `filterBy` - поиск
- можно подключить MArkdown разметку marked.min.js  `<div>{{{ input | marked }}}</div>`  `Vui.filter('marked', marked)`
- можно написать свой фильтр с заменой слов на символы и т.д.
- можно разбвивать код на отдельные компоненты в отдельных файлах, но есть проблема зависимостей 
- поэтому используются сборщики - browserify, webpack

- [Пример проекта с компонентами](https://www.youtube.com/watch?list=PL5r0NkdgM0UOxb4Hl81FV5UIgexwTf8h7&v=TdlF9_S2D3c)
	- создаем каталог и заходим в него
	- `npm init --yes`  внутри создаем `package.json`
	- добавляем список зависимостей devDependencies
	- `npm install`  установит все зависимые пакеты в node_modules
	- в main.js инициализируем Vue
	- создаем папку components и в ней `hello.vue` c template, script, style и отдаем наружу через module.exports
	- добавляем в main.js наш компонент require и его экземпляр
	- на странице уже можно взять тег `<hello>`
	- добавляем в `package.json` build запускающий browserify
	- и далее запускаем `npm run build`
	- добавляем еще watchify который будет автоматом билдить при измееннии компонет
	
- Альтернативный вариант - использование  webpack
	- много дополнительных модулей jade, sass
	- и немного все компактнее
	- watch уже встроен
	
- **vue-cli**
	- консольная утилита, помогает когда проектов много и надо быстро их создавать
	- используются готовые шаблоны или создаем собственные
	- sudo npm install -g vue-cli
	- vue init название_шаблона название_папки_установки
	- напирмер  vue init webpack-simple mytestproject
	- заходим внутрь и npm install устанавливаем зависимости
	- npm run dev запускаем сборку
- **vue-resurce**
	- плагин ассинхронных REST запросов к серверу удаленных данных
	- [video](https://www.youtube.com/watch?v=YZEm4dTnP80)
- **vue-router**
	- можно сделать одностраничное приложение 
	- [video](https://www.youtube.com/watch?v=Hv5SM19oQ6w)
	- `<router-link to="">`
- vuex
	- плагин единого хранилища данных, но это уже для сложного приложения,   т.к. много когда надо дописывать
	- вынос в отдельный файл
- [pagination](https://www.youtube.com/watch?v=Hx1jdZz7vlg)

