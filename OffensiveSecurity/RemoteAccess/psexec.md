# PsExec

## Windows 10 (10.0.18363 build 18363)
1. Чтобы видеть нормально ошибки подключения:
`chcp 1251`

2. Если при подключении значительная пауза, а потом ошибка Couldn't access _192.168.13.166_, значит проблема с сетевым подключением. Можно решить кардинально:
`netsh advfirewall set allprofiles state off`

3. С Vistа удаленное подключение запрещено для локальных учетных записей [stackoverflow](https://stackoverflow.com/questions/828432/psexec-access-denied-errors). 
Разрешено только для администраторов домена. Можно поменять локальную политику Local Policy: "Network Access: Sharing and security model for local accounts",
либо добавить нужную запись в реестр:

`reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\system /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1 /f`

4. Если подключаться не из машины домена, то у меня такой логин kstepanov@company.ru не сработал, а company\kstepanov нормально.

`PsExec64.exe \\10.100.36.4 -u company\kstepanov -p Qwerty13 cmd`

Если машина не доменная (на домен-контроллере тоже работает без указания домена), тогда:

`PsExec64.exe \\10.100.36.4 -u kstepanov -p Qwerty13 cmd`

5. Если нужно пройти UAC, то необходимо добавить ключ *-h* (https://stackoverflow.com/questions/16735900/psexec-and-uac-issue)

`PsExec64.exe -h \\10.100.36.4 -u company\kstepanov -p Qwerty13 cmd`

6. Чтобы все символы были читаемы и по-английски
`chcp 65001`

7. Выполнять команды
`PsExec64.exe -h \\192.168.1.81 -u company\eborisenko -p Qwerty13 cmd /c mkdir c:\tools`

8. Загружать файлы проще через net use

`net use * \\192.168.1.81\C$ Qwerty13 /user:eborisenko`

`net use <z:> /delete`