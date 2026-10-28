# SmartTube Compromise and Network Architecture Revision
 
## Overview
Following a supply chain malware compromise on SmartTube, an Android TV app in November 2025 (and after initial response), I implemented network segmentation as a defence in depth measure. Over the following months I extended this into a further segmented architecture with per-network VPN routing and per-device DNS visibility.
 
## Background
SmartTube, a popular open source Android TV app, had its build machine compromised in Nov 2025 and malicious code was injected into an official release. Google Play Protect flagged it and removed it from devices. The developer later confirmed the affected versions, changed the digital signature and released a clean, re-signed build.
 
## Initial response
Factory reset both affected devices, rotated all credentials, adopted a password manager, and reviewed network traffic logs and DNS settings for signs of compromise but found none. The duration of infection and any persistence mechanisms were unknown, so long-term containment seemed wise even without any indicators of compromise.
 
## Phase 1 - Initial VLAN Segmentation (Nov 2025)
Using the router's existing guest network/VLAN features (stock firmware), I isolated the affected Android TV devices onto a dedicated subnet, including a wired device via LAN VLAN assignment (guest network does not cover wired connections). Low risk smart home devices that needed app control (smart lighting hub, audio streamer) stayed on the main network as segmenting them broke app control and the risk profile of the particular devices on the main network was acceptable. This initial segmentation was the first real network architecture change I made to implement the defence in depth concept.
 
## Phase 2 - Additional Segmentation, VPN & DNS per Device Visibility (April 2026)
I decided to implement per device DNS visibility and router level VPN routing. To achieve this I replaced the stock router firmware.
 
Network segments:
- Main (personal devices, device level VPN implementation)
- Secondary (AUS VPN, segment for less technical users)
- Untrusted IoT (AUS VPN)
- Streaming (single wired device, VPN)

Each segment only has the access it needs. Untrusted IoT can reach the internet but no other VLANs on the network.

Note: Untrusted IoT has AP isolation enabled to stop untrusted devices communicating with each other.
 
**VPN:** I implemented router-level VPN across all networks initially. This destroyed throughput (~30% of line speed using OpenVPN, the router was CPU-bound). Removing the router level VPN from the main network and switching personal devices to device-level WireGuard allowed recovery to ~85% of line speed. The main network is the only network not running a router level VPN. Device-level VPN is used on laptops and phones and router-level where device-level isn't practical.
 
**DNS:** I migrated from router-level DNS over TLS to the NextDNS CLI for per-device query visibility. My goal was per device DNS query logging, to help spot anomalies and audit devices. A DNS redirect rule forces devices through NextDNS. Devices using a device level VPN handle their own DNS, so I configure those individually.
 
**Deferred:** I chose not to proceed with a "trusted IoT" tier as the additional work did not seem justified based on the risk profile. Per-user DNS profiles have also been deferred.
 
## What I Learned
This incident illustrated the importance of defence in depth to me. Prior to this event, I had read about defence in depth and could articulate why it was important, but I had not considered implementing it in my own network at the time.

I also learned the real danger of supply chain attacks and why they make up such a large portion of incidents. A supply chain attack like this targets victims in an imprecise way, but this highlighted the power of this type of attack and drove home how effective it could be when used to target a particular entity or group. If you want to read an analysis of the malware found in the compromised SmartTube versions, it can be found [here](https://github.com/yuliskov/SmartTube/issues/5131#issuecomment-3592348406).

---

## Skills demonstrated

`Network segmentation` `VLAN design` `VPN routing (OpenVPN, WireGuard)` `DNS filtering` `Principle of least privilege` `Threat modelling (informal)` `Router firmware`

---

[← Back to Portfolio](../README.md)
