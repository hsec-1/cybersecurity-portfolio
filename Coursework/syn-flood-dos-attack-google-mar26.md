# SYN Flood DoS Attack Report

**Scenario:**

*A website is returning connection timeout errors. Analyse logs to identify the cause and explain the attack mechanism.*

### Identify the attack

A DoS attack is underway, specifically a SYN flood. The logs show an unfamiliar IP address sending a high volume of SYN packets to the server. The packets all originate from one IP address. The server has been overwhelmed and is unable to respond to legitimate traffic.

### How the attack causes the website to malfunction

Under normal operation, a TCP connection is established via a three-way handshake:

1. The user machine sends a SYN packet to the server
2. The server sends a SYN/ACK packet back to the user machine
3. The user machine sends an ACK packet back to the server and the connection is established

When a malicious actor sends a large number of SYN packets all at once, the server is waiting for the client to send back an ACK packet and eventually cannot respond due to accumulated volume. The logs indicate that the server has been overwhelmed by SYN packets from a single IP address, causing it to stop responding to genuine traffic. Employees cannot access the sales page causing business disruption.

---
## Skills Demonstrated

`Network traffic analysis` `TCP/IP` `DoS attack identification` `Protocol-level reasoning`

---

[← Back to Coursework](README.md) | [← Back to Portfolio](../README.md)
