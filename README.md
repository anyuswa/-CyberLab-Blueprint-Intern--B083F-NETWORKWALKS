# -CyberLab-Blueprint-Intern--B083F-NETWORKWALKS
INTERNSHIP for cybersecurity laboratory designed for learning Linux administration, virtualization, networking, and defensive/offensive security concepts in a controlled environment.

📌 **Project Overview**

CyberLab Blueprint is a personal cybersecurity laboratory built with virtualization technology and Kali Linux.

The objective of this project is to create a self-contained environment where cybersecurity tools and networking concepts can be explored without intentionally interacting with production systems or external networks.

**The lab is designed around four principles:**

🔒 **Isolation** — keep laboratory activity separated from normal devices and networks.

🔁**Reproducibility**— make the environment easy to rebuild.

🧪 **Experimentation** — provide a safe place to test security concepts.

📝 **Documentation** — record configuration decisions, verification steps, and lessons learned.

🎯 **Project Objectives**


#	**Objective	Description**

🖥️ Install and configure a desktop virtualization platform for cybersecurity experimentation.

🐧 Deploy and configure a Kali Linux virtual machine (VM) as a controlled security-testing environment.

🌐 Design and configure virtual networking to create an isolated lab environment that does not conflict with an existing physical or corporate network.

🔄 Understand NAT-based virtual networking, including how Network Address Translation enables virtual machines to access external networks while remaining separated from the physical network.

🔗 Configure and verify VM-to-VM connectivity using appropriate network settings and basic diagnostic tools.

💾 Create snapshots/restore points before making significant configuration changes or conducting experiments, allowing the lab to be safely rolled back.

🔍 Perform basic Linux system verification, including checking system information, network configuration, connectivity, services, and resource availability.

📝 Document the cybersecurity lab in a clear and reproducible manner, including VM specifications, network configuration, commands used, test results, and troubleshooting steps.

🛠️ Troubleshoot common virtualization and networking issues, such as incorrect adapter settings, IP-address conflicts, DNS problems, routing issues, and VM connectivity failures.

🏗️ **Lab Architecture**

The laboratory uses a virtualized network rather than connecting testing machines directly to the physical LAN.
The lab should provide a safe, repeatable, and isolated environment in which cybersecurity concepts can be explored without interfering with the host computer, existing physical network, or corporate infrastructure.

Host Computer → Virtualization Platform → Isolated Virtual Network → Kali Linux VM(s)

                    HOST COMPUTER
                         │
                 ┌───────┴───────┐
                 │ Virtualization │
                 │   Platform     │
                 └───────┬───────┘
                         │
                  ┌──────┴──────┐
                  │ Virtual NAT │
                  │   Network   │
                  └──────┬──────┘
                         │
                 ┌───────┴───────┐
                 │   Kali Linux  │
                 │      VM       │
                 └───────────────┘

**Network Design**

<img width="958" height="505" alt="image" src="https://github.com/user-attachments/assets/a67d8c3e-0833-4e75-9a64-6f7177c45b6e" />

The virtual network provides a controlled communication boundary for the laboratory.

The exact subnet can be customized according to the host environment. For example:

Network:     192.168.56.0/24
Gateway:     192.168.56.1
DHCP Range:  192.168.56.100 - 192.168.56.200

Note: These addresses are examples. Use a subnet that does not conflict with your existing physical or corporate network.

💻**Lab Components**

Component	Purpose
Host Operating System	Runs the virtual laboratory
VirtualBox	Provides virtualization
Kali Linux	Security testing and learning platform

Virtual NAT Network	Provides controlled virtual connectivity
VM Snapshot	Allows the environment to be restored

GitHub	Stores documentation and configuration notes

🚀 **Lab Deployment**

1. Prepare the Host
Before creating the virtual machine, make sure the host computer has sufficient resources.

Recommended baseline:

Resource	Recommended
CPU	4+ cores
RAM	8 GB+
Storage	40 GB+ free
Virtualization	Enabled in BIOS/UEFI
Internet	Required for downloads and updates

Hardware requirements may vary depending on how many virtual machines you eventually add.

2. **Install Virtualization Software**
3. 
Install Oracle VirtualBox on the host machine.

After installation, confirm that the application starts correctly.

Verify:

VirtualBox → Help → About VirtualBox

Record the installed version in your lab notes.

Example:

Virtualization Platform: VirtualBox
Version: X.X.X
Host OS: Windows/Linux/macOS

3. Obtain Kali Linux
4. 

Possible formats include:

<img width="959" height="458" alt="image" src="https://github.com/user-attachments/assets/9d78b75e-e8f9-4b69-ad8d-3a7752273af8" />

ISO installer
VirtualBox: https://virtualbox.org/wiki/Downloads

Other supported virtual machine formats
For this laboratory, using a pre-built VirtualBox image can simplify deployment.

Only download operating-system images from trusted/official sources.

**4. Import the Kali Virtual Machine**

Open VirtualBox and import the Kali appliance.

Typical workflow:

VirtualBox
   ↓
File
   ↓
Import Appliance
   ↓
Select Kali appliance
   ↓
Review hardware settings
   ↓
Import

Before starting the VM, review:

CPU allocation
Memory allocation
Virtual disk
Network adapter
USB settings
Shared folders

Avoid allocating so many host resources that the host operating system becomes unstable.

🌐 **5. Configure the Virtual Network**

The network configuration is one of the most important parts of the laboratory.

Create a dedicated virtual NAT network for the lab.

Example:

Network Name: CyberLab-NAT
CIDR:         192.168.56.0/24
DHCP:         Enabled

The important goal is to create a predictable virtual network rather than blindly copying a particular subnet.

**Why a Separate Network?**

A dedicated virtual network makes it easier to:

Identify laboratory systems.

Add additional virtual machines later.

Troubleshoot connectivity.

Rebuild the environment.

Keep experiments organized.

🖥️ **6. Configure Kali Networking**

Open the Kali VM's network configuration and attach the network adapter to the newly created virtual network.

Start Kali and inspect the available interfaces:

ip addr

You can also inspect the routing table:

ip route

Example output might resemble:

default via 192.168.56.1 dev eth0
192.168.56.0/24 dev eth0 proto kernel scope link

Your interface name and addresses may differ.

🔎 **7. Verify the Environment**

Before performing any security exercises, verify that the laboratory is functioning correctly.

Check the hostname
hostname

Check the IP configuration
ip addr

Check routing
ip route

Test the virtual gateway
ping -c 4 192.168.56.1

Test DNS resolution
ping -c 4 example.com

If external connectivity is intentionally disabled, skip the final test.

🧪 8. <img width="953" height="456" alt="image" src="https://github.com/user-attachments/assets/0258e063-71c5-494b-ad20-b823515371e0" />

CyberLab-Clean-Baseline

The baseline snapshot provides a known-good recovery point.

For example:

<img width="243" height="121" alt="image" src="https://github.com/user-attachments/assets/7f784cbe-77c8-486d-b073-fd598b24eea2" />


If an experiment damages the VM configuration, restore the baseline instead of rebuilding the entire machine.

✅ **9. Laboratory Verification Checklist**

Use the following checklist before beginning experiments.

<img width="412" height="295" alt="image" src="https://github.com/user-attachments/assets/c820a2c2-9f9f-40b8-8efb-a2e38d1cf7e2" />

 
🔧 **Troubleshooting**

Kali has no IP address
Check:

ip addr

Then inspect the network connection:

ip link

Confirm that the VirtualBox network adapter is:

Enabled
Connected
Attached to the correct virtual network
Gateway cannot be reached
Check the routing table:

ip route

Then verify the VirtualBox NAT Network configuration.

Potential causes include:

Incorrect adapter configuration

Incorrect virtual network

Disabled adapter

Conflicting subnet

Network service failure

Internet access does not work

First determine whether the problem is connectivity or DNS.

Test the gateway:

ping -c 4 192.168.56.1

Then test an external IP address if Internet access is supposed to be available.

Finally test DNS:

getent hosts example.com

This helps distinguish between:

VM → Gateway problem

and:

VM → Internet → DNS problem

VM performance is poor
Check host resource usage.

**Possible improvements:**

🧠 Increase RAM allocation if sufficient host memory exists.

⚙️ Increase CPU allocation carefully.

🧹 Close unnecessary host applications.

🔧 Ensure hardware virtualization is enabled.

🖥️ Avoid running more VMs than the host can comfortably support.

🔐 **Security Considerations**

This project is intended for authorized cybersecurity education and laboratory experimentation.

When expanding the environment:

Use systems that you own or have explicit permission to test.

Keep intentionally vulnerable machines inside the laboratory network.

Avoid exposing vulnerable VMs directly to the public Internet.

Do not reuse production credentials.

Do not store sensitive credentials in this repository.

Review network adapter settings before starting security experiments.

Recommended Isolation Model
                 INTERNET
                    │
                    X
              Avoid direct
             exposure of lab
                    │
             ┌──────┴──────┐
             │   HOST OS   │
             └──────┬──────┘
                    │
             ┌──────┴──────┐
             │ CyberLab VM │
             │   Network   │
             └─────────────┘

The laboratory should be treated as an experimental environment, not as a production network.

📸 **Evidence & Documentation**

Screenshots should demonstrate the configuration rather than simply decorate the repository.
<img width="960" height="540" alt="Screenshot 2026-09-12 122933" src="https://github.com/user-attachments/assets/7b431568-92f6-4f42-b20a-f3da4a432340" />



🧠 **Lessons Learned**
Building the laboratory demonstrates several important cybersecurity concepts.

**Virtualization is more than running another operating system**

A virtual machine provides an isolated environment where configurations can be changed and restored without necessarily affecting the host.

**Network design matters**
Security experiments depend heavily on understanding how systems communicate.

Knowing the difference between:

Host Network
Virtual NAT
Bridged Networking
Host-Only Networking

is essential when building security labs to:

**Documentation is part of cybersecurity**
A lab that cannot be reproduced is difficult to troubleshoot, maintain, or improve.

🔭 **Future Improvements**
The laboratory can be expanded into a larger cybersecurity environment.

Potential additions include:

🐧 Additional Linux machines

🪟 Windows evaluation VM

🎯 Intentionally vulnerable machines

📊 SIEM/logging server

🔍 Network monitoring

🛡️ Firewall/router VM

🧪 Malware-analysis sandbox

📡 Packet-capture environment

🔐 Active Directory practice environment

A possible future architecture:

<img width="347" height="242" alt="image" src="https://github.com/user-attachments/assets/48886fbd-001b-4c66-96b9-8624fe8fc2b9" />


👤 **Project Status/**

Status: 🟢 Active Development

Environment: Virtualized Cybersecurity Laboratory

Primary Platform: Kali Linux

Virtualization: VirtualBox

🔐 Security & Ethical Use

Purpose: Cybersecurity education and practical laboratory development

🔗 **Tools & Resources**

7-Zip: https://7-zip.org/download.html

VirtualBox: https://virtualbox.org/wiki/Downloads

Kali Linux: https://kali.org/get-kali

👤 Author

**ASANDA LLOYD NYUSWA**

Cybersecurity Professional **B083F**

⭐ **Final Goal**
The goal of CyberLab Blueprint is not simply to install Kali Linux.

It is to build a repeatable cybersecurity environment where new technologies, configurations, defensive controls, and security concepts can be tested safely.

Build it. Break it. Restore it. Learn from it.


