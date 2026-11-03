SOC Incident Investigation Report

Incident Overview

Incident ID: LAB-12-001
Incident Type: Simulated Network Reconnaissance / TCP Port Scanning
Investigation Date: November 3, 2026
Environment: Kali Linux (WSL)
Target System: 127.0.0.1 (Localhost)
Severity: Informational
Status: Completed — Authorized Simulation

Executive Summary

This investigation examined simulated network reconnaissance against a local HTTP server. Nmap was used to scan TCP ports 8000–8100, while Wireshark captured and analyzed the resulting network traffic.

The investigation identified TCP connection attempts across multiple ports, an accessible HTTP service on port 8080, and TCP reset responses from closed ports.

The activity was intentionally generated in a controlled laboratory environment. No unauthorized access or malicious compromise was identified.

Tools Used

Kali Linux (WSL)

Wireshark

Nmap

Curl

Python HTTP Server

Linux networking utilities

Investigation Procedure

Verified that the Python HTTP server was listening on TCP port 8080.

Established a baseline by generating normal HTTP requests.

Started Wireshark packet capture on the loopback (lo) interface.

Performed a controlled Nmap TCP connect scan against localhost.

Analyzed SYN packets targeting multiple destination ports.

Examined TCP reset responses associated with closed ports.

Compared normal HTTP communication with simulated reconnaissance traffic.

Saved the packet capture for investigation evidence.

Commands Used

Verify HTTP Server

sudo ss -ltnp | grep ':8080'

Generate Normal HTTP Traffic

curl -I http://127.0.0.1:8080/

Simulate Network Reconnaissance

nmap -sT -p 8000-8100 127.0.0.1

Wireshark SYN Filter

tcp.flags.syn == 1 && tcp.flags.ack == 0

Wireshark Reset Filter

tcp.flags.reset == 1

Evidence and Findings

Evidence

Observation

Source IP

127.0.0.1

Destination IP

127.0.0.1

Scanned TCP ports

8000–8100

Open port

8080

Closed ports

100

HTTP server response

HTTP/1.0 200 OK

TCP SYN packets

Observed across multiple ports

TCP reset responses

Observed from closed ports

Activity classification

Authorized simulated reconnaissance

Security Assessment

The Nmap scan generated multiple TCP connection attempts to different destination ports within a short period.

Wireshark revealed SYN packets associated with these connection attempts and reset responses from ports without active listening services.

This pattern can indicate network reconnaissance when observed in an operational environment. However, the activity in this investigation was intentionally generated for authorized laboratory testing.

Risk Assessment: Informational. No evidence of system compromise was identified during this exercise.

Recommended Security Actions

Monitor unusual connection attempts across multiple destination ports.

Investigate repeated TCP reset responses associated with scanning patterns.

Restrict unnecessary network services and exposed ports.

Configure firewall rules to limit unauthorized access.

Correlate packet captures with firewall and intrusion detection logs.

Document suspicious activity and escalate confirmed incidents according to SOC procedures.

Evidence File

Wireshark packet capture from the controlled localhost investigation.

Evidence Type: PCAPNG
Capture Interface: Loopback (lo)
Target: 127.0.0.1
Related Activity: TCP connect scan of ports 8000–8100

Conclusion

This investigation demonstrated practical SOC analyst skills in network traffic analysis, TCP flag interpretation, port-scan identification, and incident documentation.

The exercise successfully distinguished normal HTTP communication from simulated reconnaissance activity and documented the resulting network evidence.

Final Determination: Authorized security testing; no confirmed malicious incident.
