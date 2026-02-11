# Part 1. Инструмент ipcalc

## Подними виртуальную машину (далее -- ws1)

- поднял виртуальную машину в `VirtualBox` с `Ubuntu 20.04 LTS`

## 1.1. Сети и маски

- 1) Адрес сети 192.167.38.54/13 - `192.160.0.0`

- 2) Перевод маски 255.255.255.0 в префиксную и двоичную запись - `/24` и `11111111.11111111.11111111.00000000`, /15 в обычную и двоичную - `11111111.11111110.00000000.00000000` и `255.254.0.0`, 11111111.11111111.11111111.11110000 в обычную и префиксную - `255.255.255.240` и `/28`

- 3) Минимальный и максимальный хост в сети 12.167.38.4 при масках: /8 - `12.0.0.1` и `12.255.255.254`, 11111111.11111111.00000000.00000000 - `12.167.0.1` и `12.167.255.254`, 255.255.254.0 - `12.167.38.1` и `12.167.39.254`, /4 - `0.0.0.1` и `15.255.255.254`

## 1.2. localhost

- Определи и запиши в отчёт, можно ли обратиться к приложению, работающему на localhost, со следующими IP: 194.34.23.100 - `нельзя`, 127.0.0.2 - `можно`, 127.1.0.1 - `можно`, 128.0.0.1 - `нельзя`

## 1.3. Диапазоны и сегменты сетей

- 1) Какие из перечисленных IP можно использовать в качестве публичного, а какие только в качестве частных: 10.0.0.45 - `частный`, 134.43.0.2 - `публичный`, 192.168.4.2 - `частный`, 172.20.250.4 - `частный`, 172.0.2.1 - `публичный`, 192.172.0.1 - `публичный`, 172.68.0.2 - `публичный`, 172.16.255.255 - `частный`, 10.10.10.10 - `приватный`, 192.169.168.1 - `публичный`

- 2) Какие из перечисленных IP-адресов шлюза возможны у сети 10.10.0.0/18: 10.0.0.1 - `невозможен`, 10.10.0.2 - `возможен`, 10.10.10.10 - `возможен`, 10.10.100.1 - `невозможен`, 10.10.1.255 - `возможен`

# Part 2. Статическая маршрутизация между двумя машинами

## Подними две виртуальные машины (далее -- ws1 и ws2).

- поднял две виртуальные машины в `VirtualBox` с `Ubuntu 20.04 LTS`

## С помощью команды ip a посмотри существующие сетевые интерфейсы.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_ipa.png?ref_type=heads)
- вывод команды `ip a` на `ws1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_ipa.png?ref_type=heads)
- вывод команды `ip a` на `ws2`

## Опиши сетевой интерфейс, соответствующий внутренней сети, на обеих машинах и задай следующие адреса и маски: ws1 — 192.168.100.10, маска /16, ws2 — 172.24.116.8, маска /12.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_netplan_yaml_1.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на `ws1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_netplan_yaml_1.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на `ws2`

## Выполни команду netplan apply для перезапуска сервиса сети.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_netplan_apply.png?ref_type=heads)
- вывод и вызов команды `netplan apply` на `ws1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_netplan_apply.png?ref_type=heads)
- вывод и вызов команды `netplan apply` на `ws2`

## 2.1. Добавление статического маршрута вручную

- зашел в `tools` и создал `nat network`
- изменил в настройках `ws1` и `ws2` `network` с `NAT` на `NAT network`, чтобы объединить машины в одну локальную сеть, ибо в режиме `NAT` вм изолированы друг от друга

## Добавь статический маршрут от одной машины до другой и обратно при помощи команды вида ip r add.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_ipr_add.png?ref_type=heads)
- использование команды `ip r add` на `ws1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_ipr_add.png?ref_type=heads)
- использование команды `ip r add` на `ws2`

## Пропингуй соединение между машинами.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_ping_1.png?ref_type=heads)
- пинг `ws2` на `ws1` командой `ping`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_ping_1.png?ref_type=heads)
- пинг `ws1` на `ws2` командой `ping`

## 2.2. Добавление статического маршрута с сохранением

## Перезапусти машины.

- прописал команду `reboot` на `ws1` и `ws2`

## Добавь статический маршрут от одной машины до другой с помощью файла /etc/netplan/00-installer-config.yaml.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_netplan_yaml_2.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на `ws1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_netplan_yaml_2.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на `ws2`

## Пропингуй соединение между машинами.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_ping_2.png?ref_type=heads)
- пинг `ws2` на `ws1` командой `ping`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_ping_2.png?ref_type=heads)
- пинг `ws1` на `ws2` командой `ping`

# Part 3. Утилита iperf3

## 3.1. Скорость соединения

## Переведи и запиши в отчёт: 8 Mbps в MB/s, 100 MB/s в Kbps, 1 Gbps в Mbps.

- 8 Mbps - `1 MB/s`.
- 100 MB/s - `800 000 Kbps`.
- 1 Gbps - `1000 Mbps`.

## 3.2. Утилита iperf3

## Измерь скорость соединения между ws1 и ws2.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_iperf3_result.png?ref_type=heads)
- запуск сервера на `ws2` командой `iperf3 -s` и результат замера скорости

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_iperf3_result.png?ref_type=heads)
- запуск клиента на `ws1` командой `iperf -c 172.24.116.8` и результат замера скорости

# Part 4. Сетевой экран

## 4.1. Утилита iptables

## Создай файл /etc/firewall.sh, имитирующий файрвол, на ws1 и ws2:

- создал файл командой `sudo touch /etc/firewall.sh` на `ws1` и `ws2` соответственно

## Добавление в файл правил

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_firewallsh.png?ref_type=heads)
- содержание файла `/etc/firewall.sh` на `ws1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_firewallsh.png?ref_type=heads)
- содержание файла `/etc/firewall.sh` на `ws2`

## Запусти файлы на обеих машинах командами chmod +x /etc/firewall.sh и /etc/firewall.sh.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm1_firewall_run.png?ref_type=heads)
- запуск файла на `ws1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_firewall_run.png?ref_type=heads)
- запуск файла на `ws2`

- разница заключается в том, что `iptables`, смотрит сверху-вниз и принимает решения при первом попавшем пункте правила. То есть на `ws1` он увидит `DROP` и отклонит `echo-reply`, не посмотрев на противоложное `ACCEPT` правило снизу, а на `ws2` он примет решение `ACCEPT`, не посмотрев на противоложное ему правило `DROP` снизу.

## 4.2. Утилита nmap

## Командой ping найди машину, которая не «пингуется», после чего утилитой nmap покажи, что хост машины запущен.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm2_nmap_and_ping.png?ref_type=heads)
- использование команд `ping` для того, чтобы найти машину, которая не пингуется и `nmap` для того, чтобы понять, что машина поднята

## Сохрани дампы образов виртуальных машин

- сохранил дампу образов виртуальных машин через `file` и `Export Appliance`

# Part 5. Статическая маршрутизация сети

## Подними пять виртуальных машин (3 рабочие станции (ws11, ws21, ws22) и 2 роутера (r1, r2)).

- поднял пять виртуальных машин в `VirtualBox` с `Ubuntu 20.04 LTS`

## 5.1. Настройка адресов машин

## Настрой конфигурации машин в etc/netplan/00-installer-config.yaml согласно сети на рисунке.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на ws11

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm21_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на ws21

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm22_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на ws22

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на `r2`

## Перезапусти сервис сети. Если ошибок нет, командой ip -4 a проверь, что адрес машины задан верно. Также пропингуй ws22 с ws21. Аналогично пропингуй r1 с ws11.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `ws11`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `ws21`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws22_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `ws22`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `r2`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_ping_r1.png?ref_type=heads)
- пинг `r1` с `ws11`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_ping_ws22.png?ref_type=heads)
- пинг `ws22` с `ws21`

## 5.2. Включение переадресации IP-адресов

## Для включения переадресации IP выполни команду на роутерах:

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_sysctl_w.png?ref_type=heads)
- вызов и вывод команд `sysctl -w net.ipv4.forward=1` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_sysctl_w.png?ref_type=heads)
- вызов и вывод команд `sysctl -w net.ipv4.forward=1` на `r2`

## Открой файл /etc/sysctl.conf и добавь в него следующую строку: net.ipv4.ip_forward = 1

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_sysctl_conf.png?ref_type=heads)
- вид файла конфигурации `etc/sysctl.conf` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_sysctl_conf.png?ref_type=heads)
- вид файла конфигурации `etc/sysctl.conf` на `r2`

## 5.3. Установка маршрута по умолчанию

## Настрой маршрут по умолчанию (шлюз) для рабочих станций. Для этого добавь default перед IP-роутера в файле конфигураций.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на ws11

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm21_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на ws21

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/vm22_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на ws22

## Вызови ip r и покажи, что добавился маршрут в таблицу маршрутизации.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_ip_r.png?ref_type=heads)
- вызов и вывод команд `ip r` на `ws11`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_ip_r.png?ref_type=heads)
- вызов и вывод команд `ip r` на `ws21`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws22_ip_r.png?ref_type=heads)
- вызов и вывод команд `ip r` на `ws22`

## Пропингуй с ws11 роутер r2 и покажи на r2, что пинг доходит. Для этого используй команду: tcpdump -tn -i eth0

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_tcpdump.png?ref_type=heads)
- вызов и вывод команд `tcpdump -tn -i enp0s8` на `r2`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_ping_r2.png?ref_type=heads)
- вызов и вывод команд `ping 10.100.0.12` на `ws11`

## 5.4. Добавление статических маршрутов

## Добавь в роутеры r1 и r2 статические маршруты в файле конфигураций. Пример для r1 маршрута в сетку 10.20.0.0/26:

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_yaml.png?ref_type=heads)
- вид файла конфигурации `etc/netplan/00-installer-config.yaml` на `r2`

## Вызови ip r и покажи таблицы с маршрутами на обоих роутерах. 

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_ip_r.png?ref_type=heads)
- вызов и вывод команд `ip r` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_ip_r.png?ref_type=heads)
- вызов и вывод команд `ip r` на `r2`

## Запусти команды на ws11: ip r list 10.10.0.0/[маска сети] и ip r list 0.0.0.0/0

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_ip_r_list.png?ref_type=heads)
- вызов и вывод команд `ip r list 10.10.0.0/18` и `ip r list 0.0.0.0/0` на `ws11`

- он попал под маршрут, отличный от `0.0.0.0/0`, потому что к хостам, находящимся в его сети, он может ходить напрямую, без необходимости задействования шлюза. А вот при обращении за пределы своей сети, уже необходим шлюз, который знает, куда перенаправлять пакеты.

## 5.5. Построение списка маршрутизаторов

## При помощи утилиты traceroute построй список маршрутизаторов на пути от ws11 до ws21.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_traceroute_ws21.png?ref_type=heads)
- вызов и вывод команд `traceroute 10.20.0.10` на `ws11`

## Запусти на r1 команду дампа

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_tcpdump_tnv.png?ref_type=heads)
![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_full_output_tcpdump_1.png?ref_type=heads)
![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_full_output_tcpdump_2.png?ref_type=heads)
![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_full_output_tcpdump_3.png?ref_type=heads)
- вызов и вывод команд `tcpdump -tnv -i enp0s3` на `r1`

- `traceroute` использует значение `TTL` так: первым действием он отправляет пакет с `TTL = 1`, хост, принимающий этот пакет обязан уменьшить значение `TTL` на один и, если получился ноль, то жизнь пакета закончилась, хост убивает этот пакет и отдает `ICMP` ответ отправителю, что `time excedeed`. Соответственно, `traceroute`, получая такой ответ не от того, кто являлся конечным получателем, фиксирует, что это маршрутизатор на пути, записывает его и отправляет новые пакеты с увеличенным на один `TTL`. Дальше происходит того же самое, пока не дойдет до хоста назначения. А уж хост назначение отвечает нам `port unreacheble`, потому что `traceroute` намеренно отправляет пакеты на несуществующие и не занятые порты. Получая такой ответ, он фиксирует, что хост активен и отвечает.

## 5.6. Использование протокола ICMP при маршрутизации

## Запусти на r1 перехват сетевого трафика, проходящего через eth0 с помощью команды: tcpdump -n -i eth0 icmp 

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_tcpdump_n.png?ref_type=heads)
- вызов и вывод команд `tcpdump -n -i enp0s3 icmp` на `r1`

## Пропингуй с ws11 несуществующий IP (например, 10.30.0.111) с помощью команды: ping -c 1 10.30.0.111

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_ping_c.png?ref_type=heads)
- вызов и вывод команд `ping -c 1 10.30.0.111` на `ws11`

# Part 6. Динамическая настройка IP с помощью DHCP

## Для r2 настрой в файле /etc/dhcp/dhcpd.conf конфигурацию службы DHCP:

## 1) Укажи адрес маршрутизатора по умолчанию, DNS-сервер и адрес внутренней сети

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_dhcpd_conf.png?ref_type=heads)
- вид файла `/etc/dhcp/dhcpd.conf` на `r2`

## 2) В файле resolv.conf пропиши nameserver 8.8.8.8.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_resolve_conf.png?ref_type=heads)
- вид файла `/etc/resolv.conf` на `r2`

## Перезагрузи службу DHCP командой systemctl restart isc-dhcp-server. Машину ws21 перезагрузи при помощи reboot и через ip a покажи, что она получила адрес. Также пропингуй ws22 с ws21.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_restart_isc-dhcp-server.png?ref_type=heads)
- вызов и вывод команды `systemctl restart isc-dhcp-server` на `r2`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_ipa_dhcp.png?ref_type=heads)
- вызов и вывод команд `ip a` на `ws21`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_ping_ws22_.png?ref_type=heads)
- пинг `ws22` с `ws21`

## Укажи MAC-адрес у ws11, для этого в etc/netplan/00-installer-config.yaml надо добавить строки: macaddress: 10:10:10:10:10:BA, dhcp4: true.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_dhcp_yaml.png?ref_type=heads)
- содержимое `/etc/netplan/00-installer-config.yaml` на `ws11`

## Для r1 настрой аналогично r2, но сделай выдачу адресов с жесткой привязкой к MAC-адресу (ws11). Проведи аналогичные тесты.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_dhcpd_conf.png?ref_type=heads)
- вид файла `/etc/dhcp/dhcpd.conf` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_resolv_conf.png?ref_type=heads)
- вид файла `/etc/resolv.conf` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_restart_isc-dhcp-server.png?ref_type=heads)
- вызов и вывод команды `systemctl restart isc-dhcp-server` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_ipa_dhcp.png?ref_type=heads)
- вызов и вывод команд `ip a` на `ws11`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_ping_ws22_.png?ref_type=heads)
- пинг `ws22` с `ws11`

## Запроси с ws21 обновление IP-адреса.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_ipa_last.png?ref_type=heads) 
- вызов и вывод команды `ip a` на `ws21` до смены `ip`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_dhclient_ipa.png?ref_type=heads) 
- вызов и вывод команд `dhclient -r && dhclient` и `ip a` на `ws21`

- командой `dhclient -r && dhclient` мы отправляем `DHCPRELEASE`, который говорит роутеру о том, что на данный адрес аренда больше не нужна. Командой `dhclient` мы отправляем сначала `DHCPDISCOVER` на широковещательный адрес, соответственно пакет доходит до роутера, тот его подхватывает и отправляет нам `DHCPOFFER`, в котором он предлагает взять такой-то `ip`, на что мы отвечаем `DHCPREQUEST`, соглашаясь с арендой данного адреса, потом роутер высылает `DHCPACK`, выдавая наш `lease`.

# Part 7

## В файле /etc/apache2/ports.conf на ws22 и r1 измени строку Listen 80 на Listen 0.0.0.0:80, то есть сделай сервер Apache2 общедоступным.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws22_apache2_portsconf.png?ref_type=heads) 
- вид файла `/etc/apache2/ports.conf` на `ws22`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_apache2_portconf.png?ref_type=heads) 
- вид файла `/etc/apache2/ports.conf` на `r1`

## Запусти веб-сервер Apache командой service apache2 start на ws22 и r1.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws22_apache2_start.png?ref_type=heads) 
- вызов и вывод команды `service apache2 start` на `ws22`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_apache2_start.png?ref_type=heads) 
- вызов и вывод команды `service apache2 start` на `r1`

## Проверь соединение между ws22 и r1 командой ping.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_ping_ws22.png?ref_type=heads) 
- вызов и вывод команды `ping 10.20.0.20` на `r1`

## Проверь соединение между ws22 и r1 командой ping.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_ping_ws22_2.png?ref_type=heads) 
- вызов и вывод команды `ping 10.20.0.20` на `r1`

## Добавь в фаервол, созданный по аналогии с фаерволом из Части 4, на r2 следующие правила:
## 1) Удаление правил в таблице filter — iptables -F;
## 2) Удаление правил в таблице «NAT» — iptables -F -t nat;
## 3) Отбрасывать все маршрутизируемые пакеты — iptables --policy FORWARD DROP.
## Запусти файл также, как в Части 4.
## Проверь соединение между ws22 и r1 командой ping.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_ping_ws22.png?ref_type=heads) 
- вызов и вывод команды `ping 10.20.0.20` на `r1`

## Добавь в файл ещё одно правило:
## 4) Разрешить маршрутизацию всех пакетов протокола ICMP.
## Запусти файл также, как в Части 4.
## Проверь соединение между ws22 и r1 командой ping.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_ping_ws22_2.png?ref_type=heads) 
- вызов и вывод команды `ping 10.20.0.20` на `r1`

## Добавь в файл ещё два правила:
## 5) Включи SNAT, а именно маскирование всех локальных IPиз локальной сети, находящейся за r2 (по обозначениям из Части 5 — сеть 10.20.0.0).
## 6) Включи DNAT на 8080 порт машины r2 и добавить к веб-серверу Apache, запущенному на ws22, доступ извне сети.

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r2_firewallsh_task7.png?ref_type=heads) 
- вид файла `/etc/firewall.sh`

## Проверь соединение по TCP для SNAT: для этого с ws22 подключиться к серверу Apache на r1 

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws22_telnet_r1.png?ref_type=heads) 
- вызов и вывод команды `telnet 10.100.0.11 80` на `ws22`

## Проверь соединение по TCP для DNAT: для этого с r1 подключиться к серверу Apache на ws22 командой telnet (обращаться по адресу r2 и порту 8080).

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/r1_telnet_ws22.png?ref_type=heads) 
- вызов и вывод команды `telnet 10.100.0.12 8080` на `r1`

# Part 8. Дополнительно. Знакомство с SSH Tunnels

## Запусти на r2 фаервол с правилами из Части 7.

- `chmod +x /etc/firewall.sh`
- `sudo /etc/firewall.sh`

## Запусти веб-сервер Apache на ws22 только на localhost (то есть в файле /etc/apache2/ports.conf измени строку Listen 80 на Listen localhost:80).

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws22_ports_conf_local.png?ref_type=heads) 
- содержание файла `/etc/apache2/ports.conf` на `ws22`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws22_apache2_start_local.png?ref_type=heads) 
- вызов и вывод команды `service apache2 start` на `ws22`

## Воспользуйся Local TCP forwarding с ws21 до ws22, чтобы получить доступ к веб-серверу на ws22 с ws21.

- `sudo apt update` и `sudo apt install openssh-server` на `ws22`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_local_forwarding_ws22.png?ref_type=heads) 
- вызов и вывод команды `ssh -L 9999:localhost:80 aemonhul@10.20.0.20` на `ws21`

## Для проверки, сработало ли подключение в обоих предыдущих пунктах, перейди во второй терминал

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws21_telnet_tty2.png?ref_type=heads) 
- вызов и вывод команды `telnet 127.0.0.1 9999` на `ws21`

## Воспользуйся Remote TCP forwarding c ws11 до ws22, чтобы получить доступ к веб-серверу на ws22 с ws11.

- `sudo apt update` и `sudo apt install openssh-server` на `ws11`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws22_remote_forwarding_ws11.png?ref_type=heads) 
- вызов и вывод команды `ssh -R 9999:localhost:80 aemonhul@10.10.0.2` на `ws22`

## Для проверки, сработало ли подключение в обоих предыдущих пунктах, перейди во второй терминал

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/image_for_md/ws11_telnet_ws22_remotefor.png?ref_type=heads) 
- вызов и вывод команды `telnet 127.0.0.1 9999` на `ws11`










