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

| Component | Technologies |\n|-----------|-------------|\n| IP Addressing | Static IP via netplan |\n| DHCP | isc-dhcp-server |\n| NAT | iptables + sysctl ip_forward |\n| Firewall | Bash scripts for rule management |\n| Web Server | Apache2 on ws22 |\n| Tunneling | SSH local/remote forwarding |\n| Traffic Analysis | tcpdump, telnet, iperf3 |

### 🚀 Quick Start

```bash\n# Check routing\nip route\n\n# Test connectivity\nping 1.1.1.1\n\n# Firewall rules\nsudo ./firewall.sh\n```

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

| Компонент | Технологии |\n|-----------|-----------|\n| IP-адресация | Статический IP через netplan |\n| DHCP | isc-dhcp-server |\n| NAT | iptables + sysctl ip_forward |\n| Файрвол | Bash-скрипты управления правилами |\n| Веб-сервер | Apache2 на ws22 |\n| Туннелирование | SSH local/remote forwarding |\n| Анализ трафика | tcpdump, telnet, iperf3 |

### 🚀 Быстрый старт

```bash\n# Проверка маршрутизации\nip route\n\n# Тест соединения\nping 1.1.1.1\n\n# Правила файрвола\nsudo ./firewall.sh\n```

---

<div align="center">

*Project from portfolio | Проект из портфолио*

</div>
