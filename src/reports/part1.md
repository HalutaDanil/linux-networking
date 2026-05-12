# Part 1 — IP Calculation & Subnetting

## VM Setup

- Raised virtual machine in VirtualBox with Ubuntu 20.04 LTS

## 1.1 Networks and Masks

- 1) Network address 192.167.38.54/13 — `192.160.0.0`
- 2) Mask 255.255.255.0 to prefix and binary — `/24` and `11111111.11111111.11111111.00000000`
- 3) Min and max host in network 12.167.38.4 with masks: /8 — `12.0.0.1` and `12.255.255.254`

## 1.2 localhost

- 194.34.23.100 — `no`, 127.0.0.2 — `yes`, 127.1.0.1 — `yes`, 128.0.0.1 — `no`

## 1.3 IP Ranges and Segments

- Private IPs: 10.0.0.45, 192.168.4.2, 172.20.250.4, 172.16.255.255, 10.10.10.10
- Public IPs: 134.43.0.2, 172.0.2.1, 192.172.0.1, 172.68.0.2, 192.169.168.1
