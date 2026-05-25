# Phase 3: Layer 3 Routing Design (SVIs)

## Core/Distribution Switch Logic
To enable communication between authorized zones, the Core/Distribution switches will run Layer 3 routing operations. Each user segment will target a localized Switch Virtual Interface (SVI) as its gateway.

## SVI Allocation Blueprint
* **Interface Vlan 10 (Students Gateway):** IP Address `192.168.10.1` /25
* **Interface Vlan 20 (Faculty Gateway):** IP Address `192.168.10.129` /26
* **Interface Vlan 30 (Admin Gateway):** IP Address `192.168.10.193` /27
* **Interface Vlan 40 (IoT Gateway):** IP Address `192.168.10.224` /27
## Interface & Port Connectivity Matrix

### Access Switches (Per Floor / Block)
* **Ports 1 - 10:** Configured as **Access Ports** assigned explicitly to `VLAN_STUDENTS` (VLAN 10).
* **Ports 11 - 15:** Configured as **Access Ports** assigned explicitly to `VLAN_FACULTY` (VLAN 20).
* **Ports 16 - 20:** Configured as **Access Ports** assigned explicitly to `VLAN_ADMIN` (VLAN 30).
* **Ports 21 - 22:** Configured as **Access Ports** assigned explicitly to `VLAN_IOT` (VLAN 40).
* **Ports 23 - 24:** Configured as **Trunk Ports** (802.1Q) uplinked directly to Core/Distribution switches.

### Core/Distribution Switches
* **Downlink Ports:** Configured as **Trunk Ports** running 802.1Q encapsulation to aggregate traffic from the Access layer switches.