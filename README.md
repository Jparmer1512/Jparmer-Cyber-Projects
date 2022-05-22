## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(https://github.com/Jparmer1512/Jparmer-Cyber-Projects/blob/main/Diagrams/Elk%20Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the  may be used to install only certain pieces of it, such as Filebeat.

- My-Playbook.yml- Installs DVWA Servers
- Elk-Playbook.yml- Installs the Elk Server
- Filebeat-playbook.yml- Installs and condfigures Filebeat on Elk and DVWA servers
- Metricbeat-playbook.yml- Installs and configures Metricbeat on Elk and DVWA servers
  
This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secured, in addition to restricting external access to the network.
- Load Balancing ensures the web servers are available which enforces the Availability portion of the CIA Triad.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat watches for logs and events in specified locations and forwards them to Elasticsearch
- Metricbeat records metrics and statistical data from the operating system and services running on the server

The configuration details of each machine may be found below.

| Name     | Function               | IP Address  | Operating System |
|----------|------------------------|-------------|------------------|
| Jump Box | Gateway                | 20.70.72.164| Linux            |
| Web-1    | Web Server-Docker-Dvwa | 10.0.0.5    | Linux            |
| Web-2    | Web Server-Docker-Dvwa | 10.0.0.6    | Linux            |
| Elk Svr  | ELK Stack              | 10.1.0.4    | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address

Machines within the network can only be accessed by SSH.
- The ELK Server can only be accessed using SSH from the Jump-Box-Provisioner and from my Personal IP address

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible    | Allowed IP Addresses                                       |
|----------|------------------------|------------------------------------------------------------|
| Jump Box | No                     | Personal IP Address                                        |
| Web-1    | Through Load balancer  | 52.243.82.194 Load Balancer Public IP/ 10.0.0.4 Jumpbox IP |
| Web-2    | Through Load balancer  | 52.243.82.194 Load Balancer Public IP/ 10.0.0.4 Jumpbox IP |
| ELK SVR  | No                     | SSH 10.0.0.4 Jumpbox HTTP Port 5601 Personal IP            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible can configure multiple programs onto multiple machines. The alternative is deploying each machine individually and configuring it manually. That is a time and resource consuming process.

The playbook implements the following tasks:
-Install Docker.io and Pip3
- Increases VM memory
- Downloads and configures Elk docker container
- Sets available ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(https://raw.githubusercontent.com/Jparmer1512/Jparmer-Cyber-Projects/main/Diagrams/Docker.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
-Filebeat watches for logs and files in specified locations to collect and forward log events.
-MetricBeat records metrics adn statistical data from the OS and services running on the machine.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml files to /etc/ansible/files.
- Update the configuration file to include the Name and Private IP of the ELK-Server to the Elasticsearch and Kibaba sections of the config files
- Run the playbook, and navigate to your ELK-Servers Public IP:5601/app/kibaba to check that the installation worked as expected.

- Elk-Playbook.yml- Installs the Elk Server
   -Filebeat-playbook.yml- Installs and condfigures Filebeat on Elk and DVWA servers
   -Metricbeat-playbook.yml- Installs and configures Metricbeat on Elk and DVWA servers
- Copy these files into the /etc/ansible directory
- Update this file etc/ansible/hosts.cfg to include the machines you want to use this service
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- In the hosts.cfg file, you specify which groups get each resource.
- Navigate to the public ip of the ELK Machine.  http://(ELK-IP-ADDRESS):5601

Specific commands to run the ansible configuration for the Elk-Server
- ssh azadmin@Jumpbox IP address
- sudo docker start [containername]
- sudo docker attach [containername]
- cd /etc/ansible
- ansible-playbook Elk-playbook.yml (installs and configures server)
- ansible-playbook filebeat-playbook.yml (installs and configures filebeat)
- ansible-playbook metricbeat-playbook.yml (installs and configures metricbeat)
- Elk-Server-IP-ADDRESS:5601/app/kibana in a browser window to open the kibana GUI. 
