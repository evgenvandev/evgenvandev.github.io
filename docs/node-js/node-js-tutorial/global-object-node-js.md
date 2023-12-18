---
layout: default
title: Глобальные объекты в Node.js
parent: Node.js tutorial
grand_parent: Node.js
nav_order: 4
has_toc: false
---

# Глобальные объекты в Node.js
{: .no_toc}

Хотя и браузерные приложения, и приложения Node.js пишутся на JavaScript, условия их выполнения заметно различаются. Одно из 
принципиальных различий между Node.js и его браузерным "родственником" - _буфер_ для двоичных данных. Правда, в Node.js появилась 
поддержка _типизованных массивов_ и `ArrayBuffer` из ES6. Однако большая часть функциональности двоичных данных в Node.js реализуется 
при помощи класса `Buffer`. 

Объек `buffer` принадлежит к числу глобальных объектов Node.js. Другой пример глобального объекта - сам объект `global`, хотя в Node.js 
он принципиально отличается от глобального объекта, к которому мы привыкли по браузеру. Разработчикам Node.js также доступен другой 
глобальный объект, `process`, - он связывает приложение Node.js со средой, в которой оно выполняется. 

К счастью, один из аспектов Node.js - асинхронная природа, управляемая событиями, - должен быть хорошо знаком разработчикам интерфейсных 
приложений. Просто приложение Node.js ожидает открытия файла, а не нажатия кнопки пользователем. 

Управляемость событиями также означает, что в Node.js доступны наши старые знакомые - функции-таймеры. 

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Объекты _global_ и _process_

Два важнейших объекта в Node.js - `global` и `process`. Объект `global` немного похож на глобальный объект в браузере, хотя между ними 
существуют очень серьёзные различия. Объект `process`, напротив, существует только в Node.js.

### Объект global 

В браузере переменная, объявленная на верхнем уровне, объявляется глобально. В Node.js дело обстоит иначе. Переменная, объявленная в 
модуле или приложении Node.js, не обладает глобальной доступностью; она ограничивается модулем или приложением. Таким образом, можно 
объявить "глобальную" переменную с именем `str` в модуле  и в приложении, использующем этот модуль, и никакого конфликта не будет. 

Для демонстрации создадим простую функцию, которая прибавляет число к базовому значению и возвращает результат. Функция будет создана 
как библиотека JavaScript для использования в веб-странице, а также как модуль для использования в приложении Node.js. 
