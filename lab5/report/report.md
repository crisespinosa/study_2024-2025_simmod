---
## Front matter
title: "Лабораторная работа №5"
subtitle: "Модель эпидемии (SIR)"
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

Построить модель SIR в xcos и OpenModelica.

# Задание

- Реализовать модель SIR в в xcos;
- Реализовать модель SIR с помощью блока Modelica в в xcos;
- Реализовать модель SIR в OpenModelica;
- Реализовать модель SIR с учётом процесса рождения / гибели особей в xcos (в том числе и с использованием блока Modelica), а также в OpenModelica;
- Построить графики эпидемического порога при различных значениях параметров модели (в частности изменяя параметр μ);
-Сделать анализ полученных графиков в зависимости от выбранных значений параметров модели.





# Выполнение лабораторной работы
Задача о распространении эпидемии описывается системой дифференциальных уравнений:

$$
\begin{aligned}
\dot{s} &= -\beta s(t) i(t) \\
\dot{i} &= \beta s(t) i(t) - \nu i(t) \\
\dot{r} &= \nu i(t)
\end{aligned}
$$

где β -- скорость заражения, ν-- скорость выздоровления.


# Реализация модели в xcos

Зафиксируем начальные данные: β = 1, ν= 0.3, s(0)=0.999, i(0)=0.001, r(0)=0

В меню Моделирование, Установить контекст зададим значения переменных β и ν

![](image/1.PNG){#fig:001 width=70%}

Для реализации модели будем использовать следующие блоки:

- CLOCK_c -- запуск часов модельного времени;
- CSCOPE -- регистрирующее устройство для построения графика;
- TEXT_f -- задаёт текст примечаний;
- MUX -- мультиплексер, позволяющий в данном случае вывести на графике сразу несколько кривых;
- INTEGRAL_m -- блок интегрирования;
- GAINBLK_f -- в данном случае позволяет задать значения коэффициентов β и ν;
- SUMMATION -- блок суммирования;
- PROD_f -- поэлементное произведение двух векторов на входе блока.

![](image/2.PNG){#fig:001 width=70%}

В параметрах верхнего и среднего блока интегрирования необходимо задать начальные значения:

![](image/4.PNG){#fig:001 width=70%}

![](image/5.PNG){#fig:001 width=70%}

В меню Моделирование, Установка зададим конечное время интегрирования, равным времени моделирования, в данном случае 30

![](image/3.PNG){#fig:001 width=70%}

Результат моделирования представлен на рисунке

![](image/6.PNG){#fig:001 width=70%}

# Реализовать модель SIR с помощью блока Modelica в в xcos;

Готовая модель SIR представлена на рис
Для реализации модели (5.1) с помощью языка Modelica помимо блоков CLOCK_c,
CSCOPE, TEXT_f и MUX требуются блоки CONST_m — задаёт константу; MBLOCK
(Modelica generic) — блок реализации кода на языке Modelica. Задаём значения
переменных  β и ν

![](image/9.PNG){#fig:001 width=70%}

Параметры блока Modelica:

![](image/7.PNG){#fig:001 width=70%}

![](image/8.PNG){#fig:001 width=70%}

# Упражнение

В качестве упражнения нам надо построить модель SIR на OpenModelica. 

![](image/10.PNG){#fig:001 width=70%}

 задав конечное время 30 с, В результате получаем следующий график 

![](image/11.PNG){#fig:001 width=70%}


# Задание для самостоятельного выполнения

Предположим, что в модели SIR учитываются демографические процессы, в частности, что смертность в популяции полностью уравновешивает рождаемость, а все рожденные индивидуумы появляются на свет абсолютно здоровыми. Тогда получим следующую систему уравнений:

$$
\begin{aligned}
\dot{s} &= -\beta s(t) i(t) + \mu (N - s(t)) \\
\dot{i} &= \beta s(t) i(t) - \nu i(t) - \mu i(t) \\
\dot{r} &= \nu i(t) - \mu r(t)
\end{aligned}
$$


где μ — константа, которая равна коэффициенту смертности и рождаемости.

Pеализуем модель SIR с учетом демографических процессов в xcos с помощью блоков Modelica

![](image/12.PNG){#fig:001 width=70%}

В результате получаем следующий график

![](image/13.PNG){#fig:001 width=70%}


Реализуем модель SIR с учетом демографических процессов на OpenModelica.

![](image/14.PNG){#fig:001 width=70%}

![](image/15.PNG){#fig:001 width=70%}

# Выводы

В процессе выполнения данной лабораторной работы была построена модель SIR в xcos и OpenModelica.

# Список литературы{.unnumbered}

::: {#refs}
:::
