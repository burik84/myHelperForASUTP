# Aboud STL

## INFO

- RLO - result of logic operation (результат логической операции)
- STA - status (бит состояния оригинал)
- Standard - стандартное состояние

## bit logic

Обозначение | Назначение | Комментарий|
---: | --- | --- |
A I0.0 | AND I0.0 | проверка сигнала на состояние "1" и  |
AN I0.1| AND NOT I0.1| проверка сигнала на состояние "0" и  |
= Q0.0| присвоение|  |
O I0.0 | OR I0.0 |  проверка сигнала на состояние "1" или |
ON I0.1| OR NOT I0.1| проверка сигнала на состояние "0" или |
= Q0.0| присвоение|  |

## вызов блоков

Обозначение | Назначение | Комментарий|
---: | --- | --- |
CALL FC1 | Используется для вызовва блоков, независимо от условий | --- |
UC FC1 | безусловный вызов FC/FB без параметров | аналогична команде CALL |
CC FC1 | условный вызов FC/FB | Возможна если вызываемые FC/FB не имеют параметров |
