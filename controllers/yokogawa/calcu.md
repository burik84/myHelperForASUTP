# CALCU

Что это и как его использовать.

Но главное это ограничения. Да у этого блока есть ``ограничения`` при расчетах, как оно выражается? Очень просто - перестает корректно работать или вообще не работает. Поэтому использовать его только для ``простейших операций`` с длинной кода **не более 50 строк** или меньше.

*CALCU* - вычислительный блок общего назначения. Есть еще *CALCU-C* - это блок со строчным входом/выходом.

*См. инструкцию Part D Функциональные блоки детали, D2.47*

---

## Вводная часть

Комментарии

```text
! Текст комментария
* оператор комментария
```

Оператор определения программы

```text
program
  Объявление переменных
  alias
  код
  и т.д.
end
```

Неявное объявления переменных **в начале программы**

```text
#implicit none
```

Определение псевдонима для переменной (входа, выхода и т.д.) **в начале программы**

```text
alias <псевдоним> <tag>.<параметр>
alias   _ft   FT73001.PV
alias   _d  404TIME.DAY
alias _pid_p FT22101.P
alias _pl FT22101.PL
alias _tm1  H8_2_TM1.DV
alias name {name_pid.MODE.AUTO}
alias low {name.ALRM.LO}
alias _tm3_st {H8_2_TM3.BSTS.NR}
alias _tm1  {H8_2_TM1.OP.START}
alias K1A {404COMPR_STAT_RL.X01.GE}
alias _P1IOP {209_2PT6.ALRM.IOP}
alias _P2IOP_ {209_2PT10.ALRM.IOP-}
```

Объявление локальных переменных **в начале программы**

```text
integer a !целое
long a !длинное целое
float a !действительное с запятой
double a !двойная точность с запятой
```

---

## Всё про синтаксис

Использование *{ }*

```text
Используем если нам нужно условие в программе заключаем {}
{<tag>.<параметр>.<условие>}
CPV = {tag.PV.1} + {tag2.PV.1}*2 + {tag3.PV.1}*4
```

Использование *% и %%*

```text
%%<tag>.<параметр> данные блока прибора
%.XWxxxx.<PV> если элемент не имеет имя тэга, то используем номер терминала

```

Перенос на новую строку выражения \

```text
if (условие) or \
    (условие) or \
    (условие) then
  программа
end if
```

### Функции с примером

`dlimit(arg1, arg2,arg3)` функция верхнего нижнего предела, используемые для заключения данных внутри заданных верхнего и нижнего пределов

```text
dlimit(arg1, arg2,arg3)
!arg1 данные
!arg2 нижний предел
!arg3 верхний предел
P04 = (RV+0.1)*100.0/2.6
P03 = dlimit(P04,0,1000)
```

---

### Для работы

Входные переменные *RV1...RV4*

Выходные переменные *CPV, CPV1, CPV2, CPV3, P01...P08*

```text
P04 = (RV+0.1)*100.0/2.6
CPV=tag+tag*2
```

Оператор *if else*

```text
if (условие) программа 1.0 ! в одну строчку без then и end if
if (условие) then
  программа 1.0
end if
if (условие) then
  программа 1.0
else
  программа 2.0
end if
```

Простейшие операции

```text
сложение <+>
вычитание <->
умножение <*>
деление </>
Операторы сравнения <,>,>=,<=,==,<>
логические операторы and, or, not
условия (условие1 and условие2 or условие3)
NOT()
```

### Примеры с комментариями

```text
alias AUTO {NAME_PID.MODE.AUTO}
alias LOW {NAME_KIP.ALRM.LO}

if (AUTO) cpv=1 !Если режим NAME_PID выбран AUTO, то CPV=1
if (LOW) cpv1=1 !Если для NAME_KIP сигнализация LO, то CPV1=1

E8TT_DIF.DT01 = (TT22056.PV-TT22055.PV)*not({TT22056.PV=CAL})*not({TT22055.PV=CAL})
```

```text
if ((RV - RV1) >= 0.3 or (RV1 - RV) >= 0.3) then ! используем вход RV и RV1
 CPV = 1
else
  CPV1 = 0
end if
```

!Краткая форма условий для выражений

```text
alias a1 21ZRU_S1PWR.PV
alias a2 21ZRU_QL1ON.PV
alias a5 21_AUTO.PV
alias a8 21DG1_FIRE.PV
alias a9 21DG2_FIRE.PV
alias a10 21DG3_FIRE.PV
alias a11 21DG4_FIRE.PV
alias a12 21DG5_FIRE.PV
alias a13 21_RTP2.PV

alias b1 21POWER404_AL.PV
alias b3 21AUTO_AL.PV
alias b5 21FIRE_AL.PV
alias b6 21REQ404_AL.PV


b1=a1 and a2
b3=not a5
b5=a8 or a9 or a10 or a11 or a12
b6=a13
```

```text
alias OPMK1 80_5Z200_9.OPMK
alias ST1 %WW0123.PV
alias LINK PAKSCAN_14_ALRM.PV

OPMK1=((ST1 & 2)>0 or LINK>0)*2+((ST1 & 2)==0 and LINK==0)*((ST1 & 128)>0)*3

```

```text
! Без объявления тэгов
if (V302ALT4_3_13.PV > V302BLT4_3_13.PV) then
  P01 = V302ALT4_3_13.PV
else
  P01 = V302BLT4_3_13.PV
end if
```

```text
alias OP 2071KSE4_OP.PV
alias OPN 2071KSE4_OPN.PV
alias CLS 2071KSE4_CLS.PV
alias MODE 2071KSE4_MODE.PV

OP = (RV==1)
CPV=1*(OPN==1)+2*(CLS==1)
MODE = (RV1==1)
```

```text
! Суммтор для расходомера
alias   _ft   209_2FT1_N_CALC.CPV
alias _d   404TIME.DAY
alias   _h     404TIME.HOUR

CPV1 = (_ft / 3600.0) * (_ft>=0)

CPV2 = CPV1 + CPV2  ! summator dlya ezhednevnogo sbrosa
CPV3 = CPV2

P03 = CPV1 + P03  !summator dlya ezhemesyachnogo sbrosa
CPV = P03

! ежедневный сброс в 8ч и сохранение данных
if ((_h==8) AND (P01==0)) then
  P08 = CPV3
  CPV2 = 0
  P01=1
end if

!сброс триггера ежедневного
if ((_h==9) AND (P01==1))    P01=0

! Ежемесячный сброс данных и сохранение данных
if ((_d==1) AND (P02==0)) then
  P07 = CPV
  P03 = 0
  P02=1
  end if

!Сброс триггера ежемесячного
if ((_d==2) AND (P02==1))    P02=0

end
```

### Примеры с операциями побитовыми

```text
! из примера перерасчета температур с Enraf в АСУТП (exc TT21056_CALCU)
#implicit none

alias DATA1 RV1

P01 = (DATA1 >> 24) & $FF
P02 = (DATA1 >> 16) & $FF

P03 = (DATA1 >> 8) & $FF
P04 = DATA1 & $FF

CPV1 = (P02-$30) * 100 + (P03-$30)*10 + (P04-$30)

if (P01 == $2D) CPV = CPV * (-1)

end

```

[назад](../index.md)
