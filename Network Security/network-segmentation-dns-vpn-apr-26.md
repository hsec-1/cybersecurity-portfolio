# Network Segmentation, VPN and DNS Filtering Implementation — April 2026

## Overview

Redesigned a home network around tiered segmentation, per-device DNS visibility and per-network VPN routing. Built on top of an earlier DNS filtering project (see below), this work extends the network's security posture from DNS filtering alone to a layered architecture with explicit trust zones, network-level VPN routing for specific device classes, and per-device DNS monitoring. The focus on IoT segmentation was informed by a prior real-world compromise of an IoT device on my network, which highlighted the risk of lateral movement in a flat network.

## Background

An earlier project implemented network-wide DNS filtering via NextDNS over DNS-over-TLS (see [NextDNS with DoT Implementation](nextdns-dot.md)). That work established DNS filtering and basic encrypted DNS, but had limitations: a single flat network with all devices on one subnet, no per-device visibility in NextDNS logs, and no VPN routing capability.

This project addresses those limitations by replacing stock router firmware with Asuswrt-Merlin, introducing multiple network segments with different trust levels, and moving from DoT to the NextDNS CLI for per-device DNS visibility.

## Architecture

Four network segments were created, each with a distinct purpose and routing policy:

| Segment | Devices | Router-level VPN | Rationale |
|---|---|---|---|
| Main | Personal devices (laptops, phones, tablets, PC, NAS) | AUS VPN with per-device exceptions | General privacy; exceptions where throughput matters |
| Untrusted IoT | Streaming devices, robo vacuum, smart home devices | AUS VPN | Devices with poor security hygiene; IP masking for telemetry |
| US-Streaming | Single streaming device for geo-restricted services | US dedicated IP VPN | Geo-routing for services that require a US IP |
| High risk household members | Devices belonging to household members with higher-risk browsing habits | AUS VPN | Privacy layer and containment if devices are compromised |

Each segment uses port and AP isolation within the guest network configuration to prevent lateral communication between devices on the same untrusted segment.

## Key design decisions

### Least privilege applied to network design

Each segment was assigned only the connectivity it needed. Untrusted IoT can reach the internet but cannot reach the Main network. Household devices are isolated from Main entirely. The US-Streaming segment is dedicated to one device with one specific purpose. This maps the principle of least privilege — commonly applied to user permissions — to network reachability.

### Tiered IoT handling

Two categories of IoT devices were considered: "untrusted" (devices with poor firmware update practices and telemetry habits, such as streaming boxes and robo vacuums) and "trusted" (devices with better security track records that also need local discovery, such as smart speakers and a smart lighting controller). A separate "Trusted IoT" segment was planned but ultimately deferred because cross-subnet service discovery requires either bidirectional routing (which weakens isolation) or custom firewall scripting to allow one-way access. For this iteration, trusted IoT devices were kept on the Main network while untrusted ones were segmented. This trade-off is documented as a known limitation with a plan to revisit.

### Router-level vs device-level VPN

Initial design routed all Main network traffic through a router-level VPN. Speed testing showed a significant throughput reduction — roughly 30% of the line speed — compared to direct WAN. This was consistent with the router CPU being the bottleneck for OpenVPN encryption.

Testing the vendor's VPN app directly on a laptop yielded approximately 85% of line speed using WireGuard, rather than OpenVPN. The architecture was then revised:

- Router-level VPN retained on segments where device-level VPN isn't practical and throughput is not a limiting factor
- Device-level VPN app used on personal laptops and phones where full throughput matters
- Gaming devices excluded from VPN entirely for latency reasons
- Per-device exceptions set via the router's VPN Director for specific devices on the Main network that need direct WAN

This split was driven by measured performance data rather than a preconceived design, and balances privacy coverage against real-world usability for a multi-person household.

### DNS filtering evolution

The previous DoT setup provided network-wide filtering but logged all queries under the router IP. Migrating to the NextDNS CLI (running directly on the router) enabled per-device visibility in the NextDNS dashboard. This means query logs can be filtered by device, which is significantly more useful for:

- Spotting anomalous behaviour from a single device
- Identifying which device is responsible for a surge in blocked queries
- Establishing a per-device baseline to make future anomalies easier to notice
- Auditing and devices that ignore DNS configuration

DNS Director was also configured to force all devices (including those that try to hardcode public DNS like 8.8.8.8) through the router's DNS, closing a common bypass path used by some IoT devices.

## Threat model (informal)

Assets were identified in rough order of value: NAS (irreplaceable personal data), personal devices (credentials and session tokens), and household/shared devices. Threats considered included:

- IoT device compromise leading to lateral movement toward higher-value assets
- Household user phishing or drive-by malware
- Exposure of real IP via IoT telemetry

The mitigations map to those threats: segmentation limits lateral movement, separating a household user network contains risk from higher-risk browsing, DNS filtering addresses known malicious domains and provides visibility, and VPN routing limits IP exposure. This is an informal threat model rather than a formal methodology.

## What was deliberately deferred

- **Trusted IoT tier with one-way routing.** Requires custom iptables scripting to implement properly. Deferred until the maintenance overhead is justified by a concrete need.
- **Per-household-member NextDNS profile.** A single strict profile is currently applied network-wide; splitting would add management overhead without clear benefit at this stage.
- **Intrusion detection.** No IDS layer beyond DNS-based threat intelligence. IDS implementation is a planned future project.
- **Segment restrictions** Segmentation relies primarily on router-enforced isolation rather than custom firewall rules, which is a current limitation.

## What I learned from this project

- Security measures should be implemented with mitigation of a specific threat in mind — stacking controls without clear reasoning creates maintenance burden without proportional benefit.
- Measured performance data can overturn a reasonable-looking design. The router-level VPN decision was only correct in theory.
- Segmentation design is constrained by network hardware (in this case, an existing unmanaged switch shared by multiple rooms), not just logical preference.
- How to layer controls so no single failure leads to a full compromise (defense in depth). For example, encrypted VPNs and DNS filtering reduce exposure to malicious traffic, while port isolation and network segmentation limit lateral movement. Even if one control fails, the others should still contain the impact.

---

## Skills demonstrated

`Network segmentation` `VLAN design` `VPN routing (OpenVPN, WireGuard)` `DNS filtering` `Principle of least privilege` `Threat modelling (informal)` `Router firmware (Asuswrt-Merlin)` `Performance-based architecture decisions`

---

[← Back to Portfolio](../README.md) | [See also: NextDNS with DoT Implementation](nextdns-dot.md)
