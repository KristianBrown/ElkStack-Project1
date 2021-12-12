# ElkStack-Project1
OSU Bootcamp ElkStack Project 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![AzureNetworkDiagram](https://user-images.githubusercontent.com/95951046/145700747-0cec99fc-d500-4fe3-be6a-c204e5e01a0f.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly adaptive, in addition to restricting transit to the network.

- What aspect of security do load balancers protect?
  - The off-loading function of load balancers help to defend against distributed denial-of-service (DDoS) attacks.

- What is the advantage of a jump box?
  - The advantage of jump boxes is that they are secure machines that are capable of connecting to other servers or even untrusted environments. 


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- What does Filebeat watch for?
  - Filebeat monitors log files and checks the file system for changes. It collects log events and then ships the data to Elasticsearch or Logstash for processing. 

- What does Metricbeat record?
  - Metricbeat records metrics and statistics from the operating system and from services running on different servers. 


The configuration details of each machine may be found below.

| Name     | Function   | IP Address | Operating System     |
| -------- | ---------- | ---------- | -------------------- |
| Jump Box | Gateway    | 10.0.0.4   | Linux (ubuntu 18.04) |
| Web-1    | Web Server | 10.0.0.5   | Linux (ubuntu 18.04) |
| Web-2    | Web Server | 10.0.0.6   | Linux (ubuntu 18.04) |
| Web-3    | Web Server | 10.0.0.7   | Linux (ubuntu 18.04) |
| ELKStack | ELK Server | 10.1.0.4   | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses: The Public IP of my personal host machine 24.154.69.16 is allowed access to the Jumpbox machine

Machines within the network can only be accessed by SSH via the Jumpbox machine.
- Which machine did you allow to access your ELK VM? What was its IP address?
  - The Jumpbox machine is allowed access to the ELK VM. The private IP of the Jumpbox is 10.0.0.4. 


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses   |
| -------- | ------------------- | ---------------------- |
| Jump Box | NO                  | 24.154.69.16           |
| Web-1    | NO                  | 10.0.0.4               |
| Web-2    | NO                  | 10.0.0.4               |
| Web-3    | NO                  | 10.0.0.4               |
| ELKStack | NO                  | 24.154.69.16, 10.0.0.4 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
  - Ansible allows you to spin up multiple servers and vms using a single playbook file with the same configuration. 


The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install docker module
- Increase virtual memory
- Download and launch docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(https://user-images.githubusercontent.com/95951046/145700776-323a0b1d-d5fe-49cc-a179-860c1ed0b243.PNG)
G)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring: Web-1(10.0.0.5), Web-2(10.0.0.6), Web-3(10.0.0.7)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat - collects log events for changes made against the file system.
- Metricbeat - collects metric and statistics data from the vms.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible directory.
- Update the configuration file to include the webserver and elk vm IP addresses. 
- Run the playbook, and navigate to ELK vm to check that the installation worked as expected.

Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it?
  - /etc/ansible/files/filebeat-config.yml

- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
  - Edit the /etc/ansible/hosts file to either include the ELK Server ip address or the Webservers ip addresses.

- Which URL do you navigate to in order to check that the ELK server is running?
  - The url you will want to navigate to is http://[ELKvm-external-IP]:5601/app/kibana


As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

1. SSH into your Jumpbox VM
2. Run these commands to connect to your container
   1. sudo docker container list -a
   2. sudo docker start container (name of the container)
   3. sudo docker attach container (name of the container)
3. CD into /etc/ansible
4. sudo ansible-playbook (specific playbook you want to run/update)
5. When ran, the playbook will be applied to the specified machines in the hosts file

Your end result will be a fully functioning ELK Stack Server:

[ELKStackmainpage](https://user-images.githubusercontent.com/95951046/145700798-4748a987-298c-44f4-912b-d5164cffaa4c.PNG)


