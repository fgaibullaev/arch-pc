---
## Front matter
title: "Отчёта по лабораторной работе 7"
subtitle: "Команды безусловного и условного переходов в Nasm. Программирование ветвлений"
author: "Гайбуллаев Фаррух Шухрат"

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
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
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

Целью работы является изучение команд условного и безусловного переходов. Приобретение навыков написания программ с использованием переходов. Знакомство с назначением и структурой файла листинга.

# Выполнение лабораторной работы

1. Создайте каталог для программам лабораторной работы № 7, перейдите в него и создайте файл lab7-1.asm

2. Инструкция jmp в NASM используется для реализации безусловных переходов. Рассмотрим пример программы с использованием инструкции jmp.
Введите в файл lab7-1.asm текст программы из листинга 7.1.

![Файл lab7-1.asm](image/01.png){ #fig:001 width=70%, height=70% }

```
%include 'in_out.asm'
SECTION .data
msg1: DB 'Сообщение № 1',0
msg2: DB 'Сообщение № 2',0
msg3: DB 'Сообщение № 3',0
SECTION .text
GLOBAL _start

_start:
jmp _label2

_label1:
mov eax, msg1 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 1'

_label2:
mov eax, msg2 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 2'

_label3:
mov eax, msg3 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 3'

_end:
call quit ; вызов подпрограммы завершения
```

Создайте исполняемый файл и запустите его.

![Запуск программы lab7-1.asm](image/02.png){ #fig:002 width=70%, height=70% }

Инструкция jmp позволяет осуществлять переходы не только вперед но
и назад. Изменим программу таким образом, чтобы она выводила сначала
‘Сообщение № 2’, потом ‘Сообщение № 1’ и завершала работу. Для этого в
текст программы после вывода сообщения № 2 добавим инструкцию jmp с
меткой _label1 (т.е. переход к инструкциям вывода сообщения № 1) и после
вывода сообщения № 1 добавим инструкцию jmp с меткой _end (т.е. переход к
инструкции call quit). Измените текст программы в соответствии с листингом
7.2.

![Файл lab7-1.asm:](image/03.png){ #fig:003 width=70%, height=70% }

```
%include 'in_out.asm'
SECTION .data
msg1: DB 'Сообщение № 1',0
msg2: DB 'Сообщение № 2',0
msg3: DB 'Сообщение № 3',0
SECTION .text
GLOBAL _start

_start:
jmp _label2

_label1:
mov eax, msg1 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 1'
jmp _end

_label2:
mov eax, msg2 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 2'
jmp _label1

_label3:
mov eax, msg3 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 3'

_end:
call quit ; вызов подпрограммы завершения
```

![Запуск программы lab7-1.asm:](image/04.png){ #fig:004 width=70%, height=70% }

Измените текст программы добавив или изменив инструкции jmp, чтобы
вывод программы был следующим:
```
Сообщение № 3
Сообщение № 2
Сообщение № 1
```

![Файл lab7-1.asm](image/05.png){ #fig:005 width=70%, height=70% }

```
%include 'in_out.asm'
SECTION .data
msg1: DB 'Сообщение № 1',0
msg2: DB 'Сообщение № 2',0
msg3: DB 'Сообщение № 3',0
SECTION .text
GLOBAL _start

_start:
jmp _label3

_label1:
mov eax, msg1 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 1'
jmp _end

_label2:
mov eax, msg2 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 2'
jmp _label1

_label3:
mov eax, msg3 ; Вывод на экран строки
call sprintLF ; 'Сообщение № 3'
jmp _label2

_end:
call quit ; вызов подпрограммы завершения
```

![Запуск программы lab7-1.asm](image/06.png){ #fig:006 width=70%, height=70% }

3. Использование инструкции jmp приводит к переходу в любом случае. Однако, часто при написании программ необходимо использовать условные
переходы, т.е. переход должен происходить если выполнено какое-либо
условие. В качестве примера рассмотрим программу, которая определяет
и выводит на экран наибольшую из 3 целочисленных переменных: A,B
и C. Значения для A и C задаются в программе, значение B вводиться с
клавиатуры. Создайте исполняемый файл и проверьте его работу для разных значений B.

![Файл lab7-2.asm](image/07.png){ #fig:007 width=70%, height=70% }

```
%include 'in_out.asm'
section .data
msg1 db 'Введите B: ',0h
msg2 db "Наибольшее число: ",0h
A dd '20'
C dd '50'
section .bss
max resb 10
B resb 10
section .text
global _start
_start:
; ---------- Вывод сообщения 'Введите B: '
mov eax,msg1
call sprint
; ---------- Ввод 'B'
mov ecx,B
mov edx,10
call sread
; ---------- Преобразование 'B' из символа в число
mov eax,B
call atoi ; Вызов подпрограммы перевода символа в число
mov [B],eax ; запись преобразованного числа в 'B'
; ---------- Записываем 'A' в переменную 'max'
mov ecx,[A] ; 'ecx = A'
mov [max],ecx ; 'max = A'
; ---------- Сравниваем 'A' и 'С' (как символы)
cmp ecx,[C] ; Сравниваем 'A' и 'С'
jg check_B ; если 'A>C', то переход на метку 'check_B',
mov ecx,[C] ; иначе 'ecx = C'
mov [max],ecx ; 'max = C'
; ---------- Преобразование 'max(A,C)' из символа в число
check_B:
mov eax,max
call atoi ; Вызов подпрограммы перевода символа в число
mov [max],eax ; запись преобразованного числа в `max`
; ---------- Сравниваем 'max(A,C)' и 'B' (как числа)
mov ecx,[max]
cmp ecx,[B] ; Сравниваем 'max(A,C)' и 'B'
jg fin ; если 'max(A,C)>B', то переход на 'fin',
mov ecx,[B] ; иначе 'ecx = B'
mov [max],ecx
; ---------- Вывод результата
fin:
mov eax, msg2
call sprint ; Вывод сообщения 'Наибольшее число: '
mov eax,[max]
call iprintLF ; Вывод 'max(A,B,C)'
call quit ; Выход
```

![Запуск программы lab7-2.asm](image/08.png){ #fig:008 width=70%, height=70% }

4. Обычно nasm создаёт в результате ассемблирования только объектный
файл. Получить файл листинга можно, указав ключ -l и задав имя файла
листинга в командной строке. Создайте файл листинга для программы из
файла lab7-2.asm

![Файл листинга lab7-2](image/09.png){ #fig:009 width=70%, height=70% }

Внимательно ознакомиться с его форматом и содержимым. Подробно объяснить содержимое трёх строк файла листинга по выбору.

строка 128

* 128 - номер строки

* 0000009C - адрес

* 53 - машинный код

* push ebx - код программы

строка 129

* 129 - номер строки

* 0000009D - адрес

* 51 - машинный код

* push ecx- код программы

строка 130

* 130 - номер строки

* 0000009E - адрес

* 52 - машинный код

* push edx - код программы

Откройте файл с программой lab7-2.asm и в любой инструкции с двумя
операндами удалить один операнд. Выполните трансляцию с получением файла
листинга

![ошибка трансляции lab7-2](image/10.png){ #fig:010 width=70%, height=70% }

![файл листинга с ошибкой lab7-2](image/11.png){ #fig:011 width=70%, height=70% }

Объектный файл не смог создаться из-за ошибки. Но получился листинг, где выделено место ошибки.

5. Напишите программу нахождения наименьшей из 3 целочисленных переменных a,b и c. Значения переменных выбрать из табл. 7.5 в соответствии
с вариантом, полученным при выполнении лабораторной работы № 6.
Создайте исполняемый файл и проверьте его работу

для варианта 18 - 83, 73, 30

![Файл lab7-3.asm](image/12.png){ #fig:012 width=70%, height=70% }

```
%include 'in_out.asm'
SECTION .data
    msgA:	DB 'Input A: ',0
    msgB:       DB 'Input B: ',0
    msgC:	DB 'Input C: ',0
    answer:	DB 'Smallest: ',0

SECTION .bss
    A:	RESB 80
    B:  RESB 80
    C:  RESB 80
    result:     RESB 80
    min: RESB 80

SECTION .text
    GLOBAL _start

_start:
    mov eax,msgA
    call sprint
    mov ecx,A
    mov edx,80
    call sread
    mov eax,A
    call atoi 
    mov [A],eax

    mov eax, msgB
    call sprint
    mov ecx,B
    mov edx,80
    call sread
    mov eax,B
    call atoi
    mov [B],eax

    mov eax,msgC
    call sprint
    mov ecx,C
    mov edx,80
    call sread 
    mov eax,C
    call atoi
    mov [C],eax   
;_________________algorithm____________________
    
    mov ecx,[A] ;ecx = A
    mov [min],ecx ;min = A 

    cmp ecx, [B] ; A&B
    jl check_C ; if a<b: goto check_C 
    mov ecx, [B]
    mov [min], ecx ;else min = B

check_C:
    cmp ecx, [C]
    jl finish
    mov ecx,[C]
    mov [min],ecx 

finish:
    mov eax,answer
    call sprint

    mov eax, [min]
    call iprintLF

    call quit
```

![Запуск программы lab7-3.asm](image/13.png){ #fig:013 width=70%, height=70% }

6. Напишите программу, которая для введенных с клавиатуры значений x
и a вычисляет значение заданной функции f(x) и выводит результат вычислений. Вид функции f(x) выбрать из таблицы 7.6 вариантов заданий в
соответствии с вариантом, полученным при выполнении лабораторной работы № 7. Создайте исполняемый файл и проверьте его работу для значений X и a из 7.6.

для варианта 18

$$
 \begin{cases}
	a^{2}, a \ne 1
	\\   
	x+10, a = 1
 \end{cases}
$$

![Файл lab7-4.asm](image/14.png){ #fig:014 width=70%, height=70% }

```
%include 'in_out.asm'
SECTION .data
    msgA:	DB 'Input A: ',0
    msgX:       DB 'Input X: ',0

SECTION .bss
    A:	RESB 80
    X:  RESB 80
    result:     RESB 80

SECTION .text
    GLOBAL _start

_start:
    mov eax,msgA
    call sprint
    mov ecx,A
    mov edx,80
    call sread
    mov eax,A
    call atoi 
    mov [A],eax

    mov eax,msgX
    call sprint
    mov ecx,X
    mov edx,80
    call sread 
    mov eax,X
    call atoi
    mov [X],eax   
;_________________algorithm____________________

    mov edx, [A]
    mov ebx,1
    cmp ebx, edx
    jne first
    jmp second

first:
    mov eax,[A]
    mov ebx,[A]
    mul ebx
    call iprintLF 
    call quit
second:
    mov eax,[X]
    add eax,10
    call iprintLF 
    call quit
```

![Запуск программы lab7-4.asm](image/15.png){ #fig:015 width=70%, height=70% }

# Выводы

Изучили команды условного и безусловного переходов, познакомились с фалом листинга.
