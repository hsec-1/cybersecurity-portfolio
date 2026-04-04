# NextDNS with DNS-over-TLS Implementation — April 2026

## Overview

Evaluated DNS filtering solutions and implemented NextDNS with DNS-over-TLS (DoT) encryption at the router level, providing network-wide ad blocking, malware filtering and phishing protection for a multi-device household.

---

## Background

Prior to this project, the network was using ISP-provided DNS with no filtering. Following a malware infection and broader network security review, DNS-level filtering was identified as a practical control to block known malicious domains across all household devices — including IoT devices that cannot run software-based security tools.

---

## Solution Evaluation

| Service | Ad Blocking | Malware Filtering | Account Required | Notes |
|---------|-------------|-------------------|------------------|-------|
| ISP Default | No | No | No | Baseline, no filtering |
| Cloudflare 1.1.1.1 | No | No | No | Privacy focused, speed optimised |
| Control D (free) | Limited | Yes | No | No configuration without account |
| AdGuard DNS | Yes | Yes | No | Drop-in, no configuration |
| NextDNS | Yes | Yes | Yes (free tier) | Configurable, DoT/DoH support |

**Selected: NextDNS** — chosen for configurability, support for encrypted DNS protocols, query logging for network visibility, and an active threat intelligence feed.

---

## Implementation

**Protocol:** DNS-over-TLS (DoT) on port 853 — encrypts DNS queries between the router and NextDNS, preventing ISP visibility into DNS lookups.

**Router:** ASUS GT-AX6000 (supports DoT natively in firmware)

**Configuration:**
- DoT server IPs: dedicated config-linked NextDNS IPv4 addresses
- TLS port: 853
- TLS hostname: config-linked NextDNS hostname
- Fallback plain DNS: config-linked NextDNS IPv4 addresses
- Log storage: Switzerland

---

## Considerations & Tradeoffs

**iCloud Private Relay compatibility** — DNS filtering services can conflict with iCloud Private Relay, as both attempt to handle DNS resolution. iOS detects when Private Relay's required endpoints are being intercepted and flags the network as incompatible. This is an inherent tension between two privacy-focused tools rather than a misconfiguration.

**Per-device visibility** — Router-level DNS sends all queries through a single router identity. NextDNS logs show queries but not which individual device made them. Per-device visibility would require either the NextDNS CLI (requires custom firmware on the router) or installing the NextDNS app on individual devices. Assessed as a nice-to-have for this use case.

**Free tier limits** — NextDNS free tier allows 300,000 queries/month, after which filtering pauses. For larger households this limit may be reached — the paid plan (~USD$2/month) removes this restriction.

---

## Skills Demonstrated

`DNS security` `Encrypted DNS (DoT)` `Network-level security controls` `Solution evaluation` `Router configuration` `Privacy considerations in security tooling`

---

[← Back to DNS Security](README.md) | [← Back to Portfolio](../README.md)
