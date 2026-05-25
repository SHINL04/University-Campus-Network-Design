# Phase 4: Verification and Troubleshooting Protocol

This engineering journal outlines the step-by-step verification process to ensure the campus network behaves according to design specifications.

## 1. Layer 2 Interface Verification
Run these commands on `ACAD-ACC-SW01` to verify VLAN boundaries:
* `show vlan brief` 
  * *Expected Result:* Ports 1-10 must show active in `VLAN_STUDENTS`, Ports 11-15 active in `VLAN_FACULTY`.
* `show interfaces trunk`
  * *Expected Result:* `Gi0/1` and `Gi0/2` must show tracking status as `trunking` using `802.1Q` encapsulation.

## 2. Layer 3 Routing & ACL Verification
Run these execution tests from end-user endpoints:

### Test Case 1: Student to Internet Gateway
* **Action:** Ping from Student PC (`192.168.10.15`) to Student SVI Gateway (`192.168.10.1`).
* **Expected Status:** SUCCESS. Proves Layer 2 switching and Access-to-Core uplink connectivity are operational.

### Test Case 2: Inter-VLAN Routing (Student to Faculty)
* **Action:** Ping from Student PC (`192.168.10.15`) to Faculty PC (`192.168.10.135`).
* **Expected Status:** SUCCESS. Proves global `ip routing` engine is active on the Core Switch.

### Test Case 3: Security Boundary Enforcement (Student to Admin)
* **Action:** Attempt to SSH or Ping from Student PC (`192.168.10.15`) to Admin Finance PC (`192.168.10.200`).
* **Expected Status:** **DENIED / TIMEOUT**. 
* **Reasoning:** The Extended ACL `SECURE_ADMIN_ZONE` applied *outbound* on SVI `Vlan 30` successfully matches the student source packet and drops it.