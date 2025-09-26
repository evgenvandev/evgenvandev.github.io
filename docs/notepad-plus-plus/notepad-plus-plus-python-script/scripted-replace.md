---
layout: default
title: Скрипты замены
parent: Example of Python Script
grand_parent: Notepad++
nav_order: 1
has_toc: false
---

# Скрипты замены
{: .no_toc}

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Замена номера версии и автоматическая нумерация списков

[Оригинал на скриншотах](https://sourceforge.net/projects/npppythonscript/)   
Скрипт для замены номера версии в change.log и автоматической нумерации списков.

Файл _scripted_replace.py_
```python
# -*- coding: utf-8 -*-
# Script to replace the version number in the change.log
# and auto-number the lists
# Скрипт для замены номера версии в change.log
# и автоматической нумерации списков

# Заменяем номер версии Notepad++
editor.rereplace(r'Notepad\+\+ v(([0-9]+\.){2}([0-9]+)?)', 'Notepad++ v6.5.5')

counter = 0
# Функция увеличивает или сбрасывает счётчик
def increment_counter(m):
    global counter
    if m.group(0) == '##':  # reset counter when we see ##
        # Сбрасываем счётчик, когда видим ##
        counter = 1
    else:
        counter = counter + 1
    
    return counter

# Заменяем символ решётка на нумерацию
editor.rereplace('^##?', increment_counter)
```

Первая строка файла   
`# -*- coding: utf-8 -*-`   
сообщает интерпретатору Python, что текст файла программы написан в кодировке `utf-8`.

Подготовим следующий файл `change.log` для теста скрипта:   
Файл _change.log_
```
Notepad++ v6.4.1 fixed bugs and added features:

##. Fix find "\r\n" bug in RegExpr mode.
#. Change "Delete file" command to "Move to Recycle Bin"
#. Add Remove empty lines feature.
#. Change document default value from ANSI to UTF8 w/o
#. Enable Word-completion under CJK environment for

Included plugins:

##. Spell Checker v1.3.3
#. NppFTP 0.24.1
#. NppExport v0.2.8
#. Plugin Manager 1.0.8
#. Converter 3.1
```

Тестовый файл `change.log` до изменения:
![Тестовый файл change.log до изменения]({{ site.url }}{{ site.baseurl }}/assets/images/notepad-plus-plus/notepad-plus-plus-python-script/python-script_scripted_replace_change_log.jpg "Тестовый файл change.log до изменения")

Запуск скрипта `scripted_replace.py` на файле `change.log`:
![Тестовый файл change.log запуск scripted_replace.py]({{ site.url }}{{ site.baseurl }}/assets/images/notepad-plus-plus/notepad-plus-plus-python-script/python-script_scripted_replace_change_log_start.jpg "Тестовый файл change.log запуск scripted_replace.py")

Файл `change.log` после выполнения скрипта `scripted_replace.py`:
![Тестовый файл change.log после выполнения скрипта scripted_replace.py]({{ site.url }}{{ site.baseurl }}/assets/images/notepad-plus-plus/notepad-plus-plus-python-script/python-script_scripted_replace_change_log_executed.jpg "Тестовый файл change.log после выполнения скрипта scripted_replace.py")
Видим, что изменилась версия Notepad++ и появилась автоматическая нумерация списков, взамен символов решётка.