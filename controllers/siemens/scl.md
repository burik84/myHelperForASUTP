# Aboud SCL

## create

1. Open Sources
2. Rught click - Insert New Object - SCL source
3. Change file.
4. Compile. (+Close)
5. Download ours files (+scl-source files) in controller.

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

CASE value OF
    0..3 :
        // Statements_0..3
        ;
    8 :
        // Statements_8
        ;
ELSE:
    // Statements_ELSE
    ;
END_CASE;
```

- циклы

```scl циклы
FOR i:=1 TO 100 BY 1 DO
  IF i>50 THEN
      EXIT;  //безусловный выход из цикла
  END_IF;
  IF (i MOD 2)<>0 THEN //MOD деление от остатка
      CONTINUE; // прерывание и переход на следующий цикл
  END_IF;
  ex.Arr[i]:=1;
END_FOR;

WHILE Lock DO //conditions
  //Code
  //don't forget about Exit out while
  Count:=Count+1;
  T:=T+1;
  IF T>32000 THEN
      EXIT;
  END_IF;
END_WHILE;

REPEAT
  //Code
  //don't forget about Exit out repeat
  Count:=Count+1;
  T:=T+1;
  IF T>32000 THEN
      EXIT;
  END_IF;
  UNTIL NOT Lock  //condition
END_REPEAT;
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
