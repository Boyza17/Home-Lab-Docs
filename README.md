# 🛡️ Network Wali: Home Lab Build-Out Guide
> **Goal:** A step-by-step Standard Operating Procedure (SOP) for migrating from a Windows-based laptop to a professional Proxmox Hypervisor and Ubuntu NOC.

---

## 📋 Phase 1: Preparing the Documentation Engine
Before touching any hardware, we set up the "Command Center" for our documentation.

### 1. The Toolchain
* **GitHub:** Our cloud-based "Safe" for documentation.
* **Git for Windows:** The engine that talks to GitHub.
* **VS Code:** Our primary editor for writing Markdown.
* **GitHub Desktop:** The visual interface for managing "Commits" and "Pushes."

### 2. Initial Setup & Troubleshooting
* **Task:** Install Git for Windows and link it to VS Code.
* **⚠️ Known Issue:** After installation, the VS Code terminal may say `git : The term 'git' is not recognized`.
* **✅ The Fix:** Restart VS Code. This refreshes the "Environment Variables" so the system can find the Git engine.
* **🔍 Git Diff Understanding:** In the "Changes" view, **Red** lines represent deleted/replaced code; **Green** lines represent new improvements.

---

## 💻 Phase 2: Hardware Provisioning (The HP Elitebook)
### 1. BIOS Configuration
* **Key to Enter BIOS:** Tap `F10` repeatedly during startup.
* **Key for Boot Menu:** Tap `F9` (to select the USB installer).

### 2. Critical Hardware Settings
| Setting | Selection | The "Why" (Junior Tech Explanation) |
| :--- | :--- | :--- |
| **Intel VT-x** | **Enabled** | Necessary for the Type-1 Hypervisor to share CPU power with VMs. |
| **Secure Boot** | **Disabled** | Allows the Proxmox (Debian) kernel to boot without signature errors. |
| **Boot Order** | **USB First** | Priority given to the installation media for the OS transition. |

---

## 💿 Phase 3: Creating the Bootable Media
1. **Tool:** Use **BalenaEtcher or Rusfus**.
2. **Process:** Flash the Proxmox VE 8.x ISO to a 16GB+ USB drive.
3. **Verification:** Always wait for the "Validation" step to ensure no data corruption occurred.

---

## 🚀 Phase 4: Proxmox & Linux Command Reference
Once the OS is installed, these are the commands used to manage the environment.

### 🖥️ Proxmox (PVE) Specifics
* **Web UI Access:** `https://<SERVER_IP>:8006` (Port 8006 is the PVE default).
* **CLI Management:**
    * `qm list`: Shows all Virtual Machines and their status (Running/Stopped).
    * `qm start <vmid>`: Powers on a specific VM (e.g., your Ubuntu Server).
    * `pveversion -v`: Displays detailed version info for troubleshooting.

### 🐧 Essential Linux Commands (The "Daily Drivers")
| Command | What it does | Why we use it |
| :--- | :--- | :--- |
| `sudo` | SuperUser Do | Grants temporary administrative (root) privileges. |
| `ls -la` | List All | Shows all files, including hidden ones and their permissions. |
| `cd` | Change Directory | Moves you through the folder structure (e.g., `cd ~/homepage`). |
| `ip addr` | IP Address | Verifies the current network configuration and MAC address. |
| `df -h` | Disk Free | Checks how much storage space is left on your drives. |
| `htop` | Process Monitor | A visual "Task Manager" for Linux to check CPU/RAM usage. |

---

## 🛠️ Phase 5: Troubleshooting Log & Resolutions
This section tracks the specific "Roadblocks" we hit and how we bypassed them.

### 1. The "Git Not Recognized" Error
* **Symptom:** VS Code terminal returns an error when typing `git`.
* **Resolution:** Re-initialized the PATH environment by restarting the IDE.

### 2. Docker Permission Issues
* **Symptom:** Unable to edit config files in `~/homepage` because they were owned by `root`.
* **The Fix:** Used `chown` to take ownership of the folders:
  `sudo chown -R $USER:$USER ~/homepage`
* **Why:** This allows your user account to edit YAML files without needing `sudo` every time.

### 3. PDF Editor "Paywalls"
* **Symptom:** Stirling-PDF Pro features (Direct Text Edit) asked for payment.
* **Resolution:** Utilized **LibreOffice Draw** for free direct editing and Stirling-PDF's **OCR to Word** feature for complex document conversion.

---

## 📦 Phase 6: The "NOC" Service Stack
*Note: All services are hosted on the Ubuntu Server VM at `<SERVER_IP>`.*

| Service | Internal Port | Access URL | Role |
| :--- | :--- | :--- | :--- |
| **AdGuard Home** | `3000` | `http://<SERVER_IP>:3000` | DNS Filtering & Ad Blocking. |
| **Portainer** | `9443` | `https://<SERVER_IP>:9443` | Visual Docker Management. |
| **Homepage** | `8082` | `http://<SERVER_IP>:8082` | The Central Dashboard. |
| **Stirling-PDF** | `8080` | `http://<SERVER_IP>:8080` | Privacy-focused PDF tools. |
| **Nginx Proxy Manager**| `81` | `http://<SERVER_IP>:81` | SSL & Reverse Proxy Management. |