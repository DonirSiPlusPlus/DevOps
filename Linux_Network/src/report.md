## __Part 1. Инструмент ipcalc__
---
### ___1. Сети и маски___
+ ___sudo apt install ipcalc___ - установка _ipcalc_
    1. На скриншоте ниже, вывод команды: __ipcalc 192.167.38.54/13__
    ![images/ipcalcadr.png](images/ipcalcadr.png)
        + Адрес сети - __192.160.0.0/13__
    2. На скриншоте ниже, вывод команды: __ipcalc 255.255.255.0__
        ![images/ipcalmask.png](images/ipcalcmask.png)
        + Префиксная запись: __24__
        + Двоичная запись: __11111111.11111111.11111111.00000000__
    
    * На скриншоте ниже, вывод команды: __ipcalc 15__
        ![images/ipcalc15.png](images/ipcalc15.png)
        * Обычная запись - __255.254.0.0__
        + Двоичная запись - __11111111.11111110.00000000.00000000__
    
    * Перевод __11111111.11111111.11111111.11110000__ 
        + В обычную запись - __255.255.255.240__
        + В префиксную запись - __24__
        > __ipcalc__ не принимает в качестве аргумента двоичную запись
    3. На скриншоте ниже, вывод команды: __ipcalc 12.167.38.4/8__
        ![images/min:8.png](images/min:8.png)
        * Минимальный хост: __12.0.0.1__
        + Максимальный хост: __12.255.255.254__
    + На скриншоте ниже, вывод команды: ipcalc 12.167.38.4/255.255.0.0 (11111111.11111111.00000000.00000000)
    ![images/calc3.png](images/calc3.png)
        * Минимальный хост: __12.167.0.1__
        + Максимальный хост: __12.167.255.254__
    + На скриншоте ниже, вывод команды: ipcalc 12.167.38.4/255.255.254.0
    ![images/calc:254.png](images/calc:254.png)
        * Минимальный хост: __12.167.38.1__
        + Максимальный хост: __12.167.39.254__
    + На скриншоте ниже, вывод команды: ipcalc 12.167.38.4/4
    ![images/calc:4.png](images/calc:4.png)
        * Минимальный хост: __0.0.0.1__
        + Максимальный хост: __15.255.255.254__
### ___2. localhost___
* Адреса 194.34.23.100 и 128.0.0.1 не пингуются
+ На скриншоте ниже, пинг адреса __127.0.0.2__
![images/ping002.png](images/ping002.png)
+ На скриншоте ниже, пинг адреса __127.1.0.1__
![images/ping101.png](images/ping101.png)
### ___3. Диапазоны и сегменты сетей___
1. Публичные и частные адреса
    + __10.0.0.45__ - частный. На скриншоте ниже вычисление адреса
    ![images/100045.png](images/100045.png)
    + __134.43.0.2__ - публичный. На скриншоте ниже вычисление адреса
    ![images/1344302png](images/1344302.png)
    + __192.168.4.2__ - частный. На скриншоте ниже вычисление адреса
    ![images/19216842.png](images/19216842.png)
    + __172.20.250.4__ - частный. На скриншоте ниже вычисление адреса
    ![images/172202504.png](images/172202504.png)
    + __172.0.2.1__ - публичный. На скриншоте ниже вычисление адреса
    ![images/172021.png](images/172021.png)
    + __192.172.0.1__ - публичный. На скриншоте ниже вычисление адреса
    ![images/19217201png](images/19217201.png)
    + __172.68.0.2__ - публичный. На скриншоте ниже вычисление адреса
    ![images/1726802.png](images/1726802.png)
    + __172.16.255.255__ - частный. На скриншоте ниже вычисление адреса
    ![images/17216255255.png](images/17216255255.png)
    + __10.10.10.10__ - частный. На скриншоте ниже вычисление адреса
    ![images/10101010.png](images/10101010.png)
    + __192.169.168.1__ - публичный. На скриншоте ниже вычисление адреса
    ![images/1921691681.png](images/1921691681.png)
2. На скриншоте ниже вывод: __ipcalc 10.10.0.0/18                                                           
![images/10100018.png](images/10100018.png) 
+ Возможные адреса __10.10.0.0/18__: 
    + _10.10.0.2_
    + _10.10.10.10_

## __Part 2. Статическая маршрутизация между двумя машинами__
---
+ На скриншоте ниже вызов команды в _ws1_: __ip a__
![images/ipaws1.png](images/ipaws1.png)
+ На скриншоте ниже вызов команды в _ws2_: __ip a__
![images/ipaws2.png](images/ipaws2.png)
* На скриншотах выше видно новые интерфейсы с именем _enp0s8_ внутренней сети на обоих машинах. Флаги состояния указаны как __DOWN__. Чтобы их поднять нужно прописать команду: ___ip link set enp0s8 up___
* На скриншоте ниже отредактированный yaml файл в ws1
![images/yamlws1.png](images/yamlws1.png)
* На скриншоте ниже отредактированный yaml файл в ws2
![images/yamlws2.png](images/yamlws2.png)
* На скриншоте вызов команды __sudo netplan apply__ (никакого вывода на машинах не было)
![images/napply.png](images/napply.png)
### __1. Добавление статического маршрута вручную__
* Чтобы добавить статический маршрут от одной машины до другой и обратно, нужно использовать команду:
    + на ws1: ___sudo ip r add 172.24.116.8 dev enp0s8___
    + на ws2: ___sudo ip r add 192.168.100.10 dev enp0s8___
* На скриншоте вызов команды на __ping 172.24.116.8__ ws1
![images/pingws1.png](images/pingws1.png)
* На скриншоте вызов команды на __ping 192.168.100.10__ ws2
![images/pingws2.png](images/pingws2.png)
### __2. Добавление статического маршрута с сохранением__
* Перезапуск: __reboot__
* На скриншоте ниже отредактированный yaml файл в ws1
![images/edityamlws1.png](images/edityamlws1.png)
* На скриншоте ниже отредактированный yaml файл в ws2
![images/edityamlws2.png](images/edityamlws2.png)
* На скриншоте вызов команды __ping 172.24.116.8__ на ws1
![images/ping2ws1.png](images/ping2ws1.png)
* На скриншоте вызов команды __ping 192.168.100.10__ на ws2
![images/ping2ws2.png](images/ping2ws2.png)
## __Part 3. Утилита iperf3__
---
* установка _iperf_: __sudo apt install iperf3__
1. Перевод скоростей:
    + __8 Mbps = 1 MB/s__
    + __100 MB/s = 819200 Kbps (800000 Kbps)__
    + __1 Gbps = 1024 Mbps (1000 Mbps)__
2. Чтобы проверить скорость между машинами для начала нужно вызвать на втором компьтере команду: __iperf3 -s__
    * На скриншоте ниже вызов этой команды
    ![images/iperf3s.png](images/iperf3s.png)
    * Теперь на первом компьтере надо вызвать: __iperf3 -c 172.24.116.8__. На скриншоте ниже проверка скорости соединения _ws1_ c _ws2_
    ![images/iperf3ws1.png](images/iperf3ws1.png)
    * Скорость соединения ~ __5.04 Gbps__
    * На скриншоте ниже вывод на 2-ом компьтере после проверки
    ![images/iperf3rec.png](images/iperf3rec.png)
## __Part 4. Сетевой экран__
---
1. __iptables__
    * Файрволы:
        + На скриншоте ниже скрипт _firewall.sh_ на ws1
        ![images/firews1.png](images/firews1.png)
        + На скриншоте ниже скрипт _firewall.sh_ на ws2
        ![images/firews2.png](images/firews2.png)
    + Запуск скриптов:
        + На скриншоте ниже запуск скрипта на ws1
        ![images/runfirews1.png](images/runfirews1.png)
        + На скриншоте ниже запуск скрипта на ws2
        ![images/runfirews2.png](images/runfirews2.png)
    * Отличия стратегий в этом случае, т.к. правила взаимоисключающие, работать будет то правило, которое указано раньше. Второе будет игнорироваться
2. __nmap__
    * Установка __nmap__: ___sudo apt install nmap___
    * На скриншоте ниже пинг с ws1 к ws2
    ![images/notping.png](images/notping.png)
    * На скриншоте ниже вызов команды: __nmap 172.24.116.8__
    ![images/nmap1.png](images/nmap1.png)
## __Part 5. Статическая маршрутизация сети__
---
### 1. Настройка конфигураций
#### ___WS11___
* На скриншоте ниже _yaml_ файл            
![images/yamlws11.png](images/yamlws11.png)
* На скриншоте ниже вызов __ip -4 a__ после перезагрузки
![images/ws11-4.png](images/ws11-4.png)
#### ___R1___
* На скриншоте ниже _yaml_ файл
![images/yamlr1.png](images/yamlr1.png)
+ На скриншоте ниже вызов __ip -4 a__ после перезагрузки
![images/r1-4.png](images/r1-4.png)
#### ___R2___
+ На скриншоте ниже _yaml_ файл
![images/yamlr2.png](images/yamlr2.png)
+ На скриншоте ниже вызов __ip -4 a__ после перезагрузки
![images/r2-4.png](images/r2-4.png)
#### ___WS21___
+ На скриншоте ниже _yaml_ файл 
![images/yamlws21.png](images/yamlws21.png)
+ На скриншоте ниже вызов __ip -4 a__ после перезагрузки
![images/ws21-4.png](images/ws21-4.png)
#### ___WS22___
+ На скриншоте ниже _yaml_ файл 
![images/yamlws22.png](images/yamlws22.png)
+ На скриншоте ниже вызов __ip -4 a__ после перезагрузки
![images/ws22-4.png](images/ws22-4.png)
---
* Пинг машин
    + На скриншоте ниже пинг _ws22_ с _ws21_
    ![images/ws21ping.png](images/ws21ping.png)
    + На скриншоте ниже пинг _r1_ с _ws11_
    ![images/ws11ping.png](images/ws11ping.png)
### 2. Включение переадресации IP-адресов
* На скриншоте ниже вызов "__sysctl -w net.ipv4.ip_forward=1__" и вывод на _r1_
![images/r1sysctl.png](images/r1sysctl.png)
* На скриншоте ниже вызов "__sysctl -w net.ipv4.ip_forward=1__" и вывод на _r2_
![images/r2sysctl.png](images/r2sysctl.png)
* На скриншоте ниже измененный _conf_ файл на _r1_
![images/r1pere.png](images/r1pere.png)
* На скриншоте ниже измененный _conf_ файл на _r2_
![images/r2pere.png](images/r2pere.png)
### 3. Установка маршрута по-умолчанию
#### ___WS11___
* На скриншоте ниже отредактированный _yaml_ файл
![images/ws11edyaml.png](images/ws11edyaml.png)
* На скриншоте ниже вызов команды: __ip r__
![images/ws11ipr.png](images/ws11ipr.png)
#### ___WS21___
* На скриншоте ниже отредактированный _yaml_ файл
![images/ws21edyaml.png](images/ws21edyaml.png)
* На скриншоте ниже вызов команды: __ip r__
![images/ws21ipr.png](images/ws21ipr.png)
#### ___WS22___
* На скриншоте ниже отредактированный _yaml_ файл
![images/ws22edyaml.png](images/ws22edyaml.png)
* На скриншоте ниже вызов команды: __ip r__
![images/ws22ipr.png](images/ws22ipr.png)
---
* На скриншоте ниже пинг _r2_ c _ws11_
![images/ws11pingr2.png](images/ws11pingr2.png)
* На скриншоте ниже вызов команды на r2: __tcpdump -th -i eth0__. На нем видно, что пинг с ws11 доходит до r2
![images/r2tcpdump.png](images/r2tcpdump.png)
### 4. Добавление статических маршрутов
* На скриншоте ниже измененный _yaml_ файл на _r1_
![images/r1edyaml.png](images/r1edyaml.png)
* На скриншоте ниже измененный _yaml_ файл на _r2_
![images/r2edyaml.png](images/r2edyaml.png)
* На скриншоте ниже вызов "__ip r__" на _r1_
![images/r1ipr.png](images/r1ipr.png)
* На скриншоте ниже вызов "__ip r__" на _r2_
![images/r2ipr.png](images/r2ipr.png)
* На скриншоте ниже вызов для двух адресов: ___ip r list___
![images/ws11iplists.png](images/ws11iplists.png)
> Маршрут выбран, отличный от 0.0.0.0/0, для адреса 10.10.0.0/18, потому что нужно было указать конкретный адрес назначения для случаев по умолчанию, а не случайное назначение для случаев по умолчаниюю
### 5. Построение списка маршрутизаторов
* На скриншоте ниже вызов "__tcpdump -tnv -i eth0__" на _r1_ 
![images/r1tcpdump.png](images/r1tcpdump.png)
* На скриншоте ниже построение маршрута от _ws11_ до _ws21_ c помощью утилиты ___traceroute___
![images/ws11troute.png](images/ws11troute.png)
+ > Утилита __traceroute__ использует UDP пакеты. Она отправляет пакет с TTL=1 (Time To Live) и смотрит адрес ответившего узла, дальше TTL=2, TTL=3 и так пока не достигнет цели. Каждый раз отправляется по три пакета и для каждого из них измеряется время прохождения. Пакет отправляется на случайный порт, который, скорее всего, не занят. Когда утилита traceroute получает сообщение от целевого узла о том, что порт недоступен трассировка считается завершенной.
### 6. Использование протокола ICMP при маршрутизации
* На скриншоте ниже пинг несуществующего адреса _10.30.0.111_ c _ws11_
![images/ws11pingex.png](images/ws11pingex.png)
+ На скриншоте ниже дамп с r1 и сообщение от _ICMP_
![images/r1tdump2.png](images/r1tdump2.png)
## __Part 6. Динамическая настройка IP с помощью DHCP__
---
### __R2__
1. На скриншоте ниже отредактированный файл __dhcpd.conf__
![images/r2dhcpd.png](images/r2dhcpd.png)
2. На скриншоте ниже отредактированный файл __resolv.conf__
![images/r2nameser.png](images/r2nameser.png)
    + На скриншоте ниже вызов команды "__ip a__" на _ws21_, после перезагрузки _ws22_ и службы _DHCP_ на _r2_
    ![images/ws21getdhcp.png](images/ws21getdhcp.png)
    + На скриншоте ниже ping _ws22_ c _ws21_
    ![images/ws21ping2ws22.png](images/ws21ping2ws22.png)

### __R1__
* На скриншоте ниже измененный _yaml_ файл от ws11 с новым мак-адресом
![images/ws11ed2yaml.png](images/ws11ed2yaml.png)
1. На скриншоте ниже отредактированный файл __dhcpd.conf__
![images/r1dhcpd.png](images/r1dhcpd.png)
2. На скриншоте ниже отредактированный файл __resolv.conf__
![images/r1resolv.png](images/r1resolv.png)
    * На скриншоте ниже вызов команды "__ip a__" на _ws11_, после перезагрузки службы _DHCP_ на _r1_
    ![images/ws11getdhcp.png](images/ws11getdhcp.png)
    + На скриншоте ниже пинг _ws22_ c _ws11_
    ![images/ws11pingws22.png](images/ws11pingws22.png)
3. Для обновления IP используется команда "__sudo dhclient eth0__".
    + На скриншоте ниже показан IP до обновления и после обновления
    ![images/ws21newip.png](images/ws21newip.png)
## __Part 7. NAT__
---
+ Установить _apache2_: __sudo apt-get install apache2__
* На скриншоте ниже измененный файл _ports.conf_ на _ws22_
![images/ws22apache.png](images/ws22apache.png)
+ На скриншоте ниже измененный файл _ports.conf_ на _r1_
![images/r1apache.png](images/r1apache.png)
+ На скриншоте ниже вызов "__service apache2 start__" на _ws22_
![images/ws22servap.png](images/ws22servap.png)
+ На скриншоте ниже вызов "__service apache2 start__" на _r1_
![images/r1servap.png](images/r1servap.png)
### __firewall__
+ На скриншоте ниже _firewall.sh_ от _r2_ c новыми добавленными правилами
![images/r2fire.png](images/r2fire.png)
+ На скриншоте ниже запуск _firewall.sh_ от _r2_                                                     
![images/r2runfire.png](images/r2runfire.png)
+ На скриншоте ниже пинг _ws22_ c _r1_. На нем видно, что пинг не проходит
![images/r1ping2ws22.png](images/r1ping2ws22.png)
* На скриншоте ниже _firewall.sh_ от _r2_ с разрешением на маршрутизацию всех ICMP пакетов
![images/r2fire2.png](images/r2fire2.png)
* На скриншоте ниже пинг _ws22_ c _r1_. На нем видно, что пинг проходит
![images/r1ping3ws22.png](images/r1ping3ws22.png)
### __DNAT и SNAT__
+ На скриншоте ниже firewall.sh на _r2_ с включенным _DNAT_ и _SNAT_
![images/r2fire3.png](images/r2fire3.png)
+ На скриншоте ниже проверка соединения _ws22_ c _r1_ по _TCP_ для _SNAT_
![images/ws22snat.png](images/ws22snat.png)
+ На скриншоте ниже проверка соединения _r1_ c _r2_ по _TCP_ для _DNAT_
![images/r1dnat.png](images/r1dnat.png)
## __Part 8. Дополнительно. Знакомство с SSH Tunnels__
---
+ Установка сервиса sshd: __sudo apt install openssh-server__
1. Запуск сервера apache2 на ws22: __sudo service apache2 start__
2. Чтобы получить доступ к веб-серверу на _ws22_ с _ws21_ нужно использовать команду: ___ssh -L 8080:localhost:80 10.20.0.20___. Через локальный порт 8080 идет подключение к веб-серверу на 80 порту по адресу 10.20.0.20
    + На скриншоте ниже подключение с _ws21_ к веб-серверу на _ws22_
    ![images/ws21tunel.png](images/ws21tunel.png)
    + Переключение на _ws21_ на 2-ой на терминал сочетанием клавиш "__Fn+Alt+F2__" (__Fn+option+F2__)
    + На скриншоте ниже проверка подключения к _ws22_ c _ws21_ при помощи telnet
    ![images/ws21telws22.png](images/ws21telws22.png)
3. Чтобы получить доступ к веб-серверу на _ws22_ с _ws11_ нужно использовать команду: ___ssh -R 8080:localhost:80 10.10.0.2___. Обратное подключение от _ws22_. Прокидывание удаленного порта 8080 к адресу 10.10.0.2 и его соединение с веб-сервером с портом 80
    + На скриншоте ниже соединение _ws11_ с _ws22_
    ![images/ws22pows11.png](images/ws22pows11.png)
    + На скриншоте ниже проверка подключения к _ws22_ c _ws11_ при помощи telnet
    ![images/ws11telws22.png](images/ws11telws22.png)
    ---
