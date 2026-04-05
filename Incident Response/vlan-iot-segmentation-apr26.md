# VLAN & IoT Network Segmentation — April 2026

## Overview

Following a supply chain malware compromise discovered on Android TV devices in November 2025 and subsequent remediation, conducted a network security review to assess residual risk and implement long-term controls and mitigation strategies.

---

## Background — SmartTube Supply Chain Compromise

SmartTube is a popular open source, ad-free YouTube client for Android TV. In November 2025, the developer's build machine was compromised by malware, resulting in malicious code being silently injected into official APK releases distributed via GitHub and third-party sources such as APKMirror. The injected payload — a native library not present in the public source code — collected device information, installed application data and IP addresses, and could receive further instructions from attackers.

Google Play Protect detected and disabled the compromised app on affected devices. The developer confirmed affected versions, wiped the build environment, revoked the compromised signing key and released a clean build (v30.56) under a new digital signature.

This is a textbook supply chain attack: the malware was injected at the build stage of a legitimate open source project, meaning users who installed or updated the app through official channels received compromised builds without any indication of tampering.

**Affected devices:** Android TV Streaming Device, Android TV
**Discovery:** November 2025

**Initial remediation:**

* Factory reset of both affected devices
* Uninstalled all SmartTube versions; did not restore any app backups
* Reviewed Google and YouTube account activity and permissions for unauthorised access
* Revoked all active sessions as a precaution
* Full credential rotation for associated and all critical accounts
* Adopted a password manager for unique, strong credentials across all accounts
* Updated router firmware to latest version

**Residual risk:** Duration of infection was unknown, meaning the full scope of data access during the infection period could not be determined. The malware's capability to receive remote instructions meant potential exposure was not limited to the data collection observed in static analysis. Long-term network controls and mitigation strategies were warranted.

---

## Network Security Review

**NAT table analysis** — Reviewed all active connections via the router's NAT table. Identified and verified each established connection against known devices and services. No suspicious external connections found post-remediation.

**Router log audit** — Reviewed system logs for unexpected admin login attempts. All login events were attributed to legitimate household devices and explained by router admin activity during the review.

**DNS settings** — Confirmed DNS was obtaining automatically from ISP rather than a hardcoded external server, ruling out DNS hijacking as a persistence mechanism.

---

## Network Segmentation Implementation

Designed and implemented IoT network segmentation using an ASUS GT-AX6000 router with Guest Network Pro and VLAN features.

**Approach:**

* Created a dedicated IoT network profile in Guest Network Pro with a separate subnet
* Enabled DHCP server on the VLAN with a restricted client limit
* Assigned the Android TV streaming device's physical LAN port to an isolated VLAN via LAN → VLAN port configuration (Access mode)
* Connected remaining IoT devices to the IoT WiFi SSID

**Devices isolated to IoT VLAN:**

* Android TV streaming device (wired — isolated via physical LAN port VLAN assignment)
* Android TV (wireless)
* Streaming stick (wireless)

**Devices retained on main network (mDNS bridging unavailable):**

* Smart lighting hub (requires same-network access for mobile app control)
* Network audio streamer (requires same-network access for mobile app control)

**Outcome:** High-risk devices are isolated from the main network. A compromised IoT device cannot be used as a pivot point to reach primary devices such as laptops and phones.

---

## Key Challenges

**Wired device isolation** — AP Isolation only applies to wireless clients. Isolating a wired device required assigning its physical LAN port to the IoT VLAN rather than relying on WiFi-level controls.

**mDNS bridging** — Proper VLAN isolation breaks local network discovery protocols used by Spotify Connect, AirPlay and similar services. The ASUS GT-AX6000 does not support mDNS bridging natively, requiring a decision about which devices to isolate vs retain on the main network based on risk level and functionality requirements.

---

## Key Takeaway

This incident demonstrated that sideloaded applications — even well-known open source projects with active development communities — can become attack vectors through build environment compromise. The malware was injected during the build process on the developer's compromised machine, meaning the infected APK was signed and distributed through official channels as though it were legitimate. This reinforces the value of network segmentation as a defence-in-depth control: even if a device is compromised through a trusted application, isolation limits the blast radius to the segmented network.

---

## Skills Demonstrated

`Network segmentation` `VLAN configuration` `IoT security` `Incident response` `NAT table analysis` `Router log auditing` `Threat modelling` `Supply chain attack analysis`

---

[← Back to Network Security](README.md) | [← Back to Portfolio](../README.md)
