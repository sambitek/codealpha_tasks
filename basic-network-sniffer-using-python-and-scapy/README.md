# Basic Network Sniffer Using Python and Scapy

## Overview

This project demonstrates the development of a basic network packet sniffer using Python and the Scapy library. The program captures live network traffic and displays useful information such as source and destination IP addresses, protocols, and packet payloads.

The project provides practical experience in packet analysis, network monitoring, and understanding how data flows through computer networks.

---

## Objectives

* Capture network traffic packets in real time
* Analyze packet structure and content
* Understand network communication and protocols
* Display source and destination IP addresses
* Identify common protocols such as TCP and UDP
* Extract packet payload information when available

---

## Tools and Technologies

* Python 3
* Scapy
* Kali Linux
* Terminal

---

## Installation

### Update System

```bash
sudo apt update
```

### Install Python and Pip

```bash
sudo apt install python3 python3-pip -y
```

### Install Scapy

```bash
pip3 install scapy
```

---

## Project Structure

```text
Basic-Network-Sniffer/
│
├── packet_sniffer.py
├── screenshots/
├── README.md
└── report.pdf
```

---

## Python Code

```python
from scapy.all import sniff, IP, TCP, UDP, Raw

def process_packet(packet):
    if packet.haslayer(IP):
        ip_src = packet[IP].src
        ip_dst = packet[IP].dst
        protocol = packet[IP].proto

        print("\n-----------------------------")
        print(f"Source IP: {ip_src}")
        print(f"Destination IP: {ip_dst}")
        print(f"Protocol: {protocol}")

        if packet.haslayer(TCP):
            print("Protocol Type: TCP")
        elif packet.haslayer(UDP):
            print("Protocol Type: UDP")

        if packet.haslayer(Raw):
            payload = packet[Raw].load
            print(f"Payload: {payload}")

def start_sniffing():
    print("Starting packet capture...\n")
    sniff(prn=process_packet, store=False)

start_sniffing()
```

---

## Running the Program

Execute the script with administrative privileges:

```bash
sudo python3 packet_sniffer.py
```

The program will begin capturing and displaying live network packets.

---

## Generating Test Traffic

You can generate traffic using:

### Ping

```bash
ping google.com
```

### Nmap Scan

```bash
nmap -A 192.168.56.1
```

### Web Browsing

Open websites in your browser while the packet sniffer is running.

---

## Sample Output

```text
-----------------------------
Source IP: 10.0.2.15
Destination IP: 192.168.56.1
Protocol: 6
Protocol Type: TCP

-----------------------------
Source IP: 8.8.8.8
Destination IP: 10.0.2.15
Protocol: 17
Protocol Type: UDP
```

---

## Key Concepts Learned

* Packet sniffing
* Network traffic monitoring
* TCP/IP communication
* Protocol analysis
* Packet payload inspection
* Network security fundamentals

---

## Findings

* Successfully captured live network traffic
* Identified source and destination IP addresses
* Detected TCP and UDP protocols
* Observed payload data within packets
* Gained practical understanding of network communication

---

## Conclusion

This project successfully implemented a basic network packet sniffer using Python and Scapy. The tool captured and analyzed network packets in real time, providing valuable insight into packet structure, network protocols, and data transmission. The project serves as a foundation for advanced packet analysis, network monitoring, and intrusion detection systems.

---

## Author

**Ubong Solomon**

Cybersecurity and Network Security Enthusiast
