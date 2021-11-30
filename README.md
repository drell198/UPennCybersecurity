# UPennCybersecurity
UPenn Cybersecurity Bootcamp
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![~/UpennCybersecurity/Diagrams/Project1Diagram.drawio]

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook (.yml) file may be used to install only certain pieces of it, such as Filebeat.

  - pentest.yml
  - install-elk.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- A load balancer receives any traffic that comes into the webiset and distributes it across multiple webservers. A jump box is used as an origination point for admins to connect to before launching any administrative task.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat logs information about the file system, including which files have changed and when. Filebeat helps generate and organize log files to send to Logstash and Elasticsearch.
- Metricbeat records metrics and statistical data from the operating system and from services running on the server.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| JumpBoxProvisioner | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Web Server - Docker - DVWA      | 10.0.0.7   | Linux    |
| Web-2    | Web Server - Docker - DVWA      | 10.0.0.8   | Linux    |
| ELKVM    | ELK Stack         | 10.1.0.4           | Linux          |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 76.124.166.85
- 71.185.213.147

Machines within the network can only be accessed by SSH.
- The jump box was the only machine that could access the ELKVM through SSH. Its IP address is 20.115.5.99.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBoxProvisioner| No    | 76.124.166.85, 71.185.213.147    |
| Web-1    | Yes    | 20.124.225.108 LB-IP, 10.0.0.4 - JumpBox |
| Web-2    | Yes    | 20.124.225.108 LB-IP, 10.0.0.4 - JumpBox |
| ELKVM    | No     | 10.0.0.4 - JumpBox, 76.124.166.85, 71.185.213.147 (Port 5601) |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration with Ansible is that we can deploy multiple servers without having to physically touch each server.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Increase VM memory
- Download and Configure old docker container
- Set published ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![~/UpennCybersecurity/Ansible/dockerps.png](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.7
- Web-2 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat logs information about the file system, including which files have changed and when. Filebeat helps generate and organize log files to send to Logstash and Elasticsearch.
- Metricbeat records metrics and statistical data from the operating system and from services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible.
- Update both of the configuration files to include the private IP of the ELK-Server to the ElasticSearch and Kibana sections of the Configuration file.
- Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.

- _Which file is the playbook?
  - pentest.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml
- Where do you copy it?_
  - /etc/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine?
  - /etc/ansible/hosts.cfg
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
  - In the /etc/ansible/hosts file you specify it
- _Which URL do you navigate to in order to check that the ELK server is running?
  - http://(ELKVM-IP):5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

- ssh
- docker container list -a
- docker start
- docker attach
- ansible-playbook (playbook) - runs the playbook
