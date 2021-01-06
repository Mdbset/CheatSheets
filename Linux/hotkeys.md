# Terminal 

`Ctrl + Alt + T` - открытие окна терминала

`Ctrl + A` - переход к началу строки ввода
`Ctrl + E` - переход к началу строки ввода
`Alt + B` - перемещает курсор на начало предыдущего слова
`Alt + F` - (не работает) перемещает курсор на начало следующего слова 

`Ctrl + W` - стирает слово перед курсором
`Ctrl + Y` - вставка текст, вырезанный с помощью `Ctrl + U`, `Ctrl + K` и `Ctrl + W`

`Ctrl + U` - удаляет весь текст от начала строки до курсора
`Ctrl + K` - удаляет весь текст от курсора до конца строки

`Ctrl + C` - прерывает выполнения приложения в терминале
`Ctrl + Z` - переводит выполняющее приложение в фоновый режим

`Ctrl + D` - аналог команды _exit_. Для сессии SSH - её разрыв, для терминала - его закрытие. 
`Ctrl + L` - аналог команды _clear_. 

`Ctrl + R` - поиск в истории предыдущих команд
`UpArrow/DownArrow` - пролистывание истории выполненных команд.

# Jobs
Создание job (задача, выполняющаяся в фоне) либо с помощью добавления `&` в конец команды, либо с помощью `Ctrl + Z` в процессе выполнения
`jobs` - текущий список выполняющихся задач.
`kill %4` - убивает задачу под номером 4 (не путать с PID)

# MC
Открытие аналогичной директории
`Alt + O` - открывает базовую директорию на другой панели
`Alt + I` - открывает директорию активной панели на другой панели.