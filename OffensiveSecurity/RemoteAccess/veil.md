# Veil

## Установка 

`sudo apt install veil`

`veil` - лучше выбрать silent режим, ибо дальше придеться много раз нажимать _Далее_

## Commands

`sudo veil` - запуск (посмотреть как на Kali)

`<Tab><Tab>` - список команд

`back` which will take us back to the original context of Veil

`checkvt` which will check whether any payloads you’ve generated are flagged by Virus Total

`clean` which removes any previously created payloads

`use Evasion`

`list` - список payloads

`info powershell/meterpreter/rev_tcp.py` - получение детальной информации по payload

`options` show current options

## Payloads

`coldwar_wrapper` - module takes a Windows EXE file and converts it to a Web Archive (WAR) file for execution in a Java Runtime environment

`pyinstaller_wrapper` takes a Python program and converts it to a Windows executable using the _pyinstaller_ application