# Linux-Basic
## File system
### Структура файловой системы Linux
***
В ОС Windows жесткие диски называются латинскими буквами (С:, D:, ...), и каждый из дисков представляет собой корневой каталог с собственным деревом папок. Подключение же нового устройства приведет к появлению нового корневого каталога со своей буквой (например, F:). В ОС Linux файловая система представлена единым корневым каталогом, обозначаемым как слэш (/). Соответственно, при данной файловой структуре не диски содержат каталоги, а каталог — диски.
***
**Подключение внешних носителей**. В ОС Linux имеется процедура монтирования: когда подключается съемный носитель или диск, файл устройства будет виден в каталоге /dev (devices). Чтобы увидеть содержимое этого устройства, его нужно смонтировать в отдельную директорию /mnt. Также файловая система позволяет примонтировать его и в любое другое место, например /home.
***
**Понятие файла**. Понятие «файл» в Linux имеет несколько другое значение, нежели в Windows. «Файлом» можно назвать обычный файл, содержащий данные, и интерпретируемый программой. Директория также является «файлом», содержащим в себе ссылки на другие директории или файлы с данными. Файлы устройства указывает на драйвер, благодаря которому система взаимодействует с физическими устройствами. Имеются и многие другие типы файлов.
***
**Принцип установки программ**. Если в Windows программы, зачастую, хранят все данные в одной папке, например в «C:Program FilesProgramName», то в Linux файлы программы разделяются по каталогам в зависимости от типа. Например, исполняемые файлы в /bin, библиотеки в /lib, файлы конфигураций в /etc, логи и кэш в /var.
***
**Регистр имен**. Также стоит отметить чувствительность файловой системы Linux к регистру. Файлы Temp.txt и temp.txt будут интерпретироваться как разные файлы и могут находиться в одной директории, в отличие от ОС Windows, который не различает регистр имен. То же правило действует и на каталоги — имена в разных регистрах указывают на разные каталоги.
Назначение каждой директории регламентирует «Стандарт иерархии файловой системы» FHS (Filesystem Hierarchy Standard). Ниже опишем основные директории согласно стандарту FHS:  

![image](https://serverspace.by/wp-content/uploads/2020/06/63_fhs.png)


    / — root каталог. Содержит в себе всю иерархию системы;
    /bin — здесь находятся двоичные исполняемые файлы. Основные общие команды, хранящиеся отдельно от других программ в системе (прим.: pwd, ls, cat, ps);
    /boot — тут расположены файлы, используемые для загрузки системы (образ initrd, ядро vmlinuz);
    /dev — в данной директории располагаются файлы устройств (драйверов). С помощью этих файлов можно взаимодействовать с устройствами. К примеру, если это жесткий диск, можно подключить его к файловой системе. В файл принтера же можно написать напрямую и отправить задание на печать;
    /etc — в этой директории находятся файлы конфигураций программ. Эти файлы позволяют настраивать системы, сервисы, скрипты системных демонов;
    /home — каталог, аналогичный каталогу Users в Windows. Содержит домашние каталоги учетных записей пользователей (кроме root). При создании нового пользователя здесь создается одноименный каталог с аналогичным именем и хранит личные файлы этого пользователя;
    /lib — содержит системные библиотеки, с которыми работают программы и модули ядра;
    /lost+found — содержит файлы, восстановленные после сбоя работы системы. Система проведет проверку после сбоя и найденные файлы можно будет посмотреть в данном каталоге;
    /media — точка монтирования внешних носителей. Например, когда вы вставляете диск в дисковод, он будет автоматически смонтирован в директорию /media/cdrom;
    /mnt — точка временного монтирования. Файловые системы подключаемых устройств обычно монтируются в этот каталог для временного использования;
    /opt — тут расположены дополнительные (необязательные) приложения. Такие программы обычно не подчиняются принятой иерархии и хранят свои файлы в одном подкаталоге (бинарные, библиотеки, конфигурации);
    /proc — содержит файлы, хранящие информацию о запущенных процессах и о состоянии ядра ОС;
    /root — директория, которая содержит файлы и личные настройки суперпользователя;
    /run — содержит файлы состояния приложений. Например, PID-файлы или UNIX-сокеты;
    /sbin — аналогично /bin содержит бинарные файлы. Утилиты нужны для настройки и администрирования системы суперпользователем;
    /srv — содержит файлы сервисов, предоставляемых сервером (прим. FTP или Apache HTTP);
    /sys — содержит данные непосредственно о системе. Тут можно узнать информацию о ядре, драйверах и устройствах;
    /tmp — содержит временные файлы. Данные файлы доступны всем пользователям на чтение и запись. Стоит отметить, что данный каталог очищается при перезагрузке;
    /usr — содержит пользовательские приложения и утилиты второго уровня, используемые пользователями, а не системой. Содержимое доступно только для чтения (кроме root). Каталог имеет вторичную иерархию и похож на корневой;
    /var — содержит переменные файлы. Имеет подкаталоги, отвечающие за отдельные переменные. Например, логи будут храниться в /var/log, кэш в /var/cache, очереди заданий в /var/spool/ и так далее.
***
