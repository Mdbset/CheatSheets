# Terminator 

There are several keyboard shortcuts available:

`Ctrl-Shift-E`: Split the view vertically.
`Ctrl-Shift-O`: Split the view horizontally.

`Ctrl-Shift-<Plus>`: Zoom In
`Ctrl-<Plus>`: Zoom Out

`Ctrl-Shift-P`: Focus be active on the previous view.
`Ctrl-Shift-N`: Focus be active on the next view.

`Ctrl-Shift-W`: Close the view where the focus is on.
`Ctrl-Shift-Q`: Exit terminator.
`Ctrl-Shift-X`: Enlarge active window

`Ctrl-Alt-W`: Edit window title

# Базовые команды

## mknod

mknod создает FIFO (именованный канал), специальный символьный или специальный блочный файл, с именем _имя_.

`mknod [опции] имя p`

## tail
Ключ -n <количество строк> (или просто -<количество строк>) позволяет изменить количество выводимых строк:

`tail [-20] /var/log/messages`

При использовании специального ключа -f утилита tail следит за файлом: новые строки (добавляемые в конец файла другим процессом) автоматически выводятся на экран в реальном времени. Это особенно удобно для слежения за журналами. Например:

`tail -f /var/log/messages`

Используйте опцию -F, если производится слежение за автоматически архивируемыми файлами журналов, например, с помощью logrotate. В этом случае слежение за файлом будет происходить даже в случае его переименования, пересоздания или удаления.

`tail -F /var/log/messages`

## head 

Выводит первые n строк из файла, по умолчанию n равно 10:

`head [-20] /var/log/messages`

## tee

Добавление бинарного файла в виде base64 в конец файла:

`base64 -w 0 /home/user/binary.exe |  sudo tee -a /home/user/jssmuggling.html`

## watch

watch — утилита, которая запускает определённую программу через фиксированный интервал времени, задаваемый опцией -n в секундах (по умолчанию 2). Опция -d включает подсветку изменений в выводе относительно предыдущего запуска. Завершить программу можно с помощью нажатия соответствующих клавиш (обычно <CTRL-C>)

`watch [-d] [-n sec] COMMAND [args]`

## wc -l

wc подчитывает количество слов и другое 

`wc -l` - подсчитывает количество строк

## lsof
lsof (от англ. LiSt of Open Files) — утилита, служащая для вывода информации о том, какие файлы используются теми или иными процессами. 

### Примеры

`lsof /dev/hd4` - cписок открытых файлов на устройстве /dev/hd4

`lsof -c ssh` - cписок подключений по ssh

`lsof -i tcp:80` - просмотр информации о процессе, который прослушивает 80 TCP порт

`lsof -i 4 -a -p 1437` - просмотр всех соединений IPv4, открытых процессом с PID = 1437

`lsof -Pi | grep 23` 

### Параметры

`-i` - выводить IPv4(6) файлы;
`-P` - выводит значения портов, вместо имён сервисов.


## killall 

`killall` предназначена для завершения всех процессов, имеющих одно и то же имя. 

### Пример

`killall gcalctool`

## nc



## strace

## find