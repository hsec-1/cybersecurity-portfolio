# SmartTube Compromise and Network Architecture Revision — Nov 2025 to Late April 2026
 
## Overview
Following a supply chain malware compromise on SmartTube, an Android TV app in November 2025 (and after initial response) I implemented network segmentation as a defence in depth measure. Over the following months I extended this into a four-tier segmented architecture with per-network VPN routing and per-device DNS visibility.
 
## Background
SmartTube, a popular open source Android TV app, had its build machine compromised in Nov 2025 — malicious code was injected into official release. Google Play Protect flagged it and removed it from devices. The developer later confirmed the affected versions, changed digital signature and released a clean, re-signed build.
 
## Initial response
Factory reset both affected devices, rotated all credentials, adopted a password manager, and reviewed network traffic logs and DNS settings for signs of compromise but found none. The duration of infection and any persistence mechanisms were unknown, so long-term containment seemed prudent even without any indicators of compromise.
 
## Phase 1 — Initial VLAN Segmentation (Nov 2025)
Using the router's existing guest network/VLAN features (stock firmware), I isolated the affected Android TV devices onto a dedicated subnet, including a wired device via LAN-port VLAN assignment (guest network does not cover wired connections). Low risk smart home devices needing same-network app control (smart lighting hub, audio streamer) stayed on the main network as the router had no mDNS bridging to allow discovery across segments and the risk profile of the particular devices on the main network was acceptable. This initial segmentation was the first real network architecture change I made to implement the defence in depth concept.
 
## Phase 2 — Additional Segmentation, VPN & DNS per Device Visibility (April 2026)
I decided to implement per device DNS visibility and router level VPN routing, to achieve this I replaced the stock router firmware.
 
Network segments:
- Main (personal devices, device level VPN implementation)
- Secondary (AUS VPN, segment for household members with less technical capacity)
- Untrusted IoT (AUS VPN)
- US-Streaming (single device, US VPN for geo-restricted content)
Each applies least privilege and for Untrusted IoT I have also implemented port isolation. Untrusted IoT can reach the internet but not Main.
 
**VPN:** I implemented router-level VPN across all networks initially. This turned out to be devastating for throughput (~30% of line speed using OpenVPN, the router was CPU-bound). Removing the router level VPN from the main network and switching personal devices to device-level WireGuard allowed recovery to ~85% of line speed. The main network is the only network not running a router level VPN. Device-level VPN is used on laptops and phones and router-level where device-level isn't practical. I excluded gaming devices for latency.
 
**DNS:** I migrated from DNS over TLS (see previous NextDNS set up article) to the NextDNS CLI for per-device query visibility. My goal was per device DNS query logging as it is useful for spotting anomalies and auditing devices and allows some additional block list functionality. DNS Director is set to force all devices through NextDNS, however, devices using device level VPN bypass this control and must be set manually.
 
**Deferred:** I chose not to proceed with a "trusted IoT" tier as the additional work did not seem justified based on the risk profile. Per-household-member DNS profiles has also been deferred.
 
## What I Learned
This incident illustrated the importance of defence in depth to me. Prior to this event, I had read about defence in depth and could articulate why it was important, but I had not considered implemented in my own network at the time.

I also learned the real danger of supply chain attacks and why they make up such a large portion of attacks. A supply chain attack like this targets victims in an imprecise way, but this highlighted the power of this type of attack and drove home how effective it could be when used to target a particular entity or group. If you want to read an analysis of the malware found in the compromised SmartTube versions, it can be found [here](https://github.com/yuliskov/SmartTube/issues/5131#issuecomment-3592348406).

---

## Skills demonstrated

`Network segmentation` `VLAN design` `VPN routing (OpenVPN, WireGuard)` `DNS filtering` `Principle of least privilege` `Threat modelling (informal)` `Router firmware` `Performance-based architecture decisions`

---

[← Back to Network Security](README.md) | [← Back to Portfolio](../README.md) | [See also: NextDNS with DoT Implementation](nextdns-dot-setup-arp26.md)
