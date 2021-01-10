(https://stackoverflow.com/questions/828432/psexec-access-denied-errors)
1. С Vistа удаленное подключение запрещено для локальных учетных записей. Разрешено только для администраторов домена и локальных администраторов.
Local Policy: "Network Access: Sharing and security model for local accounts"
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\system /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1 /f
2. (!!!) ОБЯЗАТЕЛЬНО ПЕРЕЗАГРУЗИТЬ КОМПЬЮТЕР

3. Естественно необходимо сетевое соединение.
netsh advfirewall set allprofiles state off

3. Если подключаться не из машины домена, то у меня такой логин kstepanov@company.ru не сработало, а company\kstepanov нормально.
PsExec64.exe \\10.100.36.4 -u company\kstepanov -p Qwerty13 cmd

4. Если нужно пройти UAC, то необходимо добавить ключ -h
(https://stackoverflow.com/questions/16735900/psexec-and-uac-issue)
PsExec64.exe -h \\10.100.36.4 -u company\kstepanov -p Qwerty13 cmd

5. Чтобы все символы были читаемы и по-английски
chcp 65001

6. Выполнять команды
PsExec64.exe -h \\192.168.1.81 -u company\eborisenko -p Qwerty13 cmd /c mkdir c:\tools

7. Загружать файлы
	PsExec64.exe -h \\192.168.1.81 -u company\eborisenko -p Qwerty13 cmd /c mkdir c:\tools
Проще через net use
	net use * \\192.168.1.81\C$ Qwerty13 /user:eborisenko
	net use <z:> /delete