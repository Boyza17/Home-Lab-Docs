# Home-Lab-Docs
Technical documentation for my Proxmox and Ubuntu Home Lab. (Beginner)
# 🛡️ Network Wali Home Lab
Comprehensive documentation of my transition from Windows to a Proxmox-based Virtual Environment.

## 🏗️ Phase 1: The Bare Metal Transition
**Objective:** Replace the Windows OS on my HP Elitebook with Proxmox VE 8.x to create a Type-1 Hypervisor.

### 1. Hardware Audit
* **Device:** HP Elitebook
* **Role:** Primary Hypervisor Node
* **Key BIOS Settings:** * **Virtualization (VT-x/AMD-V):** Enabled (Required for VMs to run).
    * **Secure Boot:** Disabled (Often required for Proxmox installation).

### 2. The Proxmox Installation Command Concepts
*Why do we use these commands during or after the ISO installation?*

| Command | Definition | Why we use it |
| :--- | :--- | :--- |
| `lsblk` | List Block Devices | To ensure we are wiping the correct hard drive and not the USB. |
| `ip addr` | Show Network Addresses | To verify our static IP is active on the local network. |
| `apt update` | Update Package List | To download the latest security metadata for our server. |

