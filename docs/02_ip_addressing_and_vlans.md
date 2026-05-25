# Phase 2: VLAN Design Matrix

## Logical Segmentation Plan
To maintain strict security boundaries across the campus, the following VLAN allocation strategy is implemented:

| VLAN ID | VLAN Name | Target Audience | Policy Restrictions |
|---|---|---|---|
| 10 | VLAN_STUDENTS | Student Devices / Labs | Internet Access Only. Blocked from Admin/IoT. |
| 20 | VLAN_FACULTY | Faculty / Staff | Access to Internet and internal local portals. |
| 30 | VLAN_ADMIN | Finance / Accounts / HR | Strictly isolated. No access from Student VLAN. |
| 40 | VLAN_IOT | Security Cameras / Smart Boards | No outbound internet access. Local recording only. |
| 99 | VLAN_MGMT | Network Administration | Restricted to IT personnel infrastructure management. |
## IP Addressing Scheme (VLSM)
The master network block `192.168.10.0/24` has been optimized using Variable Length Subnet Masking (VLSM) to prevent allocation waste:

| VLAN | Network Name | CIDR Prefix | Network Address | Usable Range | Gateway IP |
|---|---|---|---|---|---|
| 10 | VLAN_STUDENTS | /25 | 192.168.10.0 | 192.168.10.1 - 192.168.10.126 | 192.168.10.1 |
| 20 | VLAN_FACULTY | /26 | 192.168.10.128 | 192.168.10.129 - 192.168.10.190 | 192.168.10.129 |
| 30 | VLAN_ADMIN | /27 | 192.168.10.192 | 192.168.10.193 - 192.168.10.222 | 192.168.10.193 |
| 40 | VLAN_IOT | /27 | 192.168.10.224 | 192.168.10.225 - 192.168.10.254 | 192.168.10.225 |