# Windows

## BeRoot

Утилита [BeRoot](https://github.com/AlessandroZ/BeRoot/tree/master/Windows) позволяет получить возможные варианты повышения привилегий.

`BeRoot.exe`

## PowerUp (Powershell Empire)

`PS C:\Tools> Import-Module .\PowerUp.ps1`
`PS C:\Tools> Invoke-Allchecks`

PowerUp позволяет получить:
- пути к службам с пробелами и без кавычек;
- возможные уязвимости DLL Hijacking на основе %PATH%
- потенциальные уязвимости, связанных с исполняемыми файлами и разрешениями служб.

`C:\Program Files\VulnService\services dir\main.exe`

`Write-ServiceBinary -ServiceName 'Vuln Stream' -ServicePath 'C:\Program Files\VulnService\services.exe'`

По умолчанию добавляет сервис, который создает пользователя _john_ и добавляем его в группу локальных администраторов.
 

# Утилиты 

## BeRoot

Утилита [BeRoot](https://github.com/AlessandroZ/BeRoot) позволяет получить возможные варианты повышения привилегий на Windows, Linux и Mac OS. 
Проверяются пути сервисов, запланированные задачи и ключи автозапуска в реестре HKLM.
