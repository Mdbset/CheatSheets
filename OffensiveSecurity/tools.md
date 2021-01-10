#Nc

## Примеры

Открытие порта:

`nc -lvp 4444`

Подключение:

`nc 192.168.1.135 4444`

Выгрузка тексового файла пользователя:

`nc -nvlp 8080 < /etc/passwd`

Выгрузка текстого файла, требующего повышения привилегий:

`sudo cat /etc/shadow | nc -nvlp 8080`

Выгрузка бинарного файла:

`nc -vnlp 8080 < ./i.jpeg`

`nc 192.168.1.114 8080 > i.jpeg`

## Параметры

`-n` - don't perform a name lookup
`-v` - verbose, show when a connection is established
`-l` - visten
`-p` - the port to listen on
`-z` - without sending any data
`-w2` - waiting no more than two seconds for a connection to occur