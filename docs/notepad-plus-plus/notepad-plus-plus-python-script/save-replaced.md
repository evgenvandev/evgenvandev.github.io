---
layout: default
title: Скрипты сохранения
parent: Example of Python Script
grand_parent: Notepad++
nav_order: 2
has_toc: false
---

# Скрипты сохранения
{: .no_toc}

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Поиск и замена текста с сохранением файла

Файл _save_replaced.py_
```python
# -*- coding: utf-8 -*-
# Simple search and replace
# Простой поиск и замена "old_text" на "new_text"
editor.replace("old_text", "new_text")

# Get the current filename and save a modified version
# Получаем текущее имя файла и сохраняем файл с новым именем
current_filename = notepad.getCurrentFilename()
new_filename = current_filename + ".modified"
notepad.saveAs(new_filename)

# Write a message to the console
# Пишем сообщение в консоль
console.write("File saved as: %s\n" % new_filename)
```

Первая строка файла   
`# -*- coding: utf-8 -*-`   
сообщает интерпретатору Python, что текст файла программы написан в кодировке `utf-8`.

![Программа save_replaced.py]({{ site.url }}{{ site.baseurl }}/assets/images/notepad-plus-plus/notepad-plus-plus-python-script/python-script_save_replaced_text.jpg "Текст программы save_replaced.py")

Запускаем скрипт через меню `Плагины > Python Script > Scripts > save_replaced`
![Запуск save_replaced.py]({{ site.url }}{{ site.baseurl }}/assets/images/notepad-plus-plus/notepad-plus-plus-python-script/python-script_save_replaced_start.jpg "Запуск программы save_replaced.py")

Применяя скрипт к файлу `save_replaced.py` получаем файл `save_replaced.py.modified`, следующего содержания: 
![Файл save_replaced.py.modified]({{ site.url }}{{ site.baseurl }}/assets/images/notepad-plus-plus/notepad-plus-plus-python-script/python-script_save_replaced_executed.jpg "Файл save_replaced.py.modified")

Видим, что все вхождения `old_text` в комментарии и параметрах метода `editor.replace()` заменены на `new_text`.
