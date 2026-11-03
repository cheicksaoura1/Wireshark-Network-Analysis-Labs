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
