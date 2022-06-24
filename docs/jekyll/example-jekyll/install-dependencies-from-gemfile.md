---
layout: default
title: Установка зависимостей из Gemfile
parent: Example of Jekyll
grand_parent: Jekyll
nav_order: 4
has_toc: false
---

# Установка зависимостей из файла _Gemfile_
{: .no_toc }

## Оглавление
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Первый вариант

1. Вводим
```shell
bundle update
```
для использования версии программ, указанных в _Gemfile_, т.е. устанавливаем зависимости указанные в файле.
1. После запуска сайта командой: 
```shell
bundle exec jekyll serve
```
, выдаёт ошибку _jekyll 3.8.4 | Error: tzinfo_, т.е. необходимо установить программу _tzinfo_. Устанавливаем программу _tzinfo_ старых версии командой
```shell
gem install tzinfo --version 1.2.3
```
 и прописываем в _Gemfile_ следующую строку _gem ‘tzinfo’, ‘1.2.3’_
1. После запуска сайта командой
```shell
bundle exec jekyll serve
```
, выдаёт ошибку _jekyll 3.8.4 | Error: No source of timezone data could be found._, т.е. необходимо установить программу _tzinfo-data_. Устанавливаем программу _tzinfo-data_ старых версии
```shell
gem install tzinfo-data --version 1.2017.2
```
и прописываем в _Gemfile_ следующую строку _gem ‘tzinfo-data’, ‘1.2017.2’_

Получаем файл _Gemfile_, без расширения, в корне сайта:
```ruby
source 'https://rubygems.org'

gem 'jekyll', '3.8.4'
gem 'tzinfo', '1.2.3'
gem 'tzinfo-data', '1.2017.2'

group :jekyll_plugins do
  gem 'jekyll-feed', '0.11.0'
  gem 'jekyll-seo-tag', '2.5.0'
  gem 'jekyll-sitemap', '1.2.0'
end
```
