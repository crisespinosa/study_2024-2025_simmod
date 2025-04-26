---
## Front matter
lang: ru-RU
title: "Лабораторная работа №8"
subtitle: Модель TCP/AQM
author:
  - Эспиноса Василита К.М.
institute:
  - Российский университет дружбы народов, Москва, Россия

date: 29/03/2025

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Информация

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

  * Эспиноса Василита Кристина Микаела
  * студентка
  * Российский университет дружбы народов
  * [1032224624@pfur.ru](mailto:1032224624@pfur.ru)
  * <https://github.com/crisespinosa/>

:::
::: {.column width="30%"}



:::
::::::::::::::

# Цель работы

Реализовать модель TCP/AQM в xcos и OpenModelica

# Задание

- Реализовать модель TCP/AQM в xcos;
- Построить график динамики изменения размера TCP окна W(t) и размера очереди Q(t);
- Построить модель TCP/AQM в OpenModelica.


# Выполнение лабораторной работы

Зафиксируем начальные данные: N=1, R=1, K=5.3, X=1, W(0)=0.1, Q(0)= 1.  В меню Моделирование, Установить контекст зададим значения коэффициентов

![Начальные данные](image/1.PNG){#fig:001 width=70%}



# Реализация модели в xcos

Реализуем модель TCP/AQM, представлен на рис. [-@fig:002]. 

![Схема xcos, моделирующая систему](image/2.PNG){#fig:002 width=70%}

# Реализация модели в xcos

в результате получим динамику изменения размера TCP окна W(t) (черная линия) и размера очереди Q(t) (зеленая линия), а также фазовый портрет, 
который показывает наличие автоколебаний параметров системы — фазовая траектория осциллирует вокруг своей стационарной точки  рис. [-@fig:003], [-@fig:004] 

![Динамика изменения размера TCP окна W(t) и размера очереди Q(t)](image/3.PNG){#fig:003 width=70%}

# Реализация модели в xcos

![Фазовый портрет (W,Q)](image/4.PNG){#fig:004 width=70%}

# Реализация модели в xcos

Уменьшив скорость обработки пакетов C=0.9 увидим, что автоколебания стали более выраженными  рис. [-@fig:005], [-@fig:006].

![Динамика изменения размера TCP окна W(t) и размера очереди Q(t) при C=0.9](image/5.PNG){#fig:005 width=70%}

# Реализация модели в xcos

![Фазовый портрет (W,Q) при C=0.9](image/6.PNG){#fig:006 width=70%}

# Реализация модели в OpenModelica

Зададим параметры, начальные значения и систему уравнений, рис. [-@fig:007].

![Код в языке Modelica в OpenModelica](image/code1.PNG){#fig:007 width=70%}

# Реализация модели в OpenModelica

Выполнив симуляцию, получим динамику изменения размера TCP окна W(t)(красная линия) и размера очереди Q(t)(синяя линия), 
а также фазовый портрет, который показывает наличие автоколебаний параметров системы — фазовая траектория осциллирует вокруг своей стационарной точки рис. [-@fig:008], [-@fig:009].

![Динамика изменения размера TCP окна W(t) и размера очереди Q(t)](image/8.PNG){#fig:008 width=70%}

# Реализация модели в OpenModelica

![Фазовый портрет (W,Q)](image/7.PNG){#fig:009 width=70%}

# Реализация модели в OpenModelica

Уменьшив скорость обработки пакетов C=0.9:

![Код в языке Modelica в OpenModelica](image/code2.PNG){#fig:007 width=70%}

# Реализация модели в OpenModelica

Получим следующие графики:

![Динамика изменения размера TCP окна W(t) и размера очереди Q(t) при C=0.9](image/10.PNG){#fig:005 width=70%}

# Реализация модели в OpenModelica

![Фазовый портрет (W,Q) при C=0.9](image/6.PNG){#fig:009 width=70%}


# Выводы

В процессе выполнения данной лабораторной работы я реализовала модель TCP/AQM в xcos и OpenModelica.

# Список литературы{.unnumbered}

::: {#refs}

1. Братусь А. С., Новожилов Артем Сергеевич abd Платонов А. П. Динамические
системы и модели биологии. — М. : ФИЗМАТЛИТ, 2010. — 400 с.
2. OM overall User’s Guide. — 2020. — URL: https://www.openmodelica.org/
useresresources/userdocumentation.
3. Modelica Language. — URL: https : / / www . modelica . org /
modelicalanguage.
4. OpenModelica. — URL: https://www.openmodelica.org/.
5. Xcos. — URL: https://www.scilab.org/software/xcos.

:::
