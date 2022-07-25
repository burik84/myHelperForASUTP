# Sebol

## Об использовании

Я сталкивался с применением SEBOL'a в блоках SFC и CALCU. CALCU у меня есть отдельный файл, а SFC (функциональная схема последовательности) - графический язык программирования, применяемый для определения последовательностей управления.

SEquence and Batch Oriented Language (SEBOL) - язык программирования, предназначенный для управления процессами.

## Вводная часть

ссылка на главу самоучителя о [SEBOL](https://www.maxplant.ru/article/centum_tutorial_5.php)
Комментарии

```text
! Текст комментария
```

Специальные символы в константах

* Перевод на новую строку `\n`
* Табуляция `\t`
* Обратная косая черта `\`
* Кавычки `\"`

## Начальные шаги

Глобальная декларация.

```text
global block <block code><tag name>
global block _SFCPB TANK_DATA
global block %SW CTRLMODE alias P_CTRLMODE
```

```text
global genname <block code><global generic name>
global genname MC-2E VLV
global genname %SW VLV_M
```

Объявление переменных

```text
!Локальные переменные
long ds
integer i,sbs,conf[84,3],flow[84],m,d[2],res[2]
char*16 s,e[84],g[84],f[84],p[84],l[84]
float delta,psbs
!Глобальные переменные
global integer i,j,l,flag,vlv_tmp[14],sbs
global long tm1, tm2, tm
```

## Операторы с примерами

Список операторов

|Тип |Операторы|
|:------:|:------:|
| Арифметические  | +, -, *, / |
|Сравнения   | >, < <=, >=, ==, <>  |
|Логические  |  and, or, eor, not|
|Побитовые  | &, ^, <<, >>, <@, >@|

Оператор условия `if`

```text
if(<выражение>)<оператор>
```

```text
if(<выражение>)then
  <оператор>
else
  <оператор 2>
end if
```

```text
if(<выражение>)then
  <оператор>
else if
  <оператор 2>
else
  <оператор 3>
end if
```

Оператор цикла `for next@`

```text
for <переменная>=<начальное значение> to <конечное значение>[step <шаг>] ! по умолчанию step равен 1 и можно не писать
  <оператор>
next@
```

Оператор цикла `while` - пока выражение **истина** будут выполняться операторы между while и wend. Если выражение **ложь**, то операторы между while и wend *не выполняются*

```text
while(1) !<выражение>
 !операторы
wend@
```

Оператор `switch` (переключатель)

```text
switch(<выражение>)
 case <константа1>:
 ...
 case <константа2>
 ...
 otherwise: !Если результат не соответствует ни одной из констант, то выполняется здесь.
 ...
end switch
```

Оператор `delay` - задержка времени

```text
delay <время задержки> !время указывается в мс
delay 2000 !время 2 сек
```

Оператор `format` - задание формата симвльной строки и сохранение ее в переменной символьной строки

```text
format <форматирующая символьная строка>,<данные>;<переменная хранения символьной строки>
format "203M%d_1",i; s
format "TRUCK_STUB_T%d",i;t
```

Оператор `assign` присвоить - имя тэга может быть присвоено локальному родовому имени.

```text
assign <имя тэга> to <локальное родовое имя>
assign "PIC001" to tag001 ! присваивание имени тега PIC001 локальному родовому имени tag001
```

Оператор `message` - используется для печати в качестве сообщения произвольной строки символов и сохранения ее в файле исторических данных

```text
message <фомратирующая символьная строка>,<выходная величина>,PR,<номер элемента>,<параметр>
message "FCS0101. Блок %s MODE=AUT",t
message "Налив1. Запуск группы насосов"
message "201_%1dPT%2d 201_%1dPT%2d %d",n,i-n*10+49,n,i-n*10+59,al
```

Оператор `ssread` чтение данных подсистем

```text
ssread <номер строки>,<номер карты>,<номер доступа>,<относительное положение>;
<переменная для хранения состояния данных>;
<переменная для хранения данных>:<тип данных>,<переменная для хранения данных>:<тип данных>,...
ssread 1, 1, 1, addr; dSts; n:integer, dir:integer, flag:integer
```

Оператор `sswrite` записи данных подсистем

```text
sswrite <номер строки>,<номер карты>,<номер доступа>,<относительное положение>;<переменная>:<тип данных>,...
sswrite 1, 1, 1, 1925; char21:char16, char22:char16
```

### Встроенные функции

`dabs(arg)` функция которая взвращает абсолютное значение параметра, тип данных "double"

Оператор `mid()` извлекает произвольную символьную строку из середины символьной строки.

```text
mid(arg1, arg2, arg3)
!система возвращает символьную строку, состоящую из “arg3” символов,
!начиная с n-ого символа в “arg1”, n задается параметром “arg2”
s=mid(char1,i,1)
```

Конкатенация строк `cat(a)` - сцепляет символьные строки

```text
cat(arg1, arg2)
!Система возвращает строковый параметр “arg2”,
!подсоединенный к строковому параметру “arg1” как результат действия функции.
char22=cat(char22,s)
```

Преобразование в строку `chr(a)`

Преобразование в целое число `ichr(a)`

```text
n=ichr(s)
s=chr(n)
```

```text
format "TRUCK_STUB_T%d",i;t
message "FCS0101. Блок %s MODE=AUT",t
assign t to LOGIC
LOGIC.MODE = "AUT"
```

### Примеры с разбором

```text
for i=1 to 84
  format "203FV%d",110+i;t
  message "FCS0101. Блок %s MODE=AUT,SW=1",t
  assign t to REG
  REG.MODE = "AUT"
  REG.SW = 1
next@
```

```text
while (1)
  for i=1 to 84
      assign p[i] to PRESS
      sbs=%.SBS[i]
      if (sbs==0) then
        %.P_NAME[i] = "НЕОПРЕДЕЛЕН"
        end if
  next@
wend@
```

```text
while(1)
  for i=1 to 64
    j=i+1
    ssread 1,1,1,j;ds;t1:integer
    %.b2[i]=t1
  next@
wend@
```

[назад](../index.md)