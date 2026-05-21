# Cybersecurity Portfolio

Self-directed work toward a role in cyber security. Hands-on investigations, lab infrastructure, security research, and coursework.

For a description of how AI tools were used in producing this portfolio, see [METHODOLOGY.md](METHODOLOGY.md).

---

## Featured Work

Highlights from real-world investigations, applied research, and coursework.

| Document | Description | Date |
| --- | --- | --- |
| [IR-001 False-Positive Wazuh Rootcheck on macOS](Incident%20Response/IR-001-false-positive-wazuh-rootcheck-macos-may26.md) | Investigated Wazuh alert and determined false positive across two distinct root causes. Implemented scoped detection rule changes with documented limitations | May 2026 |
| [Network Segmentation, VPN and DNS Filtering](Network%20Security/network-segmentation-dns-vpn-apr26.md) | Tiered network architecture with per-segment VPN routing and per-device DNS visibility. Performance-driven design with documented deferrals | April 2026 |
| [SmartTube Compromise & IoT Network Segmentation](Incident%20Response/vlan-iot-segmentation-apr26.md) | Responded to a real supply chain compromise affecting IoT devices on the home network. Implemented VLAN segmentation as a defence-in-depth control | April 2026 |
| [Reverse Gandalf — System Prompt Defence Research](AI%20Security/reverse-gandalf-apr26.md) | Built and tested a defensive system prompt against adversarial input. Documented how simpler rules outperformed comprehensive ones under pressure | April 2026 |
| [Database Vulnerability Assessment](Coursework/database-vulnerability-assessment-google-may26.md) | Risk assessment of a publicly exposed database server using NIST SP 800-30. Threat modelling, likelihood/severity scoring, sequenced remediation plan | May 2026 |

---

## Portfolio Sections

<details>
<summary><b><a href="Incident%20Response/">Incident Response</a></b> — Real-world security incidents investigated and remediated</summary>

| Document | Description | Date |
| --- | --- | --- |
| [SmartTube Compromise & IoT Network Segmentation](Incident%20Response/vlan-iot-segmentation-apr26.md) | Investigated SmartTube supply chain compromise, implemented IoT network isolation | April 2026 |
| [IR-001 False-Positive Wazuh Rootcheck on macOS](Incident%20Response/IR-001-false-positive-wazuh-rootcheck-macos-may26.md) | Investigated Wazuh alert and determined false positive, implemented detection rule change to reduce noise | May 2026 |
| [IR-002 False-Positive Wazuh Trojaned Binaries](Incident%20Response/IR-002-false-positive-wazuh-trojaned-binaries-may26.md) | Investigated Wazuh alert and determined false positive, implemented detection rule change to reduce noise | May 2026 |

</details>

<details>
<summary><b><a href="Network%20Security/">Network Security</a></b> — Network architecture, segmentation, and DNS-level security controls</summary>

| Document | Description | Date |
| --- | --- | --- |
| [Network Segmentation, VPN and DNS Filtering](Network%20Security/network-segmentation-dns-vpn-apr26.md) | Tiered network segmentation, per-network VPN routing, per-device DNS visibility via NextDNS CLI on router firmware | April 2026 |
| [Encrypted DNS-over-TLS Implementation](Network%20Security/nextdns-dot-setup-apr26.md) | Evaluated DNS filtering solutions and implemented network-wide encrypted DNS with NextDNS via DoT | April 2026 |

</details>

<details>
<summary><b><a href="Risk%20%26%20Compliance/">Risk & Compliance</a></b> — Risk assessment, security audit, and compliance work</summary>

| Document | Description | Date |
| --- | --- | --- |
| [Database Vulnerability Assessment](Coursework/database-vulnerability-assessment-google-may26.md) | Risk assessment of a publicly exposed database server using NIST SP 800-30. Threat modelling, likelihood/severity scoring, sequenced remediation plan | May 2026 |
| [Data Leak — Sales Folder Exposure](Coursework/data-leak-sales-folder-google-apr26.md) | Analysed accidental external sharing of internal documents. Identified structural data separation issue missed by the course exemplar | April 2026 |

</details>

<details>
<summary><b><a href="Lab%20Infrastructure/">Lab Infrastructure</a></b> — Supporting environments for security work</summary>

| Document | Description | Date |
| --- | --- | --- |
| [Ubuntu VM Setup on Apple Silicon](Lab%20Infrastructure/ubuntu-utm-setup-apr26.md) | Deployed Ubuntu 25.10 in UTM, troubleshot VPN/NAT interference | April 2026 |
| [Local LLM Deployment with Ollama](Lab%20Infrastructure/ollama-local-llm-apr26.md) | Deployed Ollama, evaluated open source models including Mixture of Experts architectures for security-relevant inference | April 2026 |

</details>

<details>
<summary><b><a href="Scripting%20%26%20Automation/">Scripting & Automation</a></b> — Security tooling, data analysis and automation</summary>

| Document | Description | Date |
| --- | --- | --- |
| [SQL Filters for Security Log Analysis](Scripting%20%26%20Automation/sql-filters-google-cert-apr26.md) | SQL filtering exercises using AND, OR, NOT and LIKE operators to analyse login and employee data | April 2026 |

</details>

<details>
<summary><b><a href="AI%20Security/">AI Security</a></b> — Research and applied work on emerging risks in AI systems</summary>

| Document | Description | Date |
| --- | --- | --- |
| [Reverse Gandalf — System Prompt Defence Research](AI%20Security/reverse-gandalf-apr26.md) | Built and tested a defensive system prompt against adversarial input. Documented how simpler rules outperformed comprehensive ones under pressure | April 2026 |
| [OpenClaw AI Agent Security Audit & Research](AI%20Security/openclaw-security-audit-apr26.md) | Deployed and audited OpenClaw agentic framework in an isolated VM, reviewed published prompt injection research | April 2026 |

</details>

<details>
<summary><b><a href="Coursework/">Coursework</a></b> — Curated subset of work from the Google Cybersecurity Professional Certificate</summary>

Full index in [Coursework/README.md](Coursework/README.md).

| Document | Description | Date |
| --- | --- | --- |
| [Database Vulnerability Assessment](Coursework/database-vulnerability-assessment-google-may26.md) | Risk assessment of a publicly exposed database server using NIST SP 800-30. Threat modelling, likelihood/severity scoring, sequenced remediation plan | May 2026 |
| [Access Controls — Payroll Fraud Investigation](Coursework/access-controls-payroll-fraud-google-apr26.md) | Investigated unauthorised payroll transaction, identified failed offboarding and over-privileged access as root causes | April 2026 |
| [Data Leak — Sales Folder Exposure](Coursework/data-leak-sales-folder-google-apr26.md) | Analysed accidental external sharing of internal documents, identified structural data separation issue missed by the course exemplar | April 2026 |
| [SYN Flood DoS Attack Analysis](Coursework/syn-flood-dos-attack-google-mar26.md) | Identified single-source SYN flood from connection timeout logs, explained the TCP three-way handshake exploit | March 2026 |
| [HTTP & Brute Force Attack Incident](Coursework/http-brute-force-incident-google-mar26.md) | Investigated brute-forced admin account that resulted in malicious JavaScript injection and a malware redirect chain | March 2026 |

</details>

<details>
<summary><b><a href="Templates/">Templates</a></b> — Reusable documentation templates</summary>

| Document | Description |
| --- | --- |
| [Incident Response Template](Templates/incident-response-template.md) | Structured IR report template covering detection, containment, eradication, recovery and lessons learned |
| [Vulnerability Investigation Template](Templates/vulnerability-investigation-template.md) | Vulnerability triage template covering analysis, actions, outcome and risk acceptance |

</details>

---

## Skills Demonstrated Across Portfolio

**SIEM & detection** — `Wazuh` `rootcheck` `syscheck` `custom rule authoring` `false positive triage` `detection tuning`

**Network security** — `VLAN segmentation` `IoT isolation` `VPN routing (OpenVPN, WireGuard)` `encrypted DNS (DoT)` `DNS filtering` `router hardening` `mDNS bridging analysis`

**Incident response** — `Alert triage` `evidence collection` `root cause analysis` `containment` `remediation planning` `IR documentation`

**Risk & compliance** — `NIST SP 800-30` `NIST SP 800-53` `risk assessment` `threat modelling` `likelihood/severity scoring` `access controls` `principle of least privilege`

**AI security** — `Prompt injection research` `agentic framework risk assessment` `defensive prompt engineering` `local LLM deployment` `model behavioural analysis`

**Linux & virtualisation** — `Proxmox` `Ubuntu` `VM deployment` `package verification (dpkg)` `file integrity tooling` `Linux administration`

**Coursework foundations** — `SQL filtering` `tcpdump analysis` `Wireshark` `TCP/IP` `DNS` `HTTP` `protocol-level reasoning` `incident reconstruction`

---

## About

This portfolio is a working document, updated as projects are completed. Maintained under the `hsec-1` handle.

For methodology — including review process, sensitive information handling, and how AI tools are used — see [METHODOLOGY.md](METHODOLOGY.md).
