<div align="center">

# Linux Networking

**[English](#english) | [Русский](#русский)**

</div>

---

<a name="english"></a>
## 🇬🇧 English

A hands-on project configuring a multi-machine network topology in VirtualBox. The goal was to understand how data moves between machines and how to control that flow with routing, NAT, firewalls, and tunnels.

### What was done

| Topic | What & Why |
|-------|-----------|
| IP Addressing | Calculated network addresses, masks, and host ranges manually and with `ipcalc`. Set static IPs via `netplan`. |
| Static Routing | Connected two machines directly with static routes using `ip r add` and persistent config in `netplan`. |
| iperf3 | Measured bandwidth between machines. Learned to distinguish Mbps, MB/s, Gbps. |
| Firewall (iptables) | Wrote `firewall.sh` scripts with allow/deny strategies. Opened ports 22 and 80, blocked ICMP echo replies, and probed with `nmap`. |
| Multi-machine Topology | Built a network of 5 VMs (3 workstations + 2 routers). Configured IPs, routes, and verified connectivity with `ping` and `tcpdump`. |
| IP Forwarding | Enabled packet forwarding on routers via `sysctl` to let traffic pass between subnets. |
| DHCP | Configured `isc-dhcp-server` on routers for dynamic address assignment. Tested lease renewal with `dhclient`. |
| NAT | Implemented SNAT (masquerading) and DNAT (port forwarding) with `iptables`. Accessed an Apache server behind a router. |
| SSH Tunnels | Set up local and remote TCP forwarding to access a web server on a machine behind a firewall without exposing it directly. |

### Key takeaways
- A network is not magic — it is **IP addresses, routing tables, and firewall rules** working together.
- **NAT and SSH tunnels** are practical tools for accessing private networks safely.
- `tcpdump` and `traceroute` are essential for debugging connectivity issues.

### Tech Stack

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![Networking](https://img.shields.io/badge/Networking-009639?style=flat-square) ![iptables](https://img.shields.io/badge/iptables-FF6D5A?style=flat-square) ![Apache](https://img.shields.io/badge/Apache-D22128?style=flat-square&logo=apache&logoColor=white)

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=rect&color=0:58a6ff,50:1f6feb,100:0969da&height=2&section=header&text=&fontSize=1"/>
</div>

<a name="русский"></a>
## 🇷🇺 Русский

Практический проект по настройке сетевой топологии из нескольких виртуальных машин в VirtualBox. Цель — понять, как данные перемещаются между машинами и как управлять этим потоком через маршрутизацию, NAT, файрвол и туннели.

### Что было сделано

| Тема | Что и зачем |
|------|-------------|
| IP-адресация | Расчёт сетевых адресов, масок и диапазонов хостов вручную и через `ipcalc`. Настройка статических IP через `netplan`. |
| Статическая маршрутизация | Прямое соединение двух машин статическими маршрутами через `ip r add` и постоянную конфигурацию в `netplan`. |
| iperf3 | Измерение пропускной способности между машинами. Изучена разница между Mbps, MB/s, Gbps. |
| Файрвол (iptables) | Написаны скрипты `firewall.sh` со стратегиями allow/deny. Открыты порты 22 и 80, заблокированы ICMP echo reply, сканирование через `nmap`. |
| Много-машинная топология | Построена сеть из 5 ВМ (3 рабочие станции + 2 роутера). Настроены IP, маршруты, проверка связности через `ping` и `tcpdump`. |
| IP Forwarding | Включен форвардинг пакетов на роутерах через `sysctl` для прохождения трафика между подсетями. |
| DHCP | Настроен `isc-dhcp-server` на роутерах для динамической выдачи адресов. Протестировано обновление аренды через `dhclient`. |
| NAT | Реализованы SNAT (маскарадинг) и DNAT (проброс портов) через `iptables`. Доступ к Apache-серверу за роутером. |
| SSH-туннели | Настроены local и remote TCP forwarding для доступа к веб-серверу на машине за файрволом без прямого открытия порта. |

### Ключевые выводы
- Сеть — это не магия, а **IP-адреса, таблицы маршрутизации и правила файрвола**, работающие совместно.
- **NAT и SSH-туннели** — практичные инструменты для безопасного доступа к приватным сетям.
- `tcpdump` и `traceroute` незаменимы для отладки проблем со связностью.

### Стек технологий

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![Networking](https://img.shields.io/badge/Networking-009639?style=flat-square) ![iptables](https://img.shields.io/badge/iptables-FF6D5A?style=flat-square) ![Apache](https://img.shields.io/badge/Apache-D22128?style=flat-square&logo=apache&logoColor=white)

---

<div align="center">

*Project from portfolio | Проект из портфолио*

</div>
