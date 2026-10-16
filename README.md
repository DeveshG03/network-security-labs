# Cybersecurity Lab Portfolio

Hands-on cybersecurity exercises performed in a controlled VirtualBox environment. The labs focus on authorized discovery, traffic inspection, and clear defensive documentation.

## Projects

### 1. Network Reconnaissance Lab

Used Kali Linux and Nmap to identify open TCP ports and service banners on an intentionally vulnerable Metasploitable 2 virtual machine connected through a host-only lab network. Recorded observations and practical defensive recommendations.

- [Project guide and findings](projects/network-reconnaissance/README.md)

### 2. Network Traffic Analysis Lab

Captured and inspected ARP, ICMP, and HTTP traffic between Kali and Metasploitable 2 using Wireshark. Reviewed packet direction, protocol fields, and an HTTP request/response in the isolated lab.

- [Project guide and observations](projects/network-traffic-analysis/README.md)

## Lab boundaries

- Work was limited to virtual machines owned and controlled by the learner.
- Metasploitable 2 was kept on a host-only VirtualBox network.
- No third-party systems or production networks were scanned or captured.
- Findings describe the lab target and are not claims about a real organization.

## Evidence and reproducibility

The raw Nmap text output and Wireshark PCAPNG capture were saved inside the Kali VM. They are not included here because they were not transferred into this portfolio folder. The project pages summarize the observed results and provide the commands used.