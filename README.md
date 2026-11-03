Wireshark Network Analysis Labs

Hands-on network traffic analysis using Wireshark and Kali Linux.

Project Overview

This repository documents practical network traffic analysis exercises focused on understanding network protocols, packet structures, and troubleshooting techniques.

The first lab demonstrates capturing and analyzing Internet Control Message Protocol (ICMP) traffic using Wireshark.

Lab 01: ICMP Packet Capture and Analysis

Objective

Capture and analyze ICMP Echo Request and Echo Reply packets to understand how the ping utility tests network connectivity.

Tools and Technologies

Kali Linux (WSL)

Wireshark

Linux Terminal

ICMP and IPv4

Git and GitHub

Lab Procedure

1. Start Wireshark

Launch Wireshark and select the loopback interface (lo).

2. Generate ICMP Traffic

Run the following command in the Kali Linux terminal:

ping -4 -c 4 127.0.0.1

This command sends four IPv4 ICMP Echo Requests to the local machine.

3. Apply a Wireshark Display Filter

icmp

This filter displays IPv4 ICMP packets.

4. Analyze the Captured Packets

Examine the following packet characteristics:

Source IP: 127.0.0.1

Destination IP: 127.0.0.1

Protocol: ICMP

Echo Request: Type 8

Echo Reply: Type 0

Sequence numbers and packet timestamps

Results

The ping command produced the following results:

Metric

Result

Packets transmitted

4

Packets received

4

Packet loss

0%

Minimum RTT

0.120 ms

Average RTT

0.177 ms

Maximum RTT

0.264 ms

Wireshark displayed eight ICMP packets: four Echo Requests and four Echo Replies.

Key Findings

ICMP Echo Requests and Echo Replies were successfully captured.

The local loopback interface responded to all four ping requests.

No packet loss occurred during the test.

Wireshark provided visibility into ICMP packet structure, message types, and sequence numbers.

Packet Capture

File: ICMP_ping_Lab.pcapng

The capture file is included in this repository for further examination using Wireshark.

Skills Demonstrated

Network packet capture and inspection

ICMP protocol analysis

Wireshark display filtering

Linux command-line operations

Network connectivity troubleshooting

Technical documentation

Git and GitHub version control

Future Labs

DNS Traffic Analysis

TCP Three-Way Handshake Analysis

HTTP and HTTPS Traffic Analysis

ARP Protocol Analysis

Network Troubleshooting and Traffic Investigation

Disclaimer

All packet captures were generated in an authorized local lab environment for educational and cybersecurity training purposes.


Lab 02: Nmap Port Scanning and Service Detection

Objective

Perform a TCP port scan and service version detection using Nmap in Kali Linux to identify an active HTTP service on localhost.

Tools Used

Kali Linux (WSL)

Nmap 7.99

Python 3 HTTP Server

Windows Terminal

Lab Environment

Target IP: 127.0.0.1

Target Port: 8080/TCP

Protocol: HTTP

Environment: Localhost (authorized testing)

Methodology

1. Start a local HTTP server

python3 -m http.server 8080 --bind 127.0.0.1

2. Perform a TCP connect scan with service detection

nmap -sT -sV -p 8080 127.0.0.1

3. Save the scan results

nmap -sT -sV -p 8080 127.0.0.1 -oN Nmap_HTTP_Scan.txt

Scan Results

Port

State

Service

Version

8080/TCP

Open

HTTP

SimpleHTTPServer 0.6 (Python 3.14.7)

Findings

Nmap confirmed that the localhost host was reachable.

TCP port 8080 was open.

Service detection identified a Python HTTP server.

The scan demonstrated how Nmap can identify accessible network services.

Security Analysis

Open ports indicate services that may be accessible to network clients. Identifying running services is an important step in network inventory, attack surface assessment, and security auditing.

In this lab, the HTTP server was deliberately configured to listen on the loopback address, limiting direct network access to the local host.

Conclusion

Successfully performed an authorized Nmap scan against a local HTTP server, identified an open TCP port, detected the running service, and saved the results for further analysis.

Evidence: Nmap_HTTP_Scan.txt

Lab 03: DNS Traffic Analysis Using Wireshark

Objective

Capture and analyze Domain Name System (DNS) queries and responses to understand how domain names are resolved into IP addresses.

Tools Used

Kali Linux (WSL)

Wireshark

DNS Utilities (dig)

Cloudflare Public DNS (1.1.1.1)

Commands Used

dig example.com
dig @1.1.1.1 example.com

Lab Procedure

Started Wireshark and selected the eth0 network interface.

Applied the dns display filter.

Generated a DNS query using the dig command.

Queried Cloudflare's DNS server directly to capture visible DNS traffic.

Identified and analyzed the DNS query and response packets.

Results

Field

Observation

DNS Query Packet

104

DNS Response Packet

105

Client IP Address

172.17.118.185

DNS Server

1.1.1.1

Domain Queried

example.com

Protocol

UDP

Destination Port

53

DNS Record Type

A (IPv4)

Resolved IP Addresses

104.20.23.154, 172.66.147.243

Security Findings

DNS queries reveal the domain names that clients attempt to resolve.

Standard unencrypted DNS traffic can be inspected using Wireshark.

DNS responses provide IP addresses associated with requested domain names.

DNS traffic analysis is useful for network troubleshooting and investigating suspicious domain activity.

Evidence

DNS_Traffic_Lab.pcapng

Lab 04: TCP Three-Way Handshake Analysis

Objective

Capture and analyze the TCP three-way handshake to understand how a client establishes a reliable connection with a server.

Tools Used

Kali Linux (WSL)

Wireshark

Python 3 HTTP Server

curl

Commands Used

Start the local HTTP server:

python3 -m http.server 9090 --bind 127.0.0.1

Generate TCP traffic from another terminal:

curl -v http://127.0.0.1:9090

Wireshark display filter:

tcp.port == 9090

Lab Procedure

Started a Python HTTP server on localhost using TCP port 9090.

Opened Wireshark and selected the loopback (lo) interface.

Applied the tcp.port == 9090 display filter.

Generated a TCP connection using curl.

Captured and examined the SYN, SYN-ACK, and ACK packets.

Observed the HTTP request and successful server response.

Results

Packet

TCP Flag / Protocol

Description

1

SYN

Client initiates TCP connection

2

SYN-ACK

Server acknowledges and responds

3

ACK

Client completes TCP handshake

4

HTTP GET

Client requests a web resource

8

HTTP 200 OK

Server successfully responds

Network Details

Client IP: 127.0.0.1

Client TCP Port: 33988

Server IP: 127.0.0.1

Server TCP Port: 9090

Capture Interface: Loopback (lo)

Displayed Packets: 24

Security Findings

The TCP three-way handshake establishes a connection before application data is exchanged.

SYN, SYN-ACK, and ACK flags identify the connection establishment process.

TCP traffic analysis can help identify failed connections, unexpected resets, and suspicious connection attempts.

Monitoring connection patterns can support network troubleshooting and security investigations.

Evidence

TCP_Three_Way_Handshake_Lab.pcapng

Conclusion

Successfully captured and analyzed a TCP three-way handshake using Wireshark and Kali Linux. Demonstrated practical understanding of TCP connection establishment, packet flags, and HTTP communication.

Conclusion

Successfully captured and analyzed DNS query and response packets using Wireshark and Kali Linux. Demonstrated practical understanding of DNS resolution, UDP port 53, and network packet analysis.

Lab 05: HTTP and HTTPS Traffic Analysis

Objective

Capture and compare HTTP and HTTPS network traffic to understand how TLS encryption protects web communications.

Tools Used

Kali Linux (WSL)

Wireshark

Python 3 HTTP Server

curl

Commands Used

Start the local HTTP server:

python3 -m http.server 9090 --bind 127.0.0.1

Generate HTTP traffic:

curl -v http://127.0.0.1:9090

Generate HTTPS traffic:

curl -v --http1.1 https://example.com -o /dev/null

Wireshark Filters

HTTP capture:

tcp.port == 9090

HTTPS capture:

tcp.port == 443 || tls

Lab Procedure

Started a local Python HTTP server on port 9090.

Captured HTTP traffic using Wireshark's loopback (lo) interface.

Identified the HTTP GET request and HTTP 200 OK response.

Captured HTTPS traffic using the eth0 interface.

Identified the TCP handshake, TLS Client Hello, Server Hello, and encrypted application data.

Compared visible HTTP information with TLS-protected HTTPS communication.

Results

Feature

HTTP

HTTPS

Test destination

127.0.0.1

example.com

Port

9090

443

Transport

TCP

TCP

Encryption

None

TLS 1.3

Request visibility

HTTP GET visible

HTTP request encrypted

Response visibility

HTTP 200 OK visible

HTTP response encrypted

Capture interface

lo

eth0

Security Findings

Unencrypted HTTP exposes application-layer requests and responses to network observers.

HTTPS uses TLS to protect HTTP content during transmission.

TLS 1.3 provides encryption and integrity protection for application data.

Some connection metadata, such as IP addresses and certain TLS handshake information, may remain visible.

Wireshark can help analysts identify insecure protocols and investigate network communication patterns.

Evidence

HTTP_Traffic_Lab.pcapng

HTTPS_TLS_Traffic_Lab.pcapng

Conclusion

Successfully captured and compared HTTP and HTTPS traffic using Wireshark and Kali Linux. Demonstrated practical understanding of HTTP requests, server responses, TLS 1.3, and encrypted network communications.

Lab 06: Network Discovery and Enumeration Using Nmap

Objective

Identify open and closed TCP ports, detect running services, and document network exposure on an authorized local system.

Tools Used

Kali Linux (WSL)

Nmap 7.99

Python 3 HTTP Server

Target

IP Address: 127.0.0.1 (localhost)

Scan Type: TCP Connect Scan and Service Version Detection

Commands Used

TCP Port Scan

nmap -sT -p 22,80,443,8080,9090 127.0.0.1

Service Version Detection

nmap -sT -sV -p 22,80,443,8080,9090 127.0.0.1

Save Scan Results

nmap -sT -sV -p 22,80,443,8080,9090 127.0.0.1 -oN ~/Nmap-Network-Scanning-Labs/Nmap_Network_Enumeration.txt

Results

Port

State

Service

Version

22/TCP

Closed

SSH

N/A

80/TCP

Closed

HTTP

N/A

443/TCP

Closed

HTTPS

N/A

8080/TCP

Open

HTTP

SimpleHTTPServer 0.6 (Python 3.14.7)

9090/TCP

Open

HTTP

SimpleHTTPServer 0.6 (Python 3.14.7)

Security Findings

The localhost target was reachable.

Two TCP ports, 8080 and 9090, were open.

Nmap identified Python HTTP servers running on both open ports.

Ports 22, 80, and 443 were closed.

Open ports represent potential network exposure, depending on service configuration and network accessibility.

The scan was limited to the authorized local environment.

Evidence

Nmap_Network_Enumeration.txt

Conclusion

Successfully performed TCP port enumeration and service version detection using Nmap. This exercise demonstrated how security analysts identify active services, document exposed ports, and assess network configurations.

Lab 07: ARP Protocol Analysis Using Wireshark

Objective

Capture and analyze Address Resolution Protocol (ARP) traffic to understand how IPv4 addresses are mapped to MAC addresses on a local network.

Tools Used

Kali Linux (WSL)

Wireshark

Linux networking utilities

Network Configuration

Setting

Value

Interface

eth0

Kali IP Address

172.17.118.185

Default Gateway

172.17.112.1

Kali MAC Address

00:15:5d:96:42

Gateway MAC Address

00:15:5d:d0:1f

Commands Used

Identify the network interface:

ip -4 addr show eth0

Identify the default gateway:

ip route

Clear the cached gateway neighbor entry:

sudo ip neigh flush 172.17.112.1 dev eth0

Generate local network traffic:

ping -c 4 172.17.112.1

Wireshark Filter

arp

Results

Successfully captured ARP request and reply packets on the eth0 interface.

ARP Request:
Who has 172.17.112.1? Tell 172.17.118.185

ARP Reply:
172.17.112.1 is at 00:15:5d:d0:1f:ec

Security Findings

ARP resolves IPv4 addresses to MAC addresses on the local network.

ARP requests are commonly broadcast to discover a destination's MAC address.

ARP replies provide the requested MAC address.

ARP does not provide built-in authentication, making it susceptible to ARP spoofing and poisoning attacks.

Wireshark can help identify unusual ARP activity during network investigations.

Evidence

ARP_Traffic_Lab.pcapng

Conclusion

Successfully captured and analyzed ARP communication using Wireshark and Kali Linux. Demonstrated understanding of local network address resolution and the security implications of unauthenticated ARP messages.
