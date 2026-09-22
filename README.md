# NEXSECURE — Cisco CML Infrastructure

**Cisco CML · VMware · Routing & Switching · Network Security**

## Overview

As part of the NEXSECURE team project, I participated in designing, configuring, securing, and validating a simulated enterprise network. The lab connects a headquarters and a remote branch and integrates the Cisco CML network with external VMware virtual machines and physical PCs.

**Status:** Completed.

## Architecture

| Component                 | Role                                                                |
| ------------------------- | ------------------------------------------------------------------- |
| SW-DIST-HQ                | Layer 3 distribution switch and HQ VLAN gateways                    |
| SW-ACCESS-1 / SW-ACCESS-2 | HQ access switching, trunks, and LACP EtherChannel                  |
| R-EDGE                    | Routed connection between HQ and the branch                         |
| R-A / SW-A                | Branch router-on-a-stick and access switch                          |
| CML External Connector    | Connection to external VMware and physical hosts in the server VLAN |

HQ separates administration, users, voice, servers, DMZ, and management traffic into VLANs. The branch also includes Wi-Fi and guest VLANs. OSPF uses backbone Area 0 and branch Area 1.

## Work completed

* Created VLANs, 802.1Q trunks, and inter-VLAN routing.
* Configured LACP EtherChannel, Rapid-PVST, and the HQ root bridge.
* Established multi-area OSPF adjacencies and configured OSPF MD5 authentication as part of the lab.
* Applied an extended guest VLAN ACL to restrict access to server and management networks.
* Configured sticky MAC port security, violation restrict mode, PortFast, and BPDU Guard on user access ports.
* Established an IPsec site-to-site tunnel between R-EDGE and R-A.
* Connected external VMware VMs and several physical PCs to the CML server VLAN.
* Configured Cisco-side NTP and Syslog settings.

## Validation results

| Feature                       | Recorded outcome                                                         |
| ----------------------------- | ------------------------------------------------------------------------ |
| EtherChannel                  | Port-channel active                                                      |
| OSPF                          | Neighbors reached FULL; remote routes appeared in routing tables         |
| IPsec                         | ISAKMP reached QM_IDLE and encryption/decryption counters increased      |
| External connectivity         | External MAC and ARP entries appeared; pings to external hosts succeeded |
| Inter-VLAN access from VMware | Windows Server reached the server VLAN and HQ administration gateways    |

The External Connector port supports multiple external machines, so the single-MAC port-security policy used on user ports was not applied to that link.

## Troubleshooting highlight

The initial NAT-only CML setup allowed management access but did not carry external lab traffic as required. A two-adapter design separated management access through NAT from the bridged connection to the physical/VMware network.

After correcting the bridge and External Connector, external MAC addresses were learned in the server VLAN and connectivity tests succeeded.

## Documentation

This summary presents the implementation and validation results documented in my final Cisco CML project report. A runnable CML topology export and full device configurations are not included in this repository.

**Skills:** network segmentation, routing, switching, access control, VPN configuration, virtualization integration, troubleshooting, and validation.

---

[Back to my portfolio](https://github.com/laflame90210)
