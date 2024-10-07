---
layout: default
title: Руководство по tinylog
parent: Logging in Java
grand_parent: Java
nav_order: 5
has_toc: false
---

# Руководство по tinylog
{: .no_toc}
В этом руководстве показано ведение журнала в приложении Java с использованием облегчённой платформы ведения журнала 
[tinylog](https://tinylog.org/v2/)   
[Ссылка на источник](https://mkyong.com/logging/tinylog-tutorial/)

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Необходимые файлы tinylog

Для ведения журнала в _tinylog_ нам необходимо добавить `tinylog-api` и `tinylog-impl` в _classpath_ проекта.   
Скачиваем с официального сайта необходимые [файлы](https://tinylog.org/v2/download/).   
![Скачиваем tinylog]({{ site.url }}{{ site.baseurl }}/assets/images/java/java-logging/java-logging-tinylog-download.jpg "Архив с файлами tinylog-api.jar, tinylog-impl.jar")

Если используем _Maven_ в файл _pom.xml_ добавляем следующие две зависимости:

_Файл pom.xml_
```xml
<dependency>
  <groupId>org.tinylog</groupId>
  <artifactId>tinylog-api</artifactId>
  <version>2.3.2</version>
</dependency>

<dependency>
  <groupId>org.tinylog<groupId>
  <artifactId>tinylog-impl</artifactId>
  <version>2.3.2</version>
</dependency>
```

## Hello, World! с tinylog

У _tinylog_ есть статический регистратор, поэтому нам нет необходимости создавать экземпляр класса регистратора, как показано ниже:

```java
// no need to declare Logger, tinylog provide static Logger
// нет необходимости объявлять Logger, tinylog предоставляет статический Logger
// private static Logger logger = Logger.getLogger(HelloWorld.class.getName());
```

_Файл HelloWorld.java_
```java
package com.mkyong;

import org.tinylog.Logger;

public class HelloWorld {
  // no need declare Logger like other logging frameworks
  // нет необходимости объявлять Logger, как другие фреймворки для ведения журналов
  public static void main(String[] args) {
    Logger.info("Hello World tinylog!");
    Logger.trace("This is trace!");
    Logger.debug("This is debug!");
    Logger.info("This is info!");
    Logger.warn("This is warn!");
    Logger.error("This is error!");
  }
}
```

В папке проекта создаём папки _bin, libs, src/com/mkyong_.   
В папку _libs_ помещаем два файла библиотеки `tinylog`: `tinylog-api-2.7.0.jar` и `tinylog-impl-2.7.0.jar`
Компилируем файл _HelloWorld.java_ командой: 

```
javac -encoding utf-8 -sourcepath ./src -d ./bin src/com/mkyong/*.java -classpath ./libs/tinylog-api-2.7.0.jar;./libs/tinylog-impl-2.7.0.jar
```

Запускаем программу командой: 

```
java -classpath ./libs/tinylog-api-2.7.0.jar;./libs/tinylog-impl-2.7.0.jar;./bin com.mkyong.HelloWorld
```

Получаем следующий вывод программы в консоль: 
![Вывод tinylog в консоль]({{ site.url }}{{ site.baseurl }}/assets/images/java/java-logging/java-logging-tinylog-output-1.jpg "Вывод tinylog в консоль")

## Уровни ведения журнала tinylog

Tinylog поддерживает пять уровней ведения журнала: 
- trace
- debug
- info
- warn
- error

В tinylog уровень ведения журнала по умолчанию - `trace`.

## Логи с аргументами

В tinylog мы можем использовать `{}` заполнители для представления аргументов.

```java
Logger.trace("arg1 {} and arg2 {}", a, b);
Logger.debug("arg1 {} and arg2 {}", a, b);
Logger.info("arg1 {} and arg2 {}", a, b);
Logger.warn("arg1 {} and arg2 {}", a, b);
Logger.error("arg1 {} and arg2 {}", a, b);
```

Ниже приведён полный пример для журнала _tinylog_ с аргументами. 

_Файл LogWithArguments.java_
```java
package com.mkyong;

import org.tinylog.Logger;

public class LogWithArguments {
  public static void main(String[] args) {
    String msg = "info";
    int number = 9;
    
    Logger.info("This is {}, {}", msg, number);
    Logger.error("This is {}", "error");
  }
}
```

Получаем следующий вывод программы в консоль: 
![Вывод в консоль LogWithArguments, с помощью tinylog]({{ site.url }}{{ site.baseurl }}/assets/images/java/java-logging/java-logging-tinylog-output-with-arguments-1.jpg "Вывод в консоль LogWithArguments, с помощью tinylog")

## Файл tinylog.properties

