# Интерпретатор диалекта языка Forth
Первая и вторая лабораторные работы по Языкам Системного Программирования, 2 курс.

## Особенности:
- [X] Базовая Forth-машина
- [X] Комлилятор Forth-команд
- [ ] Bootstrapped

## Сборка
	
Интерпретатор расчитан для работы на Linux с 64-ех битной архитектурой и установленным **nasm**<br />
Совместимо с Windows 10 Linux Subsystem<br />
Совместимость с MacOS X не установлена<br />
Сборка:<br />

```
nasm -felf64 -g "interpreter.asm" -o interpreter.o
ld -o interpreter interpreter.o
chmod +x interpreter
```

	
## Реализованные возможности

### Интерпретатор Forth

- **.S** -- не разрушая стек печатает всё его содержимое.
- **+**, **-**, \*, **/** -- Арифметика
- **<**, **>**, **=** -- сравнение (кладёт на вершину стека 1, если условие истинно)
- **and**, **or**, **not** -- логика (истина -- число, отличное от нуля)
- **rot** --  a b c -> b c a
- **swap** -- меняет два последних элемента стека местами
- **dup** -- дублирует элемент на вершине стека
- **drop** -- снимает элемент с вершины стека
- **.** -- снимает элемент с вершины стека и печает на экран
- **key** читает символ с _stdin_ и помещает на вершину стека
- **emit** -- снимает с вершины стека символ и печатает в _stdout_
- **number** -- читает с _stdin_ знаковое число и помещает в стек
- **mem** -- загрузит в стек константу – адрес начала пользовательской памяти.
- **!** -- снимает элемент с вершины стека и записывает, по адресу, лежащему на новой вершине стека
- **@** -- читает содержимое памяти по адресу, указанному на вершине стека
- **:** -- переход в режим комплилирования
- **exit** -- Выход из интерпретатора

### Команды комлилятора

- **;** -- Выход из режима компилирования

### Команды диалекта

- **branch n** -- безусловный переход на n слов вперёд (доступно только в режиме комплирирования)
- **branch0 n** -- переход на n слов вперёд, если на вершине стека нуль

### Комплирование собственных команд

Интерпретатор Forth позволяет кодировать команду через последовательность уже известных команд. Синктаксис:
```
: имя_команды [команда/число] ;
```
Если вместо команды указано число, оно будет положено на вершину стека.

### Пример создания собственной команды

```
: sq dup * ;
: discr rot 4 * * swap sq swap - ;
1 2 3 discr .
```

Результатом выполнения этой команды **discr** будет дискриминант квадратного уравения _1x<sup>2</sup>+2x+3=0_ на вершине стека.

## IOLib-tester.py

Форк тестера функций библиотеки по вводу и выводу. 
Требуется Python 2.7.x

Всю дополнительную информацию можно узнать в группе [курса](vk.com/spifmo)
