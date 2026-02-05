# 01_scan: Network Discovery & Penetration

## 1. Objective
Identify the hidden `01_scan_RRF-CONTROL` server on a local virtual network and establish a connection by scanning for exposed services.

## 2. Methodology
The exploration follows a bottom-up approach through the network layers:

### Layer 1: Data Link (ARP)
We analyze **ARP (Address Resolution Protocol)** to map MAC addresses to IP addresses within the local network segment. 
- **Tool:** `arp-scan`

### Layer 2: Transport (TCP)
We use **TCP (Transmission Control Protocol)** to identify open ports and services on the discovered host.
- **Tool:** `nmap`

## 3. Execution
1. **Connect:** SSH into the laptop VM at port `10122`.
2. **Scan:** Perform an ARP scan on `enp0s8` to locate the server IP.
3. **Probe:** Use `nmap -T4` to find open ports on the target.
4. **Access:** Connect to the discovered port to reach the `RRF-CONTROL>` prompt.

## 4. Constraints
- **Network Speed:** 10 Mbps (Expect significant delays during scans).
- **Scope:** Focus is strictly on IP, ARP, and TCP protocols.