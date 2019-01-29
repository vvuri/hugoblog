---
title: "Установка и работа с NodeJS"
categories: ["Code"]
tags: ["JavaScript","NodeJS"]
description: ""
menu: 
    main:
        parent: "JavaScript"
date: "2019-01-10"
---

#### Пакетные менеджеры
- **bower** - древний
- **npm** - из nodejs
- **yarn** - конкурент npm но внутри он же
<!--more-->
### npm - установка
- Install:
  ```
  $ curl https://npmjs.org/install.sh | sh
  ```
- Поиск пакетов
  ```
  $ npm search hook.io
  ```
- Информация о пакете
  ```
  $ npm view hook.io
  ```
- Установка пакета
  ```
  $ npm install http-server      локально - виден только в папке установки
  $ npm install http-server -g   глобально			
  ```
- Удаление пакета
  ```
  $ npm uninstall http-server
  ```				
- Создание пакета
  ```
  $ mkdir mypackage/
  $ cd mypackage/
  $ npm init	
  ```

#### Работа с пакетами для FrontEnd  
[статья на habr](https://habrahabr.ru/company/mailru/blog/340922/)
1. заходим в папку с проектом		
2. `$ npm init`  создаст файл package.json
3. `$ npm install moment --save`  установка пакета - аналог скачивания js файлика 
4. `<script src="node_modules/moment/min/moment.min.js"></script>`
5. `$ npm install webpack --save-dev`  ставим бандлер-упаковщик всех файлов в один пакет
6. у нас есть предположим файл index.js
   ```
   var moment = require('moment');
   console.log("Hello from JavaScript!");
   console.log(moment().startOf('day').fromNow());
   ```
7. `$ ./node_modules/.bin/webpack index.js bundle.js`	
  мы зависимость requeire превратим в правильный путь и создадим один выходной файл
8. `<script src="bundle.js"></script>`  теперь вместо раннее описанного
9. `$ ./node_modules/.bin/webpack` чтобы упростить работу при каждой сборке
	где  `webpack.config.js`
	`module.exports = {entry: './index.js', output: {filename: 'bundle.js'}};`
10. Транспилирование кода - babel, TypeScript, CoffeeScript
11. `$ npm install babel-core babel-preset-env babel-loader --save-dev`
12. webpack.config.js
    ```
	module.exports = {
		entry: './index.js', 
		output: {filename: 'bundle.js'}, 
		module: {rules: 
			[{test: /\.js$/, 
			exclude: /node_modules/, 
			use: { loader: 'babel-loader', 
				options: {presets: ['env']}}}]}};  	
    ```	
13. теперь можно писать на ECMA2015 - index.js
	```
	import moment from 'moment';
	console.log("Hello from JavaScript!");
	console.log(moment().startOf('day').fromNow());
	var name = "Bob", time = "today";
	console.log(`Hello ${name}, how are you ${time}?`);
	```
14. `$ ./node_modules/.bin/webpack`	 получаем рабочую версию 
15. `$ npm install webpack-dev-server --save-dev` установка вебсервера для разработки 
16. ранее был **Grunt**, но вскоре его место занял **Gulp**
	*package.json*:
	```
	{
		"name": "modern-javascript-example", "version": "1.0.0", "description": "",  
		"main": "index.js",
		"scripts": {
		"test": "echo \"Error: no test specified\" && exit 1",
		"build": "webpack --progress -p",
		"watch": "webpack --progress --watch",
		"server": "webpack-dev-server --open"
		},
		"author": "",  "license": "ISC",  
		"dependencies": {"moment": "^2.19.1"},
		"devDependencies": {"babel-core": "^6.26.0", "babel-loader": "^7.1.2", "babel-preset-env": "^1.6.1", "webpack": "^3.7.1"}
	}
	```
17. `$ npm run build`  сборка запускает webpack (с webpack.config.js), с опцией -p для минимизации кода.
18. `$ npm run watch`  перезапуск webpack при каждом изменении JavaScript-файла
19. `$ npm run server`  запускаем сервер

описана [куча автоматизации](https://webpack.js.org/guides/development/) по sass и тд 

#### Целый ряд пакетов для тестироваия
```
npm install -g karma
npm install -g jasmine
npm install -g jasmine-core
npm install -g karma-cli
npm install -g karma-jasmine
npm install -g phantomjs-prebuilt
npm install -g karma-phantomjs-launcher
```
	
#### Ставим NodeJS на Linux
- [качаем версию для linux](https://nodejs.org/en/download/)
- распаковываем
- `mv node-v6.9.4-linux-x64/ nodejs`
- `export PATH="$HOME/soft/nodejs/bin:$PATH"`
- `vi .profile`
	```
	export PATH=$HOME/soft/nodejs/bin
	```
- `node -v`

#### алтернативный вариант - возможно как добавление к прежнему
- `curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -`
- `sudo apt-get install -y nodejs`
- `sudo apt-get install -y build-essential`
- переоткртыть терминал
- `npm version`
	```
	npm: '5.6.0',
	ares: '1.10.1-DEV',
	cldr: '31.0.1',
	http_parser: '2.7.0',
	icu: '59.1',
	modules: '57',
	nghttp2: '1.25.0',
	node: '8.9.4',
	openssl: '1.0.2n',
	tz: '2017b',
	unicode: '9.0',
	uv: '1.15.0',
	v8: '6.1.534.50',
	zlib: '1.2.11'
	```