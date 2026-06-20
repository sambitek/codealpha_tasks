INTRUSION DETECTION SYSTEM DEPLOYMENT AND PACKET ANALYSIS USING SURICATA

---

 INTRODUCTION

With the increasing sophistication of cyber threats, organizations require effective mechanisms to monitor and detect malicious network activities. Intrusion Detection Systems (IDS) such as Suricata play a critical role in identifying suspicious traffic and generating alerts for analysis.

This project demonstrates the deployment of Suricata IDS in a controlled lab environment, simulation of network attacks, and analysis of captured traffic using Wireshark. The objective is to understand how IDS detects malicious behavior and how packet-level analysis supports security investigations.

---

 AIM AND OBJECTIVES

 AIM

To deploy and configure an Intrusion Detection System and analyze malicious network activities.

OBJECTIVES

* Configure Suricata IDS in a Linux environment
* Simulate reconnaissance and application-layer attacks
* Detect malicious traffic using IDS rules
* Capture and analyze packets using Wireshark
* Correlate IDS alerts with real network traffic

---

 LAB SETUP AND ENVIRONMENT

The lab environment consists of:

* Kali Linux (attacker + IDS + analysis system)
* Metasploitable2 (target system)
* Virtual network configured using NAT (192.168.100.0/24 subnet)

This setup enables controlled communication between attacker and target systems.

📌 Figure 1: Network configuration / IP setup

---

 SURICATA IDS DEPLOYMENT

Suricata was installed and configured on Kali Linux. The configuration file was modified to define the local network range:

```
HOME_NET: "[192.168.100.0/24]"
```

Suricata was executed in IDS mode using:

```
sudo suricata -c /etc/suricata/suricata.yaml -i eth0
```

This enabled real-time monitoring of network traffic on the selected interface.

📌 Figure 2: Suricata running in terminal

---

 ATTACK SIMULATION AND DETECTION

 NMAP RECONNAISSANCE SCAN

A full port scan was performed using Nmap:

```
nmap -A -T4 -p- 192.168.100.3
```

Suricata detected scanning behavior and generated alerts indicating reconnaissance activity.

📌 Figure 3: Nmap scan execution
📌 Figure 4: Suricata alert for Nmap scan

---

SQL INJECTION SIMULATION

A SQL Injection attack was simulated on DVWA using:

```
' OR '1'='1' --
```

This demonstrates improper input validation and potential database exploitation in web applications.

DVWA was used for testing.

📌 Figure 5: SQL injection input
📌 Figure 6: Error/result page

---

 PACKET CAPTURE AND ANALYSIS (WIRESHARK)

Packet analysis was performed using Wireshark.

 Nmap Traffic Analysis

Filter used:

```
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

Multiple SYN packets confirmed port scanning activity.

📌 Figure 7: SYN packets in Wireshark

---

 SQL INJECTION TRAFFIC ANALYSIS

Filter used:

```
http
```

HTTP requests containing SQL payloads were captured, confirming malicious input transmission.

📌 Figure 8: HTTP packet showing SQL payload

---

 CORRELATION OF IDS ALERTS AND TRAFFIC

A key aspect of this project is correlating IDS alerts with actual network traffic:

* Suricata generated alerts for scanning and web attacks
* Wireshark confirmed packet-level evidence
* Source and destination IPs matched across tools
* Payload analysis validated malicious behavior

This demonstrates effective real-time intrusion detection.

---

 RESPONSE MECHANISM

To demonstrate basic intrusion response, firewall rules were applied:

```
sudo iptables -A INPUT -s 192.168.100.3 -j DROP
```

This blocks malicious traffic from the attacker system.

---

 FINDINGS

* Suricata effectively detected reconnaissance activities such as port scans
* Web-based attacks like SQL injection were identified
* Wireshark provided deep packet-level visibility
* IDS combined with packet analysis improves investigation accuracy
* Misconfigured or unvalidated inputs expose systems to exploitation

---

 VISUALIZATION OF DETECTED ATTACKS

Visualization improves interpretation of security events using dashboards and graphs.

In this project:

* Suricata logs were analyzed
* Wireshark captures were reviewed
* EveBox was used for alert visualization

📌 Figure 10: Wireshark / Suricata alerts
📌 Figure 11: EveBox dashboard

---

CONCLUSION

This project successfully demonstrated the deployment of an Intrusion Detection System using Suricata. Simulated attacks were detected in real time, and packet analysis validated the underlying network behavior. The combination of IDS monitoring, traffic inspection, and response mechanisms highlights the importance of layered cybersecurity defense in modern environments.
