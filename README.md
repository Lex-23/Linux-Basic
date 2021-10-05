### Settings and minimal requirements for instances:
- RDS: PostgreSQL 12.7-R1, db.t2.micro, `Storage type`: General Purpose SSD (gp2), `Allocated storage`: 20 GB
- EC2: Amazon Linux 2 AMI (HVM), t2.micro, `SSD Volume Type`: ami-00dfe2c7ce89a450b (64-bit x86) / ami-031dea1a744251b51 (64-bit Arm)
- Security groups:
  1. **ec2_connect**: In(`Type`: HTTP/HTTPS, `Protocol`: TCP, `Port range`: 443, `Source`: 0.0.0.0/0), Out(All traffic)
  2. **ec2_connect**: In(`Type`: HTTP/HTTPS, `Protocol`: TCP, `Port range`: 443, `Source`: 0.0.0.0/0), Out(All traffic)
# Linux-Basic
**Linux**  — семейство Unix-подобных операционных систем на базе ядра Linux, включающих тот или иной набор утилит и программ проекта GNU, и, возможно, другие компоненты. Как и ядро Linux, системы на его основе, как правило, создаются и распространяются в соответствии с моделью разработки свободного и открытого программного обеспечения. Linux-системы распространяются в основном бесплатно в виде различных дистрибутивов — в форме, готовой для установки и удобной для сопровождения и обновлений, — и имеющих свой набор системных и прикладных компонентов, как свободных, так и проприетарных (собственнических).  

За счёт использования свободного программного обеспечения и привлечения волонтёров каждая из систем Linux обладает значительными программными возможностями, трудно реализуемыми в прочих моделях разработки: например, в 2008 году расчёты показывали, что для того, чтобы «с нуля» разработать систему, аналогичную Fedora 9, потребовалось бы затратить 10,8 млрд $, а совокупная себестоимость только ядра Linux оценивалась в сумму более 1,4 млрд $, притом только за 2008 год она увеличилась на 315 млн $, совокупный труд оценён в размере 73 тыс. человеко-лет.  

Семейство систем, включающих в качестве компонентов основные программы проекта GNU, такие как bash, gcc, glibc, coreutils, GNOME и ряд других, иногда идентифицируется как GNU/Linux. Так как традиционно большинство систем было именно таким, под «Linux» обычно подразумеваются именно они; притом существует спор об именовании GNU/Linux. Существует проект стандартизации внутренней структуры Linux-систем — Linux Standard Base, часть документов которого зарегистрирована в качестве стандартов ISO; но далеко не все системы сертифицируются по нему, и в целом для Linux-систем не существует какой-либо общепризнанной стандартной комплектации или формальных условий включения в семейство. Однако есть ряд систем на базе ядра Linux, но не имеющих в основе зависимости от программ GNU, которые поэтому "GNU/Linux" не называют, в частности, таковы мобильные системы Android и FirefoxOS.  

В отличие от коммерческих систем, таких как Windows или macOS, Linux не имеет географического центра разработки. Нет и организации, которая владела бы этой системой. Linux — результат работы тысяч проектов. Некоторые из этих проектов централизованы, некоторые сосредоточены в фирмах. Многие проекты объединяют хакеров со всего света, которые знакомы только по переписке. Создать свой проект или присоединиться к уже существующему может любой и, в случае успеха, результаты работы станут известны миллионам пользователей. Пользователи принимают участие в тестировании свободных программ, общаются с разработчиками напрямую, что позволяет быстро находить и исправлять ошибки и реализовывать новые возможности.  

Большинство пользователей для установки Linux используют дистрибутивы, включающие не только набор программ, но и решающие ряд задач по обслуживанию, объединённых едиными системами установки, управления и обновления пакетов, настройки и поддержки.  

Самые распространённые в мире дистрибутивы (2017): Linux Mint, Ubuntu, Debian, Mageia, Fedora, OpenSUSE, ArchLinux, CentOS, PCLinuxOS, Slackware, Gentoo. Многие из дистрибутивов связаны друг с другом и в той или иной степени совместимы, в частности, Ubuntu основан на Debian, а дистрибутивы Mint основаны как на Ubuntu, так и Debian (LMDE) и полностью с ними совместимы, но при этом включают дополнительно поддержку по умолчанию Java, Adobe Flash и некоторых других проприетарных компонентов, а CentOS основан на исходных текстах коммерческого дистрибутива Red Hat Enterprise Linux (доступного в бинарной сборке только платным подписчикам) и при этом полностью бинарно совместимый с ним. 

[**Семь причин, почему Линукс:**](https://habr.com/ru/post/488064/)
- Прозрачность
- Доступность
- Безопасность
- Децентрализация
- Гибкость и разнообразие
- Масштабируемость
- Простота  

## File system
### Структура файловой системы Linux  
В ОС Windows жесткие диски называются латинскими буквами (С:, D:, ...), и каждый из дисков представляет собой корневой каталог с собственным деревом папок. Подключение же нового устройства приведет к появлению нового корневого каталога со своей буквой (например, F:). В ОС Linux файловая система представлена единым корневым каталогом, обозначаемым как слэш (/). Соответственно, при данной файловой структуре не диски содержат каталоги, а каталог — диски.  

**Подключение внешних носителей**. В ОС Linux имеется процедура монтирования: когда подключается съемный носитель или диск, файл устройства будет виден в каталоге /dev (devices). Чтобы увидеть содержимое этого устройства, его нужно смонтировать в отдельную директорию /mnt. Также файловая система позволяет примонтировать его и в любое другое место, например /home.  

Корневой каталог в Linux всегда только один, а все остальные каталоги в него вложены, т. е. для пользователя файловая система представляет собой единое целое. В действительности, разные части файловой системы могут находиться на совершенно разных устройствах: разных разделах жёсткого диска, на разнообразных съёмных носителях (лазерных дисках, дискетах, флэш-картах), даже на других компьютерах (с доступом через сеть). Для того, чтобы соорудить из этого хозяйства единое дерево с одним корнем, используется процедура монтирования.  

Для монтирования необходим пустой каталог — он называется точкой монтирования. Точкой монтирования может служить любой каталог, никаких ограничений на этот счёт в Linux нет. При помощи специальной команды (mount) мы объявляем, что в данном каталоге (пока пустом) нужно отображать содержимое такого-то устройства. После этой операции в каталоге (точке монтирования) появятся все те файлы и каталоги, которые находятся на соответствующем устройстве. В результате пользователь может даже и не знать, на каком устройстве какие файлы располагаются.  

Подключённую таким образом («смонтированную») файловую систему можно в любой момент отключить — размонтировать (для этого имеется специальная команда umount), после чего тот каталог, куда она была смонтирована, снова окажется пустым. 

Одно из устройств для Linux является самым важным — это корневая файловая система (root filesystem). Именно к ней затем будут подключаться (монтироваться) все остальные файловые системы на других устройствах. Обратите внимание, что корневая файловая система тоже монтируется, но только не к другой файловой системе, а к «самой Linux», причём точкой монтирования служит «/» (корневой каталог). Поэтому при загрузке системы прежде всего монтируется корневая файловая система, а при останове она размонтируется (в последнюю очередь).  

Пользователю обычно не требуется выполнять монтирование и размонтирование вручную: при загрузке системы будут смонтированы все устройства, на которых хранятся части файловой системы, а при останове (перед выключением) системы все они будут размонтированы. Файловые системы на съёмных носителях (лазерных дисках, дискетах и пр.) также монтируются и размонтируются автоматически — либо при подключении носителя, либо при обращении к соответствующему каталогу.

**Понятие файла**. Понятие «файл» в Linux имеет несколько другое значение, нежели в Windows. «Файлом» можно назвать обычный файл, содержащий данные, и интерпретируемый программой. Директория также является «файлом», содержащим в себе ссылки на другие директории или файлы с данными. Файлы устройства указывает на драйвер, благодаря которому система взаимодействует с физическими устройствами. Имеются и многие другие типы файлов.  

**Принцип установки программ**. Если в Windows программы, зачастую, хранят все данные в одной папке, например в «C:Program FilesProgramName», то в Linux файлы программы разделяются по каталогам в зависимости от типа. Например, исполняемые файлы в /bin, библиотеки в /lib, файлы конфигураций в /etc, логи и кэш в /var.  

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
    
Стандартное размещение файлов позволяет и человеку, и даже программе предсказать, где находится тот или иной компонент системы. Для человека это означает, что он сможет быстро сориентироваться в любой системе Linux (где файловая система организована в соответствии со стандартом) и найти то, что ему нужно. Для программ стандартное расположение файлов — это возможность организации автоматического взаимодействия между разными компонентами системы.  

**Типы файловых систем Linux**.  
Каждый дистрибутив Linux позволяет использовать одну из этих файловых систем, каждая из них имеет свои преимущества и недостатки. Все они включены в ядро и могут использоваться в качестве корневой файловой системы.  
- Ext2, Ext3, Ext4 или Extended Filesystem - это стандартная файловая система для Linux. Она была разработана еще для Minix. Она самая стабильная из всех существующих, кодовая база изменяется очень редко и эта файловая система содержит больше всего функций.
- JFS или Journaled File System. Сейчас она используется там, где необходима высокая стабильность и минимальное потребление ресурсов.
- ReiserFS. Она была разработана под руководством Ганса Райзера и поддерживает только Linux. Из особенностей можно отметить динамический размер блока, что позволяет упаковывать несколько небольших файлов в один блок, что предотвращает фрагментацию и улучшает работу с небольшими файлами. Еще одно преимущество - в возможности изменять размеры разделов на лету. Но минус в некоторой нестабильности и риске потери данных при отключении энергии.
- XFS. Из преимуществ файловой системы можно отметить высокую скорость работы с большими файлами
- Btrfs или B-Tree File System - это совершенно новая файловая система, которая сосредоточена на отказоустойчивости, легкости администрирования и восстановления данных. 
***
## Hard link vs Soft link
### Символические и жесткие ссылки в Linux
**Ссылка на файл в Linux** — это указатель на файл. Если проводить аналогию с Windows, то ссылки чем-то похожи на ярлыки. То есть вы создаете ссылку, которая указывает на какой-либо файл или директорию, и можете разместить эту ссылку в другом каталоге. Обращаясь к такой ссылке, вы будете обращаться к настоящему файлу или каталогу. Ссылки в Linux бывают двух типов: символические и жесткие. Не смотря на то, что оба типа называются ссылками, они имеют существенные отличия друг от друга.  

**Символическая ссылка (symbolic link)** — это специальный файл, который является ссылкой на другой файл или каталог (их еще называют целевым файлом, целевым каталогом).  

Символические ссылки также называют символьными, мягкими ссылками (soft links) или сим-ссылками (sym-link).  

Важно понимать, что символическая ссылка не содержит в себе внутри копии самого файла, на которую она указывает. Она является всего лишь указателем на файл. Не смотря на это, символическая ссылка обладает собственными правами доступа, так как сама является небольшим файлом, который содержит путь до целевого файла.  

Возвращаясь к аналогии с ярлыками в Windows, символические ссылки это своего рода ярлыки на файлы. Можно создавать несколько символических ссылок на один файл и эти ссылки могут иметь разные имена.  

Связь между символической ссылкой и файлом, на который она указывает, является «мягкой». Если удалить символическую ссылку, то файл, на который она указывает, не удаляется.  

Если удалить файл, на который указывает ссылка, то сама ссылка не обновляется и остается на диске. При этом она указывает на уже несуществующий файл. Аналогично, если переименовать или переместить целевой файл, то ссылка не обновляется автоматически.  

При создании символических ссылок можно указывать относительный путь до целевого файла. В таком случае ссылка считает, что относительный путь указан относительно каталога, в котором создана сама ссылка (но не относительно каталога, из которого она была создана).  

Схематично отношение между файлом, символической ссылкой и данными, которые хранятся в файле, можно показать следующим образом:

![image](https://pingvinus.ru/files/notes2/ln/ln-soft-link.png)

**Жесткая ссылка (hard link)** является своего рода синонимом для существующего файла. Когда вы создаете жесткую ссылку, создается дополнительный указатель на существующий файл, но не копия файла.  

Жесткие ссылки выглядят в файловой структуре как еще один файл. Если вы создаете жесткую ссылку в том же каталоге, где находится целевой файл, то они должны иметь разные имена. Жесткая ссылка на файл должна находится в той же файловой системе, где и другие жесткие ссылки на этот файл.  

В Linux каждый файл имеет уникальный идентификатор - **индексный дескриптор (inode)**. Это число, которое однозначно идентифицирует файл в файловой системе. Жесткая ссылка и файл, для которой она создавалась имеют одинаковые inode. Поэтому жесткая ссылка имеет те же права доступа, владельца и время последней модификации, что и целевой файл. Различаются только имена файлов. Фактически жесткая ссылка это еще одно имя для файла.  

Жесткие ссылки нельзя создавать для директорий.

Жесткая ссылка не может указывать на несуществующий файл.

Жесткие ссылки появились раньше, чем символические, но сейчас уже устаревают. В повседневной работе жесткие ссылки используются редко.

Схематично отношение между исходным файлом, жесткой ссылкой и данными можно показать следующей схемой:

![image](https://pingvinus.ru/files/notes2/ln/ln-hard-link.png)

**Создание символических ссылок**

Чтобы создать символическую ссылку, нужно выполнить команду ln с опцией -s:

~~~
ln -s /home/pingvinus/myfile.txt mylink
~~~
**Создание жестких ссылок**

Чтобы создать жесткую ссылку нужно использовать команду ln без опции -s.

~~~
ln myfile.txt hardlinktofile
~~~
![image](https://wiki.merionet.ru/images/myagkie-i-zhestkie-ssylki-v-linux/3.png)  
пример
***
## Users & Groups
Linux в целом и Ubuntu в частности - системы многопользовательские, т.е. на одном компьютере может быть несколько различных пользователей, каждый со своими собственными настройками, данными и правами доступа к различным системным функциям.  

Кроме пользователей в Linux для разграничения прав существуют группы. Каждая группа так же как и отдельный пользователь обладает неким набором прав доступа к различным компонентам системы и каждый пользователь-член этой группы автоматически получает все права группы. То есть группы нужны для группировки пользователей по принципу одинаковых полномочий на какие-либо действия. Каждый пользователь может состоять в неограниченном количестве групп и в каждой группе может быть сколько угодно пользователей.  
Вообще основной областью применения механизма пользователей и групп является не совсем разграничение доступа к различным функциям системы, а скорей разграничение доступа к файлам на винчестере.  
### Права доступа в Linux
Права доступа определяются по отношению к трём типам действий: 

- **Чтение (r)** - разрешает получать содержимое файла, но на запись нет. Для каталога позволяет получить список файлов и каталогов, расположенных в нем;
- **Запись (w)** - разрешает записывать новые данные в файл или изменять существующие, а также позволяет создавать и изменять файлы и каталоги;
- **Выполнение (x)** - вы не можете выполнить программу, если у нее нет флага выполнения. Этот атрибут устанавливается для всех программ и скриптов, именно с помощью него система может понять, что этот файл нужно запускать как программу.  

Но все эти права были бы бессмысленными, если бы применялись сразу для всех пользователей. Поэтому каждый файл имеет три категории пользователей, для которых можно устанавливать различные сочетания прав доступа:  

- **Владелец (u)** - набор прав для владельца файла, пользователя, который его создал или сейчас установлен его владельцем. Обычно владелец имеет все права, чтение, запись и выполнение.
- **Группа (g)** - любая группа пользователей, существующая в системе и привязанная к файлу. Но это может быть только одна группа и обычно это группа владельца, хотя для файла можно назначить и другую группу.
- **Остальные (o)** - все пользователи, кроме владельца и пользователей, входящих в группу файла.  
     
### Специальные права доступа к файлам в Linux

Для того, чтобы позволить обычным пользователям выполнять программы от имени суперпользователя без знания его пароля была придумана такая вещь, как SUID и SGID биты.   

- SUID - если этот бит установлен, то при выполнении программы, id пользователя, от которого она запущена заменяется на id владельца файла. Фактически, это позволяет обычным пользователям запускать программы от имени суперпользователя;
- SGID - этот флаг работает аналогичным образом, только разница в том, что пользователь считается членом группы, с которой связан файл, а не групп, к которым он действительно принадлежит. Если SGID флаг установлен на каталог, все файлы, созданные в нем, будут связаны с группой каталога, а не пользователя. Такое поведение используется для организации общих папок;
- Sticky-bit - этот бит тоже используется для создания общих папок. Если он установлен, то пользователи могут только создавать, читать и выполнять
### Просмотр права доступа к файлам в Linux
Чтобы узнать права на файл linux выполните такую команду, в папке где находится этот файл, надо выполнить:
~~~
ls-l
~~~
или
~~~
ll
~~~
![image](https://losst.ru/wp-content/uploads/2016/10/perm.jpeg)

За права файлов в linux тут отвечают черточки. Первая это тип файла, которые будут рассмотрены позже. Дальше же идут группы прав сначала для владельца, для группы и для всех остальных. Всего девять черточек на права и одна на тип.  
Условные значения флагов прав:

    --- - нет прав, совсем;
    --x - разрешено только выполнение файла, как программы но не изменение и не чтение;
    -w- - разрешена только запись и изменение файла;
    -wx - разрешено изменение и выполнение, но в случае с каталогом, вы не можете посмотреть его содержимое;
    r-- - права только на чтение;
    r-x - только чтение и выполнение, без права на запись;
    rw- - права на чтение и запись, но без выполнения;
    rwx - все права;
    --s - установлен SUID или SGID бит, первый отображается в поле для владельца, второй для группы;
    --t - установлен sticky-bit, а значит пользователи не могут удалить этот файл.

В нашем примере, файл test1 имеет типичные разрешения для программ, владелец может все, группа только чтение и выполнение, а все остальные - только выполнение. Для test2 дополнительно установлен флаг SUID и SGID. А для папки test3 установлен Sticky-bit. Файл test4 доступный всем. Теперь вы знаете как посмотреть права на файл linux.  
### Типы файлов в Линукс
![image](https://younglinux.info/sites/default/files/images/linux-bash/filestype.png)
## Изменение прав и наделение правами в Линукс
### sudo 
Утилита sudo (substitute user and do — дословно "подменить пользователя и выполнить") - основной способ повышать привилегии в современных системах.
Ситуаций, в которых необходимо повышать привилегии и выполнять команды от имени суперпользователя (root), довольно много:
- Установка новых программ
- Навигация по чужим директориям
- Изменение прав доступа и владельцев файлов, не принадлежащих текущему пользователю
- Создание, редактирование и удаление файлов в местах, где не хватает прав текущего пользователя
- Запуск программ, требующих повышенные привилегии 
 
Использовать sudo очень просто, достаточно написать эту команду слева от любой другой и выполнить. По умолчанию она пытается повысить привилегии до суперпользователя. В зависимости от настроек sudo в системе эта утилита может попросить ваш пароль для входа либо вообще откажется работать, сказав, что у вас нет права её использовать. Как правило, в Ubuntu sudo спрашивает пароль и запоминает его на 5 минут. На протяжении этого времени вы можете использовать sudo, не вводя пароль каждый раз.  
Иногда бывает нужно выполнить команду из-под пользователя, отличного от root. Тогда придётся добавить флаг -u:
~~~
$ sudo -u nobody mkdir /tmp/test
~~~
**Подводные камни** использования команды sudo.  
Запуск команды, которая создаёт файлы и директории из-под sudo, приводит к тому, что владельцем этих файлов становится пользователь root. Фактически все последующие обращения к этому файлу без sudo начнут выдавать ошибку об отсутствии прав доступа. Причём даже необязательно работать с этими файлами напрямую: множество программ так или иначе обращаются к файловой системе для чтения конфигурационных и других файлов.  

Правильный выход из ситуации в каждом случае свой. В некоторых случаях sudo это то, что нужно, но иногда требуется изменить права (об этом в следующем уроке), а иногда и переустановить какую-нибудь часть системы.  

Наиболее общее правило может быть таким: всё, что лежит в личных директориях пользователя, должно принадлежать пользователю, а не суперпользователю. Всё, что требует дополнительных прав, так как находится в системных путях (вне домашней директории пользователя), скорее должно запускаться с sudo (но это необязательно).
### chmod
Чтобы изменить права на файл в linux вы можете использовать утилиту chmod. Она позволяет менять все флаги, включая специальные. Эта команда имеет типичный для команд linux синтаксис, сначала команда, затем опции, а в конце файл или папка, к которой ее нужно применить:  
~~~
$ chmod опции права /путь/к/файлу
~~~
Синтаксис настройки прав такой:

**группа_пользователей**действие**вид_прав**

В качестве действий могут использоваться знаки "+" - включить или "-" - отключить. Рассмотрим несколько примеров:

    u+x - разрешить выполнение для владельца;
    ugo+x - разрешить выполнение для всех;
    ug+w - разрешить запись для владельца и группы;
    o-x - запретить выполнение для остальных пользователей;
    ugo+rwx - разрешить все для всех;

Но права можно записывать не только таким способом. Есть еще восьмеричный формат записи, он более сложен для понимания, но пишется короче и проще:

    0 - никаких прав;
    1 - только выполнение;
    2 - только запись;
    3 - выполнение и запись;
    4 - только чтение;
    5 - чтение и выполнение;
    6 - чтение и запись;
    7 - чтение запись и выполнение.
Для простоты запоминания: **4 - чтение, 2 - запись, 1 - выполнение** (все остальное -  суммируем эти три вида).  
Права на папку linux такие же, как и для файла. Во время установки прав сначала укажите цифру прав для владельца, затем для группы, а потом для остальных. Например, :

    744 - разрешить все для владельца, а остальным только чтение;
    755 - все для владельца, остальным только чтение и выполнение;
    764 - все для владельца, чтение и запись для группы, и только чтение для остальных;
    777 - всем разрешено все.

Опции команды **chmod**:

    -c - выводить информацию обо всех изменениях;
    -f - не выводить сообщения об ошибках;
    -v - выводить максимум информации;
    --preserve-root - не выполнять рекурсивные операции для корня "/";
    --reference - взять маску прав из указанного файла;
    -R - включить поддержку рекурсии;
    --version - вывести версию утилиты;
    
### chown
При создании файла, тот пользователь, от имени которого он был создан, становится его владельцем, а группой устанавливается основная группа владельца. Но владельца файла и группу можно менять, для этого используются команда chown.  
Синтаксис chown, как и других подобных команд linux очень прост:
~~~
$ chown пользователь опции /путь/к/файлу
~~~
В поле пользователь надо указать пользователя, которому мы хотим передать файл. Также можно указать через двоеточие группу, например, пользователь:группа. Тогда изменится не только пользователь, но и группа. Вот основные опции, которые могут вам понадобиться:

    -c, --changes - подробный вывод всех выполняемых изменений;
    -f, --silent, --quiet - минимум информации, скрыть сообщения об ошибках;
    --dereference - изменять права для файла к которому ведет символическая ссылка вместо самой ссылки (поведение по умолчанию);
    -h, --no-dereference - изменять права символических ссылок и не трогать файлы, к которым они ведут;
    --from - изменять пользователя только для тех файлов, владельцем которых является указанный пользователь и группа;
    -R, --recursive - рекурсивная обработка всех подкаталогов;
    -H - если передана символическая ссылка на директорию - перейти по ней;
    -L - переходить по всем символическим ссылкам на директории;
    -P - не переходить по символическим ссылкам на директории (по умолчанию).

 
Меняем владельца папки dir1 на root
~~~
$ chown root ./dir1
~~~
Если вы хотите поменять сразу владельца и группу каталога или файла запишите их через двоеточие, например, изменим пользователя и группу для каталога dir2 на root:
~~~
$ chown root:root ./dir2
~~~
## Systemd
Systemd — подсистема инициализации и управления службами в Linux, фактически вытеснившая в 2010-е годы традиционную подсистему init. Основная особенность — интенсивное распараллеливание запуска служб в процессе загрузки системы, что позволяет существенно ускорить запуск операционной системы. Основная единица управления — модуль, одним из типов модулей являются «службы» — аналог демонов — наборы процессов, запускаемые и управляемые средствами подсистемы и изолируемые контрольными группами.  
Подсистема оперирует специально оформленными файлами конфигурации — модулями (англ. unit). Каждый модуль отвечает за отдельно взятую службу, точку монтирования, подключаемое устройство, файл подкачки, виртуальную машину и тому подобные ресурсы.  Помимо простого запуска и контроля служб, systemd предлагает некоторые другие удобные функции, для использования которых ранее системным администраторам приходилось прибегать к помощи дополнительных программ-демонов. Среди таких функций:

    сокет-активация служб (заменяет inetd);
    запуск сервисов по расписанию (заменяет cron)[12];
    работа с аппаратным сторожевым таймером (заменяет watchdog);
    смена корня (заменяет chroot);
    автомонтирование томов и сетевых ресурсов (заменяет mount и fstab);
    journalctl — служба журналирования;
    systemd-analyze — анализ скорости запуска служб;
    systemd-boot — UEFI загрузчик(замена grub).
    
unit для systemd:
    
    [Unit]
    Description=MyUnit
    After=syslog.target
    After=network.target
    After=nginx.service
    After=mysql.service
    Requires=mysql.service
    Wants=redis.service

    [Service]
    Type=forking
    PIDFile=/work/www/myunit/shared/tmp/pids/service.pid
    WorkingDirectory=/work/www/myunit/current

    User=myunit
    Group=myunit

    Environment=RACK_ENV=production

    OOMScoreAdjust=-1000

    ExecStart=/usr/local/bin/bundle exec service -C /work/www/myunit/shared/config/service.rb --daemon
    ExecStop=/usr/local/bin/bundle exec service -S /work/www/myunit/shared/tmp/pids/service.state stop
    ExecReload=/usr/local/bin/bundle exec service -S /work/www/myunit/shared/tmp/pids/service.state restart
    TimeoutSec=300

    [Install]
    WantedBy=multi-user.target 

***
## Полезные ссылки
[Файловая система Linux](https://serverspace.by/support/help/struktura-fajlovoj-sistemy-linux/)  
[Символические и жесткие ссылки в Linux](https://medium.com/@krisbredemeier/the-difference-between-hard-links-and-soft-or-symbolic-links-780149244f7d)  
[Пользователи, группы и права доступа в Linux](https://losst.ru/prava-dostupa-k-fajlam-v-linux)  
[команда sudo](https://ru.hexlet.io/courses/cli-basics/lessons/sudo/theory_unit)  
[команда chmod](https://losst.ru/komanda-chmod-linux)  
[команда chown](https://losst.ru/komanda-chown-linux)  
[systemd](https://ru.wikipedia.org/wiki/Systemd)  





