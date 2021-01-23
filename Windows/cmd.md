# Hotkey

<Window> + X - открывает свойства кнопки "Пуск". Можно запустить Powershell и Powershell (Администратор)

# Firewall

*!!! Все варианты фильтрации вывода с помощью find (findstr) зависят от настроек локализации !!!*

Показывает все опции для всех профилей:

`netsh advfirewall show allprofiles`

Можно кратко посмотреть статус для всех профилей:

`netsh advfirewall show allprofiles | find /i "state"`

Выключение фаервола для всех профилей (требует повышения):

`netsh advfirewall set allprofiles state off`

# Управление локальными пользователями и группами

`net user` - вывести список локальных пользователей 

`net user User` - вывести информацию о локальном пользователе User

`net user User Password1 /add` добавить пользователя User с паролем Password1

`net user User /del` удалить пользователя User


`net localgroup` - вывести список локальных групп

`net localgroup administrators` - вывести список пользователей локальной группы администраторов

`net localgroup administrator User /add` - добавить пользователя User в группу administrator

`whoami /user` - получает SID