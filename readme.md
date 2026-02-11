# 01_scan: Network Discovery & Infiltration

## 1. Project Concept
This project simulates a network penetration test. The objective is to navigate the network stack to discover a hidden server (`01_scan_RRF-CONTROL`) from a controlled workstation (`01_scan_laptop`). 

The scenario highlights that most network entities have high discoverability by design. By analyzing different layers of the Internet protocol suite, we can identify targets and their exposed services.

---

## 2. Infrastructure & Access
* **Entry Point:** Connected to the Laptop VM via SSH on port `10122`.
* **Credentials:** User `root`, password is a single space.
* **Network Constraint:** The virtualized network is capped at 10 Mbps, requiring optimized scanning techniques to manage long wait times.

---

## 3. Methodology & Networking Layers

The project follows a bottom-up exploration of the network stack:

### Phase 1: Link Layer Discovery (ARP)
We analyzed the Link Layer using the **ARP (Address Resolution Protocol)** to gather MAC addresses and identify active hosts on the local network segment (`enp0s8`).
* **Tool:** `arp-scan`
* **Result:** Discovered target host at IP **`192.168.23.42`**.

### Phase 2: Network & Transport Layer Analysis (IP/TCP)
Once the host was identified, we analyzed the Network (IP) and Transport (TCP) layers to find exposed services.
* **Tool:** `nmap`
* **Command:** `nmap -T4 -p- 192.168.23.42`.
* **Optimization:** Used `-T4` to speed up the scan on the slow 10 Mbps link.
* **Result:** Identified an open non-standard port: **`4223/tcp`**.

---

## 4. Final Infiltration
By combining the discovered IP and the hidden TCP port, the final connection was established to the application layer (SSH):

```bash
ssh root@192.168.23.42 -p 4223