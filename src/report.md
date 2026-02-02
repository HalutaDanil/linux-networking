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

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/ws11_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `ws11`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/ws21_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `ws21`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/ws22_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `ws22`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/r1_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/r2_apply_ipa.png?ref_type=heads)
- вызов и вывод команд `netplan apply` и `ip -4 a` на `r2`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/ws11_ping_r1.png?ref_type=heads)
- пинг `r1` с `ws11`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/ws21_ping_ws22.png?ref_type=heads)
- пинг `ws22` с `ws21`

## 5.2. Включение переадресации IP-адресов

## Для включения переадресации IP выполни команду на роутерах:

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/r1_sysctl_w.png?ref_type=heads)
- вызов и вывод команд `sysctl -w net.ipv4.forward=1` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/r2_sysctl_w.png?ref_type=heads)
- вызов и вывод команд `sysctl -w net.ipv4.forward=1` на `r2`

## Открой файл /etc/sysctl.conf и добавь в него следующую строку: net.ipv4.ip_forward = 1

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/r1_sysctl_conf.png?ref_type=heads)
- вид файла конфигурации `etc/sysctl.conf` на `r1`

![](https://git.21-school.ru/students_repo/aemonhul/DO2_LinuxNetwork.ID_356275-1/raw/develop/src/r2_sysctl_conf.png?ref_type=heads)
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














