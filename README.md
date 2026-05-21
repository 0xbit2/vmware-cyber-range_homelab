# Enterprise VMware Cyber Range Lab

This project is divided into multiple modules that guide you through building a complete cybersecurity homelab with VMware Workstation Pro. By the end, you will have a secure environment for practicing penetration testing, attack simulation, threat detection, and SIEM-based security monitoring across multiple targets. 

---

# Architecture Overview

```text
                          ┌────────────────────┐
                          │  VMware Workstation │
                          └─────────┬──────────┘
                                    │
                          ┌─────────▼─────────┐
                          │     pfSense CE    │
                          └──────┬─────┬──────┘
                                 │     │
        ┌────────────────────────┘     └────────────────────────┐
        │                                                       │
┌───────▼────────┐                                   ┌──────────▼─────────┐
│ cyber-range-LAN│                                   │ cyber-range-AD-LAB│
│ 10.0.0.0/24    │                                   │ 10.80.80.0/24     │
└───────┬────────┘                                   └──────────┬─────────┘
        │                                                       │
 ┌──────▼───────┐                                  ┌────────────▼──────────┐
 │ Kali Linux   │                                  │ Windows Server 2025   │
 │ Wazuh SIEM   │                                  │ Active Directory DC   │
 └──────────────┘                                  └────────────┬──────────┘
                                                                │
                                                    ┌───────────▼──────────┐
                                                    │ Windows 11 Clients   │
                                                    └──────────────────────┘

                ┌───────────────────────────────────────────┐
                │ cyber-range-isolated (10.6.6.0/24)       │
                │ Vulnerable VMs / VulnHub / HackMyVM       │
                └───────────────────────────────────────────┘
```

---

# Features

* VMware Workstation Pro enterprise lab
* pfSense segmented firewall architecture
* Active Directory forest deployment
* Kali Linux attack workstation
* Vulnerable VM isolation
* Wazuh SIEM integration
* Suricata Network IDS
* Sysmon host telemetry
* Kerberoasting & AS-REP roasting labs
* Pivoting and lateral movement practice
* MITRE ATT&CK detection workflows
* SPAN traffic mirroring
* SOC monitoring environment

---

# Lab Networks

| Segment                | Subnet          | Purpose            |
| ---------------------- | --------------- | ------------------ |
| cyber-range-LAN        | `10.0.0.0/24`   | Management & SIEM  |
| cyber-range-isolated   | `10.6.6.0/24`   | Vulnerable Targets |
| cyber-range-ad-lab     | `10.80.80.0/24` | Active Directory   |
| cyber-range-sec-egress | `10.10.10.0/24` | Pivot / DMZ        |
| cyber-range-span       | SPAN Only       | Traffic Mirroring  |

---

# Hardware Requirements

| Component  | Minimum                | Recommended    |
| ---------- | ---------------------- | -------------- |
| CPU        | x86-64 Multi-Core      | 8+ Threads     |
| RAM        | 16 GB                  | 32 GB          |
| Storage    | 512 SSD                | 1TB NVMe SSD   |
| Hypervisor | VMware Workstation Pro | Latest Version |

---

# Core Technologies

## Infrastructure

* VMware Workstation Pro
* pfSense CE
* Windows Server 2025
* Windows 11 Enterprise
* Ubuntu Server 24.04

## Security Tooling

* Kali Linux
* Wazuh SIEM
* Suricata IDS
* Sysmon
* Filebeat

## Attack Simulation

* Kerberoasting
* AS-REP Roasting
* ACL Abuse
* Pivoting
* Lateral Movement

---

# VM Inventory

| VM                 | Role                               |
| ------------------ | ---------------------------------- |
| pfSense            | Firewall & Routing                 |
| Kali Linux         | Attacking Machine                  |
| DC01               | Active Directory Domain Controller |
| WKSTN01            | Domain Workstation                 |
| WKSTN02            | Domain Workstation                 |
| Ubuntu SIEM        | Wazuh + Suricata                   |
| Vulnerable Targets | VulnHub / HackMyVM                 |

---

# VMware Optimization

## Enable Hardware Virtualization

Enable:

* Intel VT-x / VT-d
* AMD-V / AMD-Vi

inside BIOS/UEFI before deployment.

---

## Optimize Network Drivers

Replace VMware default `e1000` drivers with `vmxnet3`.

### `.vmx` Modification

```ini
ethernet0.virtualDev = "vmxnet3"
ethernet1.virtualDev = "vmxnet3"
ethernet2.virtualDev = "vmxnet3"
ethernet3.virtualDev = "vmxnet3"
```

---

# pfSense Configuration

| Interface | Subnet        | Purpose          |
| --------- | ------------- | ---------------- |
| WAN       | VMnet8        | Internet         |
| LAN       | 10.0.0.1/24   | Management       |
| OPT1      | 10.6.6.1/24   | Isolated Targets |
| OPT2      | 10.80.80.1/24 | Active Directory |
| OPT3      | 10.10.10.1/24 | Secure Egress    |
| OPT4      | SPAN          | Packet Mirroring |

---

# Active Directory Lab

## Forest Configuration

| Setting           | Value               |
| ----------------- | ------------------- |
| Forest Name       | `ad.lab`            |
| Domain Controller | `DC01`              |
| DNS               | AD Integrated       |
| DHCP              | Windows Server      |
| Functional Level  | Windows Server 2025 |

---

# Detection & Monitoring

## Wazuh SIEM

* Centralized log aggregation
* MITRE ATT&CK mapping
* Windows event monitoring
* Sysmon integration

## Suricata IDS

* SPAN port packet inspection
* EVE JSON logging
* Threat intelligence rulesets
* Nmap & lateral movement detection

---

# Security Testing Capabilities

* Active Directory exploitation
* Credential attacks
* Kerberos abuse
* Reverse shells
* Internal pivoting
* Malware telemetry analysis
* Network intrusion detection
* Threat hunting workflows
* SOC alert validation

---

# Recommended Snapshots

| Snapshot                 | Purpose                     |
| ------------------------ | --------------------------- |
| Pristine Baseline        | Clean vulnerable VM         |
| Pre-Domain Baseline      | Before AD promotion         |
| Windows 11 Gold Template | Cloneable workstation image |

---

# References

* Ben Heater aka 0xben VMware Cyber Range Guides
* Wazuh Documentation
* Suricata Documentation
* Sysmon Documentation
* MITRE ATT&CK Framework

---

# License

MIT License

---

# Disclaimer

This lab is intended strictly for:

* Defensive security training
* Detection engineering
* Penetration testing education
* Malware analysis research

Do not expose these systems directly to the public internet.

Special Credits: The inspiration for this project comes from cybersecurity professional and ethical hacker 0xben [Ben Heater](https://benheater.com/). You can check out his blog here.
