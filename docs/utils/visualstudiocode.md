---
title: Overview Text Editors
summary: 
authors:
    - Paul van Genuchten
date: 2023-01-05
---

# Overview Text Editors

When working with a variety of text files (HTML, CSV, YAML, XML, GeoJSON, JS, Python, Markdown), you need a replacement for the basic Notepad. A magnitude of options exists, such as [Vim](https://www.vim.org/), [Notepad++](https://notepad-plus-plus.org), [PyCharm](https://www.jetbrains.com/pycharm/), [Eclipse](https://projects.eclipse.org/projects/eclipse.platform), [Sublime](https://www.sublimetext.com/). The last years my personal favourite has become [Visual Studio Code](https://code.visualstudio.com/). But let's try to stay neutral and list what features we expect from a daily used text editor:

- `Find in files` (and replace) is an important feature when looking for a certain pattern in a folder of files. 
- [Syntax highlighting](https://en.wikipedia.org/wiki/Syntax_highlighting) for xml, json, python and yml facilitate readability of the file
- Code formatting/validation. In Python and YAML indenting is essential, that's when code formatting is extra important.
- A tree view of the project structure, so you can easily open files from the project 
- Code completion/suggestions when you start typing

Optional features:

- Preview HTML & Markdown
- XML schema validation
- Git operations
- Content comparison, compare 2 (or more) files.

Many of the text editor communities have a range of plugins available to extend the functionality of the editor. Various text editors have for example a [MapServer](../cookbook/mapserver.md) Mapfile or [SLD](../cookbook/geoserver.md) plugin.
