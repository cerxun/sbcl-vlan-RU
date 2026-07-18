# Документация V

(См. https://modules.vlang.io/ — документация стандартной библиотеки V)
(См. также https://docs.vlang.io/introduction.html — та же информация, что и в этом документе,
но разбитая на отдельные страницы по разделам для удобного чтения на мобильных устройствах)
<a id="introduction"></a>
## Введение

V — статически типизированный компилируемый язык программирования, предназначенный для создания поддерживаемого программного обеспечения.

Он похож на Go, а его дизайн также был вдохновлён Oberon, Rust, Swift,
Kotlin и Python.

V — очень простой язык. Изучение этой документации займёт примерно выходные,
и к концу вы практически освоите весь язык.

Язык поощряет написание простого и понятного кода с минимальной абстракцией.

Несмотря на простоту, V даёт разработчику много возможностей.
Всё, что можно сделать на других языках, можно сделать и на V.
<a id="installing-v-from-source"></a>
## Установка V из исходников

Лучший способ получить самую свежую версию V — установить его из исходников.
Это просто и занимает всего несколько секунд:
```bash
git clone --depth=1 https://github.com/vlang/v
cd v
make
```

Примечание: если вы на Windows вне WSL, запустите `make.bat` вместо `make` в оболочке CMD.
Примечание: на Ubuntu/Debian может потребоваться сначала выполнить `sudo apt install git build-essential make`.

Подробнее см. раздел
[Installing V](https://github.com/vlang/v/blob/master/README.md#installing-v-from-source)
в README.md.
<a id="upgrading-v-to-latest-version"></a>
## Обновление V до последней версии

Если V уже установлен на машине, его можно обновить до последней версии
с помощью встроенного средства самообновления V.
Для этого выполните команду `v up`.
<a id="packaging-v-for-distribution"></a>
## Сборка пакета V для распространения
См. [заметки о подготовке пакета для V](packaging_v_for_distributions.md).
<a id="getting-started"></a>
## Начало работы

V может автоматически создать базовую структуру проекта за вас
с помощью любой из следующих команд в терминале:

* `v init` → добавляет необходимые файлы в текущую папку, чтобы сделать её проектом V
* `v new abc` → создаёт новый проект в папке `abc`, по умолчанию — проект «hello world».
* `v new --web abcd` → создаёт новый проект в папке `abcd` по шаблону vweb.
<a id="table-of-contents"></a>
## Содержание

<table>
<tr><td width=33% valign=top>

* [Привет, мир](#hello-world)
* [Запуск папки проекта](#running-a-project-folder-with-several-files)
* [Комментарии](#comments)
* [Функции](#functions)
    * [Поднятие (hoisting)](#hoisting)
    * [Возврат нескольких значений](#returning-multiple-values)
* [Видимость символов](#symbol-visibility)
* [Переменные](#variables)
    * [Изменяемые переменные](#mutable-variables)
    * [Инициализация и присваивание](#initialization-vs-assignment)
    * [Предупреждения и ошибки объявления](#warnings-and-declaration-errors)
* [Типы V](#v-types)
    * [Примитивные типы](#primitive-types)
    * [Строки](#strings)
    * [Руны](#runes)
    * [Числа](#numbers)
    * [Массивы](#arrays)
        * [Многомерные массивы](#multidimensional-arrays)
        * [Методы массивов](#array-methods)
        * [Срезы массивов](#array-slices)
    * [Массивы фиксированного размера](#fixed-size-arrays)
    * [Карты](#maps)
        * [Синтаксис обновления карты](#map-update-syntax)

</td><td width=33% valign=top>

* [Импорт модулей](#module-imports)
    * [Выборочный импорт](#selective-imports)
    * [Иерархия модулей](#module-hierarchy)
    * [Псевдонимы импорта модулей](#module-import-aliasing)
* [Операторы и выражения](#statements--expressions)
    * [If](#if)
        * [Выражения `If`](#if-expressions)
        * [Разворачивание `If`](#if-unwrapping)
    * [Match](#match)
    * [Оператор in](#in-operator)
    * [Цикл for](#for-loop)
    * [Defer](#defer)
    * [Goto](#goto)
* [Структуры](#structs)
    * [Структуры в куче](#heap-structs)
    * [Значения полей по умолчанию](#default-field-values)
    * [Обязательные поля](#required-fields)
    * [Краткий синтаксис литерала структуры](#short-struct-literal-syntax)
    * [Синтаксис обновления структуры](#struct-update-syntax)
    * [Завершающие аргументы-литералы структуры](#trailing-struct-literal-arguments)
    * [Модификаторы доступа](#access-modifiers)
    * [Анонимные структуры](#anonymous-structs)
    * [Статические методы типа](#static-type-methods)
    * [Структуры [noinit]](#noinit-structs)
    * [Методы](#methods)
    * [Вложенные структуры](#embedded-structs)
* [Объединения](#unions)
    * [Зачем использовать объединения?](#why-use-unions)
    * [Встраивание](#embedding)

</td><td valign=top>

* [Функции 2](#functions-2)
    * [Неизменяемые аргументы функций по умолчанию](#immutable-function-args-by-default)
    * [Изменяемые аргументы](#mutable-arguments)
    * [Переменное число аргументов](#variable-number-of-arguments)
    * [Анонимные и функции высшего порядка](#anonymous--higher-order-functions)
    * [Лямбда-выражения](#lambda-expressions)
    * [Замыкания](#closures)
    * [Порядок вычисления параметров](#parameter-evaluation-order)
* [Ссылки](#references)
* [Константы](#constants)
    * [Обязательный префикс модуля](#required-module-prefix)
* [Встроенные функции](#builtin-functions)
    * [println](#println)
    * [Вывод пользовательских типов](#printing-custom-types)
    * [Вывод выражений во время выполнения](#dumping-expressions-at-runtime)
* [Модули](#modules)
    * [Создание модулей](#create-modules)
    * [Особенности папок проекта](#special-considerations-for-project-folders)
    * [Функции init](#init-functions)
    * [Функции cleanup](#cleanup-functions)

</td></tr>
<tr><td width=33% valign=top>

* [Объявления типов](#type-declarations)
    * [Псевдонимы типов](#type-aliases)
    * [Перечисления](#enums)
    * [Типы функций](#function-types)
    * [Интерфейсы](#interfaces)
    * [Суммарные типы](#sum-types)
    * [Типы Option/Result и обработка ошибок](#optionresult-types-and-error-handling)
        * [Обработка option/result](#handling-optionsresults)
    * [Пользовательские типы ошибок](#custom-error-types)
    * [Обобщённые типы](#generics)
* [Параллелизм](#concurrency)
    * [Запуск параллельных задач](#spawning-concurrent-tasks)
    * [Каналы](#channels)
    * [Разделяемые объекты](#shared-objects)
* [JSON](#json)
    * [Декодирование JSON](#decoding-json)
    * [Кодирование JSON](#encoding-json)
* [Тестирование](#testing)
    * [Assert](#asserts)
    * [Assert с дополнительным сообщением](#asserts-with-an-extra-message)
    * [Assert без прерывания программы](#asserts-that-do-not-abort-your-program)
    * [Тестовые файлы](#test-files)
    * [Запуск тестов](#running-tests)
* [Управление памятью](#memory-management)
    * [Контроль](#control)
    * [Стек и куча](#stack-and-heap)
* [ORM](#orm)
* [Написание документации](#writing-documentation)
    * [Переносы строк в комментариях документации](#newlines-in-documentation-comments)

</td><td width=33% valign=top>

* [Инструменты](#tools)
    * [v fmt](#v-fmt)
    * [v shader](#v-shader)
    * [Профилирование](#profiling)
* [Управление пакетами](#package-management)
    * [Команды пакетов](#package-commands)
    * [Публикация пакета](#publish-package)
* [Продвинутые темы](#advanced-topics)
    * [Атрибуты](#attributes)
    * [Условная компиляция](#conditional-compilation)
        * [Псевдопеременные времени компиляции](#compile-time-pseudo-variables)
        * [Рефлексия времени компиляции](#compile-time-reflection)
        * [Код времени компиляции](#compile-time-code)
        * [Типы времени компиляции](#compile-time-types)
        * [Файлы для конкретных окружений](#environment-specific-files)
	* [Отладчик](#debugger)
 		* [Стек вызовов](#call-stack)
   		* [Трассировка](#trace)
    * [Небезопасный по памяти код](#memory-unsafe-code)
    * [Структуры с полями-ссылками](#structs-with-reference-fields)
    * [sizeof и __offsetof](#sizeof-and-__offsetof)
    * [Ограниченная перегрузка операторов](#limited-operator-overloading)
    * [Настройка производительности](#performance-tuning)
    * [Атомарные операции](#atomics)
    * [Глобальные переменные](#global-variables)
    * [Статические переменные](#static-variables)
    * [Кросс-компиляция](#cross-compilation)
    * [Отладка](#debugging)
        * [Бинарники C-бэкенда (по умолчанию)](#c-backend-binaries-default)
        * [Бинарники Native-бэкенда](#native-backend-binaries)
        * [Javascript-бэкенд](#javascript-backend)

</td><td valign=top>

* [V и C](#v-and-c)
    * [Вызов C из V](#calling-c-from-v)
    * [Вызов V из C](#calling-v-from-c)
    * [Передача флагов компиляции C](#passing-c-compilation-flags)
    * [#pkgconfig](#pkgconfig)
    * [Подключение кода C](#including-c-code)
    * [Типы C](#c-types)
    * [Объявления C](#c-declarations)
    * [Экспорт в разделяемую библиотеку](#export-to-shared-library)
    * [Перевод C в V](#translating-c-to-v)
    * [Обход проблем C](#working-around-c-issues)
* [Другие возможности V](#other-v-features)
    * [Встроенный ассемблер](#inline-assembly)
    * [Горячая перезагрузка кода](#hot-code-reloading)
    * [Кроссплатформенные shell-скрипты на V](#cross-platform-shell-scripts-in-v)
    * [Vsh-скрипты без расширения](#vsh-scripts-with-no-extension)
* [Приложения](#appendices)
    * [Ключевые слова](#appendix-i-keywords)
    * [Операторы](#appendix-ii-operators)
    * [Другие онлайн-ресурсы](#other-online-resources)

</td></tr>
</table>

<!--
Примечание: после ограждений кода для v можно указывать специальные ключевые слова:
compile, cgen, live, ignore, failcompile, okfmt, oksyntax, badsyntax, wip, nofmt
Подробнее: `v check-md`
-->
<a id="hello-world"></a>
## Привет, мир

```v
fn main() {
	println('hello world')
}
```

Сохраните этот фрагмент в файл с именем `hello.v`. Затем выполните: `v run hello.v`.

> Это предполагает, что вы создали симлинк для V командой `v symlink`, как описано
[здесь](https://github.com/vlang/v/blob/master/README.md#symlinking).
> Если вы ещё этого не сделали, придётся указывать путь к V вручную.

Поздравляем — вы только что написали и запустили свою первую программу на V!

Программу можно скомпилировать без запуска командой `v hello.v`.
Все поддерживаемые команды см. в `v help`.

Из примера выше видно, что функции объявляются ключевым словом `fn`.
Тип возвращаемого значения указывается после имени функции.
В данном случае `main` ничего не возвращает, поэтому тип возврата не указан.

Как и во многих других языках (C, Go, Rust), `main` — точка входа в программу.

[`println`](#println) — одна из немногих [встроенных функций](#builtin-functions).
Она выводит переданное значение в стандартный поток вывода.

Объявление `fn main()` можно опустить в однофайловых программах.
Это удобно при написании небольших программ, «скриптов» или при изучении языка.
Для краткости в этом руководстве `fn main()` будет опускаться.

То есть программа «hello world» на V может быть такой простой:

```v
println('hello world')
```

> [!NOTE]
> Если вы явно не используете `fn main() {}`, убедитесь, что все
> объявления идут до любых присваиваний переменным или вызовов функций верхнего уровня,
> поскольку V считает всё после первого присваивания/вызова функции частью
> неявной функции main.
<a id="running-a-project-folder-with-several-files"></a>
## Запуск папки проекта с несколькими файлами

Допустим, у вас есть папка с несколькими файлами `.v`, один из которых
содержит функцию `main()`, а в остальных — вспомогательные
функции. Они могут быть сгруппированы по темам, но пока *ещё недостаточно* структурированы,
чтобы стать отдельными переиспользуемыми модулями, и вы хотите скомпилировать
всё в одну программу.

В других языках пришлось бы использовать include или систему сборки,
чтобы перечислить все файлы, скомпилировать их отдельно в объектные файлы,
а затем слинковать в один исполняемый файл.

В V же можно скомпилировать и запустить всю папку с файлами `.v` целиком
одной командой `v run .`. Передача параметров тоже работает, например:
`v run . --yourparam some_other_stuff`

Сначала V скомпилирует ваши файлы в одну программу (с именем
папки/проекта), а затем запустит её, передав
`--yourparam some_other_stuff` как параметры командной строки.

Программа может использовать параметры CLI так:

```v
import os

println(os.args)
```

> [!NOTE]
> После успешного запуска V удалит сгенерированный исполняемый файл.
> Чтобы сохранить его, используйте `v -keepc run .` или скомпилируйте
> вручную командой `v .`.

> [!NOTE]
> Флаги компилятора V нужно передавать *до* команды `run`.
> Всё, что идёт после исходного файла/папки, передаётся программе
> как есть — V это не обрабатывает.
<a id="comments"></a>
## Комментарии

```v
// This is a single line comment.
/*
This is a multiline comment.
   /* It can be nested. */
*/
```
<a id="functions"></a>
## Функции

```v
fn main() {
	println(add(77, 33))
	println(sub(100, 50))
}

fn add(x int, y int) int {
	return x + y
}

fn sub(x int, y int) int {
	return x - y
}
```

Как и раньше, тип указывается после имени аргумента.

Как в Go и C, функции нельзя перегружать.
Это упрощает код и улучшает поддерживаемость и читаемость.
<a id="hoisting"></a>
### Поднятие (hoisting)

Функции можно использовать до их объявления:
`add` и `sub` объявлены после `main`, но их всё равно можно вызывать из `main`.
Это верно для всех объявлений в V и избавляет от необходимости в заголовочных файлах
или задумываться о порядке файлов и объявлений.
<a id="returning-multiple-values"></a>
### Возврат нескольких значений

```v
fn foo() (int, int) {
	return 2, 3
}

a, b := foo()
println(a) // 2
println(b) // 3
c, _ := foo() // ignore values using `_`
```
<a id="symbol-visibility"></a>
## Видимость символов

```v
pub fn public_function() {
}

fn private_function() {
}
```

Функции по умолчанию приватные (не экспортируются).
Чтобы другие [модули](#module-imports) могли их использовать, добавьте `pub`. То же относится
к [структурам](#structs), [константам](#constants) и [типам](#type-declarations).

> [!NOTE]
> `pub` можно использовать только из именованного модуля.
> О создании модуля см. [Модули](#modules).
<a id="variables"></a>
## Переменные

```v
name := 'Bob'
age := 20
large_number := i64(9999999999)
println(name)
println(age)
println(large_number)
```

Переменные объявляются и инициализируются с помощью `:=`. Это единственный
способ объявления переменных в V. Переменные всегда имеют начальное
значение.

Тип переменной выводится из значения справа.
Чтобы выбрать другой тип, используйте преобразование типа:
выражение `T(v)` преобразует значение `v` к
типу `T`.

В отличие от большинства языков, в V переменные можно объявлять только внутри функций.
По умолчанию V **не разрешает глобальные переменные**. Подробнее см. [здесь](#global-variables).

Для единообразия в разных кодовых базах все имена переменных и функций
должны быть в стиле `snake_case`, в отличие от имён типов, которые должны быть в `PascalCase`.
<a id="mutable-variables"></a>
### Изменяемые переменные

```v
mut age := 20
println(age)
age = 21
println(age)
```

Чтобы изменить значение переменной, используйте `=`. В V переменные
по умолчанию неизменяемы.
Чтобы менять значение, объявите переменную с `mut`.

Попробуйте скомпилировать программу выше, убрав `mut` из первой строки.
<a id="initialization-vs-assignment"></a>
### Инициализация и присваивание

Обратите внимание на (важное) различие между `:=` и `=`.
`:=` используется для объявления и инициализации, `=` — для присваивания.

```v failcompile
fn main() {
	age = 21
}
```

Этот код не скомпилируется, потому что переменная `age` не объявлена.
В V все переменные нужно объявлять.

```v
fn main() {
	age := 21
}
```

Значения нескольких переменных можно изменить в одной строке.
Так их значения можно поменять местами без промежуточной переменной.

```v
mut a := 0
mut b := 1
println('${a}, ${b}') // 0, 1
a, b = b, a
println('${a}, ${b}') // 1, 0
```
<a id="warnings-and-declaration-errors"></a>
### Предупреждения и ошибки объявления

В режиме разработки компилятор предупредит, что переменная не использована
(предупреждение «unused variable»).
В production-режиме (включается флагом `-prod` — `v -prod foo.v`)
код вообще не скомпилируется (как в Go).
```v
fn main() {
	a := 10
	// warning: unused variable `a`
}
```

Чтобы игнорировать значения, возвращаемые функцией, можно использовать `_`
```v
fn foo() (int, int) {
	return 2, 3
}

fn main() {
	c, _ := foo()
	print(c)
	// no warning about unused variable returned by foo.
}
```

В отличие от большинства языков, затенение переменных (variable shadowing) запрещено. Объявление переменной с именем,
уже используемым во внешней области видимости, вызовет ошибку компиляции.
```v failcompile nofmt
fn main() {
	a := 10
	{
		a := 20 // error: redefinition of `a`
	}
}
```
Затенение переменных запрещено, но затенение полей разрешено.
```v
pub struct Dimension {
	width  int = -1
	height int = -1
}

pub struct Test {
	Dimension
	width int = 100
	// height int
}

fn main() {
	test := Test{}
	println('${test.width} ${test.height} ${test.Dimension.width}') // 100 -1 -1
}
```
<a id="v-types"></a>
## Типы V
<a id="primitive-types"></a>
### Примитивные типы

```v ignore
bool

string

i8    i16  int  i64      i128 (soon)
u8    u16  u32  u64      u128 (soon)

rune // represents a Unicode code point

f32 f64

isize, usize // platform-dependent, the size is how many bytes it takes to reference any location in memory

voidptr // this one is mostly used for [C interoperability](#v-and-c)
```

> [!NOTE]
> В отличие от C и Go, `int` всегда является 32-битным целым числом.

Существует исключение из правила, согласно которому все операторы в V должны иметь значения одного и того же типа по обе стороны. Маленький примитивный тип на одной стороне может быть автоматически повышен, если он полностью вписывается в диапазон данных типа на другой стороне.
Вот допустимые возможности:

```v ignore
   i8 → i16 → int → i64
                  ↘     ↘
                    f32 → f64
                  ↗     ↗
   u8 → u16 → u32 → u64 ⬎
      ↘     ↘     ↘      ptr
   i8 → i16 → int → i64 ⬏
```

Например, значение `int` может быть автоматически повышено до `f64` или `i64`, но не до `u32`. (`u32` означало бы потерю знака для отрицательных значений).
Однако повышение с `int` до `f32` в настоящее время выполняется автоматически (но может привести к потере точности для больших значений).

Литералы вроде `123` или `4.56` обрабатываются особым образом. Они не приводят к повышению типов, однако по умолчанию становятся `int` и `f64` соответственно, когда необходимо определить их тип:

```v nofmt
u := u16(12)
v := 13 + u    // v is of type `u16` - no promotion
x := f32(45.6)
y := x + 3.14  // y is of type `f32` - no promotion
a := 75        // a is of type `int` - default for int literal
b := 14.7      // b is of type `f64` - default for float literal
c := u + a     // c is of type `int` - automatic promotion of `u`'s value
d := b + x     // d is of type `f64` - automatic promotion of `x`'s value
```
<a id="strings"></a>
### Строки

В V строки кодируются в UTF-8 и по умолчанию являются неизменяемыми (только для чтения):

```v
s := 'hello 🌎' // the `world` emoji takes 4 bytes, and string length is reported in bytes
assert s.len == 10

arr := s.bytes() // convert `string` to `[]u8`
assert arr.len == 10

s2 := arr.bytestr() // convert `[]u8` to `string`
assert s2 == s

name := 'Bob'
assert name.len == 3
// indexing gives a byte, u8(66) == `B`
assert name[0] == u8(66)
// slicing gives a string 'ob'
assert name[1..3] == 'ob'

// escape codes
// escape special characters like in C
windows_newline := '\r\n'
assert windows_newline.len == 2

// arbitrary bytes can be directly specified using `\x##` notation where `#` is
// a hex digit
aardvark_str := '\x61ardvark'
assert aardvark_str == 'aardvark'
assert '\xc0'[0] == u8(0xc0)

// or using octal escape `\###` notation where `#` is an octal digit
aardvark_str2 := '\141ardvark'
assert aardvark_str2 == 'aardvark'

// Unicode can be specified directly as `\u####` where # is a hex digit
// and will be converted internally to its UTF-8 representation
star_str := '\u2605' // ★
assert star_str == '★'
// UTF-8 can be specified this way too, as individual bytes.
assert star_str == '\xe2\x98\x85'
```

Поскольку строки неизменяемы, вы не можете напрямую изменять символы в строке:

```v failcompile
mut s := 'hello 🌎'
s[0] = `H` // not allowed
```

> error: cannot assign to `s[i]` since V strings are immutable

Обратите внимание, что индексирование строки обычно дает `u8` (байт), а не `rune` или другую строку.
Индексы соответствуют _байтам_ в строке, а не символам Unicode.
Если вы хотите преобразовать `u8` в строку, используйте метод `.ascii_str()` для `u8`:

```v
country := 'Netherlands'
println(country[0]) // Output: 78
println(country[0].ascii_str()) // Output: N
```

Тем не менее, вы можете легко получить руны для строки с помощью метода `runes()`, который вернет массив символов UTF-8 из строки. Затем вы можете индексировать этот массив. Просто имейте в виду, что в массиве `rune` может быть меньше индексов, чем в байтах строки, если в ней _есть_ не-ASCII символы.

```v
mut s := 'hello 🌎'
// there are 10 bytes in the string (as shown earlier), but only 7 runes, since the `world` emoji
// only counts as one `rune` (one Unicode character)
assert s.runes().len == 7
println(s.runes()[6])
```

Если вы хотите получить кодовую точку из определенного индекса строки или провести более сложную обработку и преобразования UTF-8, обратитесь к
модулю [vlib/encoding/utf8](https://modules.vlang.io/encoding.utf8.html).

Для обозначения строк могут использоваться как одинарные, так и двойные кавычки. Для единообразия `vfmt` преобразует двойные кавычки в одинарные, если строка не содержит символ одинарной кавычки.

Добавьте `r` для необрабатываемых строк. Экранирование не обрабатывается, поэтому вы получите именно то, что ввели:

```v
s := r'hello\nworld' // the `\n` will be preserved as two characters
println(s) // "hello\nworld"
```

Строки легко преобразуются в целые числа:

```v
s := '42'
n := s.int() // 42

// all int literals are supported
assert '0xc3'.int() == 195
assert '0o10'.int() == 8
assert '0b1111_0000_1010'.int() == 3850
assert '-0b1111_0000_1010'.int() == -3850
```

Для более сложной обработки и преобразований строк обратитесь к
модулю [vlib/strconv](https://modules.vlang.io/strconv.html).
<a id="string-interpolation"></a>
#### Интерполяция строк

Базовый синтаксис интерполяции очень прост — используйте `${` перед именем переменной и `}` после. Переменная будет преобразована в строку и встроена в литерал:

```v
name := 'Bob'
println('Hello, ${name}!') // Hello, Bob!
```

Это также работает с полями: `'age = ${user.age}'`. Вы также можете использовать более сложные выражения:
`'can register = ${user.age > 13}'`.

Также поддерживаются спецификаторы формата, аналогичные `printf()` в C. `f`, `g`, `x`, `o`, `b` и т. д. являются необязательными и задают формат вывода. Компилятор заботится о размере хранилища, поэтому нет `hd` или `llu`.

Чтобы использовать спецификатор формата, следуйте этому шаблону:

`${varname:[flags][width][.precision][type]}`

- flags (флаги): может быть ноль или более из следующих: `-` для выравнивания вывода по левому краю в пределах поля, `0` для использования `0` в качестве символа заполнения вместо символа пробела по умолчанию.
  > **Примечание**
  >
  > V в настоящее время не поддерживает использование `'` или `#` в качестве флагов формата, а V поддерживает, но не требует `+` для выравнивания по правому краю, так как это является поведением по умолчанию.
- width (ширина): может быть целочисленным значением, описывающим минимальную ширину всего поля для вывода.
- precision (точность): целочисленное значение, предваренное `.`, гарантирует указанное количество цифр после десятичной запятой без незначащих завершающих нулей. Если требуется отображение незначащих нулей, добавьте спецификатор `f` к значению точности (см. примеры ниже). Применяется только к переменным с плавающей запятой и игнорируется для целочисленных переменных.
- type (тип): `f` и `F` указывают, что входные данные являются числом с плавающей запятой и должны быть отображены как таковые, `e` и `E` указывают, что входные данные являются числом с плавающей запятой и должны быть отображены как показатель степени (частично сломано), `g` и `G` указывают, что входные данные являются числом с плавающей запятой—отображатель будет использовать десятичную запись для малых значений и экспоненциальную запись для больших значений, `d` указывает, что входные данные являются целым числом и должны быть отображены в десятичной системе счисления, `x` и `X` требуют целого числа и отобразят его как шестнадцатеричные цифры, `o` требует целого числа и отобразит его как восьмеричные цифры, `b` требует целого числа и отобразит его как двоичные цифры, `s` требует строку (почти никогда не используется).

  > **Примечание**
  >
  > Когда числовой тип может отображать алфавитные символы, например, шестнадцатеричные строки или специальные значения вроде `infinity`, строчная версия типа принудительно использует строчные буквы, а прописная версия принудительно использует прописные буквы.

  > **Примечание**
  >
  > В большинстве случаев лучше оставить тип формата пустым. Числа с плавающей запятой по умолчанию будут отображаться как `g`, целые числа по умолчанию как `d`, а `s` почти всегда избыточен.
  > Есть только три случая, когда рекомендуется указывать тип:

- строки формата разбираются во время компиляции, поэтому указание типа может помочь обнаружить ошибки на этом этапе
- строки формата по умолчанию используют строчные буквы для шестнадцатеричных цифр и `e` в показателях степени. Используйте прописной тип, чтобы принудительно использовать прописные шестнадцатеричные цифры и прописную `E` в показателях степени.
- строки формата являются самым удобным способом получить шестнадцатеричные, двоичные или восьмеричные строки из целого числа.

Смотрите
[Format Placeholder Specification](https://en.wikipedia.org/wiki/Printf_format_string#Format_placeholder_specification)
для получения дополнительной информации.

```v
x := 123.4567
println('[${x:.2}]') // round to two decimal places => [123.46]
println('[${x:10}]') // right-align with spaces on the left => [   123.457]
println('[${int(x):-10}]') // left-align with spaces on the right => [123       ]
println('[${int(x):010}]') // pad with zeros on the left => [0000000123]
println('[${int(x):b}]') // output as binary => [1111011]
println('[${int(x):o}]') // output as octal => [173]
println('[${int(x):X}]') // output as uppercase hex => [7B]

println('[${10.0000:.2}]') // remove insignificant 0s at the end => [10]
println('[${10.0000:.2f}]') // do show the 0s at the end, even though they do not change the number => [10.00]
```

В V также есть переключатели `r` и `R`, которые будут повторять строку указанное количество раз.

```v
println('[${'abc':3r}]') // [abcabcabc]
println('[${'abc':3R}]') // [ABCABCABC]
```
<a id="string-operators"></a>
#### Операторы строк

```v
name := 'Bob'
bobby := name + 'by' // + is used to concatenate strings
println(bobby) // "Bobby"
mut s := 'hello '
s += 'world' // `+=` is used to append to a string
println(s) // "hello world"
```

Все операторы в V должны иметь значения одного и того же типа по обе стороны. Вы не можете склеить целое число со строкой:

```v failcompile
age := 10
println('age = ' + age) // not allowed
```

> error: infix expr: cannot use `int` (right expression) as `string`

Мы должны либо преобразовать `age` в строку:

```v
age := 11
println('age = ' + age.str())
```

либо использовать интерполяцию строк (предпочтительно):

```v
age := 12
println('age = ${age}')
```

Смотрите все методы [string](https://modules.vlang.io/index.html#string)
и связанные модули [strings](https://modules.vlang.io/strings.html),
[strconv](https://modules.vlang.io/strconv.html).
<a id="runes"></a>
### Руны

`rune` представляет один символ Unicode, закодированный в UTF-32, и является псевдонимом для `u32`.
Для их обозначения используйте <code>`</code> (обратные кавычки):

```v
rocket := `🚀`
```

`rune` может быть преобразован в строку UTF-8 с помощью метода `.str()`.

```v
rocket := `🚀`
assert rocket.str() == '🚀'
```

`rune` может быть преобразован в байты UTF-8 с помощью метода `.bytes()`.

```v
rocket := `🚀`
assert rocket.bytes() == [u8(0xf0), 0x9f, 0x9a, 0x80]
```

Шестнадцатеричные, юникодные и восьмеричные escape-последовательности также работают в литерале `rune`:

```v
assert `\x61` == `a`
assert `\141` == `a`
assert `\u0061` == `a`

// multibyte literals work too
assert `\u2605` == `★`
assert `\u2605`.bytes() == [u8(0xe2), 0x98, 0x85]
assert `\xe2\x98\x85`.bytes() == [u8(0xe2), 0x98, 0x85]
assert `\342\230\205`.bytes() == [u8(0xe2), 0x98, 0x85]
```

Обратите внимание, что литералы `rune` используют тот же синтаксис экранирования, что и строки, но могут содержать только один символ Unicode. Поэтому, если в вашем коде указан не один символ Unicode, вы получите ошибку во время компиляции.

Также помните, что строки индексируются по байтам, а не по рунам, поэтому будьте осторожны:

```v
rocket_string := '🚀'
assert rocket_string[0] != `🚀`
assert 'aloha!'[0] == `a`
```

Строка может быть преобразована в руны методом `.runes()`.

```v
hello := 'Hello World 👋'
hello_runes := hello.runes() // [`H`, `e`, `l`, `l`, `o`, ` `, `W`, `o`, `r`, `l`, `d`, ` `, `👋`]
assert hello_runes.string() == hello
```
<a id="numbers"></a>
### Числа

```v
a := 123
```

Это присвоит значение 123 переменной `a`. По умолчанию `a` будет иметь тип `int`.

Вы также можете использовать шестнадцатеричную, двоичную или восьмеричную запись для целочисленных литералов:

```v
a := 0x7B
b := 0b01111011
c := 0o173
```

Все они будут присвоены одно и то же значение, 123. Все они будут иметь тип `int`, независимо от используемой нотации.

V также поддерживает запись чисел с `_` в качестве разделителя:

```v
num := 1_000_000 // same as 1000000
three := 0b0_11 // same as 0b11
float_num := 3_122.55 // same as 3122.55
hexa := 0xF_F // same as 255
oct := 0o17_3 // same as 0o173
```

Если вы хотите другой тип целого числа, вы можете использовать приведение типов:

```v
a := i64(123)
b := u8(42)
c := i16(12345)
```

Присвоение чисел с плавающей запятой работает так же:

```v
f := 1.0
f1 := f64(3.14)
f2 := f32(3.14)
```

Если вы не указываете тип явно, по умолчанию литералы с плавающей запятой будут иметь тип `f64`.

Литералы с плавающей запятой также могут быть объявлены как степень десяти:

```v
f0 := 42e1 // 420
f1 := 123e-2 // 1.23
f2 := 456e+2 // 45600
```
<a id="arrays"></a>
### Массивы

Массив — это коллекция элементов данных одного типа. Литерал массива — это список выражений, заключенных в квадратные скобки. К отдельному элементу можно обратиться с помощью выражения *индекса*. Индексация начинается с `0`.

```v
mut nums := [10, 20, 30]
println(nums) // `[10, 20, 30]`
println(nums[0]) // `10`
println(nums[1]) // `20`

nums[1] = 5
println(nums) // `[10, 5, 30]`
```

<a id='array-operations'></a>

Элемент можно добавить в конец массива с помощью оператора push `<<`.
Он также может добавить весь массив.

```v
mut nums := [1, 2, 3]
nums << 4
println(nums) // "[1, 2, 3, 4]"

// append array
nums << [5, 6, 7]
println(nums) // "[1, 2, 3, 4, 5, 6, 7]"
```

```v
mut names := ['John']
names << 'Peter'
names << 'Sam'
// names << 10  <-- This will not compile. `names` is an array of strings.
```

`val in array` возвращает true, если массив содержит `val`. Смотрите [`in` operator](#in-operator).

```v
names := ['John', 'Peter', 'Sam']
println('Alex' in names) // "false"
```
<a id="array-fields"></a>
#### Поля массива

Существуют два поля, которые управляют «размером» массива:

* `len`: *длина* - количество предварительно выделенных и инициализированных элементов в массиве
* `cap`: *емкость* - объем пространства памяти, зарезервированный для элементов, но не инициализированный или не учитываемый как элементы. Массив может вырасти до этого размера без перераспределения. Обычно V заботится об этом поле автоматически, но бывают случаи, когда пользователь может захотеть произвести ручную оптимизацию (см. [below](#array-initialization)).

```v
mut nums := [1, 2, 3]
println(nums.len) // "3"
println(nums.cap) // "3" or greater
nums = [] // The array is now empty
println(nums.len) // "0"
```

`data` — это поле (типа `voidptr`) с адресом первого элемента. Это предназначено для кода работы с памятью на низком уровне [`unsafe`](#memory-unsafe-code).

> [!NOTE]
> Поля доступны только для чтения и не могут быть изменены пользователем.
<a id="array-initialization"></a>
#### Инициализация массива

Тип массива определяется первым элементом:

* `[1, 2, 3]` — это массив целых чисел (`[]int`).
* `['a', 'b']` — это массив строк (`[]string`).

Пользователь может явно указать тип для первого элемента: `[u8(16), 32, 64, 128]`.
Массивы V являются гомогенными (все элементы должны иметь одинаковый тип).
Это означает, что такой код, как `[1, 'a']`, не скомпилируется.

Вышеуказанная синтаксическая конструкция подходит для небольшого количества известных элементов, но для очень больших или пустых массивов существует второй синтаксис инициализации:

```v
mut a := []int{len: 10000, cap: 30000, init: 3}
```

Это создает массив из 10000 элементов `int`, все из которых инициализированы значением `3`. Пространство памяти зарезервировано для 30000 элементов. Параметры `len`, `cap` и `init` являются необязательными; `len` по умолчанию равен `0`, а `init` — значению по умолчанию для инициализации типа элемента (`0` для числового типа, `''` для `string` и т. д.). Система времени выполнения гарантирует, что емкость не будет меньше `len` (даже если явно указано меньшее значение):

```v
arr := []int{len: 5, init: -1}
// `arr == [-1, -1, -1, -1, -1]`, arr.cap == 5

// Declare an empty array:
users := []int{}
```

Задание емкости повышает производительность добавления элементов в массив, поскольку можно избежать перераспределения:

```v
mut numbers := []int{cap: 1000}
println(numbers.len) // 0
// Now appending elements won't reallocate
for i in 0 .. 1000 {
	numbers << i
}
```

> [!NOTE]
> Вышеуказанный код использует конструкцию [range `for`](#range-for).

Вы можете инициализировать массив, обращаясь к переменной `index`, которая дает индекс, как показано здесь:

```v
count := []int{len: 4, init: index}
assert count == [0, 1, 2, 3]

mut square := []int{len: 6, init: index * index}
// square == [0, 1, 4, 9, 16, 25]
```
<a id="array-types"></a>
#### Типы массивов

Массив может быть следующих типов:

| Типы         | Пример определения                  |
|--------------|--------------------------------------|
| Число        | `[]int,[]i64`                        |
| Строка       | `[]string`                           |
| Руна         | `[]rune`                             |
| Логический   | `[]bool`                             |
| Массив       | `[][]int`                            |
| Структура    | `[]MyStructName`                     |
| Канал        | `[]chan f64`                         |
| Функция      | `[]MyFunctionType` `[]fn (int) bool` |
| Интерфейс    | `[]MyInterfaceName`                  |
| Суммарный тип | `[]MySumTypeName`                   |
| Обобщенный тип | `[]T`                              |
| Карта        | `[]map[string]f64`                   |
| Перечисление | `[]MyEnumType`                       |
| Псевдоним    | `[]MyAliasTypeName`                  |
| Поток        | `[]thread int`                       |
| Ссылка       | `[]&f64`                             |
| Общий        | `[]shared MyStructType`              |
| Опциональный | `[]?f64`                         |

**Пример кода:**

Этот пример использует [Structs](#structs) и [Sum Types](#sum-types) для создания массива, который может обрабатывать элементы данных разных типов (например, Точки, Линии).

```v
struct Point {
	x int
	y int
}

struct Line {
	p1 Point
	p2 Point
}

type ObjectSumType = Line | Point

mut object_list := []ObjectSumType{}
object_list << Point{1, 1}
object_list << Line{
	p1: Point{3, 3}
	p2: Point{4, 4}
}
dump(object_list)
/*
object_list: [ObjectSumType(Point{
    x: 1
    y: 1
}), ObjectSumType(Line{
    p1: Point{
        x: 3
        y: 3
    }
    p2: Point{
        x: 4
        y: 4
    }
})]
*/
```
<a id="multidimensional-arrays"></a>
#### Многомерные массивы

Массивы могут иметь более одного измерения.

Пример двумерного массива:

```v
mut a := [][]int{len: 2, init: []int{len: 3}}
a[0][1] = 2
println(a) // [[0, 2, 0], [0, 0, 0]]
```

Пример трехмерного массива:

```v
mut a := [][][]int{len: 2, init: [][]int{len: 3, init: []int{len: 2}}}
a[0][1][1] = 2
println(a) // [[[0, 0], [0, 2], [0, 0]], [[0, 0], [0, 0], [0, 0]]]
```
<a id="array-methods"></a>
#### Методы массивов

Все массивы можно легко распечатать с помощью `println(arr)` и преобразовать в строку с помощью `s := arr.str()`.

Копирование данных из массива выполняется методом `.clone()`:

```v
nums := [1, 2, 3]
nums_copy := nums.clone()
```

Массивы могут быть эффективно отфильтрованы и отображены с помощью методов `.filter()` и `.map()`:

```v
nums := [1, 2, 3, 4, 5, 6]
even := nums.filter(it % 2 == 0)
println(even) // [2, 4, 6]
// filter can accept anonymous functions
even_fn := nums.filter(fn (x int) bool {
	return x % 2 == 0
})
println(even_fn)
```

```v
words := ['hello', 'world']
upper := words.map(it.to_upper())
println(upper) // ['HELLO', 'WORLD']
// map can also accept anonymous functions
upper_fn := words.map(fn (w string) string {
	return w.to_upper()
})
println(upper_fn) // ['HELLO', 'WORLD']
```

`it` — это встроенная переменная, которая ссылается на обрабатываемый в данный момент элемент в методах фильтрации/отображения.

Кроме того, `.any()` и `.all()` могут использоваться для удобной проверки наличия элементов, удовлетворяющих условию.

```v
nums := [1, 2, 3]
println(nums.any(it == 2)) // true
println(nums.all(it >= 2)) // false
```

Есть и другие встроенные методы для массивов:

* `a.repeat(n)` конкатенирует элементы массива `n` раз
* `a.insert(i, val)` вставляет новый элемент `val` по индексу `i` и сдвигает все последующие элементы вправо
* `a.insert(i, [3, 4, 5])` вставляет несколько элементов
* `a.prepend(val)` вставляет значение в начало, эквивалентно `a.insert(0, val)`
* `a.prepend(arr)` вставляет элементы массива `arr` в начало
* `a.trim(new_len)` обрезает длину (если `new_len < a.len`, иначе ничего не делает)
* `a.clear()` очищает массив без изменения `cap` (эквивалентно `a.trim(0)`)
* `a.delete_many(start, size)` удаляет `size` последовательных элементов начиная с индекса `start` — вызывает перераспределение
* `a.delete(index)` эквивалентно `a.delete_many(index, 1)`
* `a.delete_last()` удаляет последний элемент
* `a.first()` эквивалентно `a[0]`
* `a.last()` эквивалентно `a[a.len - 1]`
* `a.pop()` удаляет последний элемент и возвращает его
* `a.reverse()` создает новый массив с элементами `a` в обратном порядке
* `a.reverse_in_place()` меняет порядок элементов в `a` на обратный
* `a.join(joiner)` конкатенирует массив строк в одну строку, используя строку `joiner` в качестве разделителя

Смотрите все методы [array](https://modules.vlang.io/index.html#array)

Смотрите также [vlib/arrays](https://modules.vlang.io/arrays.html).

##### Сортировка массивов

Сортировка массивов всех видов очень проста и интуитивно понятна. Специальные переменные `a` и `b` используются при задании пользовательского условия сортировки.

```v
mut numbers := [1, 3, 2]
numbers.sort() // 1, 2, 3
numbers.sort(a > b) // 3, 2, 1
```

```v
struct User {
	age  int
	name string
}

mut users := [User{21, 'Bob'}, User{20, 'Zarkon'}, User{25, 'Alice'}]
users.sort(a.age < b.age) // sort by User.age int field
users.sort(a.name > b.name) // reverse sort by User.name string field
```

V также поддерживает пользовательскую сортировку через метод массива `sort_with_compare`.
Ожидает функцию сравнения, которая определит порядок сортировки.
Полезно для одновременной сортировки по нескольким полям с помощью пользовательских правил сортировки.
Приведенный ниже код сортирует массив по возрастанию по полю `name` и по убыванию по полю `age`.

```v
struct User {
	age  int
	name string
}

mut users := [User{21, 'Bob'}, User{65, 'Bob'}, User{25, 'Alice'}]

custom_sort_fn := fn (a &User, b &User) int {
	// return -1 when a comes before b
	// return 0, when both are in same order
	// return 1 when b comes before a
	if a.name == b.name {
		if a.age < b.age {
			return 1
		}
		if a.age > b.age {
			return -1
		}
		return 0
	}
	if a.name < b.name {
		return -1
	} else if a.name > b.name {
		return 1
	}
	return 0
}
users.sort_with_compare(custom_sort_fn)
```
<a id="array-slices"></a>
#### Срезы массива

Срез — это часть родительского массива. Первоначально он ссылается на элементы между двумя индексами, разделенными оператором `..`. Правый индекс должен быть больше или равен левому индексу.

Если правый индекс отсутствует, предполагается, что это длина массива. Если левый индекс отсутствует, предполагается, что это 0.

```v
nums := [0, 10, 20, 30, 40]
println(nums[1..4]) // [10, 20, 30]
println(nums[..4]) // [0, 10, 20, 30]
println(nums[1..]) // [10, 20, 30, 40]
```

В V срезы являются сами по себе массивами (они не являются отдельными типами). В результате с ними могут выполняться все операции массива. Например, их можно добавлять в массив того же типа:

```v
array_1 := [3, 5, 4, 7, 6]
mut array_2 := [0, 1]
array_2 << array_1[..3]
println(array_2) // `[0, 1, 3, 5, 4]`
```

Срез всегда создается с наименьшей возможной емкостью `cap == len` (см. [`cap` above](#array-initialization)) независимо от емкости или длины родительского массива. В результате он немедленно перераспределяется и копируется в другое место в памяти при увеличении размера, становясь независимым от родительского массива (*копирование при росте*). В частности, добавление элементов в срез не изменяет родительский массив:

```v
mut a := [0, 1, 2, 3, 4, 5]

// Create a slice, that reuses the *same memory* as the parent array
// initially, without doing a new allocation:
mut b := unsafe { a[2..4] } // the contents of `b`, reuses the memory, used by the contents of `a`.

b[0] = 7 // Note that `b[0]` and `a[2]` refer to *the same element* in memory.
println(a) // `[0, 1, 7, 3, 4, 5]` - changing `b[0]` above, changed `a[2]` too.

// the content of `b` will get reallocated, to have room for the `9` element:
b << 9
// The content of `b`, is now reallocated, and fully independent from the content of `a`.

println(a) // `[0, 1, 7, 3, 4, 5]` - no change, since the content of `b` was reallocated,
// to a larger block, before the appending.

println(b) // `[7, 3, 9]` - the contents of `b`, after the reallocation, and appending of the `9`.
```

Добавление в родительский массив может или не может сделать его независимым от дочерних срезов. Поведение зависит от *емкости родителя* и является предсказуемым:

```v
mut a := []int{len: 5, cap: 6, init: 2}
mut b := unsafe { a[1..4] } // the contents of `b` uses part of the same memory, that is used by `a` too

a << 3
// still no reallocation of `a`, since `a.len` still fits in `a.cap`
b[2] = 13 // `a[3]` is modified, through the slice `b`.

a << 4
// the content of `a` has been reallocated now, and is independent from `b` (`cap` was exceeded by `len`)
b[1] = 3 // no change in `a`

println(a) // `[2, 2, 2, 13, 2, 3, 4]`
println(b) // `[2, 3, 13]`
```

Вы можете вызвать .clone() на срезе, если вы *хотите* иметь независимую копию сразу:

```v
mut a := [0, 1, 2, 3, 4, 5]
mut b := a[2..4].clone()
b[0] = 7 // Note: `b[0]` is NOT referring to `a[2]`, as it would have been, without the `.clone()`
println(a) // [0, 1, 2, 3, 4, 5]
println(b) // [7, 3]
```

##### Срезы с отрицательными индексами

V поддерживает срезы массивов и строк с отрицательными индексами.
Отрицательная индексация начинается с конца массива к началу,
например, `-3` равно `array.len - 3`.
Отрицательные срезы имеют другой синтаксис от обычных срезов, т.е. вам нужно
добавить `gate` между именем массива и квадратной скобкой: `a#[..-3]`.
`gate` указывает, что это другой тип среза, и помните, что
результат «заблокирован» внутри массива.
Возвращенный срез всегда является допустимым массивом, хотя он может быть пустым:

```v
a := [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
println(a#[-3..]) // [7, 8, 9]
println(a#[-20..]) // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
println(a#[-20..-8]) // [0, 1]
println(a#[..-3]) // [0, 1, 2, 3, 4, 5, 6]

// empty arrays
println(a#[-20..-10]) // []
println(a#[20..10]) // []
println(a#[20..30]) // []
```
<a id="array-method-chaining"></a>
#### Цепочки вызовов методов массива

Вы можете соединить вызовы методов массива, таких как `.filter()` и `.map()`, и использовать
встроенную переменную `it`, чтобы достичь классической функциональной парадигмы `map/filter`:

```v
// using filter, map and negatives array slices
files := ['pippo.jpg', '01.bmp', '_v.txt', 'img_02.jpg', 'img_01.JPG']
filtered := files.filter(it#[-4..].to_lower() == '.jpg').map(it.to_upper())
// ['PIPPO.JPG', 'IMG_02.JPG', 'IMG_01.JPG']
```
<a id="fixed-size-arrays"></a>
### Массивы фиксированного размера

V также поддерживает массивы фиксированного размера. В отличие от обычных массивов, их длина является постоянной. Вы не можете добавлять к ним элементы, ни уменьшать их.
Вы можете только изменять их элементы на месте.

Однако доступ к элементам массивов фиксированного размера более эффективен, они требуют меньше памяти, чем обычные массивы, и в отличие от обычных массивов, их данные находятся в стеке, поэтому вы можете захотеть использовать их в качестве буферов, если
вы не хотите дополнительных выделений в куче.

Большинство методов определены для работы с обычными массивами, а не с массивами фиксированного размера.
Вы можете преобразовать массив фиксированного размера в обычный массив с помощью среза:

```v
mut fnums := [3]int{} // fnums is a fixed size array with 3 elements.
fnums[0] = 1
fnums[1] = 10
fnums[2] = 100
println(fnums) // => [1, 10, 100]
println(typeof(fnums).name) // => [3]int

fnums2 := [1, 10, 100]! // short init syntax that does the same (the syntax will probably change)

anums := fnums[..] // same as `anums := fnums[0..fnums.len]`
println(anums) // => [1, 10, 100]
println(typeof(anums).name) // => []int
```

Обратите внимание, что срез приведет к копированию данных массива фиксированного размера в
вновь созданный обычный массив.
<a id="maps"></a>
### Карты

```v
mut m := map[string]int{} // a map with `string` keys and `int` values
m['one'] = 1
m['two'] = 2
println(m['one']) // "1"
println(m['bad_key']) // "0"
println('bad_key' in m) // Use `in` to detect whether such key exists
println(m.keys()) // ['one', 'two']
m.delete('two')
```

Карты могут иметь ключи типа string, rune, целое число, число с плавающей запятой или voidptr.

Целую карту можно инициализировать с помощью этого краткого синтаксиса:

```v
numbers := {
	'one': 1
	'two': 2
}
println(numbers)
```

Если ключ не найден, по умолчанию возвращается нулевое значение:

```v
sm := {
	'abc': 'xyz'
}
val := sm['bad_key']
println(val) // ''
```

```v
intm := {
	1: 1234
	2: 5678
}
s := intm[3]
println(s) // 0
```

Также возможно использовать блок `or {}` для обработки отсутствующих ключей:

```v
mm := map[string]int{}
val := mm['bad_key'] or { panic('key not found') }
```

Вы также можете проверить, присутствует ли ключ, и получить его значение, если он присутствует, за один раз:

```v
m := {
	'abc': 'def'
}
if v := m['abc'] {
	println('the map value for that key is: ${v}')
}
```

Та же проверка опциональности применяется и к массивам:

```v
arr := [1, 2, 3]
large_index := 999
val := arr[large_index] or { panic('out of bounds') }
println(val)
// you can also do this, if you want to *propagate* the access error:
val2 := arr[333]!
println(val2)
```

V также поддерживает вложенные карты:

```v
mut m := map[string]map[string]int{}
m['greet'] = {
	'Hello': 1
}
m['place'] = {
	'world': 2
}
m['code']['orange'] = 123
print(m)
```

Карты упорядочены по вставке, как словари в Python. Порядок является гарантированной особенностью языка. Это может измениться в будущем.

Смотрите все методы
[map](https://modules.vlang.io/builtin.html#map)
и
[maps](https://modules.vlang.io/maps.html).
<a id="map-update-syntax"></a>
### Синтаксис обновления карты

Как и в случае со структурами, V позволяет инициализировать карту с обновлением, применяемым поверх другой карты:

```v
const base_map = {
	'a': 4
	'b': 5
}

foo := {
	...base_map
	'b': 88
	'c': 99
}

println(foo) // {'a': 4, 'b': 88, 'c': 99}
```

Это функционально эквивалентно клонированию карты и ее обновлению, за исключением того, что
вам не нужно объявлять изменяемую переменную:

```v failcompile
// same as above (except mutable)
mut foo := base_map.clone()
foo['b'] = 88
foo['c'] = 99
```
<a id="module-imports"></a>
## Импорт модулей

Для получения информации о создании модуля см. [Modules](#modules).

Модули можно импортировать с помощью ключевого слова `import`:

```v
import os

fn main() {
	// read text from stdin
	name := os.input('Enter your name: ')
	println('Hello, ${name}!')
}
```

Эта программа может использовать любые публичные определения из модуля `os`, такие как функция `input`. Список распространённых модулей и их публичных символов можно найти в документации по [standard library](https://modules.vlang.io/).

По умолчанию необходимо указывать префикс модуля при каждом вызове внешней функции. Поначалу это может показаться избыточным, но делает код значительно более читаемым и понятным — всегда ясно, какая функция из какого модуля вызывается. Это особенно полезно в больших кодовых базах.

Циклические импорты модулей запрещены, как и в Go.
<a id="selective-imports"></a>
### Избирательный импорт

Вы также можете импортировать конкретные функции и типы из модулей напрямую:

```v
import os { input }

fn main() {
	// read text from stdin
	name := input('Enter your name: ')
	println('Hello, ${name}!')
}
```

> [!NOTE]
> При этом сам модуль тоже будет импортирован. Кроме того, это не допускается для
> констант — они всегда должны иметь префикс.

Можно импортировать несколько конкретных символов одновременно:

```v
import os { input, user_os }

name := input('Enter your name: ')
println('Name: ${name}')
current_os := user_os()
println('Your OS is ${current_os}.')
```
<a id="module-hierarchy"></a>
### Иерархия модулей

> [!NOTE]
> Этот раздел применим, когда файлы .v не находятся в корневой директории проекта.

Имена модулей в файлах .v должны совпадать с именем их директории.

Файл `./abc/source.v` должен начинаться с `module abc`. Все файлы .v в этой директории
принадлежат одному модулю `abc`. Они также должны начинаться с `module abc`.

Если у вас есть `abc/def/`, и файлы .v в обеих папках, вы можете выполнить `import abc`, но вам также потребуется `import abc.def`, чтобы получить доступ к символам в подпапке. Это независимое действие.

Оператор `module name` не повторяет иерархию директорий, а указывает только свою директорию.
Таким образом, в `abc/def/source.v` первой строкой будет `module def`, а не `module abc.def`.

Операторы `import module_name` должны соответствовать файловой иерархии, вы не можете выполнить `import def`, только
`abc.def`

Для обращения к символу модуля, такому как функция или константа, в качестве префикса достаточно указать только имя модуля:

```v ignore
module def

// func is a dummy example function.
pub fn func() {
	println('func')
}
```

вызов будет выглядеть так:

```v ignore
module main

import def

fn main() {
	def.func()
}
```

Функция, расположенная в `abc/def/source.v`, вызывается через `def.func()`, а не `abc.def.func()`

Это всегда подразумевает *одинарный префикс*, независимо от глубины вложенности модулей/подмодулей. Такое поведение «сплющивает»
иерархию модулей/подмодулей. Если у вас есть два модуля с одинаковым именем в разных
директориях, следует использовать псевдонимы импорта модулей (см. ниже).

<a id="module-import-aliasing"></a>
### Псевдонимы импорта модулей

Любому импортированному имени модуля можно дать псевдоним с помощью ключевого слова `as`:

> [!NOTE]
> Этот пример не будет компилироваться, если вы не создали `mymod/sha256/somename.v`
> (имена подмодулей определяются их путём, а не именами файлов .v в них).

```v failcompile
import crypto.sha256
import mymod.sha256 as mysha256

fn main() {
	v_hash := sha256.sum('hi'.bytes()).hex()
	my_hash := mysha256.sum('hi'.bytes()).hex()
	assert my_hash == v_hash
}
```

Вы не можете дать псевдоним импортированной функции или типу.
Однако вы _можете_ повторно объявить тип.

```v
import time
import math

type MyTime = time.Time

fn (mut t MyTime) century() int {
	return int(1.0 + math.trunc(f64(t.year) * 0.009999794661191))
}

fn main() {
	mut my_time := MyTime{
		year:  2020
		month: 12
		day:   25
	}
	println(time.new(my_time).utc_string())
	println('Century: ${my_time.century()}')
}
```
<a id="statements--expressions"></a>
## Операторы и выражения
<a id="if"></a>
### If

```v
a := 10
b := 20
if a < b {
	println('${a} < ${b}')
} else if a > b {
	println('${a} > ${b}')
} else {
	println('${a} == ${b}')
}
```

Операторы `if` довольно просты и аналогичны большинству других языков.
В отличие от других C-подобных языков,
условие не заключается в круглые скобки, а фигурные скобки всегда обязательны.
<a id="if-expressions"></a>
#### Выражения `if`
В отличие от C, V не имеет тернарного оператора, который позволил бы писать: `x = c ? 1 : 2`.
Вместо этого есть несколько более многословная, но и более понятная для чтения возможность использовать `if` как
выражение. Прямой перевод конструкции выше на V, при условии, что `c` является
булевым условием, будет следующим: `x = if c { 1 } else { 2 }`.

Вот ещё один пример:
```v
num := 777
s := if num % 2 == 0 { 'even' } else { 'odd' }
println(s)
// "odd"
```

Вы можете использовать несколько операторов в каждой ветви выражения `if`, за которыми следует конечное
значение, которое станет значением всего выражения `if`, когда выполняется данная ветвь:
```v
n := arguments().len
x := if n > 2 {
	dump(arguments())
	42
} else {
	println('something else')
	100
}
dump(x)
```
<a id="if-unwrapping"></a>
#### Распаковка `if`
Везде, где вы можете использовать `or {}`, вы также можете использовать «распаковку через if». Это привязывает распакованное значение
выражения к переменной, когда это выражение не является ни none, ни ошибкой.

```v
m := {
	'foo': 'bar'
}

// handle missing keys
if v := m['foo'] {
	println(v) // bar
} else {
	println('not found')
}
```

```v
fn res() !int {
	return 42
}

// functions that return a result type
if v := res() {
	println(v)
}
```

```v
struct User {
	name string
}

arr := [User{'John'}]

// if unwrapping with assignment of a variable
u_name := if v := arr[0] {
	v.name
} else {
	'Unnamed'
}
println(u_name) // John
```
<a id="type-checks-and-casts"></a>
#### Проверка и приведение типов

Вы можете проверить текущий тип объединённого типа с помощью `is` и его отрицательной формы `!is`.

Вы можете сделать это как в `if`:

```v cgen
struct Abc {
	val string
}

struct Xyz {
	foo string
}

type Alphabet = Abc | Xyz

x := Alphabet(Abc{'test'}) // sum type
if x is Abc {
	// x is automatically cast to Abc and can be used here
	println(x)
}
if x !is Abc {
	println('Not Abc')
}
```

так и с помощью `match`:

```v oksyntax
match x {
	Abc {
		// x is automatically cast to Abc and can be used here
		println(x)
	}
	Xyz {
		// x is automatically cast to Xyz and can be used here
		println(x)
	}
}
```

Это работает также и с полями структур:

```v
struct MyStruct {
	x int
}

struct MyStruct2 {
	y string
}

type MySumType = MyStruct | MyStruct2

struct Abc {
	bar MySumType
}

x := Abc{
	bar: MyStruct{123} // MyStruct will be converted to MySumType type automatically
}
if x.bar is MyStruct {
	// x.bar is automatically cast
	println(x.bar)
} else if x.bar is MyStruct2 {
	new_var := x.bar as MyStruct2
	// ... or you can use `as` to create a type cast an alias manually:
	println(new_var)
}
match x.bar {
	MyStruct {
		// x.bar is automatically cast
		println(x.bar)
	}
	else {}
}
```

Изменяемые переменные могут меняться, и приведение типа было бы небезопасным.
Однако иногда полезно выполнить приведение типа, несмотря на изменяемость.
В таких случаях разработчик должен пометить выражение ключевым словом `mut`,
чтобы сообщить компилятору, что он понимает, что делает.

Это работает так:

```v oksyntax
mut x := MySumType(MyStruct{123})
if mut x is MyStruct {
	// x is cast to MyStruct even if it's mutable
	// without the mut keyword that wouldn't work
	println(x)
}
// same with match
match mut x {
	MyStruct {
		// x is cast to MyStruct even if it's mutable
		// without the mut keyword that wouldn't work
		println(x)
	}
}
```
<a id="match"></a>
### Match

```v
os := 'windows'
print('V is running on ')
match os {
	'darwin' { println('macOS.') }
	'linux' { println('Linux.') }
	else { println(os) }
}
```

Оператор match является более короткой записью последовательности операторов `if - else`.
Когда находится подходящая ветвь, выполняется следующий блок операторов.
Ветвь else выполняется, когда ни одна из других ветвей не подходит.

```v
number := 2
s := match number {
	1 { 'one' }
	2 { 'two' }
	else { 'many' }
}
```

Оператор match также может использоваться как альтернатива `if - else if - else`:

```v
match true {
	2 > 4 { println('if') }
	3 == 4 { println('else if') }
	2 == 2 { println('else if2') }
	else { println('else') }
}
// 'else if2' should be printed
```

или как альтернатива `unless`: [unless Ruby](https://www.tutorialspoint.com/ruby/ruby_if_else.htm)

```v
match false {
	2 > 4 { println('if') }
	3 == 4 { println('else if') }
	2 == 2 { println('else if2') }
	else { println('else') }
}
// 'if' should be printed
```

Выражение match возвращает значение конечного выражения из подходящей ветви.

```v
enum Color {
	red
	blue
	green
}

fn is_red_or_blue(c Color) bool {
	return match c {
		.red, .blue { true } // comma can be used to test multiple values
		.green { false }
	}
}
```

Оператор match также может использоваться для ветвления по вариантам `enum`
с помощью сокращённого синтаксиса `.variant_here`. Ветвь `else` не допускается,
когда все ветви являются исчерпывающими.

```v
c := `v`
typ := match c {
	`0`...`9` { 'digit' }
	`A`...`Z` { 'uppercase' }
	`a`...`z` { 'lowercase' }
	else { 'other' }
}
println(typ)
// 'lowercase'
```

Оператор match также может сопоставлять типы вариантов `sumtype`. Обратите внимание,
что в этом случае сопоставление является исчерпывающим, так как все типы вариантов упомянуты
явно, поэтому необходимость в ветви `else{}` отсутствует.

```v nofmt
struct Dog {}
struct Cat {}
struct Veasel {}
type Animal = Dog | Cat | Veasel
a := Animal(Veasel{})
match a {
	Dog { println('Bay') }
	Cat { println('Meow') }
	Veasel { println('Vrrrrr-eeee') } // see: https://www.youtube.com/watch?v=qTJEDyj2N0Q
}
```

Вы также можете использовать диапазоны в качестве шаблонов `match`. Если значение попадает в диапазон
ветви, эта ветвь будет выполнена.

Обратите внимание, что диапазоны используют `...` (три точки), а не `..` (две точки). Это
потому, что диапазон *включает* последний элемент, а не исключает его
(как это делают диапазоны `..`). Использование `..` в ветви match вызовет ошибку.

```v
const start = 1

const end = 10

c := 2
num := match c {
	start...end {
		1000
	}
	else {
		0
	}
}
println(num)
// 1000
```

В выражениях ветвей диапазонов также можно использовать константы.

> [!NOTE]
> `match` как выражение не может использоваться в цикле `for` и операторах `if`.
<a id="in-operator"></a>
### Оператор in

`in` позволяет проверить, содержит ли массив или карта элемент.
Для проверки противоположного условия используйте `!in`.

```v
nums := [1, 2, 3]
println(1 in nums) // true
println(4 !in nums) // true
```

> [!NOTE]
> `in` проверяет, содержит ли карта ключ, а не значение.

```v
m := {
	'one': 1
	'two': 2
}

println('one' in m) // true
println('three' !in m) // true
```

Он также полезен для написания более ясных и компактных булевых выражений:

```v
enum Token {
	plus
	minus
	div
	mult
}

struct Parser {
	token Token
}

parser := Parser{}
if parser.token == .plus || parser.token == .minus || parser.token == .div || parser.token == .mult {
	// ...
}
if parser.token in [.plus, .minus, .div, .mult] {
	// ...
}
```

V опимизирует такие выражения,
поэтому оба оператора `if` выше генерируют одинаковый машинный код и не создают массивов.
<a id="for-loop"></a>
### Цикл for

V имеет единственное ключевое слово для циклов: `for` с несколькими формами.
<a id="forin"></a>
#### `for`/`in`

Это самая распространённая форма. Вы можете использовать её с массивом, картой или
числовым диапазоном.

##### `for` для массивов

```v
numbers := [1, 2, 3, 4, 5]
for num in numbers {
	println(num)
}
names := ['Sam', 'Peter']
for i, name in names {
	println('${i}) ${name}')
	// Output: 0) Sam
	//         1) Peter
}
```

Форма `for value in arr` используется для перебора элементов массива.
Если необходим индекс, можно использовать альтернативную форму `for index, value in arr`.

Обратите внимание, что значение доступно только для чтения.
Если вам нужно изменять массив во время цикла, необходимо объявить элемент как изменяемый:

```v
mut numbers := [0, 1, 2]
for mut num in numbers {
	num++
}
println(numbers) // [1, 2, 3]
```

По умолчанию элементы массива копируются по значению; если вам нужно получать элементы по
ссылке, используйте `&` перед массивом, по которому вы хотите итерировать:

```v
struct User {
	name string
}

users := [User{
	name: 'someuserwow99'
}, User{
	name: 'visgod'
}]
// note `&users`, this is how a reference to the elements of the array is received
for user in &users {
	// some operations with `user`
}
```

То же самое относится к картам.

Когда идентификатор является одиночным подчёркиванием, он игнорируется.

##### Пользовательские итераторы

Типы, реализующие метод `next`, возвращающий `Option`, могут итерироваться
с помощью цикла `for`.

```v
struct SquareIterator {
	arr []int
mut:
	idx int
}

fn (mut iter SquareIterator) next() ?int {
	if iter.idx >= iter.arr.len {
		return none
	}
	defer {
		iter.idx++
	}
	return iter.arr[iter.idx] * iter.arr[iter.idx]
}

nums := [1, 2, 3, 4, 5]
iter := SquareIterator{
	arr: nums
}
for squared in iter {
	println(squared)
}
```

Код выше выведет:

```
1
4
9
16
25
```

##### `for` для карт

```v
m := {
	'one': 1
	'two': 2
}
for key, value in m {
	println('${key} -> ${value}')
	// Output: one -> 1
	//         two -> 2
}
```

И ключ, и значение можно игнорировать, используя одиночное подчёркивание в качестве идентификатора.

```v
m := {
	'one': 1
	'two': 2
}
// iterate over keys
for key, _ in m {
	println(key)
	// Output: one
	//         two
}
// iterate over values
for _, value in m {
	println(value)
	// Output: 1
	//         2
}
```

##### `for` с диапазоном

```v
// Prints '01234'
for i in 0 .. 5 {
	print(i)
}
```

`low..high` означает *исключающий* диапазон, который представляет все значения
от `low` *включительно* до `high` *не включительно*.

> [!NOTE]
> Эта исключающая запись диапазона и нумерация с нуля следуют принципам
логической согласованности и уменьшения ошибок. Как описывает Эдсгер В. Дейкстра в
статье «Почему нумерация должна начинаться с нуля»
([EWD831](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD08xx/EWD831.html)),
нумерация с нуля выравнивает индекс с предыдущими элементами последовательности,
упрощая обработку и минимизируя ошибки, особенно при работе с соседними подпоследовательностями.
Этот логичный и эффективный подход формирует дизайн нашего языка, делая акцент на ясности
и уменьшении путаницы в программировании.
<a id="condition-for"></a>
#### Условный `for`

```v
mut sum := 0
mut i := 0
for i <= 100 {
	sum += i
	i++
}
println(sum) // "5050"
```

Эта форма цикла аналогична циклам `while` в других языках.
Цикл прекращает итерацию, когда булево условие принимает значение ложь.
Снова нет круглых скобок вокруг условия, а фигурные скобки всегда обязательны.
<a id="bare-for"></a>
#### Безусловный `for`

```v
mut num := 0
for {
	num += 2
	if num >= 10 {
		break
	}
}
println(num) // "10"
```

Условие можно опустить, что приведёт к бесконечному циклу.
<a id="c-for"></a>
#### C-подобный `for`

```v
for i := 0; i < 10; i += 2 {
	// Don't print 6
	if i == 6 {
		continue
	}
	println(i)
}
```

Наконец, есть традиционный цикл `for` в стиле C. Он безопаснее, чем форма `while`,
поскольку при последней легко забыть обновить счётчик и застрять
в бесконечном цикле.

Здесь `i` не нужно объявлять с помощью `mut`, так как оно всегда будет изменяемым по определению.
<a id="labelled-break-continue"></a>
#### Метки break и continue

Операторы `break` и `continue` по умолчанию управляют внутренним циклом `for`.
Вы также можете использовать `break` и `continue` с последующим именем метки для обращения к внешнему циклу `for`:

```v
outer: for i := 4; true; i++ {
	println(i)
	for {
		if i < 7 {
			continue outer
		} else {
			break outer
		}
	}
}
```

Метка должна непосредственно предшествовать внешнему циклу.
Код выше выведет:

```
4
5
6
7
```
<a id="defer"></a>
### Defer

Оператор `defer {}` откладывает выполнение блока операторов
до завершения окружающей области видимости. Это удобная возможность,
позволяющая группировать связанные действия (получение доступа к ресурсу
и очистку/освобождение после завершения) в одном месте, вместо
того чтобы разносить их по множеству потенциально удалённых строк кода.

```v
import os

fn read_log() ! {
	mut ok := false
	mut f := os.open('log.txt')!
	defer { f.close() }
	// ...
	if !ok {
		// ...
		// defer statement will be called here, the file will be closed
		return
	}
	// ...
	// defer statement will be called here too, the file will be closed
}
```

Если функция возвращает значение, блок `defer` выполняется *после* вычисления
выражения return:

```v
import os

enum State {
	normal
	write_log
	return_error
}

// write log file and return number of bytes written

fn write_log(s State) !int {
	mut f := os.create('log.txt')!
	defer {
		f.close()
	}
	if s == .write_log {
		// `f.close()` will be called after `f.write()` has been
		// executed, but before `write_log()` finally returns the
		// number of bytes written to `main()`
		return f.writeln('This is a log file')
	} else if s == .return_error {
		// the file will be closed after the `error()` function
		// has returned - so the error message will still report
		// it as open
		return error('nothing written; file open: ${f.is_opened}')
	}
	// the file will be closed here, too
	return 0
}

fn main() {
	n := write_log(.return_error) or {
		println('Error: ${err}')
		0
	}
	println('${n} bytes written')
}
```

Для доступа к результату функции внутри блока `defer` можно использовать выражение `$res()`.
`$res()` используется только при возврате одного значения, тогда как при множественном возврате
используется параметризованное `$res(idx)`.

```v ignore
fn (mut app App) auth_middleware() bool {
	defer {
		if !$res() {
			app.response.status_code = 401
			app.response.body = 'Unauthorized'
		}
	}
	header := app.get_header('Authorization')
	if header == '' {
		return false
	}
	return true
}

fn (mut app App) auth_with_user_middleware() (bool, string) {
	defer {
		if !$res(0) {
			app.response.status_code = 401
			app.response.body = 'Unauthorized'
		} else {
			app.user = $res(1)
		}
	}
	header := app.get_header('Authorization')
	if header == '' {
		return false, ''
	}
	return true, 'TestUser'
}
```
<a id="defer-in-loop-scopes"></a>
#### defer в областях видимости циклов:
Defer можно использовать и внутри циклов, при этом отложенный оператор будет выполняться один раз для каждой
итерации. В одной области видимости может быть несколько операторов defer, в этом случае они
выполняются в обратном порядке их появления в исходном коде:
```v
fn main() {
	defer { println('Program finish.') }
	println('Loop start.')
	for i in 1 .. 4 {
		defer { println('Deferred execution for ${i}. Defer 1.') }
		defer { println('Deferred execution for ${i}. Defer 2.') }
		defer { println('Deferred execution for ${i}. Defer 3.') }
		println('Loop iteration: ${i}')
	}
	println('Loop done.')
}
```

Пример выше выведет следующее:
```txt
Loop start.
Loop iteration: 1
Deferred execution for 1. Defer 3.
Deferred execution for 1. Defer 2.
Deferred execution for 1. Defer 1.
Loop iteration: 2
Deferred execution for 2. Defer 3.
Deferred execution for 2. Defer 2.
Deferred execution for 2. Defer 1.
Loop iteration: 3
Deferred execution for 3. Defer 3.
Deferred execution for 3. Defer 2.
Deferred execution for 3. Defer 1.
Loop done.
Program finish.
```
<a id="deferfn"></a>
#### defer(fn) {}

Обратите внимание, что в большинстве примеров выше оператор `defer{}` находился непосредственно внутри
области видимости функции, поэтому выполнялся при возврате из самой функции. Иногда вам
нужно отложить выполнение оператора до самого конца функции (как выше), даже
если вы находитесь во внутренней области видимости (глубоко внутри `if` или `for`).

Для этих более редких случаев вы можете использовать: `defer(fn) {}` вместо простого `defer {}`.
<a id="goto"></a>
### Goto

V допускает безусловный переход к метке с помощью `goto`. Имя метки должно находиться
внутри той же функции, что и оператор `goto`. Программа может выполнить `goto` на метку за пределами
или глубже текущей области видимости. `goto` позволяет перепрыгивать инициализацию переменной или
возвращаться к коду, который обращается к уже освобождённой памяти, поэтому он требует
`unsafe`.

```v ignore
if x {
	// ...
	if y {
		unsafe {
			goto my_label
		}
	}
	// ...
}
my_label:
```

Следует избегать использования `goto`, особенно когда вместо него можно использовать `for`.
[Labelled break/continue](#labelled-break--continue) можно использовать для выхода из
вложенного цикла, и они не нарушают безопасность памяти.
<a id="structs"></a>
## Структуры

```v
struct Point {
	x int
	y int
}

mut p := Point{
	x: 10
	y: 20
}
println(p.x) // Struct fields are accessed using a dot
// Alternative literal syntax
p = Point{10, 20}
assert p.x == 10
```

Поля структуры могут повторно использовать зарезервированные ключевые слова:

```v
struct Employee {
	type string
	name string
}

employee := Employee{
	type: 'FTE'
	name: 'John Doe'
}
println(employee.type)
```
<a id="heap-structs"></a>
### Структуры в куче

Структуры выделяются в стеке. Чтобы выделить структуру в куче
и получить [reference](#references) на неё, используйте префикс `&`:

```v
struct Point {
	x int
	y int
}

p := &Point{10, 10}
// References have the same syntax for accessing fields
println(p.x)
```

Тип `p` — `&Point`. Это [reference](#references) к `Point`.
Ссылки аналогичны указателям в Go и ссылкам в C++.

```v
struct Foo {
mut:
	x int
}

fa := Foo{1}
mut a := fa
a.x = 2
assert fa.x == 1
assert a.x == 2

// fb := Foo{ 1 }
// mut b := &fb  // error: `fb` is immutable, cannot have a mutable reference to it
// b.x = 2

mut fc := Foo{1}
mut c := &fc
c.x = 2
assert fc.x == 2
assert c.x == 2
println(fc) // Foo{ x: 2 }
println(c) // &Foo{ x: 2 } // Note `&` prefixed.
```

см. также [Stack and Heap](#stack-and-heap)
<a id="default-field-values"></a>
### Значения полей по умолчанию

```v
struct Foo {
	n   int    // n is 0 by default
	s   string // s is '' by default
	a   []int  // a is `[]int{}` by default
	pos int = -1 // custom default value
}
```

Все поля структуры по умолчанию обнуляются при создании структуры.
Поля типа массив и карта выделяются памятью.
В случае ссылочных значений см. [here](#structs-with-reference-fields).

Также возможно определить пользовательские значения по умолчанию.
<a id="required-fields"></a>
### Обязательные поля

```v
struct Foo {
	n int @[required]
}
```

Вы можете пометить поле структуры атрибутом `[required]` [attribute](#attributes), чтобы указать V, что
это поле должно быть инициализировано при создании экземпляра структуры.

Этот пример не скомпилируется, поскольку поле `n` не инициализировано явно:

```v failcompile
_ = Foo{}
```

<a id='short-struct-initialization-syntax'></a>
<a id="short-struct-literal-syntax"></a>
### Краткий синтаксис литерала структуры

```v
struct Point {
	x int
	y int
}

mut p := Point{
	x: 10
	y: 20
}
p = Point{
	x: 30
	y: 4
}
assert p.y == 4
//
// array: first element defines type of array
points := [Point{10, 20}, Point{20, 30}, Point{40, 50}]
println(points) // [Point{x: 10, y: 20}, Point{x: 20, y: 30}, Point{x: 40,y: 50}]
```

Опускание имени структуры также работает при возврате литерала структуры или передаче его
в качестве аргумента функции.
<a id="struct-update-syntax"></a>
### Синтаксис обновления структуры

V упрощает возврат изменённой версии объекта:

```v
struct User {
	name          string
	age           int
	is_registered bool
}

fn register(u User) User {
	return User{
		...u
		is_registered: true
	}
}

mut user := User{
	name: 'abc'
	age:  23
}
user = register(user)
println(user)
```
<a id="trailing-struct-literal-arguments"></a>
### Хвостовые литеральные аргументы структуры

V не имеет аргументов функций по умолчанию или именованных аргументов, для этого вместо этого
можно использовать синтаксис хвостового литерала структуры:

```v
@[params]
struct ButtonConfig {
	text        string
	is_disabled bool
	width       int = 70
	height      int = 20
}

struct Button {
	text   string
	width  int
	height int
}

fn new_button(c ButtonConfig) &Button {
	return &Button{
		width:  c.width
		height: c.height
		text:   c.text
	}
}

button := new_button(text: 'Click me', width: 100)
// the height is unset, so it's the default value
assert button.height == 20
```

Как видно, имя структуры и фигурные скобки можно опустить, вместо:

```v oksyntax nofmt
new_button(ButtonConfig{text:'Click me', width:100})
```

Это работает только для функций, принимающих структуру в качестве последнего аргумента.

> [!NOTE]
> Обратите внимание, что тег `[params]` используется, чтобы указать V, что параметр структуры
> в конце может быть опущен *полностью*, чтобы вы могли писать `button := new_button()`.
> Без него вы должны указать *хотя бы одно* имя поля, даже если оно
> имеет значение по умолчанию, иначе компилятор выдаст сообщение об ошибке,
> при вызове функции без параметров:
> `error: expected 1 arguments, but got 0`.
<a id="access-modifiers"></a>
### Модификаторы доступа

Поля структуры по умолчанию являются приватными и неизменяемыми (что делает структуры также неизменяемыми).
Их модификаторы доступа могут быть изменены с помощью
`pub` и `mut`. Всего существует 5 возможных вариантов:

```v
struct Foo {
	a int // private immutable (default)
mut:
	b int // private mutable
	c int // (you can list multiple fields with the same access modifier)
pub:
	d int // public immutable (readonly)
pub mut:
	e int // public, but mutable only in parent module
__global:
	// (not recommended to use, that's why the 'global' keyword starts with __)
	f int // public and mutable both inside and outside parent module
}
```

Приватные поля доступны только внутри того же [module](#modules), любая попытка
напрямую обратиться к ним из другого модуля вызовет ошибку компиляции.
Публичные неизменяемые поля доступны для чтения везде.
<a id="anonymous-structs"></a>
### Анонимные структуры

V поддерживает анонимные структуры: структуры, которые не обязательно объявлять отдельно
с именем структуры.

```v
struct Book {
	author struct {
		name string
		age  int
	}

	title string
}

book := Book{
	author: struct {
		name: 'Samantha Black'
		age:  24
	}
}
assert book.author.name == 'Samantha Black'
assert book.author.age == 24
```
<a id="static-type-methods"></a>
### Статические методы типов

V теперь поддерживает статические методы типов, такие как `User.new()`. Они определяются для структуры через
`fn [Имя типа].[имя функции]` и позволяют организовать все функции, связанные со структурой:

```v oksyntax
struct User {}

fn User.new() User {
	return User{}
}

user := User.new()
```

Это альтернатива фабричным функциям, таким как `fn new_user() User {}`, и её следует использовать
вместо них.

> [!NOTE]
> Обратите внимание, что это не конструкторы, а простые функции. V не имеет конструкторов или
> классов.
<a id="noinit-structs"></a>
### Структуры с атрибутом `[noinit]`

V поддерживает структуры с атрибутом `[noinit]`, которые являются структурами, которые не могут быть инициализированы вне модуля
в котором они определены. Они предназначены либо для внутреннего использования, либо могут использоваться снаружи
через _фабричные функции_.

Для примера рассмотрим следующий исходный код в каталоге `sample`:

```v oksyntax
module sample

@[noinit]
pub struct Information {
pub:
	data string
}

pub fn new_information(data string) !Information {
	if data.len == 0 || data.len > 100 {
		return error('data must be between 1 and 100 characters')
	}
	return Information{
		data: data
	}
}
```

Обратите внимание, что `new_information` — это _фабричная_ функция. Теперь, когда мы хотим использовать эту структуру
вне модуля:

```v okfmt
import sample

fn main() {
	// This doesn't work when the [noinit] attribute is present:
	// info := sample.Information{
	// 	data: 'Sample information.'
	// }

	// Use this instead:
	info := sample.new_information('Sample information.')!

	println(info)
}
```
<a id="methods"></a>
### Методы

```v
struct User {
	age int
}

fn (u User) can_register() bool {
	return u.age > 16
}

user := User{
	age: 10
}
println(user.can_register()) // "false"
user2 := User{
	age: 20
}
println(user2.can_register()) // "true"
```

V не имеет классов, но вы можете определять методы для типов.
Метод — это функция со специальным аргументом-получателем.
Получатель присутствует в собственном списке аргументов между ключевым словом `fn` и именем метода.
Методы должны находиться в том же модуле, что и тип получателя.

В этом примере метод `can_register` имеет получатель типа `User` с именем `u`.
Принято не использовать имена получателей вроде `self` или `this`,
а короткое, предпочтительно в одну букву, имя.
<a id="embedded-structs"></a>
### Встраиваемые структуры

V поддерживает встраиваемые структуры.

```v
struct Size {
mut:
	width  int
	height int
}

fn (s &Size) area() int {
	return s.width * s.height
}

struct Button {
	Size
	title string
}
```

При встраивании структура `Button` автоматически получит все поля и методы из
структуры `Size`, что позволяет вам делать следующее:

```v oksyntax
mut button := Button{
	title:  'Click me'
	height: 2
}

button.width = 3
assert button.area() == 6
assert button.Size.area() == 6
print(button)
```

вывод :

```
Button{
    Size: Size{
        width: 3
        height: 2
    }
    title: 'Click me'
}
```

В отличие от наследования, вы не можете приводить тип между структурами и встраиваемыми структурами
(встраивающая структура также может иметь собственные поля, и она также может встраивать несколько структур).

Если вам нужен прямой доступ к встраиваемым структурам, используйте явную ссылку, например `button.Size`.

Концептуально встраиваемые структуры аналогичны [mixin](https://en.wikipedia.org/wiki/Mixin)s
в ООП, *НЕ* базовым классам.

Вы также можете инициализировать встраиваемую структуру:

```v oksyntax
mut button := Button{
	Size: Size{
		width:  3
		height: 2
	}
}
```

или присваивать значения:

```v oksyntax
button.Size = Size{
	width:  4
	height: 5
}
```

Если у нескольких встраиваемых структур есть методы или поля с одинаковыми именами, или если методы или поля
с одинаковыми именами определены в структуре, вы можете вызывать методы или присваивать переменным во
встраиваемой структуре, как `button.Size.area()`.
Когда вы не указываете имя встраиваемой структуры, метод самой внешней структуры будет
целевым.
<a id="unions"></a>
## Объединения

Объединение — это особый тип структуры, который позволяет хранить различные типы данных в одном и том же месте памяти. Вы можете определить объединение с несколькими членами, но только один член может содержать действительное значение в любой момент времени, в зависимости от типов данных членов. Объединения обеспечивают эффективный способ использования одного и того же участка памяти для нескольких целей.

Все члены объединения разделяют одно и то же место в памяти. Это означает, что изменение одного члена автоматически изменяет все остальные. Самый большой член объединения определяет его размер.
<a id="why-use-unions"></a>
### Зачем использовать объединения?

Одна из причин, как указано выше, — экономия памяти при хранении данных. Поскольку размер объединения равен размеру самого большого его поля, а размер структуры равен сумме размеров всех её полей, объединение определённо лучше для снижения потребления памяти. Пока вам нужно, чтобы одно из полей было действительным в любой момент времени, объединение выигрывает.

Другая причина — обеспечение более простого доступа к частям поля. Например, без использования объединения, если вы хотите посмотреть на каждый байт 32-битного целого числа отдельно, вам понадобятся побитовые операции `ПРАВЫЙ-СДВИГ` и `И`. С объединением вы можете обращаться к отдельным байтам напрямую.
```v
union ThirtyTwo {
	a u32
	b [4]u8
}
```
Поскольку `ThirtyTwo.a` и `ThirtyTwo.b` разделяют одни и те же адреса памяти, вы можете получить прямой доступ к каждому байту `a`, обращаясь к `b[смещение_байта]`.
<a id="embedding"></a>
### Встраивание

Объединения также поддерживают встраивание, так же как и структуры.

```v
struct Rgba32_Component {
	r u8
	g u8
	b u8
	a u8
}

union Rgba32 {
	Rgba32_Component
	value u32
}

clr1 := Rgba32{
	value: 0x008811FF
}

clr2 := Rgba32{
	Rgba32_Component: Rgba32_Component{
		a: 128
	}
}

sz := sizeof(Rgba32)
unsafe {
	println('Size: ${sz}B,clr1.b: ${clr1.b},clr2.b: ${clr2.b}')
}
```

Вывод: `Size: 4B, clr1.b: 136, clr2.b: 0`

Доступ к членам объединения должен выполняться в блоке `unsafe`.

> [!NOTE]
> Встроенные аргументы структур не обязательно хранятся в указанном порядке.
<a id="functions-2"></a>
## Функции 2
<a id="immutable-function-args-by-default"></a>
### Неизменяемые аргументы функций по умолчанию

В V аргументы функций неизменяемы по умолчанию, а изменяемые аргументы должны быть помечены при вызове.

Поскольку также отсутствуют глобальные переменные, это означает, что возвращаемые значения функций являются функцией только их аргументов, и их вычисление не имеет побочных эффектов (если только функция не использует ввод/вывод).

Аргументы функции неизменяемы по умолчанию, даже когда передаются [references](#references).

> [!NOTE]
> Однако V не является чисто функциональным языком.

Существует флаг компилятора для включения глобальных переменных (`-enable-globals`), но он предназначен для низкоуровневых приложений, таких как ядра и драйверы.
<a id="mutable-arguments"></a>
### Изменяемые аргументы

Возможно изменять аргументы функций, объявляя их с помощью ключевого слова `mut`:

```v
struct User {
	name string
mut:
	is_registered bool
}

fn (mut u User) register() {
	u.is_registered = true
}

mut user := User{}
println(user.is_registered) // "false"
user.register()
println(user.is_registered) // "true"
```

В этом примере получатель (который является просто первым аргументом) явно помечен как изменяемый, поэтому `register()` может изменять объект пользователя. То же самое работает с аргументами, не являющимися получателями:

```v
fn multiply_by_2(mut arr []int) {
	for i in 0 .. arr.len {
		arr[i] *= 2
	}
}

mut nums := [1, 2, 3]
multiply_by_2(mut nums)
println(nums)
// "[2, 4, 6]"
```

Обратите внимание, что вы должны добавить `mut` перед `nums` при вызове этой функции. Это делает очевидным, что вызываемая функция будет изменять значение.

Предпочтительнее возвращать значения, а не изменять аргументы,
например, `user = register(user)` (или `user.register()`) вместо `register(mut user)`.
Изменение аргументов следует выполнять только в критических для производительности частях вашего приложения для уменьшения выделений памяти и копирования.

По этой причине V не позволяет изменять аргументы примитивных типов (например, целых чисел). Только более сложные типы, такие как массивы и карты, могут быть изменены.
<a id="variable-number-of-arguments"></a>
### Переменное количество аргументов
V поддерживает функции, принимающие произвольное, переменное количество аргументов, обозначаемое префиксом `...`.
Ниже `a ...int` относится к произвольному количеству параметров, которые будут собраны в массив с именем `a`.

```v
fn sum(a ...int) int {
	mut total := 0
	for x in a {
		total += x
	}
	return total
}

println(sum()) // 0
println(sum(1)) // 1
println(sum(2, 3)) // 5
// using array decomposition
a := [2, 3, 4]
println(sum(...a)) // <-- using prefix ... here. output: 9
b := [5, 6, 7]
println(sum(...b)) // output: 18
```
<a id="anonymous-higher-order-functions"></a>
### Анонимные и функции высшего порядка

```v
fn sqr(n int) int {
	return n * n
}

fn cube(n int) int {
	return n * n * n
}

fn run(value int, op fn (int) int) int {
	return op(value)
}

fn main() {
	// Functions can be passed to other functions
	println(run(5, sqr)) // "25"
	// Anonymous functions can be declared inside other functions:
	double_fn := fn (n int) int {
		return n + n
	}
	println(run(5, double_fn)) // "10"
	// Functions can be passed around without assigning them to variables:
	res := run(5, fn (n int) int {
		return n + n
	})
	println(res) // "10"
	// You can even have an array/map of functions:
	fns := [sqr, cube]
	println(fns[0](10)) // "100"
	fns_map := {
		'sqr':  sqr
		'cube': cube
	}
	println(fns_map['cube'](2)) // "8"
}
```
<a id="lambda-expressions"></a>
### Лямбда-выражения

Лямбда-выражения в V — это небольшие анонимные функции, определённые с использованием синтаксиса `|переменные| выражение`. Примечание: этот синтаксис действителен только внутри вызовов функций высшего порядка.

Вот некоторые примеры:
```v
mut a := [1, 2, 3]
a.sort(|x, y| x > y) // sorts the array, defining the comparator with a lambda expression
println(a.map(|x| x * 10)) // prints [30, 20, 10]
```

```v
// Lambda function can be used as callback
fn f(cb fn (a int) int) int {
	return cb(10)
}

println(f(|x| x + 4)) // prints 14
```
<a id="closures"></a>
### Замыкания

V также поддерживает замыкания.
Это означает, что анонимные функции могут наследовать переменные из области видимости, в которой они были созданы. Они должны делать это явно, перечисляя все унаследованные переменные.

```v oksyntax
my_int := 1
my_closure := fn [my_int] () {
	println(my_int)
}
my_closure() // prints 1
```

Унаследованные переменные копируются при создании анонимной функции.
Это означает, что если исходная переменная будет изменена после создания функции, изменение не отразится в функции.

```v oksyntax
mut i := 1
func := fn [i] () int {
	return i
}
println(func() == 1) // true
i = 123
println(func() == 1) // still true
```

Однако переменная может быть изменена внутри анонимной функции.
Изменение не отразится снаружи, но будет отражено в последующих вызовах функции.

```v oksyntax
fn new_counter() fn () int {
	mut i := 0
	return fn [mut i] () int {
		i++
		return i
	}
}

c := new_counter()
println(c()) // 1
println(c()) // 2
println(c()) // 3
```

Если вам нужно, чтобы значение изменялось за пределами функции, используйте ссылку.

```v oksyntax
mut i := 0
mut ref := &i
print_counter := fn [ref] () {
	println(*ref)
}

print_counter() // 0
i = 10
print_counter() // 10
```
<a id="parameter-evaluation-order"></a>
### Порядок вычисления параметров

Порядок вычисления параметров вызовов функций *НЕ* гарантирован.
Возьмём, например, следующую программу:

```v
fn f(a1 int, a2 int, a3 int) {
	dump(a1 + a2 + a3)
}

fn main() {
	f(dump(100), dump(200), dump(300))
}
```

V в настоящее время не гарантирует, что он напечатает 100, 200, 300 в этом порядке.
Единственная гарантия заключается в том, что 600 (из тела `f`) будет напечатано после всех них.

Это *может* измениться в V 1.0.
<a id="references"></a>
## Ссылки

```v
struct Foo {}

fn (foo Foo) bar_method() {
	// ...
}

fn bar_function(foo Foo) {
	// ...
}
```

Если аргумент функции неизменяем (например, `foo` в примерах выше),
V может передавать его либо по значению, либо по ссылке. Компилятор примет решение,
и разработчику не нужно об этом думать.

Вам больше не нужно помнить, следует ли передавать структуру по значению
или по ссылке.

Вы можете гарантировать, что структура всегда передаётся по ссылке, добавив `&`:

```v
struct Foo {
	abc int
}

fn (foo &Foo) bar() {
	println(foo.abc)
}
```

`foo` всё ещё неизменяем и не может быть изменён. Для этого
необходимо использовать `(mut foo Foo)`.

В целом, ссылки в V аналогичны указателям в Go и ссылкам в C++.
Например, определение обобщённой структуры дерева будет выглядеть так:

```v
struct Node[T] {
	val   T
	left  &Node[T]
	right &Node[T]
}
```

Чтобы разыменовать ссылку, используйте оператор `*`, точно так же, как в C.
<a id="constants"></a>
## Константы

```v
const pi = 3.14
const world = 'мир'

println(pi)
println(world)
```

Константы объявляются с помощью `const`. Они могут быть определены только
на уровне модуля (вне функций).
Значения констант никогда не могут быть изменены. Можно также объявить
одну константу отдельно:

```v
const e = 2.71828
```

Константы V более гибкие, чем в большинстве языков. Можно присваивать более сложные значения:

```v
struct Color {
	r int
	g int
	b int
}

fn rgb(r int, g int, b int) Color {
	return Color{
		r: r
		g: g
		b: b
	}
}

const numbers = [1, 2, 3]
const red = Color{
	r: 255
	g: 0
	b: 0
}
// evaluate function call at compile time*
const blue = rgb(0, 0, 255)

println(numbers)
println(red)
println(blue)
```

\* В разработке - на данный момент вызовы функций вычисляются при запуске программы

Глобальные переменные обычно не разрешены, поэтому это может быть очень полезно.

**Модули**

Константы можно сделать публичными с помощью `pub const`:

```v oksyntax
module mymodule

pub const golden_ratio = 1.61803

fn calc() {
	println(golden_ratio)
}
```

Ключевое слово `pub` допускается только перед ключевым словом `const` и не может использоваться внутри
блока `const ( )`.

Вне модуля `main` все константы должны иметь префикс с именем модуля.
<a id="required-module-prefix"></a>
### Обязательный префикс модуля

При именовании констант должен использоваться `snake_case`. Чтобы отличать константы
от локальных переменных, необходимо указывать полный путь к константам. Например,
чтобы обратиться к константе PI, необходимо использовать полное имя `math.pi` как за пределами модуля
`math`, так и внутри него. Это ограничение действует только для модуля `main`
(модуля, содержащего вашу `fn main()`), где вы можете использовать неqualified имя
констант, определенных там, то есть `numbers`, а не `main.numbers`.

`vfmt` заботится об этом правиле, поэтому вы можете написать `println(pi)` внутри модуля `math`,
и `vfmt` автоматически обновит его до `println(math.pi)`.

<!--
Многие предпочитают константы в верхнем регистре: `TOP_CITIES`. Это не будет работать
хорошо в V, потому что константы гораздо мощнее, чем в других языках.
Они могут представлять сложные структуры, и это используется довольно часто, поскольку
нет глобальных переменных:

```v oksyntax
println('Top cities: ${top_cities.filter(.usa)}')
```
-->
<a id="builtin-functions"></a>
## Встроенные функции

Некоторые функции являются встроенными, например `println`. Вот полный список:

```v ignore
fn print(s string) // prints anything on stdout
fn println(s string) // prints anything and a newline on stdout

fn eprint(s string) // same as print(), but uses stderr
fn eprintln(s string) // same as println(), but uses stderr

fn exit(code int) // terminates the program with a custom error code
fn panic(s string) // prints a message and backtraces on stderr, and terminates the program with error code 1
fn print_backtrace() // prints backtraces on stderr
```

> [!NOTE]
> Хотя функции `print` принимают строку, V также принимает и другие печатаемые типы.
> Подробности см. ниже.

Также существует специальная встроенная функция [`dump`](#dumping-expressions-at-runtime).
<a id="println"></a>
### println

`println` — это простая, но мощная встроенная функция, которая может печатать что угодно:
строки, числа, массивы, карты, структуры.

```v
struct User {
	name string
	age  int
}

println(1) // "1"
println('hi') // "hi"
println([1, 2, 3]) // "[1, 2, 3]"
println(User{ name: 'Bob', age: 20 }) // "User{name:'Bob', age:20}"
```

Смотрите также [String interpolation](#string-interpolation).

<a id='custom-print-of-types'></a>
<a id="printing-custom-types"></a>
### Печать пользовательских типов

Если вы хотите определить пользовательское значение для печати вашего типа, просто определите
метод `str() string`:

```v
struct Color {
	r int
	g int
	b int
}

pub fn (c Color) str() string {
	return '{${c.r}, ${c.g}, ${c.b}}'
}

red := Color{
	r: 255
	g: 0
	b: 0
}
println(red)
```
<a id="dumping-expressions-at-runtime"></a>
### Отладочный вывод выражений во время выполнения

Вы можете отслеживать/трассировать значение любого выражения V с помощью `dump(expr)`.
Например, сохраните этот пример кода как `factorial.v`, затем запустите его с помощью
`v run factorial.v`:

```v
fn factorial(n u32) u32 {
	if dump(n <= 1) {
		return dump(1)
	}
	return dump(n * factorial(n - 1))
}

fn main() {
	println(factorial(5))
}
```

Вы получите:

```
[factorial.v:2] n <= 1: false
[factorial.v:2] n <= 1: false
[factorial.v:2] n <= 1: false
[factorial.v:2] n <= 1: false
[factorial.v:2] n <= 1: true
[factorial.v:3] 1: 1
[factorial.v:5] n * factorial(n - 1): 2
[factorial.v:5] n * factorial(n - 1): 6
[factorial.v:5] n * factorial(n - 1): 24
[factorial.v:5] n * factorial(n - 1): 120
120
```

Обратите внимание, что `dump(expr)` будет трассировать как местоположение исходного кода,
так и само выражение, и значение выражения.
<a id="modules"></a>
## Модули

Каждый файл в корне папки является частью одного и того же модуля.
Простым программам не нужно указывать имя модуля, по умолчанию это 'main'.

Смотрите [symbol visibility](#symbol-visibility), [Access modifiers](#access-modifiers).
<a id="create-modules"></a>
### Создание модулей

V — это очень модульный язык. Создание переиспользуемых модулей поощряется и является
довольно простым делом.
Чтобы создать новый модуль, создайте директорию с именем вашего модуля, содержащую
файлы .v с кодом:

```shell
cd ~/code/modules
mkdir mymodule
vim mymodule/myfile.v
```

```v failcompile
// myfile.v
module mymodule

// To export a function we have to use `pub`
pub fn say_hi() {
	println('hello from mymodule!')
}
```
Все элементы внутри модуля могут использоваться между файлами модуля, независимо от того,
предваряются ли они ключевым словом `pub`.
```v failcompile
// myfile2.v
module mymodule

pub fn say_hi_and_bye() {
	say_hi() // from myfile.v
	println('goodbye from mymodule')
}
```

Теперь вы можете использовать `mymodule` в вашем коде:

```v failcompile
import mymodule

fn main() {
	mymodule.say_hi()
	mymodule.say_hi_and_bye()
}
```

* Имена модулей должны быть короткими, не более 10 символов.
* Имена модулей должны использовать `snake_case`.
* Циклические импорты не разрешены.
* Вы можете иметь столько файлов .v в модуле, сколько хотите.
* Вы можете создавать модули где угодно.
* Все модули компилируются статически в один исполняемый файл.
<a id="special-considerations-for-project-folders"></a>
### Особые соображения для папок проекта

Для верхней папки проекта (той, которая компилируется с помощью `v .`), и *только*
для этой папки, вы можете иметь несколько файлов .v, которые могут указывать на разные модули
с `module main`, `module abc` и т.д.

Это облегчает рабочий процесс прототипирования в этой папке:
- вы можете начать разработку нового проекта с одного файла .v
- разделить функциональность по необходимости на разные файлы .v в той же папке
- когда это имеет логический смысл для дальнейшей организации, переместите их в собственную директорию-модуль.

Обратите внимание, что в обычных модулях все файлы .v должны начинаться с `module имя_папки`.
<a id="init-functions"></a>
### Функции `init`

Если вы хотите, чтобы модуль автоматически вызывал некоторый код настройки/инициализации при его импорте,
вы можете определить функцию модуля `init`:

```v
fn init() {
	// your setup code here ...
}
```

Функция `init` не может быть публичной — она будет вызвана автоматически V, *только один раз*, независимо
от того, сколько раз модуль был импортирован в вашей программе. Эта функция особенно полезна для
инициализации библиотеки C.
<a id="cleanup-functions"></a>
### Функции `cleanup`

Если вы хотите, чтобы модуль автоматически вызывал некоторый код очистки/деинициализации, когда ваша программа
завершается, вы можете определить функцию модуля `cleanup`:

```v
fn cleanup() {
	// your deinitialisation code here ...
}
```

Как и функция `init`, функция `cleanup` для модуля не может быть публичной — она будет
вызвана автоматически, когда ваша программа завершается, один раз для каждого модуля, даже если модуль был импортирован
транзитивно другими модулями несколько раз, в обратном порядке вызовов init.
<a id="type-declarations"></a>
## Объявления типов
<a id="type-aliases"></a>
### Псевдонимы типов

Чтобы определить новый тип `NewType` как псевдоним для `ExistingType`,
используйте `type NewType = ExistingType`.<br/>
Это частный случай объявления [sum type](#sum-types).
<a id="enums"></a>
### Перечисления (Enums)

Перечисление — это группа целочисленных константных значений, каждое из которых имеет собственное имя,
значения которых начинаются с 0 и увеличиваются на 1 для каждого перечисленного имени.
Например:
```v
enum Color as u8 {
	red   // the default start value is 0
	green // the value is automatically incremented to 1
	blue  // the final value is now 2
}

mut color := Color.red
// V knows that `color` is a `Color`. No need to use `color = Color.green` here.
color = .green
println(color) // "green"
match color {
	.red { println('the color was red') }
	.green { println('the color was green') }
	.blue { println('the color was blue') }
}
println(int(color)) // prints 1
```

Тип перечисления может быть любым целочисленным типом, но может быть опущен, если это `int`: `enum Color {`.

Сопоставление перечисления должно быть исчерпывающим или иметь ветку `else`.
Это гарантирует, что если будет добавлено новое поле перечисления, оно будет обработано везде в коде.

Поля перечисления могут повторно использовать зарезервированные ключевые слова:

```v
enum Color {
	none
	red
	green
	blue
}

color := Color.none
println(color)
```

Целые числа могут быть присвоены полям перечисления.

```v
enum Grocery {
	apple
	orange = 5
	pear
}

g1 := int(Grocery.apple)
g2 := int(Grocery.orange)
g3 := int(Grocery.pear)
println('Grocery IDs: ${g1}, ${g2}, ${g3}')
```

Вывод: `Grocery IDs: 0, 5, 6`.

Операции над переменными перечисления не разрешены; они должны быть явно приведены к `int`.

Перечисления могут иметь методы, как и структуры.

```v
enum Cycle {
	one
	two
	three
}

fn (c Cycle) next() Cycle {
	match c {
		.one {
			return .two
		}
		.two {
			return .three
		}
		.three {
			return .one
		}
	}
}

mut c := Cycle.one
for _ in 0 .. 10 {
	println(c)
	c = c.next()
}
```

Вывод:

```
one
two
three
one
two
three
one
two
three
one
```

Перечисления могут быть созданы из строкового или целочисленного значения и преобразованы в строку.

```v
enum Cycle {
	one
	two = 2
	three
}

// Create enum from value
println(Cycle.from(10) or { Cycle.three })
println(Cycle.from('two')!)

// Convert an enum value to a string
println(Cycle.one.str())
```

Вывод:

```
three
two
one
```
<a id="function-types"></a>
### Типы функций

Вы можете использовать псевдонимы типов для именования конкретных сигнатур функций — например:

```v
type Filter = fn (string) string
```

Это работает как любой другой тип — например, функция может принимать
аргумент типа функции:

```v
type Filter = fn (string) string

fn filter(s string, f Filter) string {
	return f(s)
}
```

V имеет duck-typing (утиную типизацию), поэтому функциям не нужно объявлять совместимость с
типом функции — они просто должны быть совместимы:

```v
fn uppercase(s string) string {
	return s.to_upper()
}

// now `uppercase` can be used everywhere where Filter is expected
```

Совместимые функции также могут быть явно приведены к типу функции:

```v oksyntax
my_filter := Filter(uppercase)
```

Приведение здесь чисто информативное — снова, duck-typing означает, что
результирующий тип такой же без явного приведения:

```v oksyntax
my_filter := uppercase
```

Вы можете передать назначенную функцию в качестве аргумента:

```v oksyntax
println(filter('Hello world', my_filter)) // prints `HELLO WORLD`
```

И, конечно, вы могли бы передать ее напрямую, не используя локальную переменную:

```v oksyntax
println(filter('Hello world', uppercase))
```

И это работает также с анонимными функциями:

```v oksyntax
println(filter('Hello world', fn (s string) string {
	return s.to_upper()
}))
```

Полная справочная таблица доступна по
[example here](https://github.com/vlang/v/tree/master/examples/function_types.v).
<a id="interfaces"></a>
### Интерфейсы

```v
// interface-example.1
struct Dog {
	breed string
}

fn (d Dog) speak() string {
	return 'woof'
}

struct Cat {
	breed string
}

fn (c Cat) speak() string {
	return 'meow'
}

// unlike Go, but like TypeScript, V's interfaces can define both fields and methods.
interface Speaker {
	breed string
	speak() string
}

fn main() {
	dog := Dog{'Leonberger'}
	cat := Cat{'Siamese'}

	mut arr := []Speaker{}
	arr << dog
	arr << cat
	for item in arr {
		println('a ${item.breed} says: ${item.speak()}')
	}
}
```
<a id="implement-an-interface"></a>
#### Реализация интерфейса

Тип реализует интерфейс, реализуя его методы и поля.

Интерфейс может иметь секцию `mut:`. Реализующие типы должны
иметь приемник `mut` для методов, объявленных в секции `mut:` интерфейса.

```v
// interface-example.2
module main

interface Foo {
	write(string) string
}

// => the method signature of a type, implementing interface Foo should be:
// `fn (s Type) write(a string) string`

interface Bar {
mut:
	write(string) string
}

// => the method signature of a type, implementing interface Bar should be:
// `fn (mut s Type) write(a string) string`

struct MyStruct {}

// MyStruct implements the interface Foo, but *not* interface Bar
fn (s MyStruct) write(a string) string {
	return a
}

fn main() {
	s1 := MyStruct{}
	fn1(s1)
	// fn2(s1) -> compile error, since MyStruct does not implement Bar
}

fn fn1(s Foo) {
	println(s.write('Foo'))
}

// fn fn2(s Bar) { // does not match
//      println(s.write('Foo'))
// }
```

Существует **опциональное** ключевое слово `implements` для явного объявления
намерения, которое применяется к объявлениям `struct`.

```v
struct PathError implements IError {
	Error
	path string
}

fn (err PathError) msg() string {
	return 'Failed to open path: ${err.path}'
}

fn try_open(path string) ! {
	return PathError{
		path: path
	}
}

fn main() {
	try_open('/tmp') or { panic(err) }
}
```
<a id="casting-an-interface"></a>
#### Приведение типа интерфейса

Мы можем проверить базовый тип интерфейса с помощью операторов динамического приведения.
> [!NOTE]
> Динамическое приведение преобразует переменную `s` в указатель внутри инструкций `if` в этом примере:

```v oksyntax
// interface-example.3 (continued from interface-example.1)
interface Something {}

fn announce(s Something) {
	if s is Dog {
		println('a ${s.breed} dog') // `s` is automatically cast to `Dog` (smart cast)
	} else if s is Cat {
		println('a cat speaks ${s.speak()}')
	} else {
		println('something else')
	}
}

fn main() {
	dog := Dog{'Leonberger'}
	cat := Cat{'Siamese'}
	announce(dog)
	announce(cat)
}
```

```v
// interface-example.4
interface IFoo {
	foo()
}

interface IBar {
	bar()
}

// implements only IFoo
struct SFoo {}

fn (sf SFoo) foo() {}

// implements both IFoo and IBar
struct SFooBar {}

fn (sfb SFooBar) foo() {}

fn (sfb SFooBar) bar() {
	dump('This implements IBar')
}

fn main() {
	mut arr := []IFoo{}
	arr << SFoo{}
	arr << SFooBar{}

	for a in arr {
		dump(a)
		// In order to execute instances that implements IBar.
		if a is IBar {
			a.bar()
		}
	}
}
```

Для получения дополнительной информации смотрите [Dynamic casts](#dynamic-casts).
<a id="interface-method-definitions"></a>
#### Определения методов интерфейса

Также в отличие от Go, интерфейс может иметь собственные методы, подобно тому, как
структуры могут иметь свои методы. Эти «методы интерфейса» не обязаны
быть реализованы структурами, реализующими этот интерфейс.
Они просто являются удобным способом написать `i.some_function()` вместо
`some_function(i)`, подобно тому, как методы структур можно рассматривать как
удобство для написания `s.xyz()` вместо `xyz(s)`.

> [!NOTE]
> Эта функция НЕ является «реализацией по умолчанию», как в C#.

Например, если структура `cat` обернута в интерфейс `a`, который реализовал
метод с тем же именем `speak`, как метод, реализованный структурой,
и вы делаете `a.speak()`, то вызывается *только* метод интерфейса:

```v
interface Adoptable {}

fn (a Adoptable) speak() string {
	return 'adopt me!'
}

struct Cat {}

fn (c Cat) speak() string {
	return 'meow!'
}

struct Dog {}

fn main() {
	cat := Cat{}
	assert dump(cat.speak()) == 'meow!'

	a := Adoptable(cat)
	assert dump(a.speak()) == 'adopt me!' // call Adoptable's `speak`
	if a is Cat {
		// Inside this `if` however, V knows that `a` is not just any
		// kind of Adoptable, but actually a Cat, so it will use the
		// Cat `speak`, NOT the Adoptable `speak`:
		dump(a.speak()) // meow!
	}

	b := Adoptable(Dog{})
	assert dump(b.speak()) == 'adopt me!' // call Adoptable's `speak`
	// if b is Dog {
	// 	dump(b.speak()) // error: unknown method or field: Dog.speak
	// }
}
```
<a id="embedded-interface"></a>
#### Встроенные интерфейсы

Интерфейсы поддерживают встраивание, как и структуры:

```v
pub interface Reader {
mut:
	read(mut buf []u8) ?int
}

pub interface Writer {
mut:
	write(buf []u8) ?int
}

// ReaderWriter embeds both Reader and Writer.
// The effect is the same as copy/pasting all of the
// Reader and all of the Writer methods/fields into
// ReaderWriter.
pub interface ReaderWriter {
	Reader
	Writer
}
```
<a id="sum-types"></a>
### Суммарные типы (Sum types)

Экземпляр суммарного типа может хранить значение нескольких разных типов. Используйте ключевое слово `type`
для объявления суммарного типа:

```v
struct Moon {}

struct Mars {}

struct Venus {}

type World = Mars | Moon | Venus

sum := World(Moon{})
assert sum.type_name() == 'Moon'
println(sum)
```

Встроенный метод `type_name` возвращает имя текущего хранимого
типа.

С помощью суммарных типов можно строить рекурсивные структуры и писать на них лаконичный, но мощный код.

```v
// V's binary tree
struct Empty {}

struct Node {
	value f64
	left  Tree
	right Tree
}

type Tree = Empty | Node

// sum up all node values

fn sum(tree Tree) f64 {
	return match tree {
		Empty { 0 }
		Node { tree.value + sum(tree.left) + sum(tree.right) }
	}
}

fn main() {
	left := Node{0.2, Empty{}, Empty{}}
	right := Node{0.3, Empty{}, Node{0.4, Empty{}, Empty{}}}
	tree := Node{0.5, left, right}
	println(sum(tree)) // 0.2 + 0.3 + 0.4 + 0.5 = 1.4
}
```
<a id="dynamic-casts"></a>
#### Динамические приведения (Dynamic casts)

Чтобы проверить, хранит ли экземпляр суммарного типа определенный тип, используйте `sum is Type`.
Чтобы привести суммарный тип к одному из его вариантов, вы можете использовать `sum as Type`:

```v
struct Moon {}

struct Mars {}

struct Venus {}

type World = Mars | Moon | Venus

fn (m Mars) dust_storm() bool {
	return true
}

fn main() {
	mut w := World(Moon{})
	assert w is Moon
	w = Mars{}
	// use `as` to access the Mars instance
	mars := w as Mars
	if mars.dust_storm() {
		println('bad weather!')
	}
}
```

`as` вызовет панику, если `w` не хранит экземпляр `Mars`.
Более безопасный способ — использовать умное приведение (smart cast).
<a id="smart-casting"></a>
#### Умное приведение (Smart casting)

```v oksyntax
if w is Mars {
	assert typeof(w).name == 'Mars'
	if w.dust_storm() {
		println('bad weather!')
	}
}
```

`w` имеет тип `Mars` внутри тела инструкции `if`. Это
известно как * поточная чувствительная типизация (flow-sensitive typing)*.
Если `w` является изменяемым идентификатором, это было бы небезопасно, если бы компилятор делал умное приведение без предупреждения.
Поэтому вы должны объявить `mut` перед выражением `is`:

```v ignore
if mut w is Mars {
	assert typeof(w).name == 'Mars'
	if w.dust_storm() {
		println('bad weather!')
	}
}
```

В противном случае `w` сохранил бы свой исходный тип.
> Это работает как для простых переменных, так и для сложных выражений вроде `user.name`
<a id="matching-sum-types"></a>
#### Сопоставление суммарных типов

Вы также можете использовать `match` для определения варианта:

```v
struct Moon {}

struct Mars {}

struct Venus {}

type World = Mars | Moon | Venus

fn open_parachutes(n int) {
	println(n)
}

fn land(w World) {
	match w {
		Moon {} // no atmosphere
		Mars {
			// light atmosphere
			open_parachutes(3)
		}
		Venus {
			// heavy atmosphere
			open_parachutes(1)
		}
	}
}
```

`match` должен иметь шаблон для каждого варианта или ветку `else`.

```v ignore
struct Moon {}
struct Mars {}
struct Venus {}

type World = Moon | Mars | Venus

fn (m Moon) moon_walk() {}
fn (m Mars) shiver() {}
fn (v Venus) sweat() {}

fn pass_time(w World) {
    match w {
        // using the shadowed match variable, in this case `w` (smart cast)
        Moon { w.moon_walk() }
        Mars { w.shiver() }
        else {}
    }
}
```
<a id="optionresult-types-and-error-handling"></a>
### Типы Option/Result и обработка ошибок

Типы Option могут представлять значение или `none`. Типы Result могут
представлять значение или ошибку, возвращенную из функции.

Типы `Option` объявляются с помощью добавления префикса `?` к имени типа: `?Type`.
Типы `Result` используют `!`: `!Type`.

```v
struct User {
	id   int
	name string
}

struct Repo {
	users []User
}

fn (r Repo) find_user_by_id(id int) !User {
	for user in r.users {
		if user.id == id {
			// V automatically wraps this into a result or option type
			return user
		}
	}
	return error('User ${id} not found')
}

// A version of the function using an option
fn (r Repo) find_user_by_id2(id int) ?User {
	for user in r.users {
		if user.id == id {
			return user
		}
	}
	return none
}

fn main() {
	repo := Repo{
		users: [User{1, 'Andrew'}, User{2, 'Bob'}, User{10, 'Charles'}]
	}
	user := repo.find_user_by_id(10) or { // Option/Result types must be handled by `or` blocks
		println(err)
		return
	}
	println(user.id) // "10"
	println(user.name) // "Charles"

	user2 := repo.find_user_by_id2(10) or { return }

	// To create an Option var directly:
	my_optional_int := ?int(none)
	my_optional_string := ?string(none)
	my_optional_user := ?User(none)
}
```

Ранее V объединял `Option` и `Result` в один тип, теперь они разделены.

Объем работы, необходимый для «обновления» функции до функции option/result, минимален;
вам нужно добавить `?` или `!` к возвращаемому типу и возвращать `none` или ошибку (соответственно),
когда что-то идет не так.

Это основной механизм обработки ошибок в V. Они все еще являются значениями, как в Go,
но преимущество в том, что ошибки не могут быть необработанными, а их обработка намного менее многословна.
В отличие от других языков, V не обрабатывает исключения с помощью блоков `throw/try/catch`.

`err` определяется внутри блока `or` и устанавливается в строковое сообщение, переданное
в функцию `error()`.

```v oksyntax
user := repo.find_user_by_id(7) or {
	println(err) // "User 7 not found"
	return
}
```

Используйте `err is ...` для сравнения ошибок:
```v oksyntax
import io

x := read() or {
	if err is io.Eof {
		println('end of file')
	}
	return
}
```
<a id="optionsresults-when-returning-multiple-values"></a>
#### Option/Result при возврате нескольких значений

Из функции может быть возвращен только один `Option` или `Result`. Возможно
возвращать несколько значений и все еще сигнализировать об ошибке.

```v
fn multi_return(v int) !(int, int) {
	if v < 0 {
		return error('must be positive')
	}
	return v, v * v
}
```
<a id="handling-optionsresults"></a>
#### Обработка option/result

Есть четыре способа обработать option/result. Первый способ —
распространить ошибку:

```v
import net.http

fn f(url string) !string {
	resp := http.get(url)!
	return resp.body
}
```

`http.get` возвращает `!http.Response`. Поскольку `!` следует за вызовом, ошибка
будет распространена на вызывающую функцию `f`. При использовании `?` после вызова функции,
производящей option, окружающая функция должна также возвращать
option. Если распространение ошибок используется в функции `main()`, вместо этого будет вызвана `panic`,
поскольку ошибка не может быть распространена
дальше.

Тело `f` по существу является сокращенной версией:

```v ignore
    resp := http.get(url) or { return err }
    return resp.body
```

---
Второй способ — ранний выход из выполнения:

```v oksyntax
user := repo.find_user_by_id(7) or { return }
```

Здесь вы можете либо вызвать `panic()`, либо `exit()`, что остановит выполнение
всей программы, либо использовать оператор потока управления (`return`, `break`, `continue` и т.д)
для выхода из текущего блока.

> [!NOTE]
> `break` и `continue` могут использоваться только внутри цикла `for`.

V не имеет способа принудительно «развернуть» option (как это делают другие языки,
например, `unwrap()` в Rust или `!` в Swift). Для этого вместо этого используйте `or { panic(err) }`.

---
Третий способ — предоставить значение по умолчанию в конце блока `or`.
В случае ошибки вместо него будет присвоено это значение,
поэтому оно должно иметь тот же тип, что и содержимое обрабатываемого `Option`.

```v
fn do_something(s string) !string {
	if s == 'foo' {
		return 'foo'
	}
	return error('invalid string')
}

a := do_something('foo') or { 'default' } // a will be 'foo'
b := do_something('bar') or { 'default' } // b will be 'default'
println(a)
println(b)
```

---
Четвертый способ — использовать «разворачивание» с помощью `if`:

```v
import net.http

if resp := http.get('https://google.com') {
	println(resp.body) // resp is a http.Response, not an option
} else {
	println(err)
}
```

Выше `http.get` возвращает `!http.Response`. `resp` доступна только в первом
ветвлении `if`. `err` доступна только в ветвлении `else`.
<a id="custom-error-types"></a>
### Пользовательские типы ошибок

V дает вам возможность определять пользовательские типы ошибок через интерфейс `IError`.
Интерфейс требует два метода: `msg() string` и `code() int`. Любой тип, который
реализует эти методы, может использоваться как ошибка.

При определении пользовательского типа ошибки рекомендуется встраивать встроенную реализацию по умолчанию `Error`.
Это обеспечивает пустую реализацию по умолчанию для обоих требуемых методов,
поэтому вам нужно реализовать только то, что вам действительно нужно, и вы можете предоставить дополнительные утилиты
в будущем.

```v
struct PathError {
	Error
	path string
}

fn (err PathError) msg() string {
	return 'Failed to open path: ${err.path}'
}

fn try_open(path string) ! {
	// V automatically casts this to IError
	return PathError{
		path: path
	}
}

fn main() {
	try_open('/tmp') or { panic(err) }
}
```
<a id="generics"></a>
### Обобщения (Generics)

```v wip

struct Repo[T] {
    db DB
}

struct User {
	id   int
	name string
}

struct Post {
	id   int
	user_id int
	title string
	body string
}

fn new_repo[T](db DB) Repo[T] {
    return Repo[T]{db: db}
}

// This is a generic function. V will generate it for every type it's used with.
fn (r Repo[T]) find_by_id(id int) ?T {
    table_name := T.name // in this example getting the name of the type gives us the table name
    return r.db.query_one[T]('select * from ${table_name} where id = ?', id)
}

db := new_db()
users_repo := new_repo[User](db) // returns Repo[User]
posts_repo := new_repo[Post](db) // returns Repo[Post]
user := users_repo.find_by_id(1)? // find_by_id[User]
post := posts_repo.find_by_id(1)? // find_by_id[Post]
```

В настоящее время определения обобщенных функций должны объявлять свои типовые параметры, но в
будущих версиях V будет выводить типовые параметры обобщений по однобуквенным именам типов в
параметрах времени выполнения. Поэтому вызовы `find_by_id(1)` выше могут опускать `[T]`,
поскольку аргумент-приемник `r` в объявлении метода использует обобщенный тип `T`.

Другой пример:

```v
fn compare[T](a T, b T) int {
	if a < b {
		return -1
	}
	if a > b {
		return 1
	}
	return 0
}

// compare[int]
println(compare(1, 0)) // Outputs: 1
println(compare(1, 1)) //          0
println(compare(1, 2)) //         -1
// compare[string]
println(compare('1', '0')) // Outputs: 1
println(compare('1', '1')) //          0
println(compare('1', '2')) //         -1
// compare[f64]
println(compare(1.1, 1.0)) // Outputs: 1
println(compare(1.1, 1.1)) //          0
println(compare(1.1, 1.2)) //         -1
```
<a id="concurrency"></a>
## Параллелизм
<a id="spawning-concurrent-tasks"></a>
### Запуск параллельных задач

Модель параллелизма в V аналогична модели Go.

`go foo()` выполняет `foo()` параллельно в легковесном потоке, управляемом средой выполнения V.

`spawn foo()` выполняет `foo()` параллельно в отдельном потоке:

```v
import math

fn p(a f64, b f64) { // ordinary function without return value
	c := math.sqrt(a * a + b * b)
	println(c)
}

fn main() {
	spawn p(3, 4)
	// p will be run in parallel thread
	// It can also be written as follows
	// spawn fn (a f64, b f64) {
	// 	c := math.sqrt(a * a + b * b)
	// 	println(c)
	// }(3, 4)
}
```

> [!NOTE]
> Потоки зависят от ресурсов ЦП машины (количества ядер/потоков).
> Имейте в виду, что потоки ОС, создаваемые с помощью `spawn`,
> имеют ограничения в отношении параллелизма,
> включая накладные расходы на ресурсы и проблемы масштабируемости,
> и могут повлиять на производительность в случае большого количества потоков.

Иногда необходимо дождаться завершения параллельного потока. Это можно сделать, присвоив *дескриптор* запущенному потоку и вызвав метод `wait()` для этого дескриптора позже:

```v
import math

fn p(a f64, b f64) { // ordinary function without return value
	c := math.sqrt(a * a + b * b)
	println(c) // prints `5`
}

fn main() {
	h := spawn p(3, 4)
	// p() runs in parallel thread
	h.wait()
	// p() has definitely finished
}
```

Этот подход также можно использовать для получения возвращаемого значения из функции, выполняемой в параллельном потоке. Нет необходимости изменять саму функцию, чтобы иметь возможность вызывать её параллельно.

```v
import math { sqrt }

fn get_hypot(a f64, b f64) f64 { //       ordinary function returning a value
	c := sqrt(a * a + b * b)
	return c
}

fn main() {
	g := spawn get_hypot(54.06, 2.08) // spawn thread and get handle to it
	h1 := get_hypot(2.32, 16.74) //   do some other calculation here
	h2 := g.wait() //                 get result from spawned thread
	println('Results: ${h1}, ${h2}') //   prints `Results: 16.9, 54.1`
}
```

Если существует большое количество задач, управлять ими может быть проще с помощью массива потоков.

```v
import time

fn task(id int, duration int) {
	println('task ${id} begin')
	time.sleep(duration * time.millisecond)
	println('task ${id} end')
}

fn main() {
	mut threads := []thread{}
	threads << spawn task(1, 500)
	threads << spawn task(2, 900)
	threads << spawn task(3, 100)
	threads.wait()
	println('done')
}

// Output:
// task 1 begin
// task 2 begin
// task 3 begin
// task 3 end
// task 1 end
// task 2 end
// done
```

Кроме того, для потоков, возвращающих один и тот же тип, вызов `wait()` для массива потоков вернет все вычисленные значения.

```v
fn expensive_computing(i int) int {
	return i * i
}

fn main() {
	mut threads := []thread int{}
	for i in 1 .. 10 {
		threads << spawn expensive_computing(i)
	}
	// Join all tasks
	r := threads.wait()
	println('All jobs finished: ${r}')
}

// Output: All jobs finished: [1, 4, 9, 16, 25, 36, 49, 64, 81]
```
<a id="channels"></a>
### Каналы

Каналы являются предпочтительным способом обмена данными между потоками. Они позволяют потокам безопасно обмениваться данными без необходимости явной блокировки. Каналы V аналогичны каналам в Go, позволяя вам помещать объекты в канал с одной стороны и извлекать их с другой стороны.
Каналы могут быть буферизированными или небуферизированными, и вы можете использовать оператор `select` для одновременного мониторинга нескольких каналов.
<a id="syntax-and-usage"></a>
#### Синтаксис и использование

Каналы объявляются с типом `chan objtype`.
Вы можете по желанию указать длину буфера с помощью поля `cap`:

```v
ch := chan int{} // unbuffered - "synchronous"
ch2 := chan f64{cap: 100} // buffered with a capacity of 100
```

Каналы не обязательно объявлять как `mut`. Длина буфера не является частью типа, а является полем отдельного объекта канала. Каналы могут передаваться в потоки как обычные переменные:

```v
import time

fn worker(ch chan int) {
	for i in 0 .. 5 {
		ch <- i // push values into the channel
	}
}

fn clock(ch chan int) {
	for i in 0 .. 5 {
		time.sleep(1 * time.second)
		println('Clock tick')
		ch <- (i + 1000) // push a value into the channel
	}
	ch.close() // close the channel when done
}

fn main() {
	ch := chan int{cap: 5}
	spawn worker(ch)
	spawn clock(ch)
	for {
		value := <-ch or { // receive/pop values from the channel
			println('Channel closed')
			break
		}
		println('Received: ${value}')
	}
}
```
<a id="buffered-channels"></a>
#### Буферизированные каналы

Буферизированные каналы позволяют помещать несколько элементов без блокировки, при условии, что буфер не полон:

```v
ch := chan string{cap: 2}
ch <- 'hello'
ch <- 'world'
// ch <- '!' // This would block because the buffer is full

println(<-ch) // "hello"
println(<-ch) // "world"
```
<a id="closing-channels"></a>
#### Закрытие каналов

Канал может быть закрыт, чтобы указать, что в него больше нельзя помещать объекты. Любая попытка сделать это впоследствии приведет к панике во время выполнения (за исключением `select` и `try_push()` - см. ниже). Попытки извлечения данных вернутся немедленно, если связанный канал был закрыт и буфер пуст. Эту ситуацию можно обработать с помощью блока `or {}` (см. [Handling options/results](#handling-optionsresults)).

```v wip
ch := chan int{}
ch2 := chan f64{}
// ...
ch.close()
// ...
m := <-ch or {
    println('channel has been closed')
}

// propagate error
y := <-ch2 ?
```

Примечание: буферизированные каналы могут быть закрыты, пока в них есть непрочитанные значения.
Буферизированные значения могут быть извлечены даже после закрытия:
```v
ich := chan int{cap: 5}
for i in 0 .. 5 {
	ich <- i
}

for _ in 0 .. 2 {
	x := <-ich or { break }
	eprintln('>>  loop 0..2 | x: ${x} | ich.closed: ${ich.closed}')
}

ich.close()

for {
	x := <-ich or { break }
	eprintln('>> final loop | x: ${x} | ich.closed: ${ich.closed}')
}
```
... выведет:
```
>>  loop 0..2 | x: 0 | ich.closed: false
>>  loop 0..2 | x: 1 | ich.closed: false
>> final loop | x: 2 | ich.closed: true
>> final loop | x: 3 | ich.closed: true
>> final loop | x: 4 | ich.closed: true
```

Примечание: чтение из поля .closed канала в примере сделано только для наглядности. Рекомендуемый способ извлечения значений из канала - это `x := <-ich or { break }` в цикле `for`, который безопасно прервет цикл, когда канал закрыт и пуст.
Избегайте ручной проверки того, был ли канал закрыт или нет, так как это может привести к гонке данных, если вы не будете осторожны.
<a id="channel-select"></a>
#### Выбор каналов

Оператор `select` позволяет отслеживать несколько каналов одновременно без заметной нагрузки на ЦП. Он состоит из списка возможных передач и связанных ветвей операторов - аналогично команде [match](#match):

```v
import time

fn main() {
	ch := chan f64{}
	ch2 := chan f64{}
	ch3 := chan f64{}
	mut b := 0.0
	c := 1.0
	// ... setup spawn threads that will send on ch/ch2
	spawn fn (the_channel chan f64) {
		time.sleep(5 * time.millisecond)
		the_channel <- 1.0
	}(ch)
	spawn fn (the_channel chan f64) {
		time.sleep(1 * time.millisecond)
		the_channel <- 1.0
	}(ch2)
	spawn fn (the_channel chan f64) {
		_ := <-the_channel
	}(ch3)

	select {
		a := <-ch {
			// do something with `a`
			eprintln('> a: ${a}')
		}
		b = <-ch2 {
			// do something with predeclared variable `b`
			eprintln('> b: ${b}')
		}
		ch3 <- c {
			// do something if `c` was sent
			time.sleep(5 * time.millisecond)
			eprintln('> c: ${c} was send on channel ch3')
		}
		500 * time.millisecond {
			// do something if no channel has become ready within 0.5s
			eprintln('> more than 0.5s passed without a channel being ready')
		}
	}
	eprintln('> done')
}
```

Ветвь тайм-аута является необязательной. Если ее нет, `select` будет ждать неограниченное количество времени.
Также возможно продолжить немедленно, если ни один канал не готов в момент вызова `select`, добавив ветвь `else { ... }`. `else` и `<timeout>` взаимоисключающие.

Оператор `select` может использоваться как *выражение* типа `bool`, которое становится `false`, если все каналы закрыты:

```v wip
if select {
    ch <- a {
        // ...
    }
} {
    // channel was open
} else {
    // channel is closed
}
```
<a id="special-channel-features"></a>
#### Особые возможности каналов

Для особых целей есть некоторые встроенные поля и методы:

```v
ch := chan int{cap: 2}
println(ch.try_push(42)) // `.success` if pushed, `.not_ready` if full, `.closed` if closed
println(ch.len) // Number of items in the buffer
println(ch.cap) // Buffer capacity
println(ch.closed) // Whether the channel is closed
```

```v
struct Abc {
	x int
}

a := 2.13
ch := chan f64{}
res := ch.try_push(a) // try to perform `ch <- a`
println(res)
l := ch.len // number of elements in queue
c := ch.cap // maximum queue length
is_closed := ch.closed // bool flag - has `ch` been closed
println(l)
println(c)
mut b := Abc{}
ch2 := chan Abc{}
res2 := ch2.try_pop(mut b) // try to perform `b = <-ch2`
```

Методы `try_push/pop()` вернутся немедленно с одним из результатов:
`.success`, `.not_ready` или `.closed` - в зависимости от того, был ли объект передан или по какой причине это не произошло.
Использование этих методов и полей в производственной среде не рекомендуется -
алгоритмы, основанные на них, часто подвержены состояниям гонки. Особенно `.len` и
`.closed` не следует использовать для принятия решений.
Вместо этого используйте ветви `or`, распространение ошибок или `select` (см. [Syntax and Usage](#syntax-and-usage)
и [Channel Select](#channel-select) выше).
<a id="shared-objects"></a>
### Общие объекты

Данные могут обмениваться между потоком и вызывающим потоком через общую переменную.
Такие переменные должны создаваться как `shared` и передаваться в поток также в таком виде.
Внутренняя `структура` содержит скрытый *мьютекс*, который позволяет блокировать доступ
с помощью `rlock` для доступа только для чтения и `lock` для доступа для чтения/записи.

Примечание: общие переменные должны быть структурами, массивами или картами.
<a id="example-of-shared-objects"></a>
#### Пример общих объектов

```v
struct Counter {
mut:
	value int
}

fn (shared counter Counter) increment() {
	lock counter {
		counter.value += 1
		println('Incremented to: ${counter.value}')
	}
}

fn main() {
	shared counter := Counter{}

	spawn counter.increment()
	spawn counter.increment()

	rlock counter {
		println('Final value: ${counter.value}')
	}
}
```
<a id="difference-between-channels-and-shared-objects"></a>
### Разница между каналами и общими объектами

**Назначение**:
- Каналы: Используются для передачи сообщений между потоками, обеспечивая безопасную коммуникацию.
- Общие объекты: Используются для прямого обмена данными и модификации между потоками.

**Синхронизация**:
- Каналы: Неявная (через операции с каналами)
- Общие объекты: Явная (через блоки `rlock`/`lock`)
<a id="json"></a>
## JSON

Благодаря повсеместному распространению JSON, поддержка этого формата встроена непосредственно в V.

V генерирует код для кодирования и декодирования JSON.
Рефлексия времени выполнения не используется. Это обеспечивает значительно лучшую производительность.
<a id="decoding-json"></a>
### Декодирование JSON

```v
import json

struct Foo {
	x int
}

struct User {
	// Adding a [required] attribute will make decoding fail, if that
	// field is not present in the input.
	// If a field is not [required], but is missing, it will be assumed
	// to have its default value, like 0 for numbers, or '' for strings,
	// and decoding will not fail.
	name string @[required]
	age  int
	// Use the `@[skip]` attribute to skip certain fields.
	// You can also use `@[json: '-']`, and `@[sql: '-']`, which will cause only
	// the `json` module to skip the field, or only the SQL orm to skip it.
	foo Foo @[skip]
	// If the field name is different in JSON, it can be specified
	last_name string @[json: lastName]
}

data := '{ "name": "Frodo", "lastName": "Baggins", "age": 25, "nullable": null }'
user := json.decode(User, data) or {
	eprintln('Failed to decode json, error: ${err}')
	return
}
println(user.name)
println(user.last_name)
println(user.age)
// You can also decode JSON arrays:
sfoos := '[{"x":123},{"x":456}]'
foos := json.decode([]Foo, sfoos)!
println(foos[0].x)
println(foos[1].x)
```

Функция `json.decode` принимает два аргумента:
первый — тип, в который должно быть декодировано значение JSON,
а второй — строка, содержащая данные JSON.
<a id="encoding-json"></a>
### Кодирование JSON

```v
import json

struct User {
	name  string
	score i64
}

mut data := map[string]int{}
user := &User{
	name:  'Pierre'
	score: 1024
}

data['x'] = 42
data['y'] = 360

println(json.encode(data)) // {"x":42,"y":360}
println(json.encode(user)) // {"name":"Pierre","score":1024}
```

Модуль `json` также поддерживает анонимные поля структуры, что помогает работать со сложными JSON API, имеющими множество уровней.
<a id="testing"></a>
## Тестирование
<a id="asserts"></a>
### Утверждения

```v
fn foo(mut v []int) {
	v[0] = 1
}

mut v := [20]
foo(mut v)
assert v[0] < 4
```

Оператор `assert` проверяет, что результат вычисления его выражения равен `true`. Если утверждение не выполняется, программа обычно прерывается. Утверждения следует использовать только для обнаружения ошибок программирования. При срабатывании утверждение выводится в *stderr*, и по возможности печатаются значения с каждой стороны оператора сравнения (например, `<`, `==`). Это полезно для быстрого нахождения неожиданного значения. Операторы `assert` могут использоваться в любой функции, а не только в тестовых, что удобно при разработке нового функционала для поддержания инвариантов.

> [!NOTE]
> Все операторы `assert` *удаляются* при компиляции программы с флагом `-prod`.
<a id="asserts-with-an-extra-message"></a>
### Утверждения с дополнительным сообщением

Эта форма оператора `assert` выводит дополнительное сообщение при срабатывании. Обратите внимание, что здесь можно использовать любое строковое выражение — строковые литералы, функции, возвращающие строку, строки с интерполяцией переменных и т.д.

```v
fn test_assertion_with_extra_message_failure() {
	for i in 0 .. 100 {
		assert i * 2 - 45 < 75 + 10, 'assertion failed for i: ${i}'
	}
}
```
<a id="asserts-that-do-not-abort-your-program"></a>
### Утверждения, не прерывающие программу

При начальном прототипировании функционала и тестов иногда бывает желательно иметь утверждения, которые не останавливают программу, а только выводят сообщения о сбоях. Этого можно добиться, пометив функции, содержащие утверждения, тегом `[assert_continues]`. Например, запуск этой программы:

```v
@[assert_continues]
fn abc(ii int) {
	assert ii == 2
}

for i in 0 .. 4 {
	abc(i)
}
```

... приведет к следующему выводу:

```
assert_continues_example.v:3: FAIL: fn main.abc: assert ii == 2
   left value: ii = 0
   right value: 2
assert_continues_example.v:3: FAIL: fn main.abc: assert ii == 2
   left value: ii = 1
  right value: 2
assert_continues_example.v:3: FAIL: fn main.abc: assert ii == 2
   left value: ii = 3
  right value: 2
```

> [!NOTE]
> V также поддерживает командный флаг `-assert continues`, который глобально изменит поведение всех утверждений, как если бы вы пометили каждую функцию тегом `[assert_continues]`.
<a id="test-files"></a>
### Файлы тестов

```v
// hello.v
module main

fn hello() string {
	return 'Hello world'
}

fn main() {
	println(hello())
}
```

```v failcompile
// hello_test.v
module main

fn test_hello() {
	assert hello() == 'Hello world'
}
```

Для запуска файла теста выше используйте `v hello_test.v`. Это проверит, что функция `hello` генерирует правильный вывод. V выполняет все функции-тесты в файле.

> [!NOTE]
> Все файлы `_test.v` (как внешние, так и внутренние) компилируются как *отдельные программы*.
> Другими словами, вы можете иметь столько файлов `_test.v` и тестов в них, сколько захотите, они не повлияют на компиляцию вашего другого кода в файлах `.v` в нормальном режиме, но только при явном выполнении `v file_test.v` или `v test .`.

* Все функции-тесты должны находиться в файле теста, имя которого заканчивается на `_test.v`.
* Имена функций-тестов должны начинаться с `test_`, чтобы их пометить для выполнения.
* Обычные функции также могут определяться в файлах тестов и должны вызываться вручную. В файлах тестов также могут определяться другие символы, например, типы.
* Существует два вида тестов: внешние и внутренние.
* Внутренние тесты должны *объявлять* свой модуль, как и все остальные .v файлы из того же модуля. Внутренние тесты даже могут вызывать приватные функции в том же модуле.
* Внешние тесты должны *импортировать* модули, которые они тестируют. У них нет доступа к приватным функциям/типам модулей. Они могут тестировать только внешний/публичный API, который предоставляет модуль.

В приведенном выше примере `test_hello` является внутренним тестом, который может вызвать приватную функцию `hello()`, потому что `hello_test.v` содержит `module main`, как и `hello.v`, т.е. оба файла являются частью одного модуля. Также обратите внимание, что поскольку `module main` является обычным модулем, как и остальные, внутренние тесты могут использоваться для тестирования приватных функций в ваших основных .v файлах программы.

Вы также можете определить эти специальные функции-тесты в файле теста:

* `testsuite_begin`, которая будет запущена *перед* всеми другими функциями-тестами.
* `testsuite_end`, которая будет запущена *после* всех других функций-тестов.

Если функция-тест имеет тип возврата ошибки, любые распространенные ошибки приведут к сбою теста:

```v
import strconv

fn test_atoi() ! {
	assert strconv.atoi('1')! == 1
	assert strconv.atoi('one')! == 1 // test will fail
}
```
<a id="running-tests"></a>
### Запуск тестов

Для запуска функций-тестов в отдельном файле теста используйте `v foo_test.v`.

Для тестирования целого модуля используйте `v test mymodule`. Вы также можете использовать `v test .` для тестирования всего в текущей папке (и подпапках). Вы можете передать опцию `-stats` для получения дополнительных сведений о выполненных отдельных тестах.

Вы можете поместить дополнительные тестовые данные, включая .v исходные файлы, в папку с именем `testdata`, находящуюся рядом с вашими _test.v файлами. Тестовый фреймворк V будет *игнорировать* такие папки при сканировании для запуска тестов. Это полезно, если вы хотите поместить .v файлы с некорректным исходным кодом V или другие тесты, включая заведомо падающие, которые должны выполняться определенным образом/с опциями из родительского _test.v файла.

> [!NOTE]
> Путь к компилятору V доступен через @VEXE, поэтому _test.v файл может легко запускать *другие* файлы тестов следующим образом:

```v oksyntax
import os

fn test_subtest() {
	res := os.execute('${os.quoted_path(@VEXE)} other_test.v')
	assert res.exit_code == 1
	assert res.output.contains('other_test.v does not exist')
}
```
<a id="memory-management"></a>
## Управление памятью

V избегает выполнения ненужных выделений памяти, используя типы значений, строковые буферы, продвигая простой абстрактно-свободный стиль кода.

Существует 4 способа управления памятью в V.

По умолчанию используется минимальный и высокоэффективный трассирующий GC (сборщик мусора).

Второй способ — автосвобождение памяти (autofree), его можно включить с помощью `-autofree`. Он заботится о большинстве объектов (~90-100%): компилятор автоматически вставляет необходимые вызовы освобождения во время компиляции. Оставшийся небольшой процент объектов освобождается через GC. Разработчику не нужно менять ничего в своем коде. «Это просто работает», как в Python, Go или Java, только нет тяжелого GC, отслеживающего все, или дорогого подсчета ссылок (RC) для каждого объекта.

Для разработчиков, желающих иметь более низкоуровневый контроль, память может управляться вручную с помощью `-gc none`.

Выделение памяти на арене доступно через флаг `-prealloc`. Примечание: в настоящее время этот режим подходит только для ускорения короткоживущих, однопоточных пакетных программ (таких как компиляторы).
<a id="control"></a>
### Контроль

Вы можете воспользоваться преимуществами движка автосвобождения V и определить метод `free()` для пользовательских типов данных:

```v
struct MyType {}

@[unsafe]
fn (data &MyType) free() {
	// ...
}
```

Так же, как компилятор освобождает типы данных C с помощью `free()` из C, он будет статически вставлять вызовы `free()` для вашего типа данных в конце времени жизни каждой переменной.

Автосвобождение можно включить с помощью флага `-autofree`.

Для разработчиков, желающих иметь более низкоуровневый контроль, автосвобождение можно отключить с помощью `-manualfree` или добавив атрибут `[manualfree]` к каждой функции, которая хочет управлять своей памятью вручную. (См. [attributes](#attributes)).

> [!NOTE]
> Автосвобождение все еще в разработке. Пока оно не стабилизируется и не станет по умолчанию, пожалуйста, избегайте его использования. В настоящее время выделения памяти обрабатываются минимальным и высокоэффективным GC, пока движок автосвобождения V не будет готов к producción.

**Примеры**

```v
import strings

fn draw_text(s string, x int, y int) {
	// ...
}

fn draw_scene() {
	// ...
	name1 := 'abc'
	name2 := 'def ghi'
	draw_text('hello ${name1}', 10, 10)
	draw_text('hello ${name2}', 100, 10)
	draw_text(strings.repeat(`X`, 10000), 10, 50)
	// ...
}
```

Строки не выходят за пределы `draw_text`, поэтому они очищаются при выходе из функции.

На самом деле, с флагом `-prealloc` первые два вызова вообще не приведут к выделениям памяти. Эти две строки маленькие, поэтому V будет использовать для них предварительно выделенный буфер.

```v
struct User {
	name string
}

fn test() []int {
	number := 7 // stack variable
	user := User{} // struct allocated on stack
	numbers := [1, 2, 3] // array allocated on heap, will be freed as the function exits
	println(number)
	println(user)
	println(numbers)
	numbers2 := [4, 5, 6] // array that's being returned, won't be freed here
	return numbers2
}
```
<a id="stack-and-heap"></a>
### Стек и куча
<a id="stack-and-heap-basics"></a>
#### Основы стека и кучи

Как и в большинстве других языков программирования, данные могут храниться в двух местах:

* *Стек* обеспечивает быстрые выделения с минимальными накладными расходами на управление. Стек расширяется и сужается с глубиной вызова функции — поэтому каждая вызванная функция имеет свой сегмент стека, который остается действительным до возврата из функции. Освобождение не требуется, однако это также означает, что ссылка на объект стека становится недействительной при возврате из функции. Кроме того, пространство стека ограничено (обычно до нескольких Мегабайт на поток).
* *Куча* — это большая область памяти (обычно несколько Гигабайт), которая управляется операционной системой. Объекты кучи выделяются и освобождаются специальными вызовами функций, которые делегируют задачи управления ОС. Это означает, что они могут оставаться действительными в течение нескольких вызовов функций, однако управление ими связано с расходами.
<a id="vs-default-approach"></a>
#### Подход V по умолчанию
Из соображений производительности V старается размещать объекты на стеке, если это возможно, но выделяет их на куче, когда это явно необходимо. Пример:

```v
struct MyStruct {
	n int
}

struct RefStruct {
	r &MyStruct
}

fn main() {
	q, w := f()
	println('q: ${q.r.n}, w: ${w.n}')
}

fn f() (RefStruct, &MyStruct) {
	a := MyStruct{
		n: 1
	}
	b := MyStruct{
		n: 2
	}
	c := MyStruct{
		n: 3
	}
	e := RefStruct{
		r: &b
	}
	x := a.n + c.n
	println('x: ${x}')
	return e, &c
}
```

Здесь `a` хранится на стеке, поскольку его адрес никогда не покидает функцию `f()`. Однако ссылка на `b` является частью `e`, которая возвращается. Также возвращается ссылка на `c`. По этой причине `b` и `c` будут выделены в куче.

Ситуация становится менее очевидной, когда ссылка на объект передается в качестве аргумента функции:

```v
struct MyStruct {
mut:
	n int
}

fn main() {
	mut q := MyStruct{
		n: 7
	}
	w := MyStruct{
		n: 13
	}
	x := q.f(&w) // references of `q` and `w` are passed
	println('q: ${q}\nx: ${x}')
}

fn (mut a MyStruct) f(b &MyStruct) int {
	a.n += b.n
	x := a.n * b.n
	return x
}
```

Здесь вызов `q.f(&w)` передает ссылки на `q` и `w`, потому что в объявлении `f()` `a` имеет модификатор `mut`, а `b` имеет тип `&MyStruct`, поэтому технически эти ссылки покидают `main()`. Однако *время жизни* этих ссылок находится внутри области видимости `main()`, поэтому `q` и `w` выделяются на стеке.
<a id="manual-control-for-stack-and-heap"></a>
#### Ручное управление стеком и кучой

В последнем примере компилятор V мог поместить `q` и `w` на стек, потому что он предположил, что в вызове `q.f(&w)` эти ссылки использовались только для чтения и изменения значений, на которые они указывают, а не для передачи самих ссылок куда-либо еще. Это можно рассматривать как то, что ссылки на `q` и `w` только *заимствуются* для `f()`.

Ситуация меняется, если `f()` выполняет какие-то действия с самой ссылкой:

```v
struct RefStruct {
mut:
	r &MyStruct
}

// see discussion below
@[heap]
struct MyStruct {
	n int
}

fn main() {
	mut m := MyStruct{}
	mut r := RefStruct{
		r: &m
	}
	r.g()
	println('r: ${r}')
}

fn (mut r RefStruct) g() {
	s := MyStruct{
		n: 7
	}
	r.f(&s) // reference to `s` inside `r` is passed back to `main() `
}

fn (mut r RefStruct) f(s &MyStruct) {
	r.r = s // would trigger error without `[heap]`
}
```

Здесь `f()` выглядит совершенно безобидно, но делает неприятные вещи — она вставляет ссылку на `s` в `r`. Проблема в том, что `s` существует только пока выполняется `g()`, но `r` используется в `main()` после этого. По этой причине компилятор будет жаловаться на присваивание в `f()`, потому что `s` *"может ссылаться на объект, хранящийся на стеке"*. Предположение, сделанное в `g()`, что вызов `r.f(&s)` только заимствует ссылку на `s`, неверно.

Решением этой дилеммы является тег `[heap]` [attribute](#attributes) в объявлении `struct MyStruct`. Он указывает компилятору *всегда* выделять объекты `MyStruct` в куче. Таким образом, ссылка на `s` остается действительной даже после возврата из `g()`. Комилятор учитывает, что объекты `MyStruct` всегда выделяются в куче при проверке `f()` и позволяет присваивать ссылку на `s` полю `r.r`.

Есть паттерн, который часто встречается в других языках программирования:

```v failcompile
fn (mut a MyStruct) f() &MyStruct {
	// do something with a
	return &a // would return address of borrowed object
}
```

Здесь `f()` принимает ссылку `a` в качестве получателя, которая передается обратно вызывающему и одновременно возвращается как результат. Назначением такого объявления является цепочка вызовов методов, например `y = x.f().g()`. Однако проблема этого подхода заключается в том, что создается вторая ссылка на `a` — поэтому она не просто заимствуется, и `MyStruct` должен быть объявлен с атрибутом `[heap]`.

В V лучший подход — это:

```v
struct MyStruct {
mut:
	n int
}

fn (mut a MyStruct) f() {
	// do something with `a`
}

fn (mut a MyStruct) g() {
	// do something else with `a`
}

fn main() {
	x := MyStruct{} // stack allocated
	mut y := x
	y.f()
	y.g()
	// instead of `mut y := x.f().g()
}
```

Таким образом можно избежать атрибута `[heap]` — что обеспечивает лучшую производительность.

Однако, как упоминалось выше, пространство стека очень ограничено. По этой причине атрибут `[heap]` может быть подходящим для очень больших структур, даже если это не требуется такими варианты использования, как упомянутые выше.

Есть альтернативный способ ручного управления выделением в каждом конкретном случае. Этот подход не рекомендуется, но приводится здесь для полноты:

```v
struct MyStruct {
	n int
}

struct RefStruct {
mut:
	r &MyStruct
}

// simple function - just to overwrite stack segment previously used by `g()`

fn use_stack() {
	x := 7.5
	y := 3.25
	z := x + y
	println('${x} ${y} ${z}')
}

fn main() {
	mut m := MyStruct{}
	mut r := RefStruct{
		r: &m
	}
	r.g()
	use_stack() // to erase invalid stack contents
	println('r: ${r}')
}

fn (mut r RefStruct) g() {
	s := &MyStruct{ // `s` explicitly refers to a heap object
		n: 7
	}
	// change `&MyStruct` -> `MyStruct` above and `r.f(s)` -> `r.f(&s)` below
	// to see data in stack segment being overwritten
	r.f(s)
}

fn (mut r RefStruct) f(s &MyStruct) {
	r.r = unsafe { s } // override compiler check
}
```

Здесь проверка компилятора подавляется блоком `unsafe`. Чтобы `s` выделялся в куче даже без атрибута `[heap]`, литерал `struct` помечается амперсандом: `&MyStruct{...}`.

Этот последний шаг не требуется компилятором, но без него ссылка внутри `r` становится недействительной (область памяти, на которую она указывает, будет перезаписана `use_stack()`) и программа может аварийно завершиться (или по крайней мере выдать непредсказуемый конечный вывод). Вот почему этот подход *небезопасен* и его следует избегать!
<a id="orm"></a>
## ORM

(Это всё ещё находится на стадии альфа-тестирования)

V имеет встроенную ORM (объектно-реляционное отображение), которая поддерживает SQLite, MySQL и Postgres,
но вскоре также будет поддерживать MS SQL и Oracle.

ORM в V предоставляет ряд преимуществ:

- Единый синтаксис для всех диалектов SQL. (Миграция между базами данных становится гораздо проще.)
- Запросы строятся с использованием синтаксиса V. (Нет необходимости изучать другой синтаксис.)
- Безопасность. (Все запросы автоматически очищаются для предотвращения SQL-инъекций.)
- Проверки на этапе компиляции. (Это предотвращает опечатки, которые можно обнаружить только во время выполнения.)
- Читаемость и простота. (Вам не нужно вручную разбирать результаты запроса и затем вручную конструировать объекты из разобранных результатов.)

```v
import db.sqlite

// sets a custom table name. Default is struct name (case-sensitive)
@[table: 'customers']
struct Customer {
	id        int @[primary; serial] // a field named `id` of integer type must be the first field
	name      string
	nr_orders int
	country   ?string
}

db := sqlite.connect('customers.db')!

// You can create tables from your struct declarations. For example the next query will issue SQL similar to this:
// CREATE TABLE IF NOT EXISTS `Customer` (
//      `id` INTEGER PRIMARY KEY,
//      `name` TEXT NOT NULL,
//      `nr_orders` INTEGER NOT NULL,
//      `country` TEXT
// )
sql db {
	create table Customer
}!

// insert a new customer:
new_customer := Customer{
	name:      'Bob'
	country:   'uk'
	nr_orders: 10
}
sql db {
	insert new_customer into Customer
}!

us_customer := Customer{
	name:      'Martin'
	country:   'us'
	nr_orders: 5
}
sql db {
	insert us_customer into Customer
}!

none_country_customer := Customer{
	name:      'Dennis'
	country:   none
	nr_orders: 2
}
sql db {
	insert none_country_customer into Customer
}!

// update a customer:
sql db {
	update Customer set nr_orders = nr_orders + 1 where name == 'Bob'
}!

// select count(*) from customers
nr_customers := sql db {
	select count from Customer
}!
println('number of all customers: ${nr_customers}')

// V's syntax can be used to build queries:
uk_customers := sql db {
	select from Customer where country == 'uk' && nr_orders > 0 order by id desc limit 10
}!
println('We found a total of ${uk_customers.len} customers matching the query.')
for c in uk_customers {
	println('customer: ${c.id}, ${c.name}, ${c.country}, ${c.nr_orders}')
}

none_country_customers := sql db {
	select from Customer where country is none
}!
println('We found a total of ${none_country_customers.len} customers, with no country set.')
for c in none_country_customers {
	println('customer: ${c.id}, ${c.name}, ${c.country}, ${c.nr_orders}')
}

// delete a customer
sql db {
	delete from Customer where name == 'Bob'
}!
```

Больше примеров и документацию см. в [vlib/orm](https://github.com/vlang/v/tree/master/vlib/orm).
<a id="troubleshooting-compilation-problems-with-sqlite-on-windows"></a>
### Устранение проблем компиляции с SQLite на Windows
На Windows, если вы получаете ошибку компиляции, связанную с отсутствующим файлом sqlite3.h, вам необходимо выполнить:
`v vlib/db/sqlite/install_thirdparty_sqlite.vsh` один раз, а затем повторить попытку компиляции.
<a id="using-the-self-contained-sqlite-module"></a>
### Использование автономного модуля SQLite
V также поддерживает отдельный модуль `sqlite`, который оборачивает объединение SQLite, но в остальном имеет такой же API, как модуль `db.sqlite`. Его преимущество в том, что с ним вам не нужно устанавливать отдельный системный пакет/библиотеку sqlite в вашей системе (что может быть затруднительно в некоторых системах, например, Windows или системах с musl).
Его недостаток в том, что он может немного замедлить ваши компиляции (так как он компилирует SQLite из C, вдобавок к вашему собственному коду).

Для использования этого модуля сделайте:
```sh
v install sqlite
```
а затем, в вашем коде, используйте это:
```v ignore
import sqlite
```
вместо:
```v ignore
import db.sqlite
```
<a id="writing-documentation"></a>
## Написание документации

Принцип работы очень похож на Go. Это очень просто: нет необходимости
отдельно писать документацию для вашего кода,
vdoc сгенерирует её из строк документации в исходном коде.

Документация для каждой функции/типа/константы должна быть размещена непосредственно перед объявлением:

```v
// clearall clears all bits in the array
fn clearall() {
}
```

Комментарий должен начинаться с имени определения.

Иногда одной строки недостаточно, чтобы объяснить, что делает функция. В таких случаях комментарии должны
охватывать документируемую функцию с использованием комментариев в одну строку:

```v
// copy_all recursively copies all elements of the array by their value,
// if `dupes` is false all duplicate values are eliminated in the process.
fn copy_all(dupes bool) {
	// ...
}
```

По соглашению предпочтительно, чтобы комментарии писались в *настоящем времени*.

Обзор модуля должен быть помещён в первый комментарий сразу после имени модуля.

Для генерации документации используйте vdoc, например `v doc net.http`.
<a id="newlines-in-documentation-comments"></a>
### Переносы строк в комментариях к документации

Комментарии, охватывающие несколько строк, объединяются с помощью пробелов, если только

- строка пуста
- строка состоит из как минимум 3 символов `-`, `=`, `_`, `*`, `~` (горизонтальная линия)
- строка начинается как минимум с одного `#` и пробела (заголовок)
- строка начинается и заканчивается символом `|` (таблица)
- строка начинается с `- ` (список)
<a id="tools"></a>
## Инструменты
<a id="v-fmt"></a>
### v fmt

Вам не нужно беспокоиться о форматировании вашего кода или установке стандартов стиля.
`v fmt` позаботится об этом:

```shell
v fmt file.v
```

Рекомендуется настроить ваш редактор так, чтобы `v fmt -w` выполнялся при каждом сохранении.
Выполнение vfmt обычно очень быстрое (занимает <30 мс).

Всегда запускайте `v fmt -w file.v` перед отправкой вашего кода.
<a id="disabling-the-formatting-locally"></a>
#### Отключение форматирования локально

Чтобы отключить форматирование для блока кода, оберните его комментариями `// vfmt off` и
`// vfmt on`.

```bash
// Not affected by fmt
// vfmt off

... your code here ...

// vfmt on

// Affected by fmt
... your code here ...
```
<a id="v-shader"></a>
### v shader

Вы можете использовать GPU шейдеры в графических приложениях на V. Вы пишете ваши шейдеры на
[annotated GLSL dialect](https://github.com/vlang/v/blob/master/examples/sokol/02_cubes_glsl/cube_glsl.glsl)
и используете `v shader` для их компиляции для всех поддерживаемых целевых платформ.

```shell
v shader /path/to/project/dir/or/file.v
```

В настоящее время вам необходимо
[include a header and declare a glue function](https://github.com/vlang/v/blob/master/examples/sokol/02_cubes_glsl/cube_glsl.v#L25-L28)
перед использованием шейдера в вашем коде.
<a id="profiling"></a>
### Профилирование

V имеет хорошую поддержку профилирования ваших программ: `v -profile profile.txt run file.v`
Это создаст файл profile.txt, который вы затем сможете проанализировать.

Сгенерированный файл profile.txt будет содержать строки с 4 столбцами:

1. Сколько раз была вызвана функция.
2. Сколько времени в общей сложности заняла функция (в мс).
3. Сколько времени заняла функция (в мс) сама по себе, без вызовов внутри неё.
   Это надёжно для многопоточных программ, когда tcc не используется.
4. Сколько времени в среднем занимал один вызов функции (в нс).
5. Имя функции v.

Вы можете отсортировать по 3-му столбцу (среднее время на функцию), используя:
`sort -n -k3 profile.txt|tail`

Вы также можете использовать секундомеры для явного измерения только частей вашего кода:

```v
import time

fn main() {
	sw := time.new_stopwatch()
	println('Hello world')
	println('Greeting the world took: ${sw.elapsed().nanoseconds()}ns')
}
```
<a id="package-management"></a>
## Управление пакетами

V *модуль* — это одна папка с файлами .v внутри. V *пакет* может
содержать один или несколько модулей V. V *пакет* должен иметь файл `v.mod`
в его корневой папке, описывающий содержимое пакета.

Пакеты V устанавливаются обычно в вашу папку `~/.vmodules`. Это
местоположение можно переопределить, установив переменную среды `VMODULES`.
<a id="package-commands"></a>
### Команды пакетов

Вы можете использовать интерфейс V для выполнения операций с пакетами, так же, как вы можете
использовать его для компиляции кода, форматирования кода, проверки кода и т.д.

```powershell
v [package_command] [param]
```

где команда пакета может быть одной из:

```
   install           Install a package from VPM.
   remove            Remove a package that was installed from VPM.
   search            Search for a package from VPM.
   update            Update an installed package from VPM.
   upgrade           Upgrade all the outdated packages.
   list              List all installed packages.
   outdated          Show installed packages that need updates.
```

Вы можете устанавливать пакеты, уже созданные кем-то другим, с помощью [VPM](https://vpm.vlang.io/):

```powershell
v install [package]
```

**Пример:**

```powershell
v install ui
```

Пакеты могут быть установлены непосредственно из git или mercurial репозиториев.

```powershell
v install [--once] [--git|--hg] [url]
```

**Пример:**

```powershell
v install --git https://github.com/vlang/markdown
```

Иногда вы можете захотеть установить зависимости **ТОЛЬКО** в том случае, если они ещё не установлены:

```
v install --once [package]
```

Удаление пакета с помощью v:

```powershell
v remove [package]
```

**Пример:**

```powershell
v remove ui
```

Обновление установленного пакета из [VPM](https://vpm.vlang.io/):

```powershell
v update [package]
```

**Пример:**

```powershell
v update ui
```

Или вы можете обновить все ваши пакеты:

```powershell
v update
```

Чтобы увидеть все установленные вами пакеты, вы можете использовать:

```powershell
v list
```

**Пример:**

```powershell
> v list
Installed packages:
  markdown
  ui
```

Чтобы увидеть все пакеты, которым требуются обновления:

```powershell
v outdated
```

**Пример:**

```powershell
> v outdated
Package are up to date.
```
<a id="publish-package"></a>
### Публикация пакета

1. Поместите файл `v.mod` в корневую папку вашего пакета (если вы
   создали ваш пакет с помощью команды `v new mypackage` или `v init`,
   у вас уже есть файл `v.mod`).

   ```sh
   v new mypackage
   Input your project description: My nice package.
   Input your project version: (0.0.0) 0.0.1
   Input your project license: (MIT)
   Initialising ...
   Complete!
   ```

   Пример `v.mod`:
   ```v ignore
   Module {
       name: 'mypackage'
       description: 'My nice package.'
       version: '0.0.1'
       license: 'MIT'
       dependencies: []
   }
   ```

   Минимальная структура файлов:
   ```
   v.mod
   mypackage.v
   ```

   Имя вашего пакета должно использоваться с директивой `module`
   в начале всех файлов в вашем пакете. Для `mypackage.v`:
   ```v
   module mypackage

   pub fn hello_world() {
       println('Hello World!')
   }
   ```

2. Создайте git-репозиторий в папке с файлом `v.mod`
   (это не требуется, если вы использовали `v new` или `v init`):
   ```sh
   git init
   git add .
   git commit -m "INIT"
   ````

3. Создайте публичный репозиторий на github.com.
4. Подключите ваш локальный репозиторий к удалённому репозиторию и отправьте изменения.
5. Добавьте ваш пакет в публичный реестр пакетов V VPM:
   https://vpm.vlang.io/new

   Вам потребуется войти в систему с помощью вашего аккаунта Github для регистрации пакета.
   **Предупреждение:** _В настоящее время невозможно изменить вашу запись после отправки.
   Внимательно проверьте имя вашего пакета и URL github, так как вы не сможете изменить это позже._
6. Итоговое имя пакета — это комбинация вашего аккаунта github и
   предоставленного вами имени пакета, например, `mygithubname.mypackage`.

**По желанию:** пометьте ваш пакет V тегами `vlang` и `vlang-package` на github.com
для улучшения поиска.

# Продвинутые темы
<a id="attributes"></a>
## Атрибуты

V имеет несколько атрибутов, которые изменяют поведение функций и структур.

Атрибут — это инструкция компилятора, указанная внутри `[]` непосредственно перед объявлением
функции/структуры/перечисления и применяемая только к следующему объявлению.

```v
// @[flag] enables Enum types to be used as bitfields

@[flag]
enum BitField {
	read
	write
	other
}

fn main() {
	assert 1 == int(BitField.read)
	assert 2 == int(BitField.write)
	mut bf := BitField.read
	assert bf.has(.read | .other) // test if *at least one* of the flags is set
	assert !bf.all(.read | .other) // test if *all* of the flags are set
	bf.set(.write | .other)
	assert bf.has(.read | .write | .other)
	assert bf.all(.read | .write | .other)
	bf.toggle(.other)
	assert bf == BitField.read | .write
	assert bf.all(.read | .write)
	assert !bf.has(.other)
	empty := BitField.zero()
	assert empty.is_empty()
	assert !empty.has(.read)
	assert !empty.has(.write)
	assert !empty.has(.other)
	mut full := empty
	full.set_all()
	assert int(full) == 7 // 0x01 + 0x02 + 0x04
	assert full == .read | .write | .other
	mut v := full
	v.clear(.read | .other)
	assert v == .write
	v.clear_all()
	assert v == empty
	assert BitField.read == BitField.from('read')!
	assert BitField.other == BitField.from('other')!
	assert BitField.write == BitField.from(2)!
	assert BitField.zero() == BitField.from('')!
}
```

```v
// @[_allow_multiple_values] allows an enum to have multiple duplicate values.
// Use it carefully, only when you really need it.

@[_allow_multiple_values]
enum ButtonStyle {
	primary   = 1
	secondary = 2
	success   = 3

	blurple = 1
	grey    = 2
	gray    = 2
	green   = 3
}

fn main() {
	assert int(ButtonStyle.primary) == 1
	assert int(ButtonStyle.blurple) == 1

	assert int(ButtonStyle.secondary) == 2
	assert int(ButtonStyle.gray) == 2
	assert int(ButtonStyle.grey) == 2

	assert int(ButtonStyle.success) == 3
	assert int(ButtonStyle.green) == 3

	assert ButtonStyle.primary == ButtonStyle.blurple
	assert ButtonStyle.secondary == ButtonStyle.grey
	assert ButtonStyle.secondary == ButtonStyle.gray
	assert ButtonStyle.success == ButtonStyle.green
}
```

Устаревшие поля структур:

```v oksyntax
module abc

// Note that only *direct* accesses to Xyz.d in *other modules*, will produce deprecation notices/warnings:
pub struct Xyz {
pub mut:
	a int
	d int @[deprecated: 'use Xyz.a instead'; deprecated_after: '2999-03-01']
	// the tags above, will produce a notice, since the deprecation date is in the far future
}
```

Устаревшие функции/методы:

Функции устаревают до окончательного удаления, чтобы дать пользователям время на миграцию кода.
В большинстве случаев предпочтительнее указывать дату. Немедленное изменение без даты устаревания
может использоваться для функций, которые оказались концептуально сломанными и устаревшими из-за
появления гораздо лучшей функциональности. В остальных случаях рекомендуется устанавливать дату,
чтобы предоставить пользователям льготный период.

Устаревшие функции вызывают предупреждения, которые становятся ошибками при сборке с флагом `-prod`.
Чтобы избежать немедленного нарушения CI, рекомендуется устанавливать будущую дату, предшествующую
дате слияния кода. Это дает возможность разработчикам активных проектов на V увидеть уведомление
об устаревании хотя бы один раз и исправить использования. Установка даты в ближайшие 30 дней
предполагает, что они скомпилировали свои проекты вручную хотя бы раз в этот период. Для небольших
изменений этого должно быть достаточно. Для сложных изменений это время может потребоваться больше.

Различные проекты и сопровождающие V могут обоснованно выбирать разные политики устаревания.
В зависимости от типа и воздействия изменения, возможно, стоит сначала проконсультироваться с ними,
прежде чем устаревать функцию.


```v
// Calling this function will result in a deprecation warning

@[deprecated]
fn old_function() {
}

// It can also display a custom deprecation message

@[deprecated: 'use new_function() instead']
fn legacy_function() {}

// You can also specify a date, after which the function will be
// considered deprecated. Before that date, calls to the function
// will be compiler notices - you will see them, but the compilation
// is not affected. After that date, calls will become warnings,
// so ordinary compiling will still work, but compiling with -prod
// will not (all warnings are treated like errors with -prod).
// 6 months after the deprecation date, calls will be hard
// compiler errors.

@[deprecated: 'use new_function2() instead']
@[deprecated_after: '2021-05-27']
fn legacy_function2() {}
```

```v globals
// This function's calls will be inlined.
@[inline]
fn inlined_function() {
}

// This function's calls will NOT be inlined.
@[noinline]
fn function() {
}

// This function will NOT return to its callers.
// Such functions can be used at the end of or blocks,
// just like exit/1 or panic/1. Such functions can not
// have return types, and should end either in for{}, or
// by calling other `[noreturn]` functions.
@[noreturn]
fn forever() {
	for {}
}

// The following struct must be allocated on the heap. Therefore, it can only be used as a
// reference (`&Window`) or inside another reference (`&OuterStruct{ Window{...} }`).
// See section "Stack and Heap"
@[heap]
struct Window {
}

// Calls to following function must be in unsafe{} blocks.
// Note that the code in the body of `risky_business()` will still be
// checked, unless you also wrap it in `unsafe {}` blocks.
// This is useful, when you want to have an `[unsafe]` function that
// has checks before/after a certain unsafe operation, that will still
// benefit from V's safety features.
@[unsafe]
fn risky_business() {
	// code that will be checked, perhaps checking pre conditions
	unsafe {
		// code that *will not be* checked, like pointer arithmetic,
		// accessing union fields, calling other `[unsafe]` fns, etc...
		// Usually, it is a good idea to try minimizing code wrapped
		// in unsafe{} as much as possible.
		// See also [Memory-unsafe code](#memory-unsafe-code)
	}
	// code that will be checked, perhaps checking post conditions and/or
	// keeping invariants
}

// V's autofree engine will not take care of memory management in this function.
// You will have the responsibility to free memory manually yourself in it.
// Note: it is NOT related to the garbage collector. It will only make the
// -autofree mechanism, ignore the body of that function.
@[manualfree]
fn custom_allocations() {
}

// The memory pointed to by the pointer arguments of this function will not be
// freed by the garbage collector (if in use) before the function returns
// For C interop only.
@[keep_args_alive]
fn C.my_external_function(voidptr, int, voidptr) int

// A @[weak] tag tells the C compiler, that the next declaration will be weak, i.e. when linking,
// if there is another declaration of a symbol with the same name (a 'strong' one), it should be
// used instead, *without linker errors about duplicate symbols*.
// For C interop only.

@[weak]
__global abc = u64(1)

// Tell V, that the following global was defined on the C side,
// thus V will not initialise it, but will just give you access to it.
// For C interop only.

@[c_extern]
__global my_instance C.my_struct
struct C.my_struct {
	a int
	b f64
}

// Tell V that the following struct is defined with `typedef struct` in C.
// For C interop only.
@[typedef]
pub struct C.Foo {}

// Used to add a custom calling convention to a function, available calling convention: stdcall, fastcall and cdecl.
// This list also applies for type aliases (see below).
// For C interop only.
@[callconv: 'stdcall']
fn C.DefWindowProc(hwnd int, msg int, lparam int, wparam int)

// Used to add a custom calling convention to a function type aliases.
// For C interop only.

@[callconv: 'fastcall']
type FastFn = fn (int) bool

// Calls to the following function, will have to use its return value somehow.
// Ignoring it, will emit warnings.
@[must_use]
fn f() int {
	return 42
}

fn g() {
	// just calling `f()` here, will produce a warning
	println(f()) // this is fine, because the return value was used as an argument
}

// Windows only (and obsolete; instead of it, use `-subsystem windows` when compiling)
// Without this attribute all graphical apps will have the following behavior on Windows:
// If run from a console or terminal; keep the terminal open so all (e)println statements can be viewed.
// If run from e.g. Explorer, by double-click; app is opened, but no terminal is opened, and no
// (e)println output can be seen.
// Use it to force-open a terminal to view output in, even if the app is started from Explorer.
// Valid before main() only.
@[console]
fn main() {
}
```
<a id="conditional-compilation"></a>
## Условная компиляция

Целью этой функции является указание V *не компилировать* функцию и все ее вызовы в итоговом
исполняемом файле, если не передан указанный пользовательский флаг.

V по-прежнему будет выполнять проверку типов функции и всех ее вызовов, *даже* если они не будут
присутствовать в итоговом исполняемом файле из-за переданных флагов -d.

Чтобы увидеть это в действии, запустите следующий пример с помощью `v run example.v` один раз,
а затем во второй раз с помощью `v -d trace_logs run example.v`:
```v
@[if trace_logs ?]
fn elog(s string) {
	eprintln(s)
}

fn main() {
	elog('some expression: ${2 + 2}') // such calls will not be done *at all*, if `-d trace_logs` is not passed
	println('hi')
	elog('finish')
}
```

Условная компиляция, основанная на пользовательских флагах, также может использоваться для создания
несколько различных исполняемых файлов, которые разделяют большую часть общего кода, но в которых
часть логики требуется только время от времени. Например, программу сетевого сервера/клиента можно
написать следующим образом:
```v ignore
fn act_as_client() { ... }
fn act_as_server() { ... }
fn main() {
	$if as_client ? {
		act_as_client()
	}
	$if as_server ? {
		act_as_server()
	}
}
```
Чтобы создать исполняемый файл `client.exe`, выполните: `v -d as_client -o client.exe .`
Чтобы создать исполняемый файл `server.exe`, выполните: `v -d as_server -o server.exe .`
<a id="compile-time-pseudo-variables"></a>
### Псевдопеременные времени компиляции

V также предоставляет вашему коду доступ к набору псевдостроковых переменных,
которые заменяются во время компиляции:

- `@FN` => заменяется именем текущей функции V.
- `@METHOD` => заменяется на ReceiverType.MethodName.
- `@MOD` => заменяется именем текущего модуля V.
- `@STRUCT` => заменяется именем текущей структуры V.
- `@FILE` => заменяется абсолютным путем к исходному файлу V.
- `@DIR` => заменяется абсолютным путем к *папке*, в которой находится исходный файл V.
- `@LINE` => заменяется номером строки V, где она появляется (как строка).
- `@FILE_LINE` => как `@FILE:@LINE`, но часть файла является относительным путем.
- `@LOCATION` => файл, строка и имя текущего типа + метода; подходит для журналирования.
- `@COLUMN` => заменяется номером столбца, где он появляется (как строка).
- `@VEXE` => заменяется путем к компилятору V.
- `@VEXEROOT`  => будет заменен на *папку*, в которой находится исполняемый файл V (как строка).
- `@VHASH`  => заменяется сокращенным хэшем коммита компилятора V (как строка).
- `@VCURRENTHASH` => Похоже на `@VHash`, но изменяется, когда компилятор перекомпилируется
  на другом коммите (после локальных изменений или использования git bisect и т.д.).
- `@VMOD_FILE` => заменяется содержимым ближайшего файла v.mod (как строка).
- `@VMODHASH` => заменяется сокращенным хэшем коммита, полученным из директории .git
  рядом с ближайшим файлом v.mod (как строка).
- `@VMODROOT` => будет заменен на *папку*, в которой находится ближайший файл v.mod (как строка).
- `@BUILD_DATE` => заменяется датой сборки, например '2024-09-13'.
- `@BUILD_TIME` => заменяется временем сборки, например '12:32:07'.
- `@BUILD_TIMESTAMP` => заменяется временной меткой сборки, например '1726219885'.
- `@OS` => заменяется типом ОС, например 'linux'.
- `@CCOMPILER` => заменяется типом компилятора C, например 'gcc'.
- `@BACKEND` => заменяется текущим бэкендом языка, например 'c' или 'golang'.
- `@PLATFORM` => заменяется типом платформы, например 'amd64'.
Примечание: `@BUILD_DATE`, `@BUILD_TIME`, `@BUILD_TIMESTAMP` представляют время в часовом поясе UTC.
По умолчанию они основаны на текущем времени компиляции/сборки. Их можно переопределить,
установив переменную окружения `SOURCE_DATE_EPOCH`. Это также полезно при создании релизов,
поскольку вы можете использовать эквивалент этого в вашей системе сборки/скрипте:
`export SOURCE_DATE_EPOCH=$(git log -1 --pretty=%ct) ;`, а затем использовать `@BUILD_DATE` и т.д.
в вашей программе, когда вы, например, печатаете информацию о версии для пользователей.
См. также https://reproducible-builds.org/docs/source-date-epoch/.

Псевдопеременные времени компиляции позволяют вам выполнить следующий
пример, который полезен при отладке/журналировании/трассировке вашего кода:

```v
eprintln(@LOCATION)
```

Еще один пример — если вы хотите встроить версию/имя из v.mod *внутрь* вашего исполняемого файла:

```v ignore
import v.vmod

vm := vmod.decode( @VMOD_FILE )!
eprintln('${vm.name} ${vm.version}\n${vm.description}')
```

Программа, которая печатает собственный исходный код (квин):
```v
print($embed_file(@FILE).to_string())
```

> [!NOTE]
> в файле может быть произвольный исходный код без проблем, поскольку весь файл
> будет встроен в исполняемый файл, полученный его компиляцией. Также обратите внимание, что печать
> выполняется с помощью `print`, а не `println`, чтобы не добавлять еще одну новую строку, отсутствующую в
> исходном коде.

Программа, которая печатает время своей сборки:
```v
import time

println('This program, was compiled at ${time.unix(@BUILD_TIMESTAMP.i64()).format_ss_milli()} .')
```
<a id="compile-time-reflection"></a>
### Отражение времени компиляции

`$` используется как префикс для операций времени компиляции (также называемых «comptime»).

Наличие встроенной поддержки JSON — это хорошо, но V также позволяет вам создавать эффективные
сериализаторы для любого формата данных. V имеет конструкции `if` и `for` времени компиляции:
<a id="comptime-fields"></a>
#### <h4 id="comptime-fields">.fields</h4>

Вы можете перебирать поля структуры с помощью `.fields`, это также работает с generic типами
(например, `T.fields`) и generic аргументами (например, `param.fields` где `fn gen[T](param T) {`).

```v
struct User {
	name string
	age  int
}

fn main() {
	$for field in User.fields {
		$if field.typ is string {
			println('${field.name} is of type string')
		}
	}
}

// Output:
// name is of type string
```
<a id="comptime-values"></a>
#### <h4 id="comptime-values">.values</h4>

Вы можете читать [Enum](#enums) значения и их атрибуты.

```v
enum Color {
	red   @[RED]  // first attribute
	blue  @[BLUE] // second attribute
}

fn main() {
	$for e in Color.values {
		println(e.name)
		println(e.attrs)
	}
}

// Output:
// red
// ['RED']
// blue
// ['BLUE']
```
<a id="comptime-attrs"></a>
#### <h4 id="comptime-attrs">.attributes</h4>

Вы можете читать [Struct](#structs) атрибуты.

```v
@[COLOR]
struct Foo {
	a int
}

fn main() {
	$for e in Foo.attributes {
		println(e)
	}
}

// Output:
// StructAttribute{
//    name: 'COLOR'
//    has_arg: false
//    arg: ''
//    kind: plain
// }
```
<a id="comptime-variants"></a>
#### <h4 id="comptime-variants">.variants</h4>

Вы можете читать вариантные типы из [Sum type](#sum-types).

```v
type MySum = int | string

fn main() {
	$for v in MySum.variants {
		$if v.typ is int {
			println('has int type')
		} $else $if v.typ is string {
			println('has string type')
		}
	}
}

// Output:
// has int type
// has string type
```
<a id="comptime-methods"></a>
#### <h4 id="comptime-methods">.methods</h4>

Вы можете получить информацию о методах структуры.

```v
struct Foo {
}

fn (f Foo) test() int {
	return 123
}

fn (f Foo) test2() string {
	return 'foo'
}

fn main() {
	foo := Foo{}
	$for m in Foo.methods {
		$if m.return_type is int {
			print('${m.name} returns int: ')
			println(foo.$method())
		} $else $if m.return_type is string {
			print('${m.name} returns string: ')
			println(foo.$method())
		}
	}
}

// Output:
// test returns int: 123
// test2 returns string: foo
```
<a id="comptime-method-params"></a>
#### <h4 id="comptime-method-params">.params</h4>

Вы можете получить информацию о параметрах метода структуры.

```v
struct Test {
}

fn (t Test) foo(arg1 int, arg2 string) {
}

fn main() {
	$for m in Test.methods {
		$for param in m.params {
			println('${typeof(param.typ).name}: ${param.name}')
		}
	}
}

// Output:
// int: arg1
// string: arg2
```

См. [`examples/compiletime/reflection.v`](/examples/compiletime/reflection.v)
для более полного примера.
<a id="compile-time-code"></a>
### Код времени компиляции
<a id="if-condition"></a>
#### Условие `$if`

```v
fn main() {
	// Support for multiple conditions in one branch
	$if ios || android {
		println('Running on a mobile device!')
	}
	$if linux && x64 {
		println('64-bit Linux.')
	}
	// Usage as expression
	os := $if windows { 'Windows' } $else { 'UNIX' }
	println('Using ${os}')
	// $else-$if branches
	$if tinyc {
		println('tinyc')
	} $else $if clang {
		println('clang')
	} $else $if gcc {
		println('gcc')
	} $else {
		println('different compiler')
	}
	$if test {
		println('testing')
	}
	// v -cg ...
	$if debug {
		println('debugging')
	}
	// v -prod ...
	$if prod {
		println('production build')
	}
	// v -d option ...
	$if option ? {
		println('custom option')
	}
}
```

Если вы хотите, чтобы `if` вычислялся во время компиляции, он должен иметь префикс в виде символа `$`.
В настоящее время его можно использовать для обнаружения ОС, компилятора, платформы или опций компиляции.
`$if debug` — специальная опция, аналогично `$if windows` или `$if x32`, она включена, если программа
скомпилирована с `v -g` или `v -cg`.
Если вы используете пользовательский ifdef, то вам действительно нужен `$if option ? {}` и компиляция с `v -d option`.
Полный список встроенных опций:

| ОС                             | Компиляторы        | Платформы                     | Прочее                                         |
|--------------------------------|------------------|-------------------------------|-----------------------------------------------|
| `windows`, `linux`, `macos`    | `gcc`, `tinyc`   | `amd64`, `arm64`, `aarch64`   | `debug`, `prod`, `test`                       |
| `darwin`, `ios`, `bsd`         | `clang`, `mingw` | `i386`, `arm32`               | `js`, `glibc`, `prealloc`                     |
| `freebsd`, `openbsd`, `netbsd` | `msvc`           | `rv64`, `rv32`, `s390x`       | `no_bounds_checking`, `freestanding`          |
| `android`, `mach`, `dragonfly` | `cplusplus`      | `ppc64le`                     | `no_segfault_handler`, `no_backtrace`         |
| `gnu`, `hpux`, `haiku`, `qnx`  |                  | `x64`, `x32`                  | `no_main`, `fast_math`, `apk`, `threads`      |
| `solaris`, `termux`            |                  | `little_endian`, `big_endian` | `js_node`, `js_browser`, `js_freestanding`    |
| `serenity`, `vinix`, `plan9`   |                  |                               | `interpreter`, `es5`, `profile`, `wasm32`     |
|                                |                  |                               | `wasm32_emscripten`, `wasm32_wasi`            |
|                                |                  |                               | `native`, `autofree`                          |
<a id="embed_file"></a>
#### `$embed_file`

```v ignore
import os
fn main() {
	embedded_file := $embed_file('v.png')
	os.write_file('exported.png', embedded_file.to_string())!
}
```

V может встраивать произвольные файлы в исполняемый файл с помощью вызова времени компиляции
`$embed_file(<path>)`. Пути могут быть абсолютными или относительно исходного файла.

Обратите внимание, что по умолчанию использование `$embed_file(file)` всегда встраивает все содержимое
файла, но вы можете изменить это поведение, передав: `-d embed_only_metadata`
при компиляции вашей программы. В этом случае файл не будет встроен. Вместо этого,
он будет загружен *в первый раз*, когда ваша программа вызовет `embedded_file.data()` во время выполнения,
что упрощает изменение в внешних редакторах программ без необходимости перекомпиляции
вашей программы.

Встраивание файла в ваш исполняемый файл увеличит его размер, но
сделает его более самодостаточным и, таким образом, более удобным для распространения.
Когда это происходит (по умолчанию), `embedded_file.data()` *не выполняет ввода/вывода*
и всегда возвращает одни и те же данные.

`$embed_file` поддерживает сжатие встроенного файла при компиляции с `-prod`.
В настоящее время поддерживается только один тип сжатия: `zlib`.

```v ignore
import os
fn main() {
	embedded_file := $embed_file('x.css', .zlib) // compressed using zlib
	os.write_file('exported.css', embedded_file.to_string())!
}
```

Примечание: сжатие бинарных ресурсов, таких как файлы png или zip, обычно не дает особой выгоды,
а в некоторых случаях может даже занять больше места в итоговом исполняемом файле, поскольку они
уже сжаты.

`$embed_file` возвращает
[EmbedFileData](https://modules.vlang.io/v.embed_file.html#EmbedFileData)
который может использоваться для получения содержимого файла как `string` или `[]u8`.
<a id="tmpl-for-embedding-and-parsing-v-template-files"></a>
#### `$tmpl` для встраивания и разбора файлов шаблонов V

V имеет простой язык шаблонов для текстовых и html шаблонов, и их можно легко
встраивать через `$tmpl('path/to/template.txt')`:

```v ignore
fn build() string {
	name := 'Peter'
	age := 25
	numbers := [1, 2, 3]
	return $tmpl('1.txt')
}

fn main() {
	println(build())
}
```

1.txt:

```
name: @name

age: @age

numbers: @numbers

@for number in numbers
  @number
@end
```

вывод:

```
name: Peter

age: 25

numbers: [1, 2, 3]

1
2
3
```

См. больше [details](https://github.com/vlang/v/blob/master/vlib/v/TEMPLATES.md)
<a id="env"></a>
#### `$env`

```v
module main

fn main() {
	compile_time_env := $env('ENV_VAR')
	println(compile_time_env)
}
```

V может получать значения во время компиляции из переменных окружения.
`$env('ENV_VAR')` также может использоваться в верхнеуровневых операторах `#flag` и `#include`:
`#flag linux -I $env('JAVA_HOME')/include`.
<a id="d"></a>
#### `$d`

V может получать значения во время компиляции из определений флагов `-d ident=value`,
переданных в командной строке компилятору. Вы также можете передать `-d ident`, что будет иметь
тот же смысл, что и передача `-d ident=true`.

Чтобы получить значение в вашем коде, используйте: `$d('ident', default)`, где `default`
может быть `false` для булевых, `0` или `123` для чисел i64, `0.0` или `113.0`
для чисел f64, `'a string'` для строк.

Когда флаг не предоставлен через командную строку, `$d()` вернет значение `default`,
указанное как *второй* аргумент.

```v
module main

const my_i64 = $d('my_i64', 1024)

fn main() {
	compile_time_value := $d('my_string', 'V')
	println(compile_time_value)
	println(my_i64)
}
```

Запуск приведенного выше кода с помощью `v run .` выведет:
```
V
1024
```

Запуск приведенного выше кода с помощью `v -d my_i64=4096 -d my_string="V rocks" run .` выведет:
```
V rocks
4096
```

Вот пример того, как использовать значения по умолчанию, которые должны быть *чистыми* литералами:
```v
fn main() {
	val_str := $d('id_str', 'value') // can be changed by providing `-d id_str="my id"`
	val_f64 := $d('id_f64', 42.0) // can be changed by providing `-d id_f64=84.0`
	val_i64 := $d('id_i64', 56) // can be changed by providing `-d id_i64=123`
	val_bool := $d('id_bool', false) // can be changed by providing `-d id_bool=true`
	val_char := $d('id_char', `f`) // can be changed by providing `-d id_char=v`
	println(val_str)
	println(val_f64)
	println(val_i64)
	println(val_bool)
	println(rune(val_char))
}
```

`$d('ident','value')` также может использоваться в верхнеуровневых операторах, таких как `#flag` и `#include`:
`#flag linux -I $d('my_include','/usr')/include`. Значение по умолчанию для `$d` при использовании в этих
операторах должно быть литералом `string`.

`$d('ident', false)` также может использоваться внутри операторов `$if $d('ident', false) {`,
предоставляя вам возможность избирательно включать/выключать определенные фрагменты кода во время компиляции,
без изменения исходного кода или поддержки различных его версий.
<a id="compile_error-and-compile_warn"></a>
#### `$compile_error` и `$compile_warn`

Эти две функции времени компиляции очень полезны для отображения пользовательских ошибок/предупреждений во время
компиляции.

Обе принимают в качестве единственного аргумента строковый литерал, содержащий отображаемое сообщение:

```v failcompile nofmt
// x.v
module main

$if linux {
    $compile_error('Linux is not supported')
}

fn main() {
}

$ v run x.v
x.v:4:5: error: Linux is not supported
    2 |
    3 | $if linux {
    4 |     $compile_error('Linux is not supported')
      |     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    5 | }
    6 |
```
<a id="compile-time-types"></a>
### Типы времени компиляции

Типы времени компиляции группируют несколько типов в общий более высокий тип. Это полезно в
функциях с generic параметрами, где входной тип должен иметь определенное свойство, например
атрибут `.len` в массивах.

V поддерживает следующие типы времени компиляции:

- `$alias` => соответствует [Type aliases](#type-aliases).
- `$array` => соответствует [Arrays](#arrays) и [Fixed Size Arrays](#fixed-size-arrays).
- `$array_dynamic` => соответствует [Arrays](#arrays), но не [Fixed Size Arrays](#fixed-size-arrays).
- `$array_fixed` => соответствует [Fixed Size Arrays](#fixed-size-arrays), но не [Arrays](#arrays)
- `$enum` => соответствует [Enums](#enums).
- `$float` => соответствует `f32`, `f64` и литералам с плавающей точкой.
- `$function` => соответствует [Function Types](#function-types).
- `$int` => соответствует `int`, `i8`, `i16`, `i32`, `i64`, `u8`, `u16`, `u32`, `u64`, `isize`, `usize`
  и целочисленным литералам.
- `$interface` => соответствует [Interfaces](#interfaces).
- `$map` => соответствует [Maps](#maps).
- `$option` => соответствует [Option Types](#optionresult-types-and-error-handling).
- `$shared` => соответствует [Shared Types](#shared-objects).
- `$struct` => соответствует [Structs](#structs).
- `$sumtype` => соответствует [Sum Types](#sum-types).
- `$string` => соответствует [Strings](#strings).
- `$pointer` => соответствует [Reference Types](#references).
- `$voidptr` => соответствует `void*` в C.
<a id="environment-specific-files"></a>
### Файлы, специфичные для окружения

Если файл имеет суффикс, специфичный для окружения, он будет компилироваться только для этого окружения.

- `.js.v` => будет использоваться только бэкендом JS. Эти файлы могут содержать код JS.
- `.c.v` => будет использоваться только бэкендом C. Эти файлы могут содержать код C.
- `.native.v` => будет использоваться только нативным бэкендом V.
- `_nix.c.v` => будет использоваться только в системах Unix (не Windows).
- `_${os}.c.v` => будет использоваться только в указанной системе `os`.
  Например, `_windows.c.v` будет использоваться только при компиляции в Windows или с `-os windows`.
- `_default.c.v` => будет использоваться только если НЕТ более специфичного файлa для платформы.
  Например, если у вас есть оба файла `file_linux.c.v` и `file_default.c.v`,
  и вы компилируете для linux, то будет использоваться только `file_linux.c.v`,
  а `file_default.c.v` будет проигнорирован.

Вот более полный пример:

`main.v`:

```v ignore
module main
fn main() { println(message) }
```

`main_default.c.v`:

```v ignore
module main
const message = 'Hello world'
```

`main_linux.c.v`:

```v ignore
module main
const message = 'Hello linux'
```

`main_windows.c.v`:

```v ignore
module main
const message = 'Hello windows'
```

С приведенным выше примером:

- когда вы компилируете для Windows, вы получите `Hello windows`
- когда вы компилируете для Linux, вы получите `Hello linux`
- когда вы компилируете для любой другой платформы, вы получите
  неспецифичное сообщение `Hello world`.

- `_d_customflag.v` => будет использоваться *только* если вы передаете `-d customflag` в V.
  Это соответствует `$if customflag ? {}`, но для целого файла, а не только для
  одного блока. `customflag` должен быть идентификатором в формате snake_case, он не может
  содержать произвольные символы (только строчные латинские буквы + цифры + `_`).
  > **Примечание**
  >
  > Комбинированный суффикс `_d_customflag_linux.c.v` не будет работать.
  > Если вам действительно нужен файл с пользовательским флагом, содержащий зависимый от платформы код, используйте
  > суффикс `_d_customflag.v`, а затем используйте условные блоки времени компиляции, зависящие от платформы,
  > внутри него, то есть `$if linux {}` и т.д.

- `_notd_customflag.v` => подобно _d_customflag.v, но будет использоваться
  *только* если вы НЕ передаете `-d customflag` в V.

См. также [Cross Compilation](#cross-compilation).
<a id="debugger"></a>
## Отладчик

Для использования встроенного *отладчика V* добавьте оператор `$dbg` в исходный код в том месте, где вы хотите вызвать отладчик.

```v
fn main() {
	a := 1
	$dbg;
}
```

При запуске этого кода V вы получите перерыв в REPL отладчика, когда выполнение достигнет оператора `$dbg`.

```
$ v run example.v
Break on [main] main in example.v:3
example.v:3 vdbg>
```

В этот момент выполнение приостанавливается, и отладчик становится доступным.

Чтобы увидеть доступные команды, введите
?, h или help. (Автодополнение команд работает - только для не-Windows ОС)

```
example.v:3 vdbg> ?
vdbg commands:
  anon?                 check if the current context is anon
  bt                    prints a backtrace
  c, continue           continue debugging
  generic?              check if the current context is generic
  heap                  show heap memory usage
  h, help, ?            show this help
  l, list [lines]       show some lines from current break (default: 3)
  mem, memory           show memory usage
  method?               check if the current context is a method
  m, mod                show current module name
  p, print <var>        prints an variable
  q, quit               exits debugging session in the code
  scope                 show the vars in the current scope
  u, unwatch <var>      unwatches a variable
  w, watch <var>        watches a variable
```

Попробуем команду `scope` для проверки контекста текущей области видимости.

```
example.v:3 vdbg> scope
a = 1 (int)
```

Отлично! Мы видим имя переменной, её значение и имя типа.

А если нужно вывести только одну переменную, а не всю область видимости?

Просто введите `p a`.

Чтобы отслеживать переменную по её имени, используйте:

`w a` (где `a` - это имя переменной)

Чтобы прекратить отслеживание переменной (снять `watch`), используйте `u a`.

Посмотрим ещё один пример:

```
fn main() {
	for i := 0; i < 4; i++ {
		$dbg
	}
}
```

При повторном запуске мы получим:
`Break on [main] main in example.v:3`

Если мы хотим прочитать контекст исходного кода, мы можем использовать команду `l` или `list`.

```
example.v:3 vdbg> l
0001  fn main() {
0002    for i := 0; i < 4; i++ {
0003>           $dbg
0004    }
0005  }
```

По умолчанию читаются 3 строки до и 3 строки после, но вы можете
передать параметр команде для чтения большего количества строк, например, `l 5`.

Теперь давайте посмотрим, как изменяется переменная в этом цикле.

```
example.v:3 vdbg> w i
i = 0 (int)
```

Чтобы продолжить до следующей точки останова, введите команду `c` или `continue`.

```
example.v:3 vdbg> c
Break on [main] main in example.v:3
i = 1 (int)
```

`i` и его значение печатаются автоматически, так как она находится в списке отслеживания.

Чтобы повторить последнюю выполненную команду, в данном случае команду `c`,
просто нажмите клавишу *enter*.

```
example.v:3 vdbg>
Break on [main] main in example.v:3
i = 2 (int)
example.v:3 vdbg>
Break on [main] main in example.v:3
i = 3 (int)
example.v:3 vdbg>
```

Вы также можете увидеть использование памяти с помощью команды `mem` или `memory`, и
проверить, является ли текущий контекст анонимной функцией (`anon?`), методом (`method?`)
или обобщённым методом (`generic?`), а также очистить окно терминала (`clear`).
<a id="call-stack"></a>
## Стек вызовов

Вы также можете показать текущий стек вызовов с помощью `v.debug`.

Для включения этой функции добавьте ключ `-d callstack` при сборке или запуске
вашего кода:

```v
import v.debug

fn test(i int) {
	if i > 9 {
		debug.dump_callstack()
	}
}

fn do_something() {
	for i := 0; i <= 10; i++ {
		test(i)
	}
}

fn main() {
	do_something()
}
```

```
$ v -d callstack run example.v
Backtrace:
--------------------------------------------------
example.v:16   | > main.main
example.v:11   |  > main.do_something
example.v:5    |   > main.test
--------------------------------------------------
```
<a id="trace"></a>
## Трассировка

Другой возможностью `v.debug` является возможность добавить функции-хуки
до и после каждого вызова функции.

Для включения этой функции добавьте ключ `-d trace` при сборке или запуске
вашего кода:

```v
import v.debug

fn main() {
	hook1 := debug.add_before_call(fn (fn_name string) {
		println('> before ${fn_name}')
	})
	hook2 := debug.add_after_call(fn (fn_name string) {
		println('> after ${fn_name}')
	})
	anon := fn () {
		println('call')
	}
	anon()

	// optionally you can remove the hooks:
	debug.remove_before_call(hook1)
	debug.remove_after_call(hook2)
	anon()
}
```

```
$ v -d trace run example.v
> before anon
call
> after anon
call
```
<a id="memory-unsafe-code"></a>
## Код, небезопасный по отношению к памяти

Иногда для эффективности вам может понадобиться написать низкоуровневый код, который потенциально
может повредить память или быть уязвимым к эксплойтам безопасности. V поддерживает написание такого кода,
но не по умолчанию.

V требует, чтобы любые потенциально небезопасные для памяти операции были намеренно помечены.
Пометка также указывает любому читающему код, что возможны
нарушения безопасности памяти в случае ошибки.

Примеры потенциально небезопасных для памяти операций:

* Арифметика указателей
* Индексация указателей
* Преобразование в указатель несовместимого типа
* Вызов определённых C-функций, например, `free`, `strlen` и `strncmp`.

Для пометки потенциально небезопасных для памяти операций заключите их в блок `unsafe`:

```v wip
// allocate 2 uninitialized bytes & return a reference to them
mut p := unsafe { malloc(2) }
p[0] = `h` // Error: pointer indexing is only allowed in `unsafe` blocks
unsafe {
    p[0] = `h` // OK
    p[1] = `i`
}
p++ // Error: pointer arithmetic is only allowed in `unsafe` blocks
unsafe {
    p++ // OK
}
assert *p == `i`
```

Лучшей практикой является избегание помещения безопасных для памяти выражений в блок `unsafe`,
чтобы причина использования `unsafe` была как можно более ясной. Обычно любой код,
который вы считаете безопасным для памяти, не должен находиться внутри блока `unsafe`, чтобы компильтор
мог его проверить.

Если вы подозреваете, что ваша программа нарушает безопасность памяти, вы имеете преимущество в
поиске причины: посмотрите на блоки `unsafe` (и как они взаимодействуют с
окружающим кодом).

> [!NOTE]
> Это находится в процессе разработки.
<a id="structs-with-reference-fields"></a>
## Структуры с полями-ссылками

Структуры с ссылками требуют явной установки начального значения в
значение ссылки, если только структура уже не определяет собственное начальное значение.

Ссылки с нулевым значением, или нулевые указатели, **НЕ** будут поддерживаться в будущем.
На данный момент структуры данных, такие как связные списки или двоичные деревья, которые полагаются на поля-ссылки,
могут использовать значение `0`, понимая, что это небезопасно, и что это может
вызвать панику.

```v
struct Node {
	a &Node
	b &Node = unsafe { nil } // Auto-initialized to nil, use with caution!
}

// Reference fields must be initialized unless an initial value is declared.
// Nil is OK but use with caution, it's a nil pointer.
foo := Node{
	a: unsafe { nil }
}
bar := Node{
	a: &foo
}
baz := Node{
	a: unsafe { nil }
	b: unsafe { nil }
}
qux := Node{
	a: &foo
	b: &bar
}
println(baz)
println(qux)
```
<a id="sizeof-and-__offsetof"></a>
## sizeof и __offsetof

* `sizeof(Type)` возвращает размер типа в байтах.
* `__offsetof(Struct, field_name)` возвращает смещение поля структуры в байтах.

```v
struct Foo {
	a int
	b int
}

assert sizeof(Foo) == 8
assert __offsetof(Foo, a) == 0
assert __offsetof(Foo, b) == 4
```
<a id="limited-operator-overloading"></a>
## Ограниченная перегрузка операторов

Перегрузка операторов определяет поведение определённых бинарных операторов для определённых типов.

```v
struct Vec {
	x int
	y int
}

fn (a Vec) str() string {
	return '{${a.x}, ${a.y}}'
}

fn (a Vec) + (b Vec) Vec {
	return Vec{a.x + b.x, a.y + b.y}
}

fn (a Vec) - (b Vec) Vec {
	return Vec{a.x - b.x, a.y - b.y}
}

fn main() {
	a := Vec{2, 3}
	b := Vec{4, 5}
	mut c := Vec{1, 2}

	println(a + b) // "{6, 8}"
	println(a - b) // "{-2, -2}"
	c += a
	//^^ autogenerated from + overload
	println(c) // "{3, 5}"
}
```

> Перегрузка операторов противоречит философии простоты и предсказуемости V.
> Но поскольку научные и графические приложения входят в домены V, перегрузка операторов является важной функцией для улучшения читаемости:
>
> `a.add(b).add(c.mul(d))` гораздо менее читаемо, чем `a + b + c * d`.

Перегрузка операторов возможна для следующих бинарных операторов: `+, -, *, /, %, <, ==`.
<a id="implicitly-generated-overloads"></a>
### Неявно генерируемые перегрузки

- `==` автоматически генерируется компилятором, но может быть переопределён.

- `!=`, `>`, `<=` и `>=` автоматически генерируются, когда определены `==` и `<`.
  Они не могут быть явно переопределены.
- Операторы присваивания (`*=`, `+=`, `/=` и т.д.) автоматически генерируются, когда определены соответствующие
  операторы и операнды имеют одинаковый тип.
  Они не могут быть явно переопределены.
<a id="restriction"></a>
### Ограничения

Для улучшения безопасности и поддерживаемости перегрузка операторов ограничена.
<a id="type-restrictions"></a>
#### Ограничения типов

- При переопределении `<` и `==` возвращаемый тип должен быть строго `bool`.
- Оба аргумента должны иметь одинаковый тип (как и для всех операторов в V).
- Перегруженные операторы должны возвращать тот же тип, что и аргумент
  (исключения - `<` и `==`).
<a id="other-restrictions"></a>
#### Другие ограничения

- Аргументы не могут быть изменены внутри перегрузок.
- Вызов других функций внутри функций операторов запрещён (**планируется**).
<a id="performance-tuning"></a>
## Оптимизация производительности

При компиляции с флагом `-prod` сгенерированный C-код V обычно показывает хорошую производительность. Однако в специализированных сценариях дополнительные флаги компилятора и атрибуты могут further оптимизировать исполняемый файл для производительности, использования памяти или размера.

> [!NOTE]
> Это требуется *крайне редко*, и не следует их использовать, если вы не *профилируете свой код*, а затем не видите, что они дают значительные преимущества.
> Цитируя документацию GCC: "Программисты печально известны своей неспособностью предсказать, как на самом деле работают их программы".

| Операция оптимизации      | Преимущества                    | Недостатки                                          |
|---------------------------|---------------------------------|-----------------------------------------------------|
| `@[inline]`               | Производительность              | Увеличение размера исполняемого файла               |
| `@[direct_array_access]`  | Производительность              | Риски безопасности                                  |
| `@[packed]`               | Использование памяти            | Возможная потеря производительности                 |
| `@[minify]`               | Производительность, Использование памяти | Может нарушить бинарную сериализацию/рефлексию |
| `_likely_/_unlikely_`     | Производительность              | Риск отрицательного влияния на производительность    |
| `-fast-math`              | Производительность              | Риск некорректных результатов математических операций |
| `-d no_segfault_handler`  | Время компиляции, Размер        | Потеря трассировки при нарушении сегментации        |
| `-cflags -march=native`   | Производительность              | Риск снижения совместимости с CPU                   |
| `-compress`               | Размер                          | Затрудняет отладку, дополнительная зависимость `upx` |
| `PGO`                     | Производительность, Размер      | Сложность использования                             |
<a id="tuning-operations-details"></a>
### Детали операций оптимизации
<a id="inline"></a>
#### `@[inline]`

Вы можете пометить функции атрибутом `@[inline]`, чтобы C-компилятор попытался их встроить, что в некоторых
случаях может быть полезно для производительности, но может повлиять на размер вашего исполняемого файла.

**Когда использовать**

- Функции, которые часто вызываются в критических по производительности циклах.

**Когда избегать**

- Больших функций, так как это может привести к раздутию кода и фактически снизить производительность.
- Больших функций в выражениях `if` — может оказать негативное влияние на кэш инструкций.
<a id="direct_array_access"></a>
#### `@[direct_array_access]`

В функциях, помеченных атрибутом `@[direct_array_access]`, компилятор будет преобразовывать операции с массивами
напрямую в операции с массивами C — пропуская проверку границ. Это может сэкономить много времени в
функции, которая итерирует по массиве, но ценой делает функцию небезопасной — если только проверка
границ не будет выполнена пользователем.

**Когда использовать**

- В жестких циклах, которые обращаются к элементам массива, где границы были проверены вручную или вы
уверены, что индекс доступа будет допустимым.

**Когда избегать**

- Везде в других случаях.
<a id="packed"></a>
#### `@[packed]`

Атрибут `@[packed]` может быть применен к структуре для создания невыровненного расположения в памяти,
что уменьшает общий объем памяти, используемый структурой. Использование атрибута `@[packed]`
может негативно повлиять на производительность или даже быть запрещенным на некоторых архитектурах CPU.

**Когда использовать**

- Когда использование памяти критичнее производительности, например, во встроенных системах.

**Когда избегать**

- На архитектурах CPU, которые не поддерживают невыровненный доступ к памяти, или когда требуется высокоскоростной доступ к памяти.
<a id="aligned"></a>
#### `@[aligned]`

Атрибут `@[aligned]` может быть применен к структуре или объединению для указания минимального выравнивания
(в байтах) для переменных этого типа. Используя атрибут `@[aligned]`, вы можете только *увеличить*
выравнивание по умолчанию. Используйте `@[packed]`, если хотите *уменьшить* его. Выравнивание любой структуры
или объединения должно быть, по крайней мере, точным кратным наименьшему общему кратному выравниваний всех
членов этой структуры или объединения.

Пример:
```v
// Each u16 in the `data` field below, takes 2 bytes, and we have 3 of them = 6 bytes.
// The smallest power of 2, bigger than 6 is 8, i.e. with `@[aligned]`, the alignment
// for the entire struct U16s, will be 8:
@[aligned]
struct U16s {
	data [3]u16
}
```
**Когда использовать**

- Только если экземпляры ваших типов будут использоваться в критических по производительности разделах или со
специализированными машинными инструкциями, которые требуют определенного выравнивания для работы.

**Когда избегать**

- На архитектурах CPU, которые не поддерживают невыровненный доступ к памяти. Если вы не работаете над
алгоритмами, критичными к производительности, вам это действительно не нужно, так как правильное минимальное выравнивание
специфично для CPU, и компилятор уже обычно выбирает хорошие значения по умолчанию для вас.

> [!NOTE]
> Вы можете опустить коэффициент выравнивания, то есть использовать просто `@[aligned]`, в этом случае компилятор
> выровняет тип по максимально полезному выравниванию для целевой машины, для которой вы компилируете,
> то есть выравнивание будет самым большим выравниванием, которое когда-либо использовалось для любого типа данных на
> целевой машине. Часто это может сделать операции копирования более эффективными, потому что компилятор
> может выбрать инструкции, копирующие наибольшие блоки памяти, при выполнении копирования в или
> из переменных, которые имеют типы, выровненные таким образом.

См. также ["What Every Programmer Should Know About Memory", by Ulrich Drepper](https://people.freebsd.org/~lstewart/articles/cpumemory.pdf) .
<a id="minify"></a>
#### `@[minify]`

Атрибут `@[minify]` может быть добавлен к структуре, позволяя компилятору переупорядочить поля таким образом,
чтобы минимизировать внутренние промежутки, сохраняя при этом выравнивание. Использование атрибута `@[minify]` может
вызвать проблемы с бинарной сериализацией или рефлексией. Учитывайте эти потенциальные побочные эффекты
при использовании этого атрибута.

**Когда использовать**

- Когда вы хотите минимизировать использование памяти и не используете бинарную сериализацию или рефлексию.

**Когда избегать**

- При использовании бинарной сериализации или рефлексии, так как это может привести к непредвиденному поведению.
<a id="_likely__unlikely_"></a>
#### `_likely_/_unlikely_`

`if _likely_(bool expression) {` — подсказывает C-компилятору, что переданное логическое выражение
очень вероятно истинно, чтобы он мог сгенерировать ассемблерный код с меньшей вероятностью неверного предсказания ветвления.
В бэкенде JS это ничего не делает.

`if _unlikely_(bool expression) {` аналогично `_likely_(x)`, но подсказывает, что логическое
выражение крайне маловероятно. В бэкенде JS это ничего не делает.

**Когда использовать**

- В условных конструкциях, где одна ветвь явно выполняется чаще другой.

**Когда избегать**

- Когда предсказание может быть неверным, так как это может привести к снижению производительности из-за неверного
предсказания ветвления.

**Когда использовать**

- Для production-сборок, где вы хотите уменьшить размер исполняемого файла и улучшить производительность во время выполнения.

**Когда избегать**

- Там, где это не работает для вас.
<a id="fast-math"></a>
#### `-fast-math`

Этот флаг включает оптимизации, игнорирующие строгое соответствие стандарту IEEE для
арифметики с плавающей запятой. Хотя это может привести к более быстрому коду, это может давать некорректные или
менее точные математические результаты.

Полный спектр математических операций, на которые влияет `-fast-math`, можно найти
[here](https://clang.llvm.org/docs/UsersManual.html#cmdoption-ffast-math).

**Когда использовать**

- В приложениях, где производительность критичнее точности, как в некоторых задачах рендеринга
графики.

**Когда избегать**

- В приложениях, требующих строгой математической точности, таких как научные моделирования или
финансовые расчеты.
<a id="d-no_segfault_handler"></a>
#### `-d no_segfault_handler`

Использование этого флага опускает обработчик нарушения сегментации, уменьшая размер исполняемого файла и potentially улучшая
время компиляции. Однако, в случае нарушения сегментации, вывод не будет содержать информацию о стеке,
что затрудняет отладку.

**Когда использовать**

- В небольших, хорошо протестированных утилитах, где трассировка стека неessential для отладки.

**Когда избегать**

- В крупномасштабных, сложных приложениях, где требуется надежная отладка.
<a id="cflags-marchnative"></a>
#### `-cflags -march=native`

Этот флаг указывает C-компилятору генерировать инструкции, оптимизированные для хост-процессора. Это может
улучшить производительность, но создаст исполняемый файл, несовместимый с другими/старыми процессорами.

**Когда использовать**

- Когда ПО предназначено для запуска только на машине сборки или в контролируемой среде
с одинаковым оборудованием.

**Когда избегать**

- При распространении ПО пользователям с потенциально более старыми процессорами.
<a id="compress"></a>
#### `-compress`

Этот флаг выполняет `upx` для сжатия результирующего исполняемого файла, уменьшая его размер примерно на 50%-70%.
Исполняемый файл будет распакован во время выполнения, поэтому на запуск потребуется чуть больше времени.
Также потребуется дополнительная оперативная память в начале, так как сжатая версия приложения будет загружена в
память, а затем расширена до другого блока памяти.
Отладка такого приложения может быть сложнее, если вы не учитываете это.
Некоторые антивирусные программы также используют эвристику, которая чаще срабатывает для сжатых приложений.

**Когда использовать**

- Действительно для крошечных сред, где размер исполняемого файла на файловой системе
важен при развертывании (контейнеры Docker, диски для восстановления и т. д.).

**Когда избегать**

- Когда вам нужно отлаживать приложение
- Когда время запуска приложения крайне важно (где 1-2мс могут иметь значение для вас)
- Когда вы не можете выделить больше памяти при запуске приложения
- Когда вы развертываете приложение у пользователей с антивирусным ПО, которое может неправильно идентифицировать ваше
приложение как вредоносное, просто потому, что оно распаковывает свой код во время выполнения.
<a id="pgo-profile-guided-optimization"></a>
#### PGO (Profile-Guided Optimization)

PGO позволяет компилятору оптимизировать код на основе его поведения во время образцовых запусков. Это может улучшить
производительность и уменьшить размер результирующего исполняемого файла, но увеличивает сложность процесса сборки.

**Когда использовать**

- Для приложений, критичных к производительности, где увеличение сложности сборки оправдано.

**Когда избегать**

- Для небольших, кратковременных или быстро меняющихся проектов, где увеличение сложности сборки не
оправдано.

**PGO с Clang**

Это пример bash-скрипта, который вы можете использовать для оптимизации вашей CLI-программы на V без взаимодействия с пользователем.
В большинстве случаев вам придется изменить этот скрипт, чтобы он подходил для вашей конкретной программы.

```bash
#!/usr/bin/env bash

# Get the full path to the current directory
CUR_DIR=$(pwd)

# Remove existing PGO data
rm -f *.profraw
rm -f default.profdata

# Initial build with PGO instrumentation
v -cc clang -prod -cflags -fprofile-generate -o pgo_gen .

# Run the instrumented executable 10 times
for i in {1..10}; do
    ./pgo_gen
done

# Merge the collected data
llvm-profdata merge -o default.profdata *.profraw

# Compile the optimized version using the PGO data
v -cc clang -prod -cflags "-fprofile-use=${CUR_DIR}/default.profdata" -o optimized_program .

# Remove PGO data and instrumented executable
rm *.profraw
rm pgo_gen
```
<a id="atomics"></a>
## Атомарные операции

V пока не имеет специальной поддержки атомарных операций, тем не менее, можно рассматривать переменные как атомарные
с помощью [calling C](#v-and-c) функций из V. Стандартные атомарные функции C11, такие как `atomic_store()`,
обычно определяются с помощью макросов и "магии" компилятора C для предоставления как бы
*перегруженных C-функций*.
Поскольку V намеренно не поддерживает перегрузку функций, в заголовочных файлах C, которые являются частью инфраструктуры компилятора V, определены функции-обертки с именем `atomic.h`.

Существуют специальные обертки для всех беззнаковых целочисленных типов и для указателей.
(`u8` не полностью поддерживается в Windows) &ndash; имена функций включают имя типа
в качестве суффикса, например, `C.atomic_load_ptr()` или `C.atomic_fetch_add_u64()`.

Для использования этих функций необходимо включить заголовочный файл C для используемой ОС и объявить функции,
которые предполагается использовать. Пример:

```v globals
$if windows {
	#include "@VEXEROOT/thirdparty/stdatomic/win/atomic.h"
} $else {
	#include "@VEXEROOT/thirdparty/stdatomic/nix/atomic.h"
}

// declare functions we want to use - V does not parse the C header
fn C.atomic_store_u32(&u32, u32)
fn C.atomic_load_u32(&u32) u32
fn C.atomic_compare_exchange_weak_u32(&u32, &u32, u32) bool
fn C.atomic_compare_exchange_strong_u32(&u32, &u32, u32) bool

const num_iterations = 10000000

// see section "Global Variables" below
__global (
	atom u32 // ordinary variable but used as atomic
)

fn change() int {
	mut races_won_by_change := 0
	for {
		mut cmp := u32(17) // addressable value to compare with and to store the found value
		// atomic version of `if atom == 17 { atom = 23 races_won_by_change++ } else { cmp = atom }`
		if C.atomic_compare_exchange_strong_u32(&atom, &cmp, 23) {
			races_won_by_change++
		} else {
			if cmp == 31 {
				break
			}
			cmp = 17 // re-assign because overwritten with value of atom
		}
	}
	return races_won_by_change
}

fn main() {
	C.atomic_store_u32(&atom, 17)
	t := spawn change()
	mut races_won_by_main := 0
	mut cmp17 := u32(17)
	mut cmp23 := u32(23)
	for i in 0 .. num_iterations {
		// atomic version of `if atom == 17 { atom = 23 races_won_by_main++ }`
		if C.atomic_compare_exchange_strong_u32(&atom, &cmp17, 23) {
			races_won_by_main++
		} else {
			cmp17 = 17
		}
		desir := if i == num_iterations - 1 { u32(31) } else { u32(17) }
		// atomic version of `for atom != 23 {} atom = desir`
		for !C.atomic_compare_exchange_weak_u32(&atom, &cmp23, desir) {
			cmp23 = 23
		}
	}
	races_won_by_change := t.wait()
	atom_new := C.atomic_load_u32(&atom)
	println('atom: ${atom_new}, #exchanges: ${races_won_by_main + races_won_by_change}')
	// prints `atom: 31, #exchanges: 10000000`)
	println('races won by\n- `main()`: ${races_won_by_main}\n- `change()`: ${races_won_by_change}')
}
```

В этом примере и `main()`, и порожденный поток `change()` пытаются заменить значение `17`
в глобальной переменной `atom` на значение `23`. Замена в обратном направлении выполняется
точно 10000000 раз. Последняя замена будет на `31`, что заставит порожденный поток завершиться.

Непредсказуемо, сколько замен произойдет в каком потоке, но сумма всегда будет
10000000. (С неатомарными командами из комментариев значение будет больше или программа
зависнет — в зависимости от используемой оптимизации компилятора.)
<a id="global-variables"></a>
## Глобальные переменные

По умолчанию V не допускает глобальные переменные. Однако в приложениях низкого уровня они имеют место, поэтому их использование может быть включено с помощью флага компилятора `-enable-globals`.
Объявления глобальных переменных должны быть окружены спецификацией `__global ( ... )` – как в примере [above](#atomics).

Инициализатор для глобальных переменных должен быть явно преобразован в
желаемый целевой тип. Если инициализатор не указан, выполняется инициализация по умолчанию.
Некоторые объекты, такие как семафоры и мьютексы, требуют явной инициализации *на месте*, т.е.
не со значением, возвращенным из вызова функции, а с вызовом метода по ссылке.
Для этой цели может использоваться отдельная функция `init()` – она будет вызвана перед `main()`:

```v globals
import sync

__global (
	sem   sync.Semaphore // needs initialization in `init()`
	mtx   sync.RwMutex // needs initialization in `init()`
	f1    = f64(34.0625) // explicitly initialized
	shmap shared map[string]f64 // initialized as empty `shared` map
	f2    f64 // initialized to `0.0`
)

fn init() {
	sem.init(0)
	mtx.init()
}
```

Имейте в виду, что в многопоточных приложениях доступ к глобальным переменным подвержен
состояниям гонки. Есть несколько подходов для решения этой проблемы:

- используйте типы `shared` для объявлений переменных и блоки `lock` для доступа.
  Это наиболее подходит для крупных объектов, таких как структуры, массивы или карты.
- обрабатывайте примитивные типы данных как "атомарные", используя специальные C-функции (см. [above](#atomics)).
- используйте явные примитивы синхронизации, такие как мьютексы, для контроля доступа. Компилятор
  в этом случае не может реально помочь, поэтому вы должны знать, что делаете.
- не обращайте внимания – этот подход возможен, но имеет смысл только если точные значения
  глобальных переменных действительно не важны. Пример можно найти в модуле `rand`,
  где глобальные переменные используются для генерации (некриптографических) псевдослучайных чисел.
  В этом случае гонки данных приводят к тому, что случайные числа в разных потоках становятся
  в некоторой степени коррелированными, что приемлемо, учитывая штраф за производительность,
  который представляет использование примитивов синхронизации.
<a id="static-variables"></a>
## Статические переменные

V также поддерживает *статические переменные*, которые похожи на *глобальные переменные*, но
доступны только *внутри* отдельной небезопасной функции (их можно рассматривать как
глобальные в пространстве имен).

Примечание: их использование также не рекомендуется по причинам, аналогичным тем, почему
не рекомендуются глобальные переменные. Эта функция поддерживается для возможности трансляции существующего
кода низкого уровня на C в код V с помощью `v translate`.

Примечание: функция, в которой вы используете статическую переменную, должна быть помечена
с помощью @[unsafe]. Также, в отличие от использования глобальных переменных, использование статических переменных не
требует передачи флага `-enable-globals`, потому что они могут только
читаться/изменяться внутри одной функции, которая имеет полный контроль над
состоянием, хранимым в них.

Вот небольшой пример того, как могут использоваться статические переменные:
```v
@[unsafe]
fn counter() int {
	mut static x := 42
	// Note: x is initialised to 42, just _once_.
	x++
	return x
}

fn f() int {
	return unsafe { counter() }
}

println(f()) // prints 43
println(f()) // prints 44
println(f()) // prints 45
```
<a id="cross-compilation"></a>
## Кросс-компиляция

Поддерживается кросс-компиляция для Windows, Linux и FreeBSD.

Для кросс-компиляции вашего проекта просто выполните:

```shell
v -os windows .
```

или

```shell
v -os linux .
```

или

```shell
v -os freebsd .
```

> [!NOTE]
> Кросс-компиляция Windows-бинарного файла на машине Linux требует установки GNU C компилятора для
> MinGW-w64 (нацеленного на Win64).

Для дистрибутивов на базе Ubuntu/Debian:

```shell
sudo apt install gcc-mingw-w64-x86-64
```

Для дистрибутивов на базе Arch:

```shell
sudo pacman -S mingw-w64-gcc
```

(Кросс-компиляция для macOS в настоящее время невозможна.)

Если у вас нет никаких C-зависимостей, вот и все, что вам нужно сделать. Это работает даже
при компиляции GUI-приложений с использованием модуля `ui` или графических приложений с использованием `gg`.

Вам нужно будет установить Clang, линковщик LLD и загрузить zip-файл с
библиотеками и файлами заголовков для Windows и Linux. V предоставит вам ссылку.
<a id="debugging"></a>
## Отладка
<a id="c-backend-binaries-default"></a>
### Бинарные файлы C-бэкенда (по умолчанию)

Для отладки проблем в сгенерированном бинарном файле (флаг: `-b c`) вы можете передать эти флаги:

- `-g` - создает менее оптимизированный исполняемый файл с большим количеством отладочной информации.
  V будет выводить номера строк из .v файлов в трассировках стека, которые
  исполняемый файл будет генерировать при панике. Обычно лучше передавать -g, если
  вы не пишете код низкого уровня, в этом случае используйте следующий вариант `-cg`.
- `-cg` - создает менее оптимизированный исполняемый файл с большим количеством отладочной информации.
  В этом случае исполняемый файл будет использовать номера строк C-исходного кода. Это часто
  используется в сочетании с `-keepc`, чтобы вы могли изучить сгенерированную
  C-программу в случае паники, или чтобы ваш отладчик (`gdb`, `lldb` и т.д.)
  мог показать вам сгенерированный C-исходный код.
- `-showcc` - печатает команду C, используемую для сборки программы.
- `-show-c-output` - печатает вывод, который ваш C-компилятор произвел
  при компиляции вашей программы.
- `-keepc` - не удалять сгенерированный файл C-исходного кода после успешной
  компиляции. Также сохранять тот же путь к файлу, чтобы он был более стабильным
  и его было легче держать открытым в редакторе/IDE.

Для получения наилучшего опыта отладки, если вы пишете обертку низкого уровня для существующей
C-библиотеки, вы можете передать несколько этих флагов одновременно:
`v -keepc -cg -showcc yourprogram.v`, а затем просто запустите ваш отладчик (gdb/lldb) или IDE
над созданным исполняемым файлом `yourprogram`.

Если вы просто хотите изучить сгенерированный C-код,
без дальнейшей компиляции, вы также можете использовать флаг `-o` (например, `-o file.c`).
Это заставит V сгенерировать `file.c`, а затем остановиться.

Если вы хотите увидеть сгенерированный C-исходный код *только* для одной C-функции,
например `main`, вы можете использовать: `-printfn main -o file.c`.

Для отладки самого исполняемого файла V вам нужно компилировать из src с помощью `./v -g -o v cmd/v`.

Вы можете отладить тесты, например, с помощью `v -g -keepc prog_test.v`. Флаг `-keepc` необходим,
чтобы исполняемый файл не был удален после его создания и запуска.

Чтобы увидеть подробный список всех поддерживаемых флагов V,
используйте `v help`, `v help build` и `v help build-c`.

**Отладка через командную строку**

1. скомпилируйте ваш бинарный файл с отладочной информацией `v -g hello.v`
2. отладка с помощью [lldb](https://lldb.llvm.org) или [GDB](https://www.gnu.org/software/gdb/)
   например, `lldb hello`

[Troubleshooting (debugging) executables created with V in GDB](https://github.com/vlang/v/wiki/Troubleshooting-(debugging)-исполняемые-файлы-созданные-с-помощью-V-в-GDB)

**Настройка визуальной отладки:**

* [Visual Studio Code](vscode.md)
<a id="native-backend-binaries"></a>
### Бинарные файлы Native-бэкенда

В настоящее время отсутствует поддержка отладки для бинарных файлов, созданных
native-бэкендом (флаг: `-b native`).
<a id="javascript-backend"></a>
### Javascript-бэкенд

Для отладки сгенерированного Javascript-вывода вы можете активировать source maps:
`v -b js -sourcemap hello.v -o hello.js`

Для просмотра всех поддерживаемых опций проверьте последнюю справку:
`v help build-js`
<a id="v-and-c"></a>
## V и C

Базовое соответствие между типами C и V описано в
[C and V Type Interoperability](https://github.com/vlang/v/blob/master/doc/c_and_v_type_interoperability.md).
<a id="calling-c-from-v"></a>
### Вызов C из V

В настоящее время V не имеет парсера для C-кода. Это означает, что даже
хотя он позволяет вам использовать `#include` для включения существующих C-заголовков и файлов исходного кода,
он не будет знать о каких-либо объявлениях в них. Оператор `#include`
появится только в сгенерированном C-коде, для использования самим
C-компилятором.

**Пример #include**
```v oksyntax
#include <stdio.h>
```
После этого оператора V *не* будет знать ничего о функциях и
структурах, объявленных в `stdio.h`, но если вы попытаетесь скомпилировать .v файл,
он добавит включение в сгенерированный C-код, так что если этот файл заголовка
отсутствует, вы получите ошибку C (в этом конкретном случае вы не получите, если у вас
правильная настройка C-компилятора, поскольку `<stdio.h>` является частью
стандартной C-библиотеки).

Чтобы преодолеть это ограничение (что V не имеет C-парсера), V требует, чтобы вы
переобъявляли C-функции и структуры на стороне V, в ваших `.c.v` файлах.
Обратите внимание, что такие повторные объявления должны содержать только достаточно деталей о
функциях/структурах, которые вы хотите использовать.
Также обратите внимание, что они *не должны* быть полными, в отличие от тех, что находятся в .h файлах.

**Повторные объявления C-структур**
Например, если структура имеет 3 поля на стороне C, но вы хотите
обратиться только к 1 из них, вы можете объявить ее следующим образом:

**Пример повторного объявления C-структуры**
```v oksyntax
struct C.NameOfTheStruct {
	a_field int
}
```
Другая особенность, которая очень часто необходима для совместимости с C, - это атрибут `@[typedef]`.
Он используется для пометки `C.` структур,
которые определяются с помощью `typedef struct SomeName { ..... } TypeName;` в C-заголовках.

В этом случае вам придется написать что-то вроде следующего в вашем .c.v файле:
```v oksyntax
@[typedef]
pub struct C.TypeName {
}
```
Обратите внимание, что имя `C.` структуры в V - это имя *после* `struct SomeName {...}`.

**Повторные объявления C-функций**
Ситуация аналогична для `C.` функций. Если вы собираетесь вызывать только 1 функцию в
библиотеке, но ее .h заголовок объявляет десятки, вам нужно будет объявить только эту одну
функцию, например:

**Пример повторного объявления C-функции**
```v oksyntax
fn C.name_of_the_C_function(param1 int, const_param2 &char, param3 f32) f64
```
... и тогда позже вы сможете вызывать ее так же, как и V-функцию:
```v oksyntax
f := C.name_of_the_C_function(123, c'here is some C style string', 1.23)
dump(f)
```

**Пример использования C-функции из stdio путем ее повторного объявления на стороне V**
```v
#include <stdio.h>

// int dprintf(int fd, const char *format, ...)
fn C.dprintf(fd int, const_format &char, ...voidptr) int

value := 12345
x := C.dprintf(0, c'Hello world, value: %d\n', value)
dump(x)
```

Если ваш C-компилятор бэкенда правильно настроен, вы должны увидеть что-то подобное,
когда попытаетесь запустить его:
```console
#0 10:42:32 /v/examples> v run a.v
Hello world, value: 12345
[a.v:8] x: 26
#0 10:42:33 /v/examples>
```

Обратите внимание, что повторные объявления C-функций очень похожи на V, с некоторыми различиями:
1) У них нет тела (они определены на стороне C).
2) Их имена начинаются с `C.`.
3) Их имена могут содержать заглавные буквы (в отличие от V-функций, которые обязаны использовать snake_case).

Также обратите внимание на второй параметр `const char *format`, который был повторно объявлен как `const_format &char`.
Префикс `const_` в этом повторном объявлении может показаться произвольным, но он важен, если вы хотите
скомпилировать свой код с `-cstrict` или сторонними инструментами статического анализа C. В настоящее время V не
имеет другого способа выразить, что этот параметр является const (это, вероятно, изменится в V 1.0).

Для некоторых C-функций, которые используют вариадики (`...`) как параметры, V поддерживает специальный синтаксис для
параметров - `...voidptr`, который недоступен для обычных V-функций (вариадики V *обязаны* иметь абсолютно одинаковый тип). Обычно это функции семейства printf/scanf,
т.е. для `printf`, `fprintf`, `scanf`, `sscanf` и т.д., а также других функций форматирования/парсинга/логирования.

**Пример**

```v
#flag freebsd -I/usr/local/include -L/usr/local/lib
#flag -lsqlite3
#include "sqlite3.h"
// See also the example from https://www.sqlite.org/quickstart.html
pub struct C.sqlite3 {
}

pub struct C.sqlite3_stmt {
}

type FnSqlite3Callback = fn (voidptr, int, &&char, &&char) int

fn C.sqlite3_open(&char, &&C.sqlite3) int

fn C.sqlite3_close(&C.sqlite3) int

fn C.sqlite3_column_int(stmt &C.sqlite3_stmt, n int) int

// ... you can also just define the type of parameter and leave out the C. prefix

fn C.sqlite3_prepare_v2(&C.sqlite3, &char, int, &&C.sqlite3_stmt, &&char) int

fn C.sqlite3_step(&C.sqlite3_stmt)

fn C.sqlite3_finalize(&C.sqlite3_stmt)

fn C.sqlite3_exec(db &C.sqlite3, sql &char, cb FnSqlite3Callback, cb_arg voidptr, emsg &&char) int

fn C.sqlite3_free(voidptr)

fn my_callback(arg voidptr, howmany int, cvalues &&char, cnames &&char) int {
	unsafe {
		for i in 0 .. howmany {
			print('| ${cstring_to_vstring(cnames[i])}: ${cstring_to_vstring(cvalues[i]):20} ')
		}
	}
	println('|')
	return 0
}

fn main() {
	db := &C.sqlite3(unsafe { nil }) // this means `sqlite3* db = 0`
	// passing a string literal to a C function call results in a C string, not a V string
	C.sqlite3_open(c'users.db', &db)
	// C.sqlite3_open(db_path.str, &db)
	query := 'select count(*) from users'
	stmt := &C.sqlite3_stmt(unsafe { nil })
	// Note: You can also use the `.str` field of a V string,
	// to get its C style zero terminated representation
	C.sqlite3_prepare_v2(db, &char(query.str), -1, &stmt, 0)
	C.sqlite3_step(stmt)
	nr_users := C.sqlite3_column_int(stmt, 0)
	C.sqlite3_finalize(stmt)
	println('There are ${nr_users} users in the database.')

	error_msg := &char(unsafe { nil })
	query_all_users := 'select * from users'
	rc := C.sqlite3_exec(db, &char(query_all_users.str), my_callback, voidptr(7), &error_msg)
	if rc != C.SQLITE_OK {
		eprintln(unsafe { cstring_to_vstring(error_msg) })
		C.sqlite3_free(error_msg)
	}
	C.sqlite3_close(db)
}
```
<a id="calling-v-from-c"></a>
### Вызов V из C

Поскольку V может компилироваться в C, вызывать V-код из C очень просто, когда вы знаете как.

Используйте `v -o file.c your_file.v` для генерации C-файла, соответствующего V-коду.

Подробнее в [call_v_from_c example](../examples/call_v_from_c).
<a id="passing-c-compilation-flags"></a>
### Передача флагов компиляции C

Добавьте директивы `#flag` в начало ваших V-файлов для указания флагов компиляции C, таких как:

- `-I` для добавления путей поиска C-файлов заголовков
- `-l` для добавления имен C-библиотек, которые вы хотите линковать
- `-L` для добавления путей поиска файлов C-библиотек
- `-D` для установки переменных времени компиляции

Вы можете (опционально) использовать разные флаги для разных целевых платформ.
В настоящее время поддерживаются флаги `linux`, `darwin`, `freebsd` и `windows`.

> [!NOTE]
> Каждый флаг должен находиться на отдельной строке (пока)

```v oksyntax
#flag linux -lsdl2
#flag linux -Ivig
#flag linux -DCIMGUI_DEFINE_ENUMS_AND_STRUCTS=1
#flag linux -DIMGUI_DISABLE_OBSOLETE_FUNCTIONS=1
#flag linux -DIMGUI_IMPL_API=
```

В команде сборки через консоль вы можете использовать:

* `-cc` для замены компилятора C-бэкенда по умолчанию.
* `-cflags` для передачи пользовательских флагов компилятору C-бэкенда (передаются перед другими опциями C).
* `-ldflags` для передачи пользовательских флагов линковщику C-бэкенда (передаются после всех других опций C).
* Например: `-cc gcc-9 -cflags -fsanitize=thread`.

Вы можете определить переменную окружения `VFLAGS` в вашем терминале для хранения настроек `-cc`
и `-cflags`, вместо того чтобы включать их в команду сборки каждый раз.
<a id="pkgconfig"></a>
### #pkgconfig

Добавьте директивы `#pkgconfig`, чтобы сообщить компилятору, какие модули должны использоваться для компиляции
и линковки с помощью файлов pkg-config, предоставленных соответствующими зависимостями.

Поскольку обратные кавычки не могут использоваться в `#flag` и порождение процессов нежелательно по соображениям безопасности
и переносимости, V использует собственную библиотеку pkgconfig, совместимую со стандартной
freedesktop.

Если флаги не переданы, он добавит `--cflags` и `--libs` к pkgconfig (не к V).
Другими словами, обе строки ниже делают одно и то же:

```v oksyntax
#pkgconfig r_core
#pkgconfig --cflags --libs r_core
```

Файлы `.pc` ищутся в жестко заданном списке путей pkg-config по умолчанию, пользователь может добавить
дополнительные пути, используя переменную окружения `PKG_CONFIG_PATH`. Можно передать несколько модулей.

Для проверки существования pkg-config используйте `$pkgconfig('pkg')` в качестве условия "если" во время компиляции,
чтобы проверить, существует ли pkg-config. Если он существует, ветвь будет создана. Используйте `$else` или `$else $if`
для обработки других случаев.

```v ignore
$if $pkgconfig('mysqlclient') {
	#pkgconfig mysqlclient
} $else $if $pkgconfig('mariadb') {
	#pkgconfig mariadb
}
```
<a id="including-c-code"></a>
### Включение C-кода

Вы также можете включить C-код непосредственно в ваш V-модуль.
Например, предположим, что ваш C-код находится в папке с именем 'c' внутри папки вашего модуля.
Тогда:

* Поместите файл v.mod в корневую папку вашего модуля (если вы
  создали свой модуль с помощью `v new`, у вас уже есть файл v.mod). Например:

```v ignore
Module {
	name: 'mymodule',
	description: 'My nice module wraps a simple C library.',
	version: '0.0.1'
	dependencies: []
}
```

* Добавьте эти строки в начало вашего модуля:

```v oksyntax
#flag -I @VMODROOT/c
#flag @VMODROOT/c/implementation.o
#include "header.h"
```

> [!NOTE]
> @VMODROOT будет заменен V на *ближайшую родительскую папку,
> где находится файл v.mod*.
> Любой .v файл рядом или ниже папки, где находится файл v.mod,
> может использовать `#flag @VMODROOT/abc` для обращения к этой папке.
> Папка @VMODROOT также *добавляется в начало* пути поиска модулей,
> поэтому вы можете *импортировать* другие модули под вашей @VMODROOT, просто называя их.

Вышеприведенные инструкции заставят V искать скомпилированный .o файл в
папке вашего модуля `folder/c/implementation.o`.
Если V найдет его, .o файл будет связан с основным исполняемым файлом, использовавшим модуль.
Если он его не найдет, V предполагает, что существует файл `@VMODROOT/c/implementation.c`,
и пытается скомпилировать его в .o файл, а затем использует его.

Это позволяет вам иметь C-код, который содержится в V-модуле, чтобы его распространение было проще.
Вы можете увидеть полный минимальный пример использования C-кода в V-модуле-обертке здесь:
[project_with_c_code](https://github.com/vlang/v/tree/master/vlib/v/tests/project_with_c_code).
Еще один пример, демонстрирующий передачу структур из C в V и обратно:
[interoperate between C to V to C](https://github.com/vlang/v/tree/master/vlib/v/tests/project_with_c_code_2).
<a id="c-types"></a>
### Типы C

Обычные нуль-терминированные C-строки могут быть преобразованы в строки V с помощью
`unsafe { &char(cstring).vstring() }` или, если вы уже знаете их длину, с помощью
`unsafe { &char(cstring).vstring_with_len(len) }`.

> [!NOTE]
> Методы `.vstring()` и `.vstring_with_len()` НЕ создают копию `cstring`,
> поэтому вам НЕ следует освобождать его после вызова метода `.vstring()`.
> Если вам нужно сделать копию C-строки (некоторые libc API, такие как `getenv`, практически требуют этого,
> поскольку они возвращают указатели на внутреннюю память libc), вы можете использовать `cstring_to_vstring(cstring)`.

В Windows C-части API часто возвращают так называемые строки `wide` (кодировка UTF-16).
Они могут быть преобразованы в строки V с помощью `string_from_wide(&u16(cwidestring))`.

V имеет следующие типы для более легкой совместимости с C:

- `voidptr` для C- `void*`,
- `&u8` для C- `byte*` и
- `&char` для C- `char*`.
- `&&char` для C- `char**`

Для приведения `voidptr` к ссылке V используйте `user := &User(user_void_ptr)`.

`voidptr` также может быть разыменован в структуру V через приведение: `user := User(user_void_ptr)`.

[an example of a module that calls C code from V](https://github.com/vlang/v/blob/master/vlib/v/tests/project_with_c_code/mod1/wrapper.c.v)
<a id="c-declarations"></a>
### Объявления C

C-идентификаторы доступны с префиксом `C`, аналогично тому, как доступны
специфичные для модуля идентификаторы. Функции должны быть переобъявлены в V перед использованием.
Любые C-типы могут использоваться за префиксом `C`, но типы должны быть переобъявлены в V, чтобы
получить доступ к членам типа.

Для переобъявления сложных типов, таких как в следующем C-коде:

```c
struct SomeCStruct {
	uint8_t implTraits;
	uint16_t memPoolData;
	union {
		struct {
			void* data;
			size_t size;
		};

		DataView view;
	};
};
```

члены под-структуры данных могут быть напрямую объявлены в содержащей структуре, как показано ниже:

```v
pub struct C.SomeCStruct {
	implTraits  u8
	memPoolData u16
	// These members are part of sub data structures that can't currently be represented in V.
	// Declaring them directly like this is sufficient for access.
	// union {
	// struct {
	data voidptr
	size usize
	// }
	view C.DataView
	// }
}
```

Наличие членов данных делается известным V, и они могут использоваться без
точного воссоздания оригинальной структуры.

Как альтернатива, вы можете [embed](#embedded-structs) под-структуры данных для поддержания
параллельной структуры кода.
<a id="export-to-shared-library"></a>
### Экспорт в разделяемую библиотеку

По умолчанию все V-функции в C имеют следующую схему именования: `[имя модуля]__[имя_функции]`.

Например, `fn foo() {}` в модуле `bar` даст `bar__foo()`.

Для использования пользовательского имени экспорта используйте атрибут `@[export]`:

```
@[export: 'my_custom_c_name']
fn foo() {
}
```
<a id="translating-c-to-v"></a>
### Трансляция C в V

V может транслировать ваш C-код в читаемый V-код и генерировать V-обертки
поверх C-библиотек.

C2V в настоящее время использует AST Clang для генерации V, поэтому для трансляции C-файла в V
вам нужно иметь установленный Clang на вашей машине.

Давайте сначала создадим простую программу `test.c`:

```c
#include "stdio.h"

int main() {
	for (int i = 0; i < 10; i++) {
		printf("hello world\n");
	}
        return 0;
}
```

Запустите `v translate test.c`, и V сгенерирует `test.v`:

```v
fn main() {
	for i := 0; i < 10; i++ {
		println('hello world')
	}
}
```

Для генерации обертки поверх C-библиотеки используйте эту команду:

```bash
v translate wrapper c_code/libsodium/src/libsodium
```

Это создаст каталог `libsodium` с V-модулем.

Пример V-обертки libsodium, сгенерированной C2V:

https://github.com/vlang/libsodium

<br>

Когда следует транслировать C-код, а когда просто вызывать C-код из V?

Если у вас есть хорошо написанный, протестированный C-код,
то, конечно, вы всегда можете просто вызывать этот C-код из V.

Трансляция его в V дает вам несколько преимуществ:

- Если вы планируете разрабатывать этот кодовую базу, теперь у вас все на одном языке,
  который намного безопаснее и проще для разработки, чем C.
- Кросс-компиляция становится намного проще. Вам вообще не нужно об этом беспокоиться.
- Больше никаких флагов сборки и файлов заголовков.
<a id="working-around-c-issues"></a>
### Обход проблем C

В некоторых случаях совместимость с C может быть чрезвычайно сложной.
Один из таких случаев - когда заголовки конфликтуют друг с другом.
Например, V должен включать библиотеки заголовков Windows, чтобы ваши V-бинарные файлы работали
бесперебойно на всех платформах.

Однако, поскольку библиотеки заголовков Windows используют чрезмерно общие имена, такие как `Rectangle`,
это вызовет конфликт, если вы захотите использовать C-код, в котором также определено имя `Rectangle`.

Для очень специфических случаев, подобных этому, V имеет директивы `#preinclude` и `#postinclude`.

Эти директивы позволяют настроить вещи *до* того, как V добавит свои встроенные библиотеки,
и *после* того, как вся генерация кода V завершена (и, следовательно, все прототипы,
объявления и определения уже присутствуют).

Пример использования:
```v ignore
// This will include before built in libraries are used.
#preinclude "pre_include.h"

// This will include after built in libraries are used.
#include "include.h"

// This will include after all of the V code generation is complete,
// including the one for the main function of the project
#postinclude "post_include.h"
```

Пример того, что может быть включено в `pre_include.h`,
может быть [found here](https://github.com/irishgreencitrus/raylib.v/blob/main/include/pre.h)

Директива `#postinclude`, с другой стороны, полезна для возможности интеграции
таких фреймворков, как SDL3 или Sokol, которые настаивают на наличии колбэков в вашем коде, вместо
того чтобы вести себя как обычные библиотеки, и позволяют вам решать, когда их вызывать.

ПРИМЕЧАНИЕ: это продвинутые функции, и они не будут необходимы вне очень специфических случаев
совместимости с C. Кроме тех случаев, их использование может вызвать больше проблем, чем решить.

Рассмотрите возможность их использования как крайнюю меру!
<a id="other-v-features"></a>
## Другие возможности V
<a id="inline-assembly"></a>
### Встраиваемая ассемблерная вставка

<!-- игнорируется, потому что не проходит проверку форматирования (почему?) -->

```v ignore
a := 100
b := 20
mut c := 0
asm amd64 {
    mov eax, a
    add eax, b
    mov c, eax
    ; =r (c) as c // output
    ; r (a) as a // input
      r (b) as b
}
println('a: ${a}') // 100
println('b: ${b}') // 20
println('c: ${c}') // 120
```

Для получения дополнительных примеров см.
[vlib/v/slow_tests/assembly/asm_test.amd64.v](https://github.com/vlang/v/tree/master/vlib/v/slow_tests/assembly/asm_test.amd64.v)
<a id="hot-code-reloading"></a>
### Горячая перезагрузка кода

```v live
module main

import time

@[live]
fn print_message() {
	println('Hello! Modify this message while the program is running.')
}

fn main() {
	for {
		print_message()
		time.sleep(500 * time.millisecond)
	}
}
```

Соберите этот пример командой `v -live message.v`.

Вы также можете запустить этот пример командой `v -live run message.v`.
Убедитесь, что в команде вы указываете путь к файлу V,
**а не** путь к каталогу (например, `v -live run .`) —
в этом случае вам потребуется изменить содержимое каталога (добавить новый файл и т.д.),
поскольку изменения в *message.v* не будут иметь эффекта.

Функции, которые вы хотите сделать перезагружаемыми, должны иметь атрибут `@[live]`
перед их определением.

На данный момент невозможно изменять типы во время выполнения программы.

Больше примеров, включая графическое приложение:
[github.com/vlang/v/tree/master/examples/hot_reload](https://github.com/vlang/v/tree/master/examples/hot_reload).
<a id="about-keeping-states-in-hot-reloading-functions-with-v-live-run"></a>
#### О сохранении состояния в функциях горячей перезагрузки при использовании v -live run
Горячая перезагрузка кода V основана на отметке функций, которые вы хотите перезагружать, с помощью `@[live]`,
затем компиляции разделяемой библиотеки из этих функций `@[live]`, и затем
ваша программа V загружает эту разделяемую библиотеку во время выполнения.

V (с опцией -live) запускает новый поток, который отслеживает изменения в исходных файлах,
и при обнаружении модификаций перекомпилирует разделяемую библиотеку и перезагружает её во время выполнения,
так что новые вызовы к этим функциям @[live] будут направляться в только что загруженную библиотеку.

Она сохраняет всё накопленное состояние (от локальных переменных вне функций @[live],
от переменных в куче и от глобальных переменных), что позволяет быстро подстраивать код в объединённых функциях.

Когда вносятся более существенные изменения (в структуры данных или в функции, которые не были отмечены),
вам придется вручную перезапускать работающее приложение.
<a id="cross-platform-shell-scripts-in-v"></a>
### Кроссплатформенные скрипты оболочки на V

V может использоваться как альтернатива Bash для написания скриптов развёртывания, сборки и т.д.

Преимуществом использования V для этого является простота и предсказуемость языка, а также
кроссплатформенная поддержка. «V-скрипты» работают в Unix-подобных системах, а также в Windows.

Чтобы использовать режим скриптов V, сохраните исходный файл с расширением `.vsh`.
Это сделает все функции в модуле `os` глобальными (так что вы сможете использовать `mkdir()` вместо
`os.mkdir()`, например).

V также умеет компилировать и запускать файлы `.vsh` немедленно, поэтому вам не потребуется отдельный
этап их компиляции. V также перекомпилирует исполняемый файл, созданный из `.vsh` файла,
*только если он старее исходного файла .vsh*, т.е. последующие запуски будут
быстрее, поскольку нет необходимости в повторной компиляции скрипта, который не был изменён.

Пример `deploy.vsh`:

```v oksyntax
#!/usr/bin/env -S v

// Note: The shebang line above, associates the .vsh file to V on Unix-like systems,
// so it can be run just by specifying the path to the .vsh file, once it's made
// executable, using `chmod +x deploy.vsh`, i.e. after that chmod command, you can
// run the .vsh script, by just typing its name/path like this: `./deploy.vsh`

// print command then execute it
fn sh(cmd string) {
	println('❯ ${cmd}')
	print(execute_or_exit(cmd).output)
}

// Remove if build/ exits, ignore any errors if it doesn't
rmdir_all('build') or {}

// Create build/, never fails as build/ does not exist
mkdir('build')!

// Move *.v files to build/
result := execute('mv *.v build/')
if result.exit_code != 0 {
	println(result.output)
}

sh('ls')

// Similar to:
// files := ls('.')!
// mut count := 0
// if files.len > 0 {
//     for file in files {
//         if file.ends_with('.v') {
//              mv(file, 'build/') or {
//                  println('err: ${err}')
//                  return
//              }
//         }
//         count++
//     }
// }
// if count == 0 {
//     println('No files')
// }
```

Теперь вы можете либо скомпилировать это как обычную программу V и получить исполняемый файл, который можно развёрнуть и запустить
где угодно:
`v -skip-running deploy.vsh && ./deploy`

Либо запустить его как традиционный Bash-скрипт:
`v run deploy.vsh` (или просто `v deploy.vsh`)

На Unix-подобных платформах файл можно запустить напрямую после предоставления ему прав на исполнение с помощью `chmod +x`:
`./deploy.vsh`
<a id="vsh-scripts-with-no-extension"></a>
### Vsh-скрипты без расширения

Хотя V обычно не разрешает vsh-скрипты без предназначенного расширения файла, есть способ
обойти это правило и иметь файл с полностью пользовательским именем и shebang. Хотя эта функция
существует, она рекомендуется только для определённых сценариев использования, таких как скрипты, которые будут помещены в путь и
**не** должны использоваться для таких задач, как скрипты сборки или развёртывания. Чтобы получить доступ к этой функции, начните
файл со строки `#!/usr/bin/env -S v -raw-vsh-tmp-prefix tmp`, где `tmp` — это префикс для
скомпилированного исполняемого файла. Это будет работать в режиме crun, т.е. он будет пересобираться только при изменениях в скрипте
и сохранять бинарный файл как `tmp.<имяскрипта>`. **Внимание**: если этот файл уже
существует, он будет перезаписан. Если вы хотите пересобирать каждый раз и не сохранять этот бинарный файл,
используйте `#!/usr/bin/env -S v -raw-vsh-tmp-prefix tmp run`.

Примечание: существует небольшой скрипт оболочки `cmd/tools/vrun`, который может быть полезен для систем, у которых есть
программа `env` (`/usr/bin/env`), которая всё ещё не поддерживает опцию `-S` (например, BusyBox).
Подробнее см. https://github.com/vlang/v/blob/master/cmd/tools/vrun.

# Приложения
<a id="appendix-i-keywords"></a>
## Приложение I: Ключевые слова

V имеет 45 зарезервированных ключевых слов (3 являются литералами):

```v ignore
as
asm
assert
atomic
break
const
continue
defer
else
enum
false
fn
for
go
goto
if
implements
import
in
interface
is
isreftype
lock
match
module
mut
none
or
pub
return
rlock
select
shared
sizeof
spawn
static
struct
true
type
typeof
union
unsafe
volatile
__global
__offsetof
```

См. также [V Types](#v-types).
<a id="appendix-ii-operators"></a>
## Приложение II: Операторы

Здесь перечислены операторы только для [primitive types](#primitive-types).

```v ignore
+    sum                    integers, floats, strings
-    difference             integers, floats
*    product                integers, floats
/    quotient               integers, floats
%    remainder              integers

~    bitwise NOT            integers
&    bitwise AND            integers
|    bitwise OR             integers
^    bitwise XOR            integers

!    logical NOT            bools
&&   logical AND            bools
||   logical OR             bools
!=   logical XOR            bools

<<   left shift             integer << unsigned integer
>>   right shift            integer >> unsigned integer
>>>  unsigned right shift   integer >> unsigned integer


Precedence    Operator
    5            *  /  %  <<  >> >>> &
    4            +  -  |  ^
    3            ==  !=  <  <=  >  >=
    2            &&
    1            ||


Assignment Operators
+=   -=   *=   /=   %=
&=   |=   ^=
>>=  <<=  >>>=
&&= ||=
```

Примечание: в V `assert -10 % 7 == -3` проходит проверку. В программировании знак остатка
зависит от знаков делителя и делимого.
<a id="other-online-resources"></a>
## Другие онлайн-ресурсы
<a id="v-contributing-guidehttpsgithubcomvlangvblobmastercontributingmd"></a>
### [V contributing guide](https://github.com/vlang/v/blob/master/CONTRIBUTING.md)

V был бы гораздо меньше того, что он сегодня представляет, без помощи всех
своих контрибьюторов. Если вам нравится V и вы хотите помочь проекту добиться успеха,
пожалуйста, прочитайте этот документ, выберите задачу и приступайте!
<a id="v-language-documentationhttpsdocsvlangiointroductionhtml"></a>
### [V language documentation](https://docs.vlang.io/introduction.html)
Этот сайт содержит ту же информацию, что и этот документ, но разделённую на страницы
для более удобного чтения на мобильных устройствах. Обновляется автоматически при каждом
коммите в основной репозиторий.
<a id="v-standard-module-documentationhttpsmodulesvlangio"></a>
### [V standard module documentation](https://modules.vlang.io/)
Этот сайт содержит документацию по всем модулям стандартной
библиотеки V (vlib). Обновляется автоматически при каждом коммите в основной
репозиторий.
<a id="v-online-playgroundhttpsplayvlangio"></a>
### [V online playground](https://play.vlang.io/)
Этот сайт позволяет вводить и редактировать небольшие программы на V, а затем компилировать
и запускать их. Обновляется автоматически при каждом коммите в основной
репозиторий. Используйте его для тестирования ваших идей, когда у вас нет доступа
к компьютеру или телефону Android, на который уже установлена V.
<a id="awesome-vhttpsgithubcomvlangawesome-v"></a>
### [Awesome V](https://github.com/vlang/awesome-v)
Когда вы создаёте крутой проект или библиотеку, вы можете отправить их в этот
список. Вы также можете использовать список для получения идей о новых проектах для
V.
<a id="the-v-language-discordhttpsdiscordggvlang"></a>
### [The V language Discord](https://discord.gg/vlang)
Это место для обсуждения языка V, изучения последних
разработок, получения быстрой помощи по проблемам, участия в
~~эпических войнах в комментариях~~ конструктивных обсуждениях и принятия решений по дизайну.
Присоединяйтесь и узнайте больше о языках, играх, редакторах, людях, клингонах,
законе Конвея и вселенной.
