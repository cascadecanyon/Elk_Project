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

Machines within the network can only be accessed by Jump-Box-Provisioner (IP 10.0.0.4)
- The Jump Box can access the ELK VM using SSH.  The Elk's VM IP address is 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump Box             | Yes                 | My IP Address (ssh)  |
| Elk-stack            | Yes                 | My IP Address (ssh)  |
| Web-1                | No                  | 10.0.0.5             |
| Web-2                | No                  | 10.0.0.6             |
| Web-3                | No                  | 10.0.0.7             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous 
because it allows a configuration that is consistent and predictable. Automation allows for setup and deployment to be created and implemented in a timely manner. Ansible is a very flexible and powerful deployment that can model the most complex IT workflows. Because it does not require any extra software, the user is left with more server space for applications.

The playbook implements the following tasks:
- Install Elk-Docker container
- Increase VM memory in configuration file
- Install Docker Python module
- Create playbook to launch container
- Run playbook to launch the container

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.
![Elkm_Docker](https://user-images.githubusercontent.com/82729821/138626071-312e6f99-0260-453b-a2c8-d0e80785b11b.png)
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1: 10.0.0.5  
- Web 2: 10.0.0.6 
- Web 3: 10.0.0.7
- We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- **Filebeat**  - Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for preperation to be displayed in a graphical interface called  Kibana. (ELK)
- **Metricbeat** - Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server. This also is rendered and displayed in Kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

- SSH into the control node and follow the steps below:
- Copy the playbook files to Ansible Docker Container.
- Update the Ansible hosts file `/etc/ansible/hosts` to include the following: 

```
[webservers]
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3
10.0.0.7 ansible_python_interpreter=/usr/bin/python3

[elkserver]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3
```

- Update the Ansible configuration file `/etc/ansible/ansible.cfg` and set the remote_user parameter to the admin user of the web servers.

#### Running the Playbooks
1. Start an ssh session with the Jump Box `~$ ssh username@<Jump Box Public IP>`
2. Start the Ansible Docker container `~$ sudo docker start <Ansible Container>`
3. Attach a shell to the Ansible Docker container with the command `~$ sudo docker attach <Ansible Container Name>`
4. Run the playbooks with the following commands:
	* `ansible-playbook /etc/ansible/dvwa-playbook.yml`
	* `ansible-playbook /etc/ansible/Install-Elk.yml`
	* `ansible-playbook /etc/ansible/roles/Filebeat-playbook.yml`

- `Install_Elk.yml` configures only the server(s) listed as `[elkserver]` in `/etc/ansible/hosts`
- `Filebeat-playbook.yml` configures the servers listed as `[webservers]` in `/etc/ansible/hosts`

- After running the playbooks, go to Kibana to check that the installation was successful by viewing Filebeat and Metricbeat data     and reports in the Kibana Dashboard
- Kibana can be accessed at [http://\<Elk-server-ip\>:5601/app/kibana]()
