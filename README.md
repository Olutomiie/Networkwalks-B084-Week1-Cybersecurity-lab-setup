# Networkwalks-B084-Week1-Cybersecurity-lab-setup
Cybersecurity Lab setup
<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Android-x86 9.0 ISO-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Tomilayo%20Amzat%20-C00000?style=flat-square" />
</p>

This repository documents my first cybersecurity lab setup, completed as Task 1 of my internship with Networkwalks.

The goal is to build a virtual environment where I can learn, experiment, troubleshoot, and gradually develop my understanding of cybersecurity and penetration testing.

## Project Objectives

## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

⚠️ **Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

---

## 🖥️ Lab Environment

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | ------------------  |
| 🖥️ Host OS         | Windows 10         |
| 🧠 Host RAM        | 8 GB               |
| ⚡ Processor       | Intel Core i7      |
| 🧰 Hypervisor      | VirtualBox 7.2  |
| 🐉 Security OS     | Kali Linux 2026.2  |
| 🧠 Kali RAM        | 2048 MB            |
| 🌐 Virtual Network | NAT Network        |
| 📡 Network Address | 10.0.0.0/24        |
| 🐧 Kali IP Address | 10.0.0.2/24        |
| 🚪 Default Gateway | 10.0.0.1           |
| 🌍 DNS Server      | 8.8.8.8            |
| 🔮 Future VM Range | 10.0.0.3–10.0.0.99 |

---

## ⚙️ Lab Setup Procedure

## Step 1. Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a `.7z` archive.

**Tool:** 7-Zip

---

## Step 2. Install VirtualBox

VirtualBox was installed as the hypervisor.

---

## Step 3. Create the NAT Network

A dedicated NAT Network was created in VirtualBox.

Configuration:
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled

![](2-screenshot-network-settings-1.png)

A **NAT Network** was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.


---

## Step 4. Import Kali Linux

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:

```text
Adapter 1
Attached to: NAT Network
Network:     NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
```

The VM was allocated:

```text
RAM: 2048 MB
```
![](3-screenshot-kali-linux.png)
A shared folder was also configured for transferring required files between the host operating system and the Kali VM.



---

## Step 5. Configure the Kali Linux Network

The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

```text
IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway: 10.0.0.1
DNS: 8.8.8.8
```

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.

![](4-screenshot-kali-network-settings.png)

---

## Step 6. Create a Clean VM Snapshot

After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:

```text
Clean Kali - Network Setup
```

The snapshot represents the clean baseline of the laboratory.

If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.

---

# 🔎 Lab Verification

| ✅ Test                        | 🧾 Command                      | 🎯 Expected Result              |
| ----------------------------- | ------------------------------- | ------------------------------- |
| 🌐 Check IP address           | `ip a`                          | Correct Kali IP displayed       |
| 📡 Test gateway               | `ping 10.0.0.1`                 | Successful replies              |
| 🌍 Test Internet connectivity | `ping 8.8.8.8`                  | Successful replies              |
| 🔎 Test DNS resolution        | `nslookup networkwalks.com`     | Domain resolves                 |
| 🧰 Verify Nmap                | `nmap --version`                | Nmap version displayed          |
| 🔄 Verify snapshot            | Restore snapshot and run `ip a` | Baseline configuration restored |

### Example Results

```text
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
8.8.8.8
```

---

# 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

## Problem 1. Internet Connectivity After Static IP Configuration

After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

The network connection was then restarted/rebooted and connectivity was tested again.

> **Important:** Network interface and connection names may differ between systems. Students should first identify their actual connection name before running an `nmcli` command.

---


# 🤖 Part 2: Android-x86 Virtual Machine Setup

## Step 1: Download Android-x86 9.0

Used the Android-x86 project as the source for the Android virtual machine installation media.

For a 64-bit VM, the release image is:

`android-x86_64-9.0-r2.iso` 

The ISO should be obtained from the official Android-x86 website or its linked release repository.

## Step 2: Create the Android Virtual Machine

Create a new virtual machine in VirtualBox with the following configuration.

| Setting | Value |
|---|---|
| VM Name | `Android9-Lab` |
| Type | Linux |
| Version | Other Linux (64-bit) |
| RAM | 2048 MB |
| Virtual Disk Format | VDI |
| Disk Allocation | Dynamically allocated |
| Virtual Disk Size | At least 10 GB |
| Video Memory | At least 64 MB |

Attach the Android-x86 ISO through **Settings → Storage** and start the VM.

## Step 3: Install Android-x86

From the Android-x86 boot menu, I selected:

`Installation - Install Android-x86 to harddisk`

The installation involved creating or selecting a partition, formatting it with the supported filesystem, and completing the bootloader and installation prompts.

After installation, reboot the virtual machine and detached the installation ISO when necessary to ensure the VM booted from its virtual hard disk.

## Step 4: Connect Android-x86 to the NAT Network

Open the Android VM's VirtualBox network settings and configured its network adapter.

| Setting | Value |
|---|---|
| Adapter | Adapter 1 |
| Attached To | NAT Network |
| Network Name | `NatNetwork` |
| Adapter Type | Intel PRO/1000 MT Desktop |

The Android VM and Kali Linux VM were now configured to use the same VirtualBox NAT Network.

---

# 🔧 Part 3: Android-x86 Network Configuration

## Step 1: Identify the Network Interface

The Android-x86 network interface required manual configuration because the available interface and network settings did not work as expected through the graphical configuration.

The interface used for this exercise was:

`eth0`

## Step 2: Configure the IP Address Manually

I used the following commands in the Android-x86 environment:

```bash
ip addr add 10.0.0.9/24 dev eth0
ip link set eth0 up
ip route add 10.0.0.0/24 dev eth0
```

### What the commands do

| Command | Purpose |
|---|---|
| `ip addr add 10.0.0.9/24 dev eth0` | Assigns the IPv4 address `10.0.0.9/24` to `eth0` |
| `ip link set eth0 up` | Activates the network interface |
| `ip route add 10.0.0.0/24 dev eth0` | Adds a route for the local `10.0.0.0/24` subnet through `eth0` |

**Important networking note:** The subnet route above is for local network traffic. It does not set the default gateway or guarantee internet connectivity. A default route through `10.0.0.1` may also be needed, depending on the existing routing table and Android-x86 network configuration.

The configuration can be inspected with:

```bash
ip addr show eth0
ip route
```

## Step 3: Test Connectivity from Android-x86 to Kali Linux

I ran the following command from Android-x86:

```bash
ping -c 3 10.0.0.2
```

This sends three ICMP echo requests to the Kali Linux VM.

**Expected result:** Replies from `10.0.0.2` indicate that Kali Linux is reachable from Android-x86.

## Step 4: Test Connectivity from Kali Linux to Android-x86

On the Kali Linux VM, I ran:

```bash
ping -c 3 10.0.0.9
```

**Expected result:** Replies from `10.0.0.9` indicate that Android-x86 is reachable from Kali Linux.

## Step 5: Test Internet Connectivity

From a terminal that supports the relevant networking commands, test the external IP address:

```bash
ping -c 3 8.8.8.8
```

Then test DNS resolution:

```bash
nslookup networkwalks.com
```

Successful IP connectivity and DNS resolution provide separate checks of outbound networking and name resolution.

> **Note:** ICMP requests can be blocked, and Android-x86 builds may not include a terminal application by default. A failed ping does not by itself prove that all network communication is broken.

---

# 🗺️ Part 4: Lab Network Summary

The intended lab addressing scheme is shown below.

| Network Component | IP Address / Value |
|---|---|
| Network | `10.0.0.0/24` |
| Subnet Mask | `255.255.255.0` |
| Gateway | `10.0.0.1` |
| Kali Linux | `10.0.0.2/24` |
| Android-x86 | `10.0.0.9/24` |
| DNS Server | `8.8.8.8` |
| Future VM Address Range | `10.0.0.3–10.0.0.99` |

The future VM range is a planning range, not a reservation. Before assigning additional static addresses, I will check the DHCP pool and existing IP assignments to avoid address conflicts.

### Network Layout

```text
                 Internet
                    |
              VirtualBox NAT
                    |
             NatNetwork
             10.0.0.0/24
                    |
          +---------+---------+
          |                   |
     Kali Linux           Android-x86
     10.0.0.2             10.0.0.9
          |                   |
          +---- Lab traffic ---+
```

---

# ✅ Part 5: Verification Checklist

The following checklist records the checks used to validate the environment. Mark each item only after confirming the result.

- [x] Kali Linux VM created and configured.
- [x] Android-x86 VM installed.
- [x] Both VMs configured to use `NatNetwork`.
- [x] Android-x86 interface manually configured using `ip` commands.
- [x] Ran `ping -c 3 10.0.0.2` from Android-x86.
- [ ] Confirmed successful replies from Kali Linux.
- [ ] Ran `ping -c 3 10.0.0.9` from Kali Linux.
- [ ] Confirmed successful replies from Android-x86.
- [ ] Verified outbound internet connectivity.
- [ ] Verified DNS resolution.
- [x] Created a baseline Kali Linux snapshot.

**Connectivity note:** The manual configuration commands were executed and the machines were reported as connected. The individual test boxes above should be updated according to the actual command output.

---

# 🐞 Part 6: Troubleshooting and Lessons Learned

## Challenge: Android-x86 Network Interface Configuration

The expected graphical network configuration was not sufficient for my environment, so I configured the interface manually.

```bash
ip addr add 10.0.0.9/24 dev eth0
ip link set eth0 up
ip route add 10.0.0.0/24 dev eth0
ping -c 3 10.0.0.2
```

This gave me direct practice with interface configuration, link state, routing, and connectivity testing.

### Further Troubleshooting Commands

If a VM cannot reach the other machine, I would check:

```bash
ip addr
ip route
```

On Kali Linux, I can also inspect the interface and test the peer:

```bash
ip a
ip route
ping -c 3 10.0.0.9
```

Things to verify include:

- Both VMs are connected to the exact same NAT Network.
- Each VM has a unique address within the subnet.
- The network interface is up.
- The subnet mask and routes are correct.
- The guest OS is not blocking ICMP traffic.
- The NAT Network DHCP pool does not conflict with static addresses.

### Important Note About Persistence

Commands entered with `ip addr` and `ip route` may not persist after a reboot. Persistent configuration depends on the Android-x86 build and its network management setup.

---

# 💡 Part 7: What I Learned

### 1. Virtualisation

I gained practical experience creating and configuring multiple virtual machines without replacing the host operating system.

### 2. NAT Network vs NAT

I learned why a NAT Network is useful when multiple VMs need to communicate with each other while maintaining outbound network connectivity.

### 3. IPv4 Addressing

I worked with IPv4 addresses, CIDR notation, subnet masks, and network interfaces.

### 4. Linux Networking Commands

Using `ip addr`, `ip link`, `ip route`, and `ping` helped me understand the relationship between interface configuration, routing, and connectivity.

### 5. Troubleshooting

The Android-x86 configuration required manual intervention, reinforcing the importance of checking actual interface and routing information instead of relying solely on graphical settings.

### 6. Documentation

I learned to document system specifications, commands, configuration decisions, and troubleshooting steps so that the environment can be understood and reproduced.

---
# 🔐 Security & Ethical Use

This laboratory is intended strictly for education purposes only.

---

# 🔗 Tools & Resources

- **7-Zip:** [https://7-zip.org/download.html](https://7-zip.org/download.html)
- **VirtualBox:** [https://virtualbox.org/wiki/Downloads](https://virtualbox.org/wiki/Downloads)
- **Kali Linux:** [https://kali.org/get-kali](https://kali.org/get-kali)
- **Android-x86 9.0 ISO: **[https://www.android-x86.org/download](https://www.android-x86.org/download)

---

# 👤 Author

**Tomilayo Amzat**\
Cybersecurity Professional B084

LinkedIn: [https://www.linkedin.com/in/tomilayoamzat](https://www.linkedin.com/in/tomilayoamzat)

---

## 📌 Project Information

**Program Name:** Cybersecurity at Networkwalks | **Week:** 01 | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub
