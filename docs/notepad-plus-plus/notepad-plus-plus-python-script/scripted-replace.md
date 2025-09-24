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

Скрипт для замены номера версии в change.log и автоматической нумерации списков.

Файл _scripted_replace.py_
```python
# -*- coding: utf-8 -*-
# Script to replace the version number in the change.log
# and auto-number the lists
# Скрипт для замены номера версии в change.log
# и автоматической нумерации списков

editor.rereplace(r'Notepad\+\+ v(([0-9]+\.){2}([0-9]+)?)', 'Notepad++ v6.5.5')

counter = 0
def increment_counter(m):
    global counter
    if m.group(0) == '##':  # reset counter when we see ##
        counter = 1
    else:
        counter = counter + 1
    
    return counter

editor.rereplace('^##?', increment_counter)
```

