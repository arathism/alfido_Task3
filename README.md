# Wireshark Packet Analysis Report

### Task 3 – Network Packet Capture & Protocol Analysis
**Author:** Arathi Shekhar Munavalli
**Internship:** Alfido Tech
**Date:** 05 April 2026

---

## Overview

As part of this task, live network traffic was captured and analyzed 
using Wireshark on a Windows 11 machine. The goal was to identify 
protocols, analyze packet structure and flags, and detect any 
unusual or suspicious traffic.

- **Interface:** Wi-Fi (192.168.31.139)
- **Total Packets Captured:** 9,815
- **Capture Duration:** ~86 seconds
- **Tool:** Wireshark 4.6.4 + Npcap 1.86

---

## Tools Utilized

- **Wireshark** – for live packet capture and protocol analysis
- **Npcap 1.86** – packet capture driver for Windows

---

## Approach Followed

The task was completed in three stages:

1. **Packet Capture**
   Live traffic captured on Wi-Fi interface for ~86 seconds
   while browsing HTTP and HTTPS websites.

2. **Protocol Filtering**
   Each protocol was filtered and analyzed separately using
   Wireshark display filters.

3. **Anomaly Detection**
   Suspicious and unusual packets were identified using
   tcp.analysis.flags filter.

---

## Filters Applied & Results

| Filter | Protocol | Packets | Purpose |
|--------|----------|---------|---------|
| `dns` | DNS | 290 | Domain name queries |
| `tcp.flags.syn==1 && tcp.flags.ack==0` | TCP SYN | 56 | Handshake initiation |
| `tls` | TLS 1.2/1.3 | 781 | Encrypted HTTPS traffic |
| `arp` | ARP | 6 | Gateway MAC discovery |
| `tcp.analysis.flags` | TCP Anomalies | 135 | Retransmissions, errors |

---

## Key Findings

### Protocols Identified
- **DNS** – Queries to google.com, example.com, googleapis.com
- **TCP** – Normal 3-way handshakes to port 443 and 80
- **TLS 1.2/1.3** – Encrypted HTTPS web traffic
- **ARP** – Normal gateway MAC address discovery
- **QUIC** – Google/YouTube modern protocol traffic

### Anomalies Detected
- TCP Retransmissions (minor packet loss)
- TCP ZeroWindow (temporary buffer full)
- TCP Out-of-Order (normal Wi-Fi reordering)
- TCP Dup ACK (retransmission recovery)

---

## Risk Evaluation

- **High Risk:** None detected
- **Medium Risk:** None detected
- **Low Risk:** TCP Retransmissions, ZeroWindow, Out-of-Order
- **Info:** ARP Broadcasts, TLS Encrypted Alert, QUIC Protocol

---

## Recommendations

- Monitor DNS queries regularly to detect tunneling or exfiltration
- Investigate TCP retransmissions for network instability
- Enable HTTPS inspection for encrypted traffic monitoring
- Set up ZeroWindow alerts in Wireshark/IDS
- Periodically analyze ARP traffic to detect poisoning attempts

---

## Files in this Repository

| File | Description |
|------|-------------|
| `Task3_Wireshark_Analysis_Report.pdf` | Full packet analysis report with screenshots |
| `task3_capture.pcapng` | Raw Wireshark capture file |
| `DNS Traffic.png` | DNS filter screenshot |
| `TCP SYN Handshake.png` | TCP SYN filter screenshot |
| `TLS Encrypted Traffic.png` | TLS filter screenshot |
| `ARP Packets.png` | ARP filter screenshot |
| `Suspicious Packets.png` | tcp.analysis.flags screenshot |

---

## Conclusion

The network traffic analysis revealed normal everyday web browsing 
activity with no signs of malicious traffic, port scanning, DNS 
tunneling, or ARP poisoning. Minor TCP anomalies detected are 
consistent with normal Wi-Fi network behavior.

Regular packet analysis is an essential skill for network 
monitoring and early threat detection in real environments.

---

## Disclaimer

All packet captures were performed on the analyst's own network 
interface for learning purposes only, as part of the 
Alfido Tech Cybersecurity Internship program.
