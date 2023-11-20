---
layout: default
title: Node.js
nav_order: 44
has_children: true
has_toc: false
permalink: /docs/node-js
---

# Node.js
{: .no_toc}

Node.js представляет среду выполнения кода на JavaScript, которая построена на основе движка JavaScript Chrome V8, который позволяет 
транслировать вызовы на языке JavaScript в машинный код. Node.js прежде всего предназначен для создания серверных приложений на языке JavaScript. 
Хотя также существуют проекты по написанию десктопных приложений (Electron) и даже по созданию кода для микроконтроллеров.   
Node.js является открытым проектом, исходники которого можно посмотреть на [github.com](https://github.com/nodejs).
{: .fs-6 .fw-300}

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Установка

Для загрузки перейдём на официальный сайт [https://nodejs.org/en](https://nodejs.org/en/). На главной странице мы сразу увидим две 
возможные опции для загрузки: самая последняя версия Node.js и LTS-версия. 

![Страница загрузки Node.js]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/install_node_js_site_download.jpg "Страница загрузки Node.js")

Для Windows установщик представляет файл с расширением `msi`. 

Последние версии Node.js работают только на Windows 10.
{: .text-red-200 }

Для Windows 7 необходимо скачать предыдущие версии. Для этого перейдём на страницу [https://nodejs.org/en/download](https://nodejs.org/en/download), нажав вверху предыдущей страницы ссылку `DOWNLOAD`.   
Прокручиваем вниз страницы до текста `Previous releases`, нажимаем, переходим дальше:

![Предыдущие версии Node.js]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/install_node_js_site_download_previous_releases.jpg "Предыдущие версии Node.js")

Прокручиваем вниз до таблицы `Looking for latest release of a version branch? (Ищете последние выпуски версии ветки?)`. 
Нажимаем на `Releases`. 

![Версия Node.js v10.24.1]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/install_node_js_site_download_previous_releases_v10.24.1.jpg "Версия Node.js v10.24.1")

Мы оказались на странице загрузки для версии Node.js `v10.24.1`, а нам нужна версия Node.js `v10.16.3`, а именно файл `node-v10.16.3-x64.msi`. 
Для этого перейдём в папку выше, нажав на двоеточие: 

![Вверх версии Node.js v10.24.1]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/install_node_js_site_download_previous_releases_v10.24.1-1.jpg "Вверх версии Node.js v10.24.1")

На странице всех версии прокручиваем до версии Node.js `v10.16.3`, переходим по ссылке.

![Переход к версии Node.js v10.16.3]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/install_node_js_site_download_previous_releases_v10.16.3.jpg "Переход к версии Node.js v10.16.3")

Мы оказываемся на странице загрузки для Node.js версии `v10.16.3`. Здесь находим файл `node-v10.16.3-x64.msi` и скачиваем его. 
Файл с расширением `msi` является архивом и его можно разархивировать любой программой архиватором. 

![Файл node-v10.16.3-x64.msi]({{ site.url }}{{ site.baseurl }}/assets/images/node-js/install_node_js_site_download_previous_releases_v10.16.3-1.jpg "Файл node-v10.16.3-x64.msi")

