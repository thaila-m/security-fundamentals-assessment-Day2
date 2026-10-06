# SWYNEX Network Security Analysis

## Overview

This project demonstrates defensive network traffic analysis performed in a controlled VMware laboratory environment using Kali Linux and Wireshark.

The objective was to capture and analyze network traffic, identify network protocols, examine communication patterns, and document security considerations.

## Environment

- Operating System: Kali Linux
- Virtualization: VMware
- Network Analysis Tool: Wireshark 4.6.6
- Network Interface: eth0
- Capture Format: PCAPNG

## Protocols Analyzed

- ARP
- DNS
- ICMP
- TCP
- TLS 1.3

## Key Findings

### DNS

DNS queries and responses for `example.com` were observed during the capture.

### ICMP

ICMP Echo Requests and Echo Replies demonstrated successful network connectivity between the local system and the remote destination.

### TCP

TCP traffic showed a connection to destination port 443, including the standard TCP three-way handshake.

### TLS 1.3

TLS 1.3 traffic included Client Hello, Server Hello, and encrypted Application Data.

## Security Considerations

The analysis demonstrates several areas that defenders can monitor:

- DNS queries and unusual domain requests
- Outbound network connections
- Unusual ICMP activity
- TCP connections and destination ports
- Encrypted TLS connections
- Repeated connection failures or unusual traffic patterns

The traffic in this project was generated and analyzed in a controlled laboratory environment.

## Repository Contents

```text
.
├── evidence/
│   ├── dns_analysis.png
│   ├── icmp_analysis.png
│   ├── tcp_analysis.png
│   ├── tls_analysis.png
│   └── overall_capture.png
├── report/
│   └── Network_Security_Analysis_Report.md
├── network_security_lab.pcapng
└── README.md
