# FlashStack Virtual Server Infrastructure for End-to-End 100 Gigabit with Cisco UCS X-Series and Cisco UCS 5th Generation Fabric Technology

This repository  contains Ansible playbooks to configure all the components of FlashStack including: <br />
&emsp;&emsp; •	 Cisco UCS in Intersight Managed Mode (IMM) <br />
&emsp;&emsp; •	 Cisco Nexus and MDS Switches <br />
&emsp;&emsp; •	 Pure FlashArray   <br />
&emsp;&emsp; •	 VMware ESXi and VMware vCenter.  <br />

This repository can be used to automate the Virtual Server Infrastrcutre Deployment incorporating the Cisco Unified Computing System™ (Cisco UCS®) **X-Series modular platform**, Cisco Unified Computing System™ **5th Generation Fabric Technology** (5th Generation Fabric Interconnects 6536, 5th Generation Cisco UCS Virtual Interface Card and X9108-IFM-100G IFM) into the FlashStack Virtual Server Infrastructure (VSI) to enable end-to-end 100G Ethernet and 32G Fibre Channel. 

Details are covered in the following Cisco Validated Design (CVD): 

The CVD lays out the complete process for configuring the FlashStack using Ansible. Since these playbooks are intended to save time in setting up a working FlashStack, a complete FlashStack as shown below is needed to execute the playbooks. 

## FlashStack - Physical Topologies

IP connectivity             |  FC connectivity
:-------------------------:|:-------------------------:
![](https://user-images.githubusercontent.com/25094641/190374265-daef542b-cdc6-40f6-9c7a-6cf76f99bbe2.jpg)  |  ![](https://user-images.githubusercontent.com/25094641/190374304-b505b0e6-1011-4312-aca8-3d729d7fa1c4.jpg)

<br />
<br />

## How to execute these playbooks?

### High-Level FlashStack Automation

![image](https://user-images.githubusercontent.com/3585414/144472418-e5559aad-88bc-4ceb-a10c-c25f4fab8a53.png)
<br />
<br />


###  FlashStack Automated Deployment Workflow

![image](https://user-images.githubusercontent.com/3585414/144469881-a647e3fa-f48e-411c-b13c-822bfb9a15ea.png)
<br />
<br />


## Set up the execution environment
To execute various ansible playbooks, a Linux based system will need to be setup as described in the CVD with the packages listed at the following pages: <br />
 •	Cisco Intersight: https://galaxy.ansible.com/cisco/intersight <br />
 •	Cisco NxOS: https://galaxy.ansible.com/cisco/nxos <br />
 •	Pure FlashArray: https://galaxy.ansible.com/purestorage/flasharray <br />
 •	VMware: https://galaxy.ansible.com/community/vmware <br />
 
 You might already have this collection installed. 

- To check whether it is installed, run: `ansible-galaxy collection list`
- To install it, use: <br />
- `ansible-galaxy collection install cisco.intersight` (For Intersight Collection) <br />
`ansible-galaxy collection install cisco.nxos` (For Cisco NX-OS collection)  <br /> 
`ansible-galaxy collection install purestorage.flasharray` (Pure Storage FlashArray Collection) <br />
`ansible-galaxy collection install community.vmware` (For VMWare Ansible Collection) <br />
 
<br />

### Playbook Execution Commands – Summary:
Setup all the variables before executing the playbooks as detailed in the CVD: https://www.cisco.com/c/en/us/td/docs/unified_computing/ucs/UCS_CVDs/flashstack_vSphere7.0U2.html

1.	Setup LAN on Nexus and UCS: "ansible-playbook ./Setup_Nexus.yml -i inventory"
2.	Setup Pure FlashArray Initial Config - Optional: "ansible-playbook ./Setup_Pure.yml -i inventory"
3.	Setup Cisco UCS: "ansible-playbook ./Setup_UCS.yml -i inventory"
4.	Setup Pure FlashArray: "ansible-playbook ./Setup_MDS.yml -i inventory"
5.	Setup Pure FlashArray: "ansible-playbook ./Setup_Pure.yml -i inventory"
6.	Setup VMWare ESXi servers: "ansible-playbook ./Setup_ESXi.yml -i inventory"
7.	Setup VMWare Cluster and vCenter Setup: "ansible-playbook ./Setup_vCenter.yml -i inventory"	
