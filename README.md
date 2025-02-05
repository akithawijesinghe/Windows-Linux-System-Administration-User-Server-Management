# 🖥️ Windows & Linux System Administration – User & Server Management  

## **📌 Project Overview**  
This project focuses on **setting up and managing Windows Server & Ubuntu Linux** in a virtualized environment. It includes:  
✅ **Active Directory (AD) User Management** on Windows Server  
✅ **Linux User & Permission Management** on Ubuntu  
✅ **Automating System Updates & Backups**  
✅ **Monitoring System Performance & Security**  

🔹 **Platform:** Windows Server (Azure VM) & Ubuntu (Virtual Machine)  
🔹 **Tools Used:** Active Directory, PowerShell, Bash, Azure Portal, Remote Desktop (RDP), SSH  

---

## **📌 Prerequisites**  
Before starting, ensure you have:  
🔹 **Azure Account** (to create a Windows Server VM)  
🔹 **Remote Desktop Client (RDP)** (for connecting to Windows Server)  
🔹 **VMware/VirtualBox** (for running Ubuntu)  
🔹 **Basic knowledge of Linux & Windows Server administration**  

---

# **🔹 Step 1: Setting Up Windows Server on Azure**  
First, create and configure a **Windows Server Virtual Machine (VM)** on Azure.  

### **1️⃣ Create an Azure VM**  
1. **Log in to Azure Portal** → [Azure Portal](https://portal.azure.com)  
2. Navigate to **Virtual Machines** → Click **"Create" → "Azure Virtual Machine"**  
3. **Choose Configuration:**  
   - **Image:** Windows Server 2022 Datacenter  
   - **Size:** Standard B2ms (2 vCPUs, 8 GB RAM)  
   - **Authentication:** Password  
   - **Public Inbound Ports:** Allow **RDP (3389)**  

4. Click **"Review + Create"** → Wait for VM Deployment  

---

### **2️⃣ Connect to Windows Server using Remote Desktop (RDP)**  
Once the VM is running:  
1. Go to **Azure Portal** → **Virtual Machines**  
2. Select your **Windows Server VM**  
3. Click **"Connect" → "RDP"** → Download the **.rdp file**  
4. Open the **.rdp file** → Log in with:  
   - **Username:** `Administrator`  
   - **Password:** *(The password you set during VM creation)*  

✅ You’re now connected to **Windows Server via Remote Desktop!**  

---

# **🔹 Step 2: Installing & Configuring Active Directory (AD)**
Now, install **Active Directory Domain Services (AD DS)** for **user & group management**.

### **1️⃣ Install Active Directory & Promote Server to Domain Controller**
1. **Open PowerShell (as Administrator)**  

2. Run the following command to install Active Directory:  
   ```powershell
   Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
3. Promote the server to a Domain Controller:
   ```powershell
   Install-ADDSForest -DomainName "mycompany.local"
4. Restart the server.

✅ Your Windows Server is now a Domain Controller!

---

### **2️⃣ Creating Users & Managing Permissions in Active Directory**

To create a new user in Active Directory:

1. Open "Active Directory Users and Computers" (dsa.msc)
2. Navigate to Users → Right-click → New → User
3. Enter Username, First Name, Last Name → Set Password
4. Assign permissions & group policies as needed

✅ Alternatively, create users via PowerShell:

```powershell
New-ADUser -Name "John Doe" -SamAccountName "jdoe" -UserPrincipalName "jdoe@mycompany.local" -Path "CN=Users,DC=mycompany,DC=local" -AccountPassword (ConvertTo-SecureString "SecurePass123!" -AsPlainText -Force) -Enabled $true
```

# **🔹 Step 3: Linux User & Permission Management**

Now, set up Ubuntu in a Virtual Machine for user and permission management.

### **1️⃣ Create & Manage Users in Ubuntu**

✅ Create a new user:

```bash
sudo adduser johndoe
```
✅ Grant sudo access:

```bash
sudo usermod -aG sudo johndoe
```
✅ Verify users:
```bash
cut -d: -f1 /etc/passwd
```   

# **🔹 Step 4: Automate System Updates & Backups**

To keep servers secure and stable, automate system updates & backups.

### **1️⃣ Windows Updates (PowerShell)**

```powershell
Install-Module -Name PSWindowsUpdate -Force
Get-WindowsUpdate -Install -AcceptAll -AutoReboot
```

### **2️⃣ Ubuntu Updates (Bash)**
```bash
#!/bin/bash
apt update && apt upgrade -y
echo "System updated on $(date)" >> /var/log/sys-updates.log
```

✅ Automate with cron (runs every Sunday at 3 AM):

```bash
crontab -e
```
Add:
```bash
0 3 * * 7 /path/to/update-linux.sh
```

# **🔹 Step 5: Monitor System Health & Performance**

Monitoring system health ensures smooth operations.

### **1️⃣ Windows Monitoring (PowerShell)**

✅ Check running processes:

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
```

### **2️⃣ Ubuntu Monitoring (Bash)**

✅ Check CPU usage:

```bash
top -o %CPU
```

✅ Check disk space:

```bash
df -h
```

## **📌 Final Outcome & Learning**

🎯 With this setup, you now have:

✅ Windows Server with Active Directory & User Management

✅ Ubuntu Server with User Permissions & Remote Access

✅ Automated system updates & backups for reliability

✅ Basic monitoring & troubleshooting commands

🔥 This project is a real-world demonstration of System Administration skills and is valuable for internships and DevOps roles!









