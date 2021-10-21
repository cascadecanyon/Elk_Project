William English

# Automated Elk Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Topology](https://github.com/cascadecanyon/Elk_Project/blob/main/Images/Elk-Stack_Diagram.png)
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the file may be used to install only certain pieces of it, such as Filebeat.

  - [Elk-Stack Deployment files](https://github.com/cascadecanyon/Elk_Project/tree/main/Ansible)


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Playbooks


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

The configuration details of each machine may be found below.

| Name                 | Function           | Private IP Address | Public IP Address | Operating System |
|----------------------|--------------------|--------------------|-------------------|------------------|
| Jump-Box-Provisioner | Gateway            | 10.0.0.4           | 13.88.30.70       | Ubuntu LTS 18.04 |
| Web-1                | Application Server | 10.0.0.5           | 13.88.62.8        | Ubuntu LTS 18.04 |
| Web-2                | Application Server | 10.0.0.6           | 13.88.62.8        | Ubuntu LTS 18.04 |
| Web-3                | Application Server | 10.0.0.7           | 13.88.62.8        | Ubuntu LTS 18.04 |
| Elk-Mountain         | ELK Stack          | 10.1.0.4           | 52.168.138.115    | Ubuntu LTS 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner and ELK Stack (Kibana) machines can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
'My IP'

Machines within the network can only be accessed by Jump-Box-Provisioner.

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump Box             | Yes                 | My IP Address        |
| Elk-stack            | Yes                 | My IP Address        |
| Web-1                | No                  | 10.0.0.4             |
| Web-2                | No                  | 10.0.0.4             |
| Web-3                | No                  | 10.0.0.4             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous 
because it allows a configuration that is consistent and predictable. Automation allows for setup and deployment to be created and implemented in a timely manner. Ansible is a very flexible and powerful deployemnt that can model the most complex IT workflows. Because it does not require any extra software, the user is left with more server space for applications.

The playbook implements the following tasks:
- Install Elk-Docker container
- Increase VM memory in configuration file
- Install Docker Python module
- Create playbook to launch container
- Run playbook to launch the container

