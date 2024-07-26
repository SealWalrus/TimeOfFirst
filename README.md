# TimeOfFirst
#Документация ALD PRO https://disk.yandex.ru/i/BeBFKJMopWlR9g
#Документация и дистрибутивы https://disk.yandex.ru/d/bcJ-WKIW6wpOgw
Учетки:  
WinDC  Administrator   xxXX1234

aldpro.lab  admin Aa12345678

№Задание 1
- создавать пользователей через подразделения (как в астре так и в AD)
- создание доверительных отношений (https://www.tune-it.ru/web/raist/blog/-/blogs/19054210)

===========================================================================================
Настройка АРМ Астра
===========================================================================================
1. Задать репозитории (deb http://dl.astralinux.ru/astra/frozen/1.7_x86-64/*версия ОС*/repository-base 1.7_x86-64 main non-free contrib)
                      (deb http://dl.astralinux.ru/astra/frozen/1.7_x86-64/*версия ОС*/repository-extended 1.7_x86-64 main contrib non-free)

2. Задать репу aldpro (echo -e "deb https://dl.astralinux.ru/aldpro/stable/repository-main/ 2.1.0 main" | sudo tee /etc/apt/sources.list.d/aldpro.list)
                      (echo -e "deb https://dl.astralinux.ru/aldpro/stable/repository-extended/ generic main" | sudo tee -a /etc/apt/sources.list.d/aldpro.list)

3. Установить дополнительные модули для обеспечения возможности загрузки через https (apt install apt-transport-https ca-certificates open-vm-tools open-vm-tools-desktop)
4. Настроить приоритизацию
                      (Package: *
                      (Pin: release n=generic
                      (Pin-Priority: 900

===========================================================================================
Ввод астры в домен
===========================================================================================

1. Установить пакеты (sudo DEBIAN_FRONTEND=noninteractive apt-get install -q -y aldpro-client)
2. Сменить сетевой интерфейс и задать статический адрес (через NM в графике или через /etc/network/interfaces в терминальной)
3. Запустить скрипт ввода в домен через графику или консольный режим (sudo /opt/rbta/aldpro/client/bin/aldpro-client-installer)





Время первых заметки
