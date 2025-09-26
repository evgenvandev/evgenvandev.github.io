---
layout: default
title: Скрипты подсчёта
parent: Example of Python Script
grand_parent: Notepad++
nav_order: 3
has_toc: false
---

# Скрипты подсчёта
{: .no_toc}

## Оглавление
{: .no_toc .text-delta}

1. TOC
{:toc}

---

## Подсчёт символов, слов, строк

[Оригинал статьи](https://www.sivachandran.in/2012/04/scripting-notepad-with-python.html)

```python
# -*- coding: utf-8 -*-
# Скрипт для подсчёта количества символов, слов и строк в текущем окне редактора Notepad++

from Npp import *
import re

numChars = 0
numWords = 0
numLines = 0

# Получаем текстовое содержимое активного окна редактора
editorContent = editor.getText()
for line in editorContent.splitlines():
    numLines += 1
    for word in re.findall("[a-zA-Z0-9]+", line):
        numWords += 1
        numChars += len(word)

# Выводим окно сообщений Notepad++ с информацией о количестве символов, слов и строк
notepad.messageBox("Number of characters: %d \nNumber of words: %d \nNumber of lines: %d" % (numChars, numWords, numLines))
```

Запускаем скрипт `count_characters_word_lines.py` на файле этого же скрипта:   
![Запуск скрипта count_characters_word_lines.py]({{ site.url }}{{ site.baseurl }}/assets/images/notepad-plus-plus/notepad-plus-plus-python-script/python-script_count_characters_word_lines_start.jpg "Запуск скрипта count_characters_word_lines.py")

Получаем окно сообщение:   
![Окно сообщения count_characters_word_lines.py]({{ site.url }}{{ site.baseurl }}/assets/images/notepad-plus-plus/notepad-plus-plus-python-script/python-script_count_characters_word_lines_info_window.jpg "Окно сообщения count_characters_word_lines.py")