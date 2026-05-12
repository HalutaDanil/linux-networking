# Part 2 — Static Routing

## VM Setup

- Raised two VMs (ws1 and ws2) in VirtualBox with Ubuntu 20.04 LTS

## Network Interfaces

![ws1 ip a](image_for_md/vm1_ipa.png)
- `ip a` output on ws1

![ws2 ip a](image_for_md/vm2_ipa.png)
- `ip a` output on ws2

## Netplan Configuration

![ws1 netplan](image_for_md/vm1_netplan_yaml_1.png)
- `etc/netplan/00-installer-config.yaml` on ws1

![ws2 netplan](image_for_md/vm2_netplan_yaml_1.png)
- `etc/netplan/00-installer-config.yaml` on ws2

## Applying Config

![ws1 apply](image_for_md/vm1_netplan_apply.png)
- `netplan apply` on ws1

![ws2 apply](image_for_md/vm2_netplan_apply.png)
- `netplan apply` on ws2

## 2.1 Static Route (Manual)

![ws1 route](image_for_md/vm1_ipr_add.png)
- `ip r add` on ws1

![ws2 route](image_for_md/vm2_ipr_add.png)
- `ip r add` on ws2

## Connectivity Test

![ws1 ping](image_for_md/vm1_ping_1.png)
- Ping ws2 from ws1

![ws2 ping](image_for_md/vm2_ping_1.png)
- Ping ws1 from ws2

## 2.2 Persistent Static Route

- Configured routes in `/etc/netplan/00-installer-config.yaml`
- Verified after reboot
