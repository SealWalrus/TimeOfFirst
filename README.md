# TimeOfFirst
____
#Документация
Документация ALD PRO https://disk.yandex.ru/i/BeBFKJMopWlR9g Дистрибутивы прошлых лет https://disk.yandex.ru/d/bcJ-WKIW6wpOgw https://kb.infowatch.com/
____
====================
Учетки 
====================
WinDC  Administrator xxXX1234
alddpro.lab  admin Aa12345678
Astra astra astra

№Задание 1
- создавать пользователей через подразделения (как в астре так и в AD)
- создание доверительных отношений (https://www.tune-it.ru/web/raist/blog/-/blogs/19054210)

====================
Настройка АРМ Астра
====================
1. Задать репозитории (deb http://dl.astralinux.ru/astra/frozen/1.7_x86-64/*версия ОС*/repository-base 1.7_x86-64 main non-free contrib)
                      (deb http://dl.astralinux.ru/astra/frozen/1.7_x86-64/*версия ОС*/repository-extended 1.7_x86-64 main contrib non-free)

2. Задать репу aldpro (echo -e "deb https://dl.astralinux.ru/aldpro/stable/repository-main/ 2.1.0 main" | sudo tee /etc/apt/sources.list.d/aldpro.list)
                      (echo -e "deb https://dl.astralinux.ru/aldpro/stable/repository-extended/ generic main" | sudo tee -a /etc/apt/sources.list.d/aldpro.list)

3. Установить дополнительные модули для обеспечения возможности загрузки через https (apt install apt-transport-https ca-certificates open-vm-tools open-vm-tools-desktop)
4. Настроить приоритизацию в /etc/apt/preference.d/aldpro
                      Package: *
                      Pin: release n=generic
                      Pin-Priority: 900

===========================================================================================
Ввод астры в домен
===========================================================================================

1. Установить пакеты (sudo DEBIAN_FRONTEND=noninteractive apt-get install -q -y aldpro-client)
2. Сменить сетевой интерфейс и задать статический адрес (через NM в графике или через /etc/network/interfaces в терминальной)
3. Запустить скрипт ввода в домен через графику или консольный режим (sudo /opt/rbta/aldpro/client/bin/aldpro-client-installer)

/Консольный режим/ sudo /opt/rbta/aldpro/client/bin/aldpro-client-installer -c aldpro.lab -u admin -p Aa12345678 -d astra-cli -i -f
/Графика/ sudo /opt/rbta/aldpro/client/bin/aldpro-client-installer


Порядок установки IWTM

1. Закомментить локалхост хостнейм и добавить хостнейм резолвящий тачку  
2. Прописать репу фрозен 1.7.0 base
3. Запустить установку

Если меняешь IP-то зайди в файл /opt/iw/tm5/etc/consul/consul.json

Учетка админа administrator xxXX1234

==============================================================================================================================================
УСТАНОВКА .NET
==============================================================================================================================================
Загрузка и установка пакетов .Net Core из сторонних источников
Установка из репозитория Microsoft
Обновить пакет libxkbfile1 до версии не ниже 1:1.1.0 из репозиториев Debian:
Загрузить пакет: 

wget http://archive.ubuntu.com/ubuntu/pool/main/libx/libxkbfile/libxkbfile1_1.1.0-1_amd64.deb
Установить пакет:

sudo apt install ./libxkbfile1_1.1.0-1_amd64.deb
Для включения установки пакетов с использованием протокола HTTPS установить пакеты ca-certificates и apt-transport-https, если они не были установлены ранее:

sudo apt install ca-certificates apt-transport-https
Добавить ключ подписывания пакетов Microsoft в список доверенных ключей:

wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
Загрузить параметры репозитория Microsoft (параметры сохраняются в файле /etc/apt/sources.list.d/microsoft-prod.list):

На момент обновления статьи в указанных ниже репозиториях предоставлялись одинаковые версии пакетов.
Для Astra Linux Special Edition РУСБ.10015-01 (очередное обновление 1.7):

sudo wget https://packages.microsoft.com/config/debian/10/prod.list -O /etc/apt/sources.list.d/microsoft-prod.list
Для Astra Linux Special Edition РУСБ.10015-01 (очередное обновление 1.6), Astra Linux Special Edition РУСБ.10015-16 исп. 1, Astra Linux Common Edition:

sudo wget https://packages.microsoft.com/config/debian/9/prod.list -O /etc/apt/sources.list.d/microsoft-prod.list
Не забывайте удалять ненужные сторонние репозитории после того, как установка из них завершена.

Обновить кеш пакетов:

sudo apt update

Установить пакеты:

Библиотеки разработчика:

sudo apt install dotnet-sdk-<номер_версии>

Библиотеки исполнения:

sudo apt install aspnetcore-runtime-<номер_версии>

где номер версии — 2.1, 2.2, 3.0, 3.1, 5.0, 6.0, 7.0.

==============================================================================================================================================
УСТАНОВКА POSTGRESQL
==============================================================================================================================================
Установить PSQL 11

1. sudo -u postgres psql
ALTER USER имяпользователя WITH PASSWORD 'новыйпароль';
