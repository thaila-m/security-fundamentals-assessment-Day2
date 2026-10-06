# Network Security Analysis

## 1. Introduction

This project presents a defensive analysis of network traffic captured in a controlled VMware lab environment using Wireshark.

The objective was to identify the protocols present in the traffic, understand normal communication patterns, and identify potential security considerations.

## 2. Lab Environment

- Operating System: Kali Linux
- Environment: VMware virtual machine
- Analysis Tool: Wireshark 4.6.6
- Network Interface: eth0
- Capture File: network_security_lab.pcapng

## 3. Objectives

The objectives of this analysis were:

1. Capture network traffic in a controlled environment.
2. Identify the protocols present in the capture.
3. Analyze DNS traffic.
4. Analyze ICMP traffic.
5. Analyze TCP connections.
6. Examine TLS 1.3 traffic.
7. Identify potential security concerns.
8. Document defensive recommendations.

## 4. Methodology

Network traffic was captured using Wireshark on the Kali Linux virtual machine.

Display filters were used to isolate individual protocols:

- `dns`
- `icmp`
- `tcp`
- `tls`

The captured packets were then examined using Wireshark's packet list and packet detail panels.

## 5. Protocol Analysis

### 5.1 DNS

The capture contains DNS queries and responses involving the local system and DNS server.

The traffic includes queries for `example.com`. The DNS responses contain IPv4 and IPv6 address information.

This demonstrates the normal DNS resolution process:

1. The client sends a DNS query.
2. The DNS server processes the request.
3. The DNS server returns the requested address information.

Security consideration:

DNS traffic can be useful for identifying unusual domains, unexpected DNS servers, excessive queries, or possible command-and-control activity. In this controlled capture, the observed DNS traffic appears consistent with normal name resolution.

### 5.2 ICMP

The capture contains ICMP Echo Request and Echo Reply packets.

The traffic shows communication between:

- Source: `192.168.174.129`
- Destination: `104.20.23.154`

The Echo Request packets are followed by Echo Replies, demonstrating successful ICMP connectivity.

Security consideration:

ICMP is commonly used for network troubleshooting. However, unusual volumes of ICMP traffic or unexpected external destinations can be indicators that require further investigation.

### 5.3 TCP

The capture contains TCP traffic using destination port 443.

The connection begins with the standard TCP three-way handshake:

1. SYN
2. SYN-ACK
3. ACK

The capture then shows TCP data exchange between the client and the remote server.

Security consideration:

Port 443 is commonly used for HTTPS/TLS traffic. TCP connection information can be useful for identifying unexpected destinations, unusual ports, repeated failed connections, or abnormal connection patterns.

### 5.4 TLS 1.3

The capture contains TLS 1.3 traffic.

The observed traffic includes:

- TLS Client Hello
- TLS Server Hello
- Change Cipher Spec
- Encrypted Application Data

The Client Hello identifies `example.com` through the Server Name Indication (SNI).

After the TLS handshake, application data is encrypted.

Security consideration:

Encryption protects application contents from being easily read during network monitoring. However, encrypted traffic can still be analyzed using metadata such as destination IP addresses, ports, packet sizes, timing, and TLS handshake information.

## 6. Security Observations

The following observations were made from the capture:

### Observation 1: DNS Resolution

DNS queries and responses were observed for `example.com`.

No obvious malicious DNS behavior was identified from the provided traffic.

### Observation 2: ICMP Communication

ICMP Echo Requests and Replies were observed.

The communication indicates successful connectivity between the local system and the remote destination.

### Observation 3: HTTPS/TLS Communication

TCP port 443 was used to establish a TLS 1.3 connection.

The TLS handshake was successfully observed.

### Observation 4: Encrypted Application Traffic

After the TLS handshake, application data was encrypted.

This demonstrates the importance of encryption for protecting network communications.

## 7. Potential Security Concerns

Although the traffic observed in this controlled laboratory capture appears generally consistent with normal network communication, a security analyst should consider:

- Unexpected external IP addresses.
- Unusual DNS queries.
- High volumes of ICMP traffic.
- Repeated failed TCP connections.
- Connections to unusual ports.
- Unexpected encrypted connections.
- Repeated communication with unknown destinations.

These indicators would require additional investigation in a real-world environment.

## 8. Defensive Recommendations

The following defensive practices are recommended:

1. Monitor DNS requests for unusual domains.
2. Monitor outbound connections to unexpected destinations.
3. Use secure protocols such as HTTPS/TLS.
4. Maintain firewall rules that restrict unnecessary network access.
5. Monitor unusual ICMP activity.
6. Maintain network logs for incident investigation.
7. Investigate repeated connection failures and abnormal traffic patterns.
8. Use network monitoring tools such as Wireshark for troubleshooting and investigation.

## 9. Conclusion

This laboratory exercise demonstrated how Wireshark can be used for defensive network traffic analysis.

The capture contained ARP, DNS, ICMP, TCP, and TLS 1.3 traffic. Filtering the capture by protocol made it possible to examine individual communication patterns and understand how different network protocols operate.

The analysis also demonstrated that encrypted TLS traffic can still provide useful security metadata even when the application contents are protected.

Overall, the exercise provided practical experience with packet capture, protocol identification, traffic filtering, and basic defensive network security analysis.
