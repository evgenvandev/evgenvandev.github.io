---
layout: default
title: Параметры командной строки Node.js
parent: Node.js tutorial
grand_parent: Node.js
nav_order: 3
has_toc: false
---

# Параметры командной строки Node.js
{: .no_toc}

Node.js можно запустить в командной строке с параметрами командной строки.   
Представим некоторые параметры. 

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## node -h или - -help

Чтобы получить информацию обо всех доступных параметрах, воспользуйтесь ключом `-h` или `--help`:

```
node --help
```

![Вывод команды node --help]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_node_--help.jpg "Вывод команды node --help")

## node -v или - -version

Для получения версии Node.js используется следующая команда: 

```
node --version
```

![Вывод команды node --version]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_node_--version.jpg "Вывод команды node --version")

## node -c или - -check script.js

Для проверки синтаксиса приложения Node.js используется параметр `-c`. С этим параметром команда `node` проверяет синтаксис без 
запуска приложения. 

```
node --check
```

## node - -v8-options

Чтобы получить информацию о параметрах V8, вводим следующую команду: 

```
node --v8-options
```

![Вывод команды node --v8-options]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_node_--v8-options.jpg "Вывод команды node --v8-options")

Команда выводит список разных параметров, в том числе параметр `--harmony`, используемый для включения всех завершённых функций Harmony. 
Сюда входит вся функциональность ES6, уже реализованная, но ещё не вошедшая в версию с долгосрочной поддержкой (_LTS, Long Term Support_) 
или в текущую версию. 

## node -p или - -print

Параметр Node.js `-p` или `--print` - обрабатывает строку сценария Node.js и выводит результаты. Данная возможность особенно полезна 
при проверке свойств окружения процесса. В следующем примере выводятся все значения свойства `process.env`: 

```
node --print "process.env"
```

![Вывод команды node --print_process_env]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/node-js-tutorial/output_node_--print_process_env.jpg "Вывод команды node --print_process_env")

