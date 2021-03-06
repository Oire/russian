# Локальный запуск программ D

В стандартной поставке D есть компилятор `dmd`, скрипт-подобный инструмент для запуска `rdmd` и пакетный менеджер `dub`.

### Компилятор DMD

Компилятор *DMD* компилирует исходный код на D и создаёт исполняемый файл.
В командной строке *DMD* можно вызывать с именем файла:

    dmd hello.d

Есть опции, которые позволяют изменить поведение компилятора *DMD*.
Посмотреть список доступных флагов можно изучив [онлайн документацию](https://dlang.org/dmd.html#switches) или
выполнив `dmd --help`.

### Компиляция «на лету» с помощью `rdmd`

Вспомогательный инструмент `rdmd`, распространяемый вместе с компилятором DMD,
следит за тем, чтобы скомпилировались все зависимости, и автоматически запускает
полученную программу:

    rdmd hello.d

На UNIX системах вводная (shebang) строка `#!/usr/bin/env rdmd` может быть
помещена в первую строку запускаемого D файла, чтобы разрешить скрипт-подобное использование.

Посмотреть список доступных флагов можно изучив [онлайн документацию](https://dlang.org/rdmd.html) или выполнив
`rdmd --help`.

### Менеджер пакетов `dub`

Стандартным менеджером пакетов в D является [dub](http://code.dlang.org). Когда
dub установлен локально, новый проект `hello` можно создать, используя командную
строку:

    dub init hello

Запуск `dub` внутри этой папки загрузит все зависимости, скомпилирует приложение
и запустит его.
`dub build` просто скомпилирует проект.

Посмотреть доступные команды и особенности можно изучив [онлайн документацию](https://code.dlang.org/docs/commandline) или
выполнив `dub help`.

Все доступные dub-пакеты можно посмотреть через [веб-интерфейс](https://code.dlang.org).
