# 🛡️ Isolated Cybersecurity Lab Setup (Week 1)

A fully isolated, reproducible cybersecurity lab environment built inside **Oracle VM VirtualBox** featuring **Kali Linux** on a custom **NAT Network**, verified IP leasing, outbound DNS/ICMP resolution, and an immutable clean baseline snapshot.

---

## 📌 Architectural Overview

In penetration testing and security research, creating an isolated network architecture prevents accidental scans or attacks from leaking into local home/enterprise networks while maintaining seamless outbound internet access.

| Component | Specification / Value |
| :--- | :--- |
| **Hypervisor** | Oracle VM VirtualBox 7.x |
| **Virtual Machine** | Kali Linux (amd64) |
| **Network Type** | NAT Network (Dedicated Internal Virtual Switch) |
| **Network Profile Name** | `NatNetwork` |
| **Subnet CIDR** | `10.0.2.0/24` |
| **DHCP Server** | Enabled (Auto IPv4 Leasing) |
| **Assigned Guest IP** | `10.0.2.3/24` (`eth0`) |
| **Snapshot State** | `Clean Kali - Baseline` |

---

## 🚀 Setup & Implementation Steps

### Step 1: Dedicated NAT Network Creation
1. Navigated to VirtualBox **Tools** > **Network Manager** > **NAT Networks**.
2. Created a new network profile named `NatNetwork`.
3. Configured the IPv4 prefix to `10.0.2.0/24` and enabled the built-in DHCP service to support automatic addressing across future victim VMs.

### Step 2: Guest Network Adapter Assignment
1. Opened the **Settings** menu for the **Kali Linux** virtual machine.
2. Under the **Network** tab (Adapter 1):
   - Attached to: `NAT Network`
   - Name: `NatNetwork`
   - Promiscuous Mode: `Deny`
3. Verified the interface status as connected.

### Step 3: IP Lease & Connectivity Verification
Started the Kali Linux VM and executed diagnostic commands via terminal:
* **Interface Status & IP Verification:**
  ```bash
  ip a
