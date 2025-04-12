---
## Front matter
title: "Лабораторная работа №2"
subtitle: "Исследование протокола TCP и алгоритма управления очередью RED"
author: "Эспиноса Василита Кристина Микаела"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Исследовать протокол TCP и алгоритм управления очередью RED.

# Задание

- Выполнить пример с дисциплиной RED;
- Изменить в модели на узле s1 тип протокола TCP с Reno на NewReno, затем на Vegas. Сравнить и пояснить результаты;
- Внести изменения при отображении окон с графиками (изменить цвет фона, цвет траекторий, подписи к осям, подпись траектории в легенде).

# Выполнение лабораторной работы

Описание моделируемой сети:

– сеть состоит из 6 узлов;
– между всеми узлами установлено дуплексное соединение с различными пропуск-
ной способностью и задержкой 10 мс (см. рис. 2.4);
– узел r1 использует очередь с дисциплиной RED для накопления пакетов, макси-
мальный размер которой составляет 25;
– TCP-источники на узлах s1 и s2 подключаются к TCP-приёмнику на узле s3;
– генераторы трафика FTP прикреплены к TCP-агентам.

Разработаем сценирий, реализующий модель согласно описанию в Xgraph график изменения TCP-окна, график изменения длины очереди и средней длины очереди.

![](image/code1.PNG){#fig:001 width=70%}

![](image/code2.PNG){#fig:002 width=70%}


После запуска кода получаем график изменения TCP-окна (рис. [-@fig:003]), а также график изменения длины очереди и средней длины очереди (рис. [-@fig:004]).

Здесь видно, что средняя длина очереди находится в диапазоне от 2 до 4. Максимальная длина достигает значения 14.

![](image/1.PNG){#fig:003 width=70%}

![](image/2.PNG){#fig:004 width=70%}


# Изменение протокола TCP 

Сначала именила тип Reno на NewReno. В результате получим следующие график изменения TCP-окна (рис. [-@fig:005]), а также график изменения длины очереди и средней длины очереди (рис. [-@fig:006]). 
Так же, как было в графике с типом Reno значение средней длины очереди находится в пределах от 2 до 4, а максимальное значение длины равно 14. 

![](image/3.PNG){#fig:005 width=70%}

![](image/4.PNG){#fig:006 width=70%}

Далее изменим тип Reno на Vegas В результате получим следующие график изменения TCP-окна (рис. [-@fig:007]), а также график изменения длины очереди и средней длины очереди (рис. [-@fig:008]).

Средняя длина очереди при TCP Vegas остаётся в пределах 2–4, максимальная — 14. Размер окна у Vegas не превышает 20 (у NewReno — 34). TCP Vegas раньше обнаруживает перегрузку и уменьшает окно без потерь пакетов.

![](image/5.PNG){#fig:007 width=70%}

![](image/6.PNG){#fig:008 width=70%}

# Изменение отображения окон с графиками

Внесём корректировки в отображение графиков: поменяем цвет фона, цвет линий, подписи осей и название траектории в легенде. 
Для этого обновим код: в процедуре finish изменим цвет линий и подписей, а также с помощью опций -fg и -bg зададим новый цвет текста и фона в xgraph.

![](image/code3.PNG){#fig:009 width=70%}

В результате получим следующие график изменения TCP-окна (рис. [-@fig:011]), а также график изменения длины очереди и средней длины очереди (рис. [-@fig:010]).

![](image/8.PNG){#fig:010 width=70%}

![](image/7.PNG){#fig:011 width=70%}

# Выводы

В процессе выполнения данной лабораторной работы я исследовала протокол TCP и алгоритм управления очередью RED.

# Список литературы{.unnumbered}

::: {#refs}
:::
