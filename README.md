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

## How to execute these playbooks?

### High-Level FlashStack Automation
<img width="1200" alt="Screen Shot 2022-09-15 at 5 03 58 PM" src="https://user-images.githubusercontent.com/25094641/190393678-6cafd996-fae2-4553-8f23-12cbe1c11293.png">

<br />
<br />


###  FlashStack Automated Deployment Workflow
<img width="700" src="https://user-images.githubusercontent.com/3585414/144469881-a647e3fa-f48e-411c-b13c-822bfb9a15ea.png">
<br />
<br />


### Set up the execution environment
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

### Intersight Access Requirement

To execute the playbooks against your Intersight account, you need to complete following additional steps of creating an API key and saving the Secrets_File:

https://community.cisco.com/t5/data-center-and-cloud-documents/intersight-api-overview/ta-p/3651994

The API key and Secrets_Filename information is added to the group_vars/all.yml. The default Secrets_File value in all.yml assumes Secrets_File was copied to the same folder/directory where Ansible Playbooks were cloned (alongside inventory file).

<br />

### Setting up Variables

All the variables used in this framework are defined in the following locations:

1. Variable that require customer inputs are part of group_vars/all.yml
2. Variable that do not typically require customer input (e.g. descriptions etc.) are present under role_name/defauls/main.yml.
   Setup all the variables before executing the playbooks as detailed in the CVD. Intersight's pools and policies created using these playbooks are tagged with user_defined_prefix and "ansible" to easily filter the configuration.

<br />


### Playbook Execution Commands

1.	Setup Pools in Intersight: `ansible-playbook ./create_pools.yml -i inventory`
2.	Setup Policies in Intersight: `ansible-playbook ./create_server_policies.yml -i inventory`
3.	Setup Server Profile Template(s) in Intersight: `ansible-playbook ./create_server_profile_template.yml -i inventory`
4.	Setup LAN on Nexus: `ansible-playbook ./Setup_Nexus.yml -i inventory`
5.	Setup MDS: `ansible-playbook ./Setup_MDS.yml -i inventory`
6.	Setup Pure FlashArray: `ansible-playbook ./Setup_Pure.yml -i inventory`
7.	Setup VMWare ESXi servers: `ansible-playbook ./Setup_ESXi.yml -i inventory`
8.	Setup VMWare Cluster and vCenter Setup: `ansible-playbook ./Setup_vCenter.yml -i inventory`

<br />


### Post Configuration Tasks

Execution of first three playbooks in these repositories set up Server Profile Template in Intersight. After successfully executing the playbooks, one or more server profiles can easily derived and attached to the compute node from Intersight dashboard. KVM mounted DVD option is available to install OS to these newly derived servers.

<br />
