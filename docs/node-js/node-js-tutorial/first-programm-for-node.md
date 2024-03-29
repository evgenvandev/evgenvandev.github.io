---
layout: default
title: Первая программа для Node.js
parent: Node.js tutorial
grand_parent: Node.js
nav_order: 2
has_toc: false
---

# Первая программа для Node.js
{: .no_toc}

У программистов есть традиция: начинать программирование на новом языке с приложения "Hello, World". 
{: .fs-6 .fw-300}

Приложение обычно выводит слова "Hello, World" в выходной поток (каким бы он ни был), демонстрируя тем самым, что 
приложение создаётся, запускается и может выполнять операции ввода/вывода.   
Эта традиция соблюдается и для Node.js: приложение "Hello, World" на сайте _[Node.js](https://nodejs.org)_ включается в 
документацию. 

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Простейшее приложение "Hello, World"

Для начала рассмотрим версию "Hello, World" из документации Node.js. Чтобы воссоздать приложение, создайте текстовый документ 
с кодом JavaScript в текстовом редакторе, например в Notepad++. 

_Файл hello.js_
```javascript
/* Пауэрс Ш. Изучаем Node. Переходим на сторону сервера (2-е издание) - 2017
Глава-1 Листинг 1.1. Простейшее приложение Hello, World - стр. 19 */
var http = require('http');

http.createServer(function(request, response){
  response.writeHead(200, {'Content-Type': 'text/plain'});
  response.end('Hello World\n');
}).listen(8124);

// Вывод сообщения в командную строку:
console.log('Server running at http://127.0.0.1:8124/');
```

Чтобы запустить приложение, открываем окно командной строки в Windows, переходим в каталог, в котором находится файл _hello.js_ 
и вводим следующую команду для запуска приложения: 

```
node hello.js
```

Результат выводится в командной строке вызовом функции `console.log()` в приложении: 

![Вывод программы hello.js]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_hello_world.jpg "Вывод программы hello.js")

Теперь откроем браузер и введём адрес _http://localhost:8124/_ или _http://127.0.0.1:8124_ в адресной строке (или указываем 
свой домен, если разместили Node.js на сервере). Открывается простая веб-страница с сообщением "Hello, World" в верхней части. 

![Вывод программы hello.js в браузере]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_hello_world_in_browser.jpg "Вывод программы hello.js в браузере")

Чтобы завершить программу, закройте окно командной строки или нажмите Ctrl+C. Когда вы запустили приложение, оно 
выполнялось в _активном_ (foregroung) режиме. Это означает, что во время его выполнения вы не сможете ввести в командной 
строке никакую другую команду. 
Кроме того, закрытие окна командной строки приведёт к остановке процесса Node.js.

Запуск Node.js в фоновом режиме
{: .label}
> На этой стадии лучше запускать Node.js в активном режиме. Пока вы учитесь, как пользоваться этим инструментом, и не 
хотите, чтобы любой желающий смог получить внешний доступ к вашему приложению. 

Вернёмся к коду программы: JavaScript создаёт веб-сервер, который при обращении к нему из браузера выводит веб-страницу со словами 
"Hello, World". Он демонстрирует несколько ключевых компонентов приложения Node.js.   
Сначала программа включает необходимый для запуска простого сервера HTTP модуль с подходящим именем _HTTP_. Внешняя функциональность 
Node.js подключается при помощи модулей, экспортирующих определённые типы функциональности, которая может использоваться в приложении 
(или другом модуле). Модули очень похожи на библиотеки в других языках программирования. 

```javascript
var http = require('http');
```

> Модуль HTTP входит в число базовых модулей Node.js

Модуль импортируется командой Node.js `require`, а результат присваивается локальной переменной. После импортирования локальная 
переменная может использоваться для создания экземпляра веб-сервера функцией `http.createServer()`. В параметрах функции 
встречается одна из фундаментальных конструкций Node.js: функция обратного вызова (callback). 

_Листинг 1.1. Функция обратного вызова в приложении "Hello, World"_
```javascript
http.createServer(function(request, response){
  response.writeHead(200, {'Content-Type': 'text/plain'});
  response.end('Hello World\n');
}).listen(8124);
```

JavaScript - однопоточный (single-threaded) язык, и для имитации асинхронного выполнения в Node.js используется _цикл событий_, 
а функции _обратного вызова_ вызываются при срабатывании определённого события. В листинге 1.1 функция обратного вызова 
вызывается при получении веб-запроса.
{: .text-blue-200}

Сообщение `console.log()` выводится на терминал сразу же при вызове создания сервера. Программа не прекращает работу в блокирующем 
режиме, ожидая веб-запроса.

```javascript
console.log('Server running at http://127.0.0.1:8124/');
```

После того как сервер будет создан и получит запрос, функция обратного вызова передаёт браузеру простой текстовый заголовок 
с кодом статуса 200, выводит сообщение _Hello World_ и завершает ответ.

## "Hello, World" - новая версия

Обновлённый код приведён в листинге 1.2. В нём изменено базовое приложение и включена обработка входящего запроса. Имя выделяется 
из строки и используется для определения типа возвращаемого контента. Почти для любого имени будет возвращён персонализированный ответ, 
но если использовать в запросе параметр `name=burningbird`, вы получите изображение птицы феникс.

![Птица феникс]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/phoenix5a.png "Птица феникс")

Если строка запроса не используется или 
в нём не указано имя, переменной `name` присваивается значение `'world'`.

_Листинг 1.2. Программа "Hello, World" в обновлённой версии_.   
_Файл listing_1-2.js_
```javascript
/* Пауэрс Ш. Изучаем Node. Переходим на сторону сервера (2-е издание) - 2017
Глава-1 Листинг 1.2. Программа "Hello, World" в обновлённой версии - стр. 22 */
var http = require('http');
var fs = require('fs');

http.createServer(function(req, res){
  var name = require('url').parse(req.url, true).query.name;
  
  if (name === undefined) name = 'world';
  
  if (name == 'burningbird') {
    var file = 'images/phoenix5a.png';
    fs.stat(file, function(err, stat){
      if (err){
        console.error(err);
        res.writeHead(200, {'Content-Type': 'text/plain'});
        res.end("Sorry, Burningbird isn't around right now \n");
      } else {
        // Использование синхронной функции readFileSync():
        var img = fs.readFileSync(file);
        res.contentType = 'image/png';
        res.contentLength = stat.size;
        res.end(img, 'binary');
      }
    });
  } else {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello ' + name + '\n');
  }
}).listen(8124);

// Выводим сообщение в командную строку:
console.log('Server running at port 8124/');
```

Запускаем приложение командой: 

```
node listing_1-2.js
```

![Вывод программы listing_1-2.js]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_listing_1-2.jpg "Вывод программы listing_1-2.js")

В браузере вводим следующий адрес `http://localhost:8124?name=burningbird`, где параметр `name` принимает значение `burningbird`. 

![Вывод программы listing_1-2.js в браузере]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_listing_1-2_in_browser.jpg "Вывод программы listing_1-2.js в браузере")

Всё правильно, параметр `name` принял значение `burningbird`, поэтому из файла `phoenix5a.png` на страницу браузера загрузилось 
изображение птицы феникс.   
Теперь присвоим параметру `name` значение `Evgeny`, то есть в браузере вводим следующий адрес `http://localhost:8124?name=Evgeny`. 

![Вывод программы listing_1-2.js в браузере. name=Evgeny]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_listing_1-2_in_browser-1.jpg "Вывод программы listing_1-2.js в браузере. name=Evgeny")

Верно, появляется приветствие `Hello Evgeny`.   
Дополнительного кода не так уж много, но между базовым приложением "Hello, World" и обновлённой версией существует ряд различий. 
В начале кода в приложение включается новый модуль с именем `fs`, это модуль файловой системы (_File System_). При этом в программе 
импортируется ещё один модуль, но не так, как два других: 

```javascript
var name = require('url').parse(req.url, true).query.name;
```

Свойства экспортируемых модулей могут объединяться в цепочки, что позволяет импортировать модуль и использовать его функции в одной строке. 
Это часто происходит в модуле _URL_, единственная цель которого - предоставить инструменты для работы с URL-адресами. 

Имена параметров ответа (_response_) и запроса (_request_) для удобства часто сокращаются до _res_ и _req_ соответственно. После разбора 
запроса для получения значения `name` программа сначала проверяет, равен ли параметр `undefined`. Если параметр не определён, используется 
значение по умолчанию `world`. Если же значение `name` существует, оно снова проверяется и сравнивается с `burningbird`. Если 
значения не совпадают, то приложение возвращает почти такой же ответ, как в исходном приложении, не считая того, что в возвращаемое 
сообщение подставляется переданное имя. 

Но если параметр `name` содержит строку `burningbird`, это означает, что вместо текста придётся иметь дело с изображением. Метод `fs.stat()` 
не только проверяет, что файл существует, но также возвращает объект с информацией о файле, включающей его размер. Значение размера файла 
используется для создания заголовка контента. 

Если файл не существует, то приложение корректно обрабатывает ситуацию: оно выводит дружелюбное сообщение об ошибке и информацию на консоль, 
для чего на этот раз используется метод `console.error()`: 

```
{[Error: ENOENT: no such file or directory, stat 'images/phoenix5a.png']
  errno: -2,
  code: 'ENOENT',
  syscall: 'stat',
  path: 'images/phoenix5a.png'}
```

Если файл существует, то изображение загружается в переменную и приложение возвращает его в ответе (параметре _res_), изменяя 
значения в заголовке соответствующим образом. 

Метод `fs.stat()` использует стандартный для Node.js паттерн функции обратного вызова с передачей значения ошибки в первом параметре. 
Но возможно, часть с загрузкой изображения показалась вам несколько неожиданной. Она просто необычно выглядит и не похожа на другие 
функции Node.js, которые скорее всего, встретятся в других примерах в Интернете. Главное отличие - использование синхронной функции 
`readFileSync()` вместо асинхронной версии `readFile()`. 

```javascript
fs.readFile(file, function(err, data){
  res.contentType = 'image/png';
  res.contentLength = stat.size;
  res.end(data, 'binary');
});
```

Node.js поддерживает как синхронную, так и асинхронную версию большинства функций файловой системы. Обычно использование 
синхронных операций в веб-запросах в Node.js считается крайне нежелательным, но такая возможность существует. Асинхронная 
версия того же фрагмента кода используется в примере 1.3. 

_Листинг 1.3. Программа "Hello, World" в обновлённой версии,   
с асинхронной версией функций readFile()_.   
_Файл listing_1-3.js_
```javascript
/* Пауэрс Ш. Изучаем Node. Переходим на сторону сервера (2-е издание) - 2017
Глава-1 Листинг 1.3. Программа "Hello, World" в обновлённой версии, с асинхронной 
версией функции readFile() - стр. 25 */
var http = require('http');
var fs = require('fs');

http.createServer(function(req, res){
  var name = require('url').parse(req.url, true).query.name;
  
  if (name === undefined) name = 'world';
  
  if (name == 'burningbird') {
    var file = 'images/phoenix5a.png';
    fs.stat(file, function(err, stat){
      if (err){
        console.error(err);
        res.writeHead(200, {'Content-Type': 'text/plain'});
        res.end("Sorry, Burningbird isn't around right now \n");
      } else {
        // Использование асинхронной функции readFile():
        fs.readFile(file, function(err, data){
          res.contentType = 'image/png';
          res.contentLength = stat.size;
          res.end(data, 'binary');
        });
      }
    });
  } else {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello ' + name + '\n');
  }
}).listen(8124);

// Выводим сообщение в командную строку:
console.log('Server running at port 8124/');
```

Запускаем приложение командой: 

```
node listing_1-3.js
```

![Вывод программы listing_1-3.js]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_listing_1-3.jpg "Вывод программы listing_1-3.js")

В браузере вводим следующий адрес `http://localhost:8124?name=burningbird`, где параметр `name` принимает значение `burningbird`. 

![Вывод программы listing_1-3.js в браузере]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_listing_1-3_in_browser.jpg "Вывод программы listing_1-3.js в браузере")

Всё хорошо, загрузка изображения выполнена, значит асинхронная версия функции `readFile()` сработала. 

Когда какую версию стоит использовать? В некоторых обстоятельствах файловый ввод/вывод не влияет на производительность независимо от 
типа функции, а синхронная версия кажется более "чистой" и простой. Она также может уменьшить уровень вложенности кода - эта проблема 
особенно важна для системы обратного вызова Node.js. 

Кроме того, хотя в этом примере обработка исключений не используется, с синхронными функциями можно использовать конструкцию `try...catch`. 
С асинхронными функциями эта более традиционная форма обработки ошибок невозможна (отсюда и передача кода ошибки в первом параметре 
анонимной функции обратного вызова). 
{: .text-blue-200}

