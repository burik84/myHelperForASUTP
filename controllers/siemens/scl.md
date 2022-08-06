# Aboud SCL

## Starting

In folder Sources our Projects insert new Object - SCL-source

Change file. Compile. Close.

Next download ours files (+scl-source files) in controller.

## Class variables

1. ANY_INT включает типы INT, DINT
2. ANY_NUM включает типы INT, DINT, REAL
3. ANY_BIT включает типы BOOL, BYTE, WORD, DWORD

## Programming

- условные ветвления

```scl условные ветвления
if (a>b) then
  // code ;
elsif (b>c) then
  //code ;
else
  // code ;
end_if;
```

- вызов функций

```scl Создание функции
function name:= bool // void
  VAR_INPUT
    nu, vu:BOOL;
  END_VAR;
  VAR_TEMP
    i,minN,N:INT;
    hi,hihi,low,level:REAL;
    RetVal:WORD;
  END_VAR
  VAR_IN_OUT
      HowAct:INT;
  END_VAR

  begin
//code ;
end_function;
```

- вызов организационных блоков, аналогичен функциям

```scl
ORGANIZATION_BLOCK Cycle

  VAR_TEMP
       SINFO :ARRAY [1..20] OF Byte;
      i :INT;
  END_VAR

END_ORGANIZATION_BLOCK
```
