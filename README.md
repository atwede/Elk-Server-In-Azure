# Elk-Server-In-Azure
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img src="https://github.com/atwede/Elk-Server-In-Azure/blob/main/Diagrams/Azure%20Network%20Diagram.png" alt="Network">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

[install-elk.yml](https://github.com/atwede/Elk-Server-In-Azure/blob/main/Ansible/install-elk.yml)

[filebeat-config.yml](https://github.com/atwede/Elk-Server-In-Azure/blob/main/Ansible/filebeat-config.yml)

[metricbeat-config.yml](https://github.com/atwede/Elk-Server-In-Azure/blob/main/Ansible/metricbeat-config.yml)

[filebeat-playbook.yml](https://github.com/atwede/Elk-Server-In-Azure/blob/main/Ansible/filebeat-playbook.yml)

[metricbeat-playbook.yml](https://github.com/atwede/Elk-Server-In-Azure/blob/main/Ansible/metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancers help safeguard availability, protect against DDoS attacks, and can also increase the capacity of applications.
- The advantage of a jump box is that it is a monitored device that can control access between the internet and machines connected to it. It increases security and creates network segmentation.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- Filebeat watches for system logs.
- Metricbeat records metrics and system resources usage.

The configuration details of each machine may be found below.

| Name     | Function            | IP Address | Operating System |
|----------|---------------------|------------|------------------|
| Jump Box | Gateway             | 10.0.0.4   | Linux            |
| Web1     | Web Server          | 10.0.0.8   | Linux            |
| Web2     | Web Server          | 10.0.0.9   | Linux            |
| ELK      | ElasticSearch Stack | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 136.35.164.216

Machines within the network can only be accessed by the jumpbox.
- I allowed the Jumpbox to access the ELK server. Its public IP is 40.87.103.196 and its private IP is 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses  |
|----------|---------------------|-----------------------|
| Jump Box | Yes, SSH, Port 22   | Workstation Public IP |
| Web1     | No                  | 20.124.32.30          |
| Web2     | No                  | 20.124.32.30          |
| Web LB   | Yes, HTTP, Port 80  | ALL                   |
| ELK      | Yes, TCP, 5601      | Workstation Public IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this process of configuration can be replicated across any number of machines by anyone with access to the playbook. Ansible
allows for tasks to be listed out in a yml file, and Ansible will then determine from the playbook how to setup your system to your desires.

The playbook implements the following tasks:
- Install Docker: This install docker code used to build containers.
- Install Python3.pip: This allows for more modules to be installed.
- Docker Module: Alerts PIP to install important docker component modules.
- Increase and Use More Memory: This frees up more memory that the Elk Docker image can use so the server works properly. 
- Download and Launch ELK Container: This downloads and initializes the Elk Docker container with specified ports being published.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img src="https://github.com/atwede/Elk-Server-In-Azure/blob/main/Images/ELK-Server%20container.PNG" alt="Container">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.8
- 10.0.0.9

We have installed the following Beats on these machines:
 We have successfully installed Filebeat and Metricbeat on Web1, Web2.

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to collect log events which we can use for analyzing system usage and event management.
- Metricbeat collects metrics and system statistics which can give us more information on network traffic and how it impacts our networked machines.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles/elk_install.yml.
- Update the hosts file to include the filebeat installer. You can do this by running the following command:
  curl  https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb
- Run the playbook, and navigate to http://[your_elk_server_ip]:5601/app/kibana to check that the installation worked as expected.
