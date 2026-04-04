# Ubuntu VM Deployment on Apple Silicon — April 2026

## Overview

Deployed Ubuntu 25.10 Desktop in a UTM virtual machine on an M5 MacBook, troubleshooting network connectivity issues. The purpose of this VM was as an isolated environment to run a test of OpenClaw. 

---

## Environment

- **Host:** Apple M5 MacBook
- **Hypervisor:** UTM (QEMU-based)
- **Guest OS:** Ubuntu 25.10 (ARM64)
- **Network mode:** Shared Network (NAT) — UTM internal subnet 192.168.64.x

---

## What I Did

- Created a new ARM64 VM in UTM using the Ubuntu 25.10 desktop ISO
- Diagnosed network connectivity failure during installation
- Resolved connectivity issue and completed installation
- Configured static IP address for the VM
- Installed OpenSSH during setup for remote access
- Selected NAT over Bridged networking deliberately to keep the VM sandboxed from the main network — Bridged mode would have exposed the VM as a device on the home network

---

## Key Challenge — VPN Interference with VM Networking

During installation, the VM was unable to reach the Ubuntu mirror servers or the internet despite appearing correctly configured. The error presented as "Network is unreachable" in the installer.

**Root cause:** VPN was active on the host MacBook and intercepting UTM's shared network (NAT) traffic. UTM's NAT operates on an internal subnet (192.168.64.x) that routes through the Mac's network stack. VPN intercepted this traffic before it could reach the internet.

**Resolution:** Disabling VPN on the host resolved the issue immediately. This is a known limitation of this particular VPN provider on macOS — Apple's network extension restrictions prevent split tunnelling, meaning all traffic including VM NAT traffic is routed through the VPN tunnel.

**Static IP configuration:** When DHCP failed during initial installation attempts, manually configured a static IP using UTM's internal NAT subnet (192.168.64.x) rather than the home network range, which would not have been routable through the NAT gateway.

---

## Skills Demonstrated

`Virtualisation (UTM/QEMU)` `Linux installation` `Network troubleshooting` `NAT` `DHCP` `Static IP configuration` `VPN interference diagnosis` `SSH` `Linux package management`

---

[← Back to Linux & Virtualisation](README.md) | [← Back to Portfolio](../README.md)
