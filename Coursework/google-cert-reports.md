# Incident Reports & Security Assessments — Google Cybersecurity Certificate

## Overview

A collection of incident reports and security assessments completed as part of the Google Cybersecurity Professional Certificate. Each exercise is based on a simulated scenario designed to develop core security analyst skills including incident identification, network traffic analysis, risk assessment and application of the NIST Cybersecurity Framework.

---

## Access Controls — Payroll Fraud Investigation

**Scenario:** A deposit was made from the business to an unknown bank account. The finance manager denied making the transaction. Investigate the access logs to identify the threat actor and recommend mitigations.

### Notes

The event log shows a payroll event adding 'FAUX_BANK' was executed on 10/03/2023 at 8:29:57 AM from IP address 152.207.255.255 under the Legal\Administrator account from a computer named 'Up2-NoGud'. Cross-referencing the employee directory identifies this IP address as belonging to Robert Taylor Jr., a legal contractor whose end date was 12/27/19 — over three years before the incident.

### Issues

- Robert Taylor Jr.'s account was not deprovisioned on his end date, leaving active admin credentials available to a threat actor more than three years after his contract ended
- All employees regardless of role are assigned admin authorisation, violating the principle of least privilege and creating unnecessary attack surface

### Recommendations

- Implement an offboarding process that automatically deprovisions accounts on the employee end date
- Implement role-based access control — admin privileges should not be a default for all users
- Implement MFA to prevent unauthorised use of compromised credentials
- Conduct regular audits of active credentials to identify and remove accounts that should no longer have access

---

## Data Leak

*The course exemplar missed the root cause.*

The exemplar focused on procedural failures - access wasn't revoked, the folder wasn't restricted to internal users only. These are just symptoms of the underlying problem. Sensitive and non-sensitive data was housed in the same folder. Regardless of what the rep was trying to do, the folder design created unnecessary exposure to confidential information.

**Scenario:** A sales manager shared access to a folder of internal-only documents with their team during a meeting. The folder contained files associated with a new product that has not been publicly announced. It also included customer analytics and promotional materials. After the meeting, the manager did not revoke access to the internal folder, but warned the team to wait for approval before sharing the promotional materials with others. During a video call with a business partner, a member of the sales team forgot the warning from their manager. The sales representative intended to share a link to the promotional materials so that the business partner could circulate the materials to their customers. However, the sales representative accidentally shared a link to the internal folder instead. Later, the business partner posted the link on their company's social media page assuming that it was the promotional materials.


### Issue(s)

*What factors contributed to the information leak?*

Promotional materials designed for external sharing were stored in the folder along with sensitive information. This created unnecessary access to private data. This failure mode should not be possible with a properly structured file system where confidential data is separated from non-confidential data.

### Review

*What does NIST SP 800-53: AC-6 address?*

NIST SP 800-53: AC-6 addresses the principle of least privilege, where a user must be identified and only granted the least access required to perform their function. It suggests controls such as role based restriction and automatic access revocation as enhancements to bolster privacy posture.

### Recommendation(s)

*How might the principle of least privilege be improved at the company?*

PoLP Improvements:

1. Structural separation of sensitive and non-sensitive data
2. Role base access restrictions
3. Ability to share for set time with automatic revocation

### Justification

*How might these improvements address the issues?*

1. Structural separation of data categories allows users to continue performing their function without unnecessarily providing access to sensitive information.
2. Role base access restriction creates a baseline to ensure that users do not have access to information they do not need to fulfil their function.
3. Automatic revocation acts as a safety net and removes human error from the revocation process.

---

## NIST Cybersecurity Framework — Incident Report

**Scenario:** Apply the NIST Cybersecurity Framework to document and respond to a network security incident.

### Summary

The organisation's network was the target of a Denial of Service attack by a malicious actor. The incident caused a network outage for roughly two hours. The incident was traced to a flood of ICMP packets through an unconfigured firewall. The incident management team responded by stopping all non-critical network services and restoring critical services.

### Identify

The attack was an ICMP flood DoS that affected internal network operations. The primary cause of the incident was an unconfigured firewall that allowed ICMP packets without a rate limit.

### Protect

The team has implemented new firewall rules to limit the rate of incoming ICMP packets. Additionally, source IP verification has been implemented to check for spoofed IP addresses.

### Detect

New network monitoring software has been implemented to detect and flag abnormal network traffic patterns. Additionally, an IDS/IPS system has been rolled out to filter out some ICMP traffic based on suspicious characteristics.

### Respond

The team will respond to future similar incidents by rate limiting ICMP packets at the firewall, taking down non-critical network services if necessary, and restoring critical services as a priority. Communication to internal staff and external customers will be provided if the outage will be prolonged.

### Recover

After the incident, network operations were returned to normal status while prioritising critical services first. The team will continue monitoring the network for stability and seek to mitigate any future incidents using the new tools listed above.

---

## SYN Flood DoS Attack Report

**Scenario:** A website is returning connection timeout errors. Analyse logs to identify the cause and explain the attack mechanism.

### Identify the attack

A DoS attack is underway, specifically a SYN flood. The logs show an unfamiliar IP address sending a high volume of SYN packets to the server. The packets all originate from one IP address. The server has been overwhelmed and is unable to respond to legitimate traffic.

### How the attack causes the website to malfunction

Under normal operation, a TCP connection is established via a three-way handshake:

1. The user machine sends a SYN packet to the server
2. The server sends a SYN/ACK packet back to the user machine
3. The user machine sends an ACK packet back to the server and the connection is established

When a malicious actor sends a large number of SYN packets all at once, the server is waiting for the client to send back an ACK packet and eventually cannot respond due to accumulated volume. The logs indicate that the server has been overwhelmed by SYN packets from a single IP address, causing it to stop responding to genuine traffic. Employees cannot access the sales page causing business disruption.

---

## Network Traffic Analysis — DNS & ICMP

**Scenario:** A client has reported an outage. Analyse DNS and ICMP traffic logs to identify the cause.

### Summary

The UDP protocol reveals that port 53 was unreachable. The ICMP echo reply returned the error message `udp port 53 unreachable`. Port 53 is used for fetching DNS records. The most likely issue is no port listening.

### Analysis

**Time of incident:** 13:24:32

**How the incident was identified:** Client reported outage.

**Investigation steps:** Attempted to access website and used network analysis tools to view network traffic.

**Key findings:** UDP port 53 unreachable, DNS server affected.

**Likely cause:** DNS server offline or misconfiguration.

---

## Security Risk Assessment — Hardening Recommendations

**Scenario:** Review the current security posture of an organisation and recommend hardening measures.

### Recommended hardening measures

**Multi-factor authentication (MFA)** — Implement MFA to ensure that each employee is using their own login information and that any compromised usernames and passwords cannot be leveraged by threat actors.

**Firewall configuration** — There is currently no firewall configuration. Updating this to filter incoming and outgoing traffic could prevent threat actors from probing and gaining access to the network.

**Password policies** — Password policies need to be implemented, especially for admin accounts. We discovered that admin accounts have been left with default credentials making brute force attacks a viable attack vector.

---

## Security Incident Report — HTTP & Brute Force Attack

**Scenario:** Customers report being prompted to download a suspicious file when visiting a website. Analyse traffic logs to document the incident and recommend remediation.

### Network protocol involved

HTTP was the internet protocol involved in this incident. From viewing the tcpdump log we can see HTTP requests to GET files from yummyrecipesforme before a large volume of traffic on port 80 (HTTP). Following the traffic on port 80, the next request is a DNS request for greatrecipesforme.com. Following the connection to greatrecipes we see a further HTTP GET request followed by significant traffic on port 80. Suspect that this further traffic is the download of malware.

### Incident documentation

Incident occurred several hours ago. Customers contacted the support team complaining of being prompted to download a file when loading yummyrecipesforme.com and that their computers were running slowly after the download.

The cybersecurity team performed the following tasks to assess the incident:

- Ran network analysis in a sandbox to observe the suspicious behaviour
- It appears that admin access to the web server was obtained by a malicious actor
- We discovered that default credentials were not changed and therefore suspect that access was gained through a brute force attack
- After altering the website source code, the malicious actor changed the admin password, locking out the authorised user
- The threat actor used admin access to alter website source code and insert malicious JavaScript prompting users to download and run a file
- The file contained further malicious JavaScript that redirected users to greatrecipesforme.com
- Senior analyst has confirmed that this website is hosting malware

### Recommended remediation

- Implement password policies
- Implement CAPTCHA for admin access
- Implement 2FA for admin access

---

## Skills Demonstrated

`Incident identification` `Network traffic analysis` `TCP/IP` `DNS` `ICMP` `HTTP` `DoS attack analysis` `NIST Cybersecurity Framework` `Risk assessment` `Security hardening`

---

[← Back to Coursework](README.md) | [← Back to Portfolio](../README.md)
