---
layout: default
title: Конфигурация
nav_order: 2
---

# Конфигурация
{: .no_toc }

В "Только Документация" есть некоторые определённые параметры конфигурации, которые могут быть определены для вашего сайта на Jekyll в файле _config.yml.
{: .fs-6 .fw-300 }

## Оглавление
{: .no_toc .text-delta }

1. TOC
{:toc}

---

В качестве примера, посмотрите файл [_config.yml](https://github.com/evgenvandev/just-the-docs/tree/master/_config.yml) этого сайта.

## Логотип сайта

```yaml
# Set a path/url to a logo that will be displayed instead of the title
# Задайте путь/url к логотипу, который будет отображаться вместо заголовка
logo: "/assets/images/just-the-docs.png"
```

## Поиск

```yaml
# Enable or disable the site search
# Включение или отключение поиска по сайту
# Supports true (default) or false
# Поддерживает true (по умолчанию) или false
search_enabled: true

search:
  # Split pages into sections that can be searched individually
  # Разделите страницы на разделы, которые можно искать по отдельности
  # Supports 1 - 6, default: 2
  # Поддерживает 1 - 6, по умолчанию: 2
  heading_level: 2
  # Maximum amount of previews per search result
  # Максимальное количество превью на результат поиска
  # Default: 3
  # По умолчанию: 3
  previews: 3
  # Maximum amount of words to display before a matched word in the preview
  # Максимальное количество слов, отображаемых перед совпадающим словом в предварительном просмотре
  # Default: 5
  # По умолчанию: 5
  preview_words_before: 5
  # Maximum amount of words to display after a matched word in the preview
  # Максимальное количество слов, отображаемых после совпадающего слова в предварительном просмотре
  # Default: 10
  # По умолчанию: 10
  preview_words_after: 10
  # Set the search token separator
  # Установите разделитель токенов поиска
  # Default: /[\s\-/]+/
  # По умолчанию: /[\s\-/]+/
  # Example: enable support for hyphenated search words
  # Пример: включить поддержку поисковых слов с дефисом
  tokenizer_separator: /[\s/]+/
  # Display the relative url in search results
  # Отображать относительный URL в результатах поиска
  # Supports true (default) or false
  # Поддерживает true (по умолчанию) или false
  rel_url: true
  # Enable or disable the search button that appears in the bottom right corner of every page
  # Включение или отключение кнопки поиска, которая появляется в правом нижнем углу каждой страницы
  # Supports true or false (default)
  # Поддерживается true или false (по умолчанию)
  button: false
```

## Дополнительные ссылки

```yaml
# Aux links for the upper right navigation
# Дополнительные ссылки для верхней правой навигации
aux_links:
  "Только документация на GitHub":
    - "//github.com/evgenvandev/just-the-docs"

# Makes Aux links open in a new tab. Default is false
# Открывает дополнительные ссылки в новой вкладке. По умолчанию false
aux_links_new_tab: false
```

## Заголовочные якорные ссылки

```yaml
# Heading anchor links appear on hover over h1-h6 tags in page content
# allowing users to deep link to a particular heading on a page.
# Якорные ссылки заголовков появляются при наведении курсора на теги h1-h6 в содержимом страницы, 
# что позволяет пользователям создавать глубокие ссылки на определенный заголовок на странице.
#
# Supports true (default) or false
# Поддерживается true (по умолчанию) или false
heading_anchors: true
```

## Содержание нижнего колонтитула

```yaml
# Footer content
# Содержание нижнего колонтитула
# appears at the bottom of every page's main content
# отображается внизу основного содержимого каждой страницы.
# Note: The footer_content option is deprecated and will be removed in a future major release. 
# Please use `_includes/footer_custom.html` for more robust
# Примечание: Параметр footer_content устарел и будет удален в будущем основном выпуске.
# Для большей надежности используйте _includes / footer_custom.html.
markup / liquid-based content.
footer_content: "Copyright &copy; 2017-2020 Evgeniy. Distributed by an <a href=\"https://github.com/evgenvandev/just-the-docs/tree/master/LICENSE.txt\">MIT license.</a>"

# Footer last edited timestamp
# Отметка времени последнего редактирования нижнего колонтитула
# show or hide edit time - page must have `last_modified_date` defined in the frontmatter
# показать или скрыть время редактирования - страница должна иметь `last_modified_date`, определенную в frontmatter
last_edit_timestamp: true
# uses ruby's time format: https://ruby-doc.org/stdlib-2.7.0/libdoc/time/rdoc/Time.html
# использует формат времени Ruby: https://ruby-doc.org/stdlib-2.7.0/libdoc/time/rdoc/Time.html
last_edit_time_format: "%b %e %Y at %I:%M %p"

# Footer "Edit this page on GitHub" link text
# Нижний колонтитул "Редактировать эту страницу на GitHub" текст ссылки
# show or hide edit this page link
# показать или скрыть ссылку редактирования этой страницы
gh_edit_link: true
gh_edit_link_text: "Редактировать эту страницу на GitHub."
# the github URL for your repo
# URL github для вашего репозитория
gh_edit_repository: "https://github.com/evgenvandev/just-the-docs"
# the branch that your docs is served from
# ветка, из которой обслуживаются ваши документы
gh_edit_branch: "master"
# the source that your files originate from
# ресурс, где находятся ваши файлы
# gh_edit_source: docs
# "tree" or "edit" if you want the user to jump into the editor immediately
# "tree" или "edit", если вы хотите, чтобы пользователь сразу же перешел в редактор.
gh_edit_view_mode: "tree"
```

_note: `footer_content` is deprecated, but still supported. For a better experience we have moved this into an include called `_includes/footer_custom.html` which will allow for robust markup / liquid-based content._

_Примечание: `footer_content` устарел, но всё ещё поддерживается. Для лучшего опыта мы переместили это во включение под названием `_includes/footer_custom.html`, которое обеспечит надежную разметку / жидкий контент._

- the "page last modified" data will only display if a page has a key called `last_modified_date`, formatted in some readable date format

данные "page last modified" будут отображаться только в том случае, если страница имеет ключ с именем `last_modified_date`, отформатированный в некотором читаемом формате даты.
- `last_edit_time_format` uses Ruby's DateTime formatter; see examples and more information [at this link.](https://apidock.com/ruby/DateTime/strftime)

`last_edit_time_format` использует Ruby's DateTime formatter; смотрите примеры и дополнительную информацию [at this link.](https://apidock.com/ruby/DateTime/strftime)
- `gh_edit_repository` is the URL of the project's GitHub repository

`gh_edit_repository` это URL репозитория GitHub проекта
- `gh_edit_branch` is the branch that the docs site is served from; defaults to `master`

`gh_edit_branch` это ветка, из которой обслуживается сайт документации; по умолчанию `master`
- `gh_edit_source` is the source directory that your project files are stored in (should be the same as [site.source](https://jekyllrb.com/docs/configuration/options/))

`gh_edit_source` это исходный каталог, в котором хранятся файлы вашего проекта (должно быть таким же, как [site.source](https://jekyllrb.com/docs/configuration/options/))
- `gh_edit_view_mode` is `"tree"` by default, which brings the user to the github page; switch to `"edit"` to bring the user directly into editing mode

`gh_edit_view_mode` по умолчанию - "tree", которое переносит пользователя на страницу github;
переключитесь на "edit", чтобы перевести пользователя прямо в режим редактирования

## Цветовая схема

```yaml
# Color scheme supports "light" (default) and "dark"
# Поддерживаются цветовые схемы "light" (по умолчанию) и "dark"
color_scheme: dark
```
<button class="btn js-toggle-dark-mode">Предварительный просмотр тёмной цветовой схемы</button>

<script>
const toggleDarkMode = document.querySelector('.js-toggle-dark-mode');

jtd.addEvent(toggleDarkMode, 'click', function(){
  if (jtd.getTheme() === 'dark') {
    jtd.setTheme('light');
    toggleDarkMode.textContent = 'Preview dark color scheme';
  } else {
    jtd.setTheme('dark');
    toggleDarkMode.textContent = 'Return to the light side';
  }
});
</script>

Смотрите [Настройка]({{ site.baseurl }}{% link docs/customization.md %}) для получения дополнительной информации.

## Google Analytics

```yaml
# Google Analytics Tracking (optional)
# e.g, UA-1234567-89
ga_tracking: UA-5555555-55
# Use GDPR compliant Google Analytics settings (true by default)
# Использовать настройки Google Analytics, соответствующие GDPR (по умолчанию true)
ga_tracking_anonymize_ip: true
```

## Коллекции документов

По умолчанию навигация и поиск включают обычные [страницы](https://jekyllrb.com/docs/pages/).
Вместо этого вы также можете использовать Jekyll коллекции, [Jekyll коллекции](https://jekyllrb.com/docs/collections/) которые семантически группируют документы вместе.

Например, поместите все ваши файлы документации в папку `_docs` и создайте коллекцию `docs`:
```yaml
# Определение Jekyll коллекции
collections:
  # Определите коллекцию с именем "docs", ее документы находятся в каталоге "_docs"
  docs:
    permalink: "/:collection/:path/"
    output: true

just_the_docs:
  # Определение, какие коллекции используются в "Только документация"
  collections:
    # Ссылка на коллекцию "docs"
    docs:
      # Дайте коллекции имя
      name: Documentation
      # Исключить коллекцию из навигации
      # Поддерживается true или false (по умолчанию)
      nav_exclude: false
      # Исключить коллекцию из поиска
      # Поддерживается true или false (по умолчанию)
      search_exclude: false
```

Вы можете ссылаться на несколько коллекций.
Это создает категории в навигации с настроенными именами.
```yaml
collections:
  docs:
    permalink: "/:collection/:path/"
    output: true
  tutorials:
    permalink: "/:collection/:path/"
    output: true

just_the_docs:
  collections:
    docs:
      name: Documentation
    tutorials:
      name: Tutorials
```

