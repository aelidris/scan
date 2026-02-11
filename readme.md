# 01_scan: Matrix-Style Network Infiltration

## 1. Project Objective
The goal was to simulate a network penetration scenario: identifying a hidden server (`01_scan_RRF-CONTROL`) on a slow (10 Mbps) local network and gaining access through exposed services.

## 2. Technical Methodology

### Phase 1: Local Discovery (Link Layer)
Operating from the `01_scan_laptop` VM, I utilized the **ARP (Address Resolution Protocol)** to identify active MAC addresses on the `enp0s8` interface.
* **Command**: `arp-scan --interface=enp0s8 --localnet`
* **Discovery**: Target host found at **192.168.23.42**.

### Phase 2: Service Enumeration (Transport Layer)
I performed a comprehensive **TCP port scan** to find an entry point. Due to the 10 Mbps bandwidth limit, I used the aggressive timing flag (`-T4`).
* **Command**: `nmap -T4 -p- 192.168.23.42`
* **Discovery**: Identified hidden SSH service on port **4223/tcp**.

### Phase 3: Final Infiltration (Application Layer)
Using the gathered data, I established a secure connection to the server.
* **Connection**: `ssh root@192.168.23.42 -p 4223`
* **Authentication**: Password (single space).

## 3. Results
The mission was successful upon reaching the target system prompt:
**`RRF-CONTROL> █`**

## 4. Key Takeaways
* **Network Visibility**: Most entities have high discoverability via ARP regardless of firewall settings.
* **Security through Obscurity**: Moving SSH from port 22 to 4223 does not stop a dedicated scan, but it prevents automated bot discovery.
* **Bandwidth Constraints**: Slow networks require optimized tools (like Nmap's timing templates) to be effective.