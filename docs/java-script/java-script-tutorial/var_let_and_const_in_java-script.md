---
layout: default
title: Var, let и const в JavaScript
parent: JavaScript tutorial
grand_parent: JavaScript
nav_order: 2
has_toc: false
---

# Способы объявления переменных в JavaScript
{: .no_toc}

В JavaScript есть три способа объявления переменных `var`, `let`, `const`.
{: .fs-6 .fw-300}

Чтобы понять разницу между `var`, `let`, `const` необходимо разобраться в следующих понятиях:

* Объявление переменной;
* Инициализация переменной;
* Область видимости;
* Механизм _hoisting_ ("поднятие").

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

[Ссылка на источник](https://nuancesprog.ru/p/4522/) с сайта [nuancesprog.ru](https://nuancesprog.ru)   
Перевод статьи [Gemhar Rafi](http://js.mamydirect.com/redir/clickGate.php?u=RGm1L5B5&m=1&p=jxNX2t3h73&t=8ewnX65T&st=&s=&url=https%3A%2F%2Fmedium.com%2F%40gemhar&r=https%3A%2F%2Fnuancesprog.ru%2Fp%2F4522%2F) - [var, let and const in JavaScript Decoded...](http://js.mamydirect.com/redir/clickGate.php?u=RGm1L5B5&m=1&p=jxNX2t3h73&t=8ewnX65T&st=&s=&url=https%3A%2F%2Fmedium.com%2F%40gemhar%2Fdecoding-the-differences-of-var-let-and-const-in-javascript-es6-fac78ee84827&r=https%3A%2F%2Fnuancesprog.ru%2Fp%2F4522%2F)

## Объявление переменной

Объявление переменной - это процесс введения нового определения в программу, если быть точнее, в область видимости. 
В JavaScript переменные изначально приобретают значение _undefined_, когда мы объявляем ключевое слово `var` (это автоматически выполняется интерпретатором).

```javascript
var foo; // объявление переменной
console.log(foo); // logs->undefined
```

## Инициализация переменной

Инициализация переменной - это процесс присваивания значения переменной. При объявлений переменной ключевым словом `var`, интерпретатор присваивает значение _undefined_.

```javascript
var foo; // объявление переменной
console.log(foo); // logs->undefined
foo = "something"; // Initialization
console.log(foo); // logs->something
```

## Область видимости

Область видимости переменной определяет контекст, в котором доступны переменные и функции, на которые можно ссылаться в программе. 
Область видимости определяет видимость и время жизни переменных и параметров. Если переменной нет в определённой области видимости, то она недоступна для использования. 
Области видимости также могут распологаться в иерархическом порядке, чтобы дочерние имели доступ к родительским, а не наоборот.

Существует 2 типа области видимости:

* Функциональная область видимости;
* Блочная область видимости.

### Функциональная область видимости

Переменные, объявленные внутри функции, входят в область видимости этой функции, а также в область видимости вложенных в неё функции, независимо от блоков.

```javascript
function foo() {
  if(true) {
    var v = "var inside the if block";
    console.log(v); // logs->var inside the if block
  }
  
  v = "var outside the if block";
  console.log(v); // logs->var outside the if block
}

foo();
```

### Блочная область видимости

Переменные, объявленные внутри блока, входят в область видимости только этого блока, а также вложенных в него блоков, но не за пределами блока, даже если это всё одна функция. 
В блоки входят `if...else` и циклы.

```javascript
function bar() {
  if(true) {
    let l = "let inside the if block";
    console.log(l); // logs->let inside the if block
  }
  console.log(l); // Uncaught Reference Error: l is not defined
}

bar();
```

## Поднятие

> Поднятие - это термин, использование которого вы не найдёте ни в одной нормативной документации JavaScript до спецификации языка ES2015. 
Предполагалось, что поднятие - это обобщённый способ видения того, как работает контекст исполнения в JavaScript. Однако это понятие по началу может сбивать с толку.

> Концептуально, например, строгое определение поднятия предполагает, что объявление переменной и функции физически располагается в начале кода, но это не так. Объявление переменной и функции помещаются в память на стадии компиляции, но остаются там, где вы их набрали в своём коде.

```javascript
console.log(foo); // logs->undefined
// это не приводит к ошибке, однако значение undefined;
// это происходит из-за поднятия
var foo = "something"; // Инициализация переменной
console.log(foo); // logs->something
```

Как можно упростить оценку интерпретатора JS для кода выше:

```javascript
var foo; // Поднятое объявление 'foo'
console.log(foo); // выводит значение undefined
foo = "something"; // Инициализация переменной
console.log(foo); // выводит значение something
```

## var

Идентификатор **var** объявляет переменную, опционально присваивая ей значение. Любая переменная, объявленная идентификатором **var**, имеет функциональную область видимости. Такие переменные _поднятые_ (_hoisting_), а их первоначальное значение - _undefined_.

```javascript
console.log(foo); // logs->undefined
var foo;
// код выше не приводит к ошибке из-за поднятия;
```

## let

Идентификатор **let** объявляет локальную переменную. Любая переменная, объявленная с помощью **let**, имеет блочную область видимости. Значения подняты и не инициализированы.

```javascript
let foo;
console.log(foo); // Uncaught Reference Error: l is not defined
// код выше приводит к ошибке, потому что значение переменной не инициализировано;
```

Связи **let** создаются сверху области видимости конкретного блока, содержащего определение, часто называемые поднятием. 
В отличие от переменных, объявленных с помощью **var**, которым присваивается значение _undefined_, переменные **let** не инициализируются, пока им не присвоится значение. 
Обращение к переменной до инициализации вызовет **Reference Error**.

## const

Идентификатор **const** объявляет переменную, почти как **let**, но у него появляется ещё одно свойство. 
Он не может быть переопределён, то есть после инициализации связей **const** нельзя присвоить никакое другое значение.

Следовательно, **const** должен быть всегда инициализирован при объявлении, иначе возникнет ошибка.

```javascript
const foo = "something";
foo = "other thing"; // Uncaught TypeError: Assignment to constant variable.
const bar; // Uncaught SyntaxError: Missing initializer in const declaration
```

Стоит отметить, что когда **const** связан с объектом, саму ссылку на объект нельзя изменить, и **const** будет указывать на тот же самый объект. 
Однако изменения внутри объекта допустимы.

```javascript
const score = {visitors: 0, home: 0};
score.visitors = 1; // Можно
score = {visitors: 1, home: 1}; // Uncaught TypeError: Assignment to constant variable.
// Нельзя
```

## Один последний факт

Переменные, объявленные внутри функции без ключевого слова, станут глобальными переменными. Взглянем на это в следующем примере:

```javascript
function funFact() {
	isGloballyAvailable = true;
}

funFact();
console.log(isGloballyAvailable); // выводит true
```

Чтобы понять что происходит, нам нужно вернуться назад к понятию _поднятия_ (_hoisting_).
Обычно при инициализации переменной в нашем коде интерпретатор ищет "поднятые переменные" и затем присваивает или переназначает значение переменной. 
Однако, когда интерпретатор не может найти переменную внутри функции, он ищет её среди переменных родительской функции, пока не дойдёт до глобальной области видимости.

В нашем случае интерпретатор не найдёт `isGloballyAvailable` даже в глобальной области видимости, поэтому он автоматически туда её добавит.

Это невероятно опасный процесс, которого лучше не допускать. Поэтому имейте в виду, что объявлять переменные без ключевых слов `var`, `let` и `const` нельзя.

## Так, когда использовать var, let или const?

ES2015(ES6) представил **let** и **const**. Зачем JavaScript разработчикам их вводить? 
Может, чтобы исправить проблемы, возникающие с **var**, или для улучшения читабельности кода? 

Одна главная проблема с **var** связана с тем, что он позволяет переназначать переменные в коде, из-за чего не выбрасываются ошибки. 
Это приводит к различным побочным эффектам в коде.

## Распространённое мнение

Всегда отдавайте предпочтение **const**, если значение, присвоенное переменной, не изменится. 
Это подскажет будущим разработчикам, что у переменной неизменное значение.

А **let** используйте, если значение в будущем изменится.

Где бы был полезен **var**?