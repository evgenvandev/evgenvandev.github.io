---
layout: default
title: Search
nav_order: 7
---

# Search
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Just the Docs uses [lunr.js](http://lunrjs.com) to add a client-side search interface powered by a JSON index that Jekyll generates.
All search results are shown in an auto-complete style interface (there is no search results page).
By default, all generated HTML pages are indexed using the following data points:

- Page title
- Page content
- Page URL

## Enable search in configuration

In your site's `_config.yml`, enable search:

```yaml
# Enable or disable the site search
# Supports true (default) or false
search_enabled: true
```

### Search granularity

Pages are split into sections that can be searched individually.
The sections are defined by the headings on the page.
Each section is displayed in a separate search result.

```yaml
# Split pages into sections that can be searched individually
# Supports 1 - 6, default: 2
search.heading_level: 2
```

### Search previews

A search result can contain previews that show where the search words are found in the specific section.

```yaml
# Maximum amount of previews per search result
# Default: 3
search.previews: 3

# Maximum amount of words to display before a matched word in the preview
# Default: 5
search.preview_words_before: 5

# Maximum amount of words to display after a matched word in the preview
# Default: 10
search.preview_words_after: 10
```

### Search tokenizer

The default is for hyphens to separate tokens in search terms:
`gem-based` is equivalent to `gem based`, matching either word.
To allow search for hyphenated words:

```yaml
# Set the search token separator
# Default: /[\s\-/]+/
# Example: enable support for hyphenated search words
search.tokenizer_separator: /[\s/]+/
```

### Display URL in search results 

```yaml
# Display the relative url in search results
# Supports true (default) or false
search.rel_url: false
```

### Display search button

The search button displays in the bottom right corner of the screen and triggers the search input when clicked.

```yaml
# Enable or disable the search button that appears in the bottom right corner of every page
# Supports true or false (default)
search.button: true
```


## Hiding pages from search

Sometimes you might have a page that you don't want to be indexed for the search nor to show up in search results, e.g, a 404 page.
To exclude a page from search, add the `search_exclude: true` parameter to the page's YAML front matter:

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Page not found
nav_exclude: true
search_exclude: true
---
```


## Generate search index when used as a gem

If you use Just the Docs as a remote theme, you do not need the following steps.

If you use the theme as a gem, you must initialize the search by running this `rake` command that comes with `just-the-docs`:

```bash
$ bundle exec just-the-docs rake search:init
```

This command creates the `assets/js/zzzz-search-data.json` file that Jekyll uses to create your search index.
Alternatively, you can create the file manually with [this content]({{ site.github.repository_url }}/blob/master/assets/js/zzzz-search-data.json).


## Настройка поиска на русском языке

Для поиска на сайте используем библиотеку [lunr.js](https://lunrjs.com/). Ссылка на [GitHub source](https://github.com/olivernn/lunr.js).

### Подключение необходимых файлов в заголовке сайта

Библиотека `lunr.js` подключается с помощью трёх файлов:

1. `/assets/js/vendor/lunr.stemmer.support.js` - файл поддержки языков
1. `/assets/js/vendor/lunr.ru.js` - файл поиска только для русского языка
1. `/assets/js/vendor/lunr.multi.js` - файл поиска на нескольких языках одновременно, так как английский язык поиска используется по умолчанию

Эти файлы подключаются в файле `/_includes/head.html` в строках 29-34:

{% highlight html %}
{% raw %}{% if site.search_enabled != false %}{% endraw %}
    <script type="text/javascript" src="{{ '/assets/js/vendor/lunr.min.js' | relative_url }}"></script>
    <script type="text/javascript" src="{{ '/assets/js/vendor/lunr.stemmer.support.js' | relative_url }}"></script>
    <script type="text/javascript" src="{{ '/assets/js/vendor/lunr.ru.js' | relative_url }}"></script>
    <script type="text/javascript" src="{{ '/assets/js/vendor/lunr.multi.js' | relative_url }}"></script>
{% raw %}{% endif %}{% endraw %}
{% endhighlight %}

Соответственно сами файлы `lunr.stemmer.support.js`, `lunr.ru.js`, `lunr.multi.js` необходимо поместить в каталог `/assets/js/vendor/`.  
Эти файлы можно скачать, [например, от сюда](https://github.com/MihaiValentin/lunr-languages).  
[Инструкция поддержки поиска только для русского языка](https://github.com/MihaiValentin/lunr-languages#in-a-web-browser)  
[Инструкция поддержки поиска для нескольких языков](https://github.com/MihaiValentin/lunr-languages#indexing-multi-language-content)

### Инициализация скрипта `lunr.js`

На данном сайте код инициализации скрипта `lunr.js` находится в файле `/assets/js/just-the-docs.js.html`, в строках 80-100:

```javascript
var index = lunr(function(){
    this.ref('id');
    this.field('title', { boost: 200 });
    this.field('content', { boost: 2 });
    {%- if site.search.rel_url != false %}
    this.field('relUrl');
    {%- endif %}
    this.metadataWhitelist = ['position']

    for (var i in docs) {
        this.add({
        id: i,
        title: docs[i].title,
        content: docs[i].content,
        {%- if site.search.rel_url != false %}
        relUrl: docs[i].relUrl
        {%- endif %}
        });
    }
});
```

Переменная `index` это индекс для поиска.  
В начале функции записываем строку:

```javascript
this.use(lunr.multiLanguage('en', 'ru'));
```

Получаем:

```javascript
var index = lunr(function(){
    // the reason "en" does not appear above is that "en" is built in into lunr js
    // причина, по которой "en" не отображается выше, заключается в том, что "en" встроен в lunr js.
    this.use(lunr.multiLanguage('en', 'ru'));
    this.ref('id');
    this.field('title', { boost: 200 });
    this.field('content', { boost: 2 });
    {%- if site.search.rel_url != false %}
    this.field('relUrl');
    {%- endif %}
    this.metadataWhitelist = ['position']

    for (var i in docs) {
        this.add({
        id: i,
        title: docs[i].title,
        content: docs[i].content,
        {%- if site.search.rel_url != false %}
        relUrl: docs[i].relUrl
        {%- endif %}
        });
    }
});
```

### Операторы дополнительного поиска `lunr.js`

К вашей строке можно добавить операторы для уточнения поиска:

- Подстановочные знаки (например, foo*, *oo)
- Нечеткое совпадение, помогает с опечатками (например, foo~1)
- Определенные поля (например, title:foo, text:1911)
- Термин расширения (повышения) (например, foo^10)
