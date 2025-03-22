---
## Front matter
title: "Лабораторная работа №7"
subtitle: "Модель M|M|1|∞ »"
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

Рассмотреть пример моделирования в xcos системы массового обслуживания типа Модель M|M|1|∞ 

# Задание

- Реализовать модель системы массового обслуживания типа  M|M|1|∞ ;
- Построить график поступления и обработки заявок;
- Построить график динамики размера очереди.


# Выполнение лабораторной работы

Зафиксируем начальные данные: λ = 0.3, μ = 0.35, z0=.  В меню Моделирование, Установить контекст зададим значения коэффициентов

![](image/1.PNG){#fig:001 width=70%}


# Реализация модели 

Суперблок, моделирующий поступление заявок, представлен на рис. [-@fig:002]. Тут у нас заявки поступают в систему по пуассоновскому закону. Поступает заявка в суперблок, идет в синхронизатор входных и выходных сигналов, происходит равномерное распределение на интервале 
[0;1] (также заявка идет в обработчик событий), далее идет преобразование в экспоненциальное распределение с параметром λ, далее заявка опять попадает в обработчик событий и выходит из суперблока.

![](image/2.PNG){#fig:002 width=70%}

Суперблок, моделирующий процесс обработки заявок, представлен на рис. [-@fig:003]. Тут происходит обработка заявок в очереди по экспоненциальному закону.

![](image/3.PNG){#fig:003 width=70%}

Готовая модель представлена на рис. [-@fig:004]. 
Тут есть селектор, два суперблока, построенных ранее, первоначальное событие на вход в суперблок, суммирование, оператор задержки (имитация очереди), также есть регистрирующие блоки: регистратор размера очереди и регистратор событий.

![](image/4.PNG){#fig:004 width=70%}

# Результат моделирования


![](image/5.PNG){#fig:005 width=70%}

![](image/6.PNG){#fig:006 width=70%}


# Выводы

В процессе выполнения данной лабораторной работы я рассмотрела пример моделирования в xcos системы массового обслуживания типа M|M|1|∞

# Список литературы{.unnumbered}

::: {#refs}
:::
