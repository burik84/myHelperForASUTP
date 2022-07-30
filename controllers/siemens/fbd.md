# Aboud FBD

## bit logic

Обозначение | Назначение | Комментарий|
---: | --- | --- |
`[=]` | присвоение |
`-o` | инвертирование |
`>=1` | ИЛИ |
`&` | И |
`XOR` | строгое/исключающее ИЛИ | используется как переключатель
`[#]` | запоминание результата логической операции | используется для промежуточных результатов и далее этот результат используем по коду
`RS` | сброс и установка бита| приоритет - установка бита
`SR` | установка и сброс бита | приоритет - сброс бита
`[N]/NEG`|выделение негативного фронта сигнала|Момент перехода с 1 в 0
`[P]/POS`|выделение позитивного фронта сигнала|Момент перехода с 0 в 1