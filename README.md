<div align="center">

# Linux Networking

**[English](#english) | [Русский](#русский)**

</div>

---

<a name="english"></a>
## 🇬🇧 English

Network infrastructure configuration across multiple virtual machines: routers and workstations. Full network topology with DHCP, NAT, firewall, and tunneling.

### 🛠️ Tech Stack

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![Networking](https://img.shields.io/badge/Networking-009639?style=flat-square) ![DHCP](https://img.shields.io/badge/DHCP-00A4EF?style=flat-square)

### ✨ Features

| Component | Technologies |
|-----------|-------------|
| IP Addressing | Static IP via netplan |
| DHCP | isc-dhcp-server |
| NAT | iptables + sysctl ip_forward |
| Firewall | Bash scripts for rule management |
| Web Server | Apache2 on ws22 |
| Tunneling | SSH local/remote forwarding |
| Traffic Analysis | tcpdump, telnet, iperf3 |

### 🚀 Quick Start

```bash
# Check routing
ip route

# Test connectivity
ping 1.1.1.1

# Firewall rules
sudo ./firewall.sh
```

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=rect&color=0:58a6ff,50:1f6feb,100:0969da&height=2&section=header&text=&fontSize=1"/>
</div>

<a name="русский"></a>
## 🇷🇺 Русский

Конфигурирование сетевой инфраструктуры на нескольких виртуальных машинах: роутеры и рабочие станции. Полноценная сетевая топология с DHCP, NAT, файрволом и туннелированием.

### 🛠️ Стек технологий

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![Networking](https://img.shields.io/badge/Networking-009639?style=flat-square) ![DHCP](https://img.shields.io/badge/DHCP-00A4EF?style=flat-square)

### ✨ Возможности

| Компонент | Технологии |
|-----------|-----------|
| IP-адресация | Статический IP через netplan |
| DHCP | isc-dhcp-server |
| NAT | iptables + sysctl ip_forward |
| Файрвол | Bash-скрипты управления правилами |
| Веб-сервер | Apache2 на ws22 |
| Туннелирование | SSH local/remote forwarding |
| Анализ трафика | tcpdump, telnet, iperf3 |

### 🚀 Быстрый старт

```bash
# Проверка маршрутизации
ip route

# Тест соединения
ping 1.1.1.1

# Правила файрвола
sudo ./firewall.sh
```

---

<div align="center">

*Project from portfolio | Проект из портфолио*

</div>
