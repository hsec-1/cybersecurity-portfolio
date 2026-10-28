# Cybersecurity Portfolio

I am transitioning into cyber security, with a focus on GRC (governance, risk and compliance). This portfolio documents work I have done on my own home network and lab, including my response to a real compromise. 

I recently cut this portfolio back to reduce clutter. The majority of the Google coursework and my smaller lab notes added little value and made it more difficult to find the stronger write ups.

For how I use AI in this portfolio, see [METHODOLOGY.md](METHODOLOGY.md).

---

## Certifications

- **CompTIA Security+ (SY0-701)**, September 2026 · [Verify](https://www.credly.com/badges/4d10ae10-0af5-4fc9-a8c5-9f4156344f09/public_url)
- **Google Cybersecurity Professional Certificate**, June 2026 · [Verify](https://www.credly.com/badges/c25bf954-c66d-4886-adb0-73ba73ff7f12/public_url)

---

## Investigations

| Document | Description |
| --- | --- |
| [SmartTube Compromise and Network Architecture Revision](investigations/smarttube-network-architecture.md) | Response to a real supply chain compromise on my home network, and the changes I made afterwards (segmentation, VPN and DNS filtering) based on risk. |
| [IR-001 Wazuh Rootcheck False Positive (macOS)](investigations/ir-001-wazuh-rootcheck-macos.md) | Investigated Wazuh alert for hidden ports on my MacBook, confirmed it was a false positive and only suppressed the one port that triggered consistently. |
| [IR-002 Wazuh Trojaned Binaries False Positive (Linux)](investigations/ir-002-wazuh-trojaned-binaries.md) | Investigated a Wazuh alert for trojaned files on my Proxmox host, confirmed it was a false positive and justified suppressing it with a compensating control. |
| [Reverse Gandalf: System Prompt Defence](investigations/reverse-gandalf.md) | Wrote a system prompt to resist prompt injection. |

## Risk and Governance

| Document | Description |
| --- | --- |
| [Database Vulnerability Assessment](risk-and-governance/database-vulnerability-assessment.md) | A risk assessment of a publicly exposed database using NIST SP 800-30, with a staged plan to secure it (Google Cybersecurity Certificate coursework). |

