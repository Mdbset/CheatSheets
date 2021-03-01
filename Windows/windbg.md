# Отладка

`bp` установить breakpoint на адрес

`bp kernel32!writefile`

`bu` (Set Unresolved Breakpoint) - breakpoint привязанный к символьному имени. 
A bu breakpoint is set on a symbolic reference to the breakpoint location that is specified in the command (not on an address) and is activated whenever the module with the reference is resolved.

`bl` список breakpoint 

`lm` список загруженных модулей

`ld *` загружает символы для всех модулей 

`lm m s*` - This example includes the m and _s_ options, so only modules that begin with "s" are displayed.

`sxe ld kernel32` sx (Set Exceptions) Enable сработает breakpoint когда будет загружен модуль kernel32.

`k` - Display Stack Backtrace

`p` - исполнение следующей инструкции

`? 0n3507534215121393` - преобразования десятичного числа (0n) в шестнадцатеричное. 

`? 10 + 6 ` - вычисление выражений. По умолчанию все значения шестнадцатеричные если не указано иное (0n - десятичные).

# Чтение памяти

`dd [rsp]` - вывести DWORD (32-разряда)  по указанному адресу

`dq [rsp]` - вывести DWORD (64-разряда)  по указанному адресу

`dc [rsp]` - вывести ASCII-строку по указанному адресу

`du [rsp]` - вывести Unicode-строку по указанному адресу

`r [rax]` - список регистров 

`u [rip] [L5]` - вывести список следующий 5 инструкций начиная с RIP.

# Модификация памяти

`!vprot 00007fffaa08250a` - получить информацию о странице памяти

ed (enter values)

`ed rsp 0` -  ed (enter dword) 



# Базовые комбинации клавиш

`Ctrl + Break` - оставновить долгую операцию (загрузка символов и т.д.)