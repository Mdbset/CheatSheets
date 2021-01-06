# Firewall

## !!! Все варианты фильтрации вывода с помощью find (findstr) зависят от настроек локализации !!!

Показывает все опции для всех профилей:

`netsh advfirewall show allprofiles`

Можно кратко посмотреть статус для всех профилей:

`netsh advfirewall show allprofiles | find /i "state"`

Выключение фаервола для всех профилей (требует повышения):

`netsh advfirewall set allprofiles state off`