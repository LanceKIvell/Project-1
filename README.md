## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


<br>

![](diagrams))

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

- [filebeat-config](ansible/filebeat-config.yml)
- [filebeat-playbook](ansible/filebeat-playbook.yml)
- [metricbeat-config](ansible/metricbeat-config.yml)
- [metricbeat-playbook](ansible/metricbeat-playbook.yml)<br>


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly ____available_, in addition to restricting __access___ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _network____ and system _configuration____.
- _TODO: What does Filebeat watch for?_
- _TODO: What does Metricbeat record?_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function           | IP Address | Operating System |   |
|------------|--------------------|------------|------------------|---|
| Jump Box   | Gateway            | 10.0.0.4   | Ubuntu 18.04     |   |
| Web-1      | Traffic Monitoring | 10.0.0.5   | Ubuntu18.04      |   |
| Web-2      | Traffic Monitoring | 10.0.0.6   | Ubuntu 18.04     |   |
| Elk Server | Data Analytics     | 10.2.0.4   | Ubuntu 18.04     |   |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_Jump box ansible containers 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP addresses  |
|------------|---------------------|-----------------------|
| Jump Box   | Yes                 | ssh from whitelist IP |
| Web -1     | No                  |                       |
| Web -2     | No                  |                       |
| Elk Server | Yes                 | ssh from whitelist IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_ Allows for multiple VMs to be spun up at the same time

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...Install Docker.io
Install Pip3
Install Docker Python
Configure Sysctl modeules
Enables docker service on boot
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Docker ps](images/Elk%20docker%20ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: Web-1 10.0.0.5
Web-2 10.0.0.6_

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeats collects file system data
- Metricbeats collects data related to the system and services

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __filebeat-config.yml and metricbeat-config.yml___ file to _ansible container____.
- Update the __configuration___ files to include the correct IP address for the Elk Server (10.2.0.4:5601 and 10.2.0.4:9200)
- Run the playbooks, and navigate to __GUI of the Elk Server (currect public IP)__ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_filebeat-playbook.yml and metricbeat-playbook.yml both located in the /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine?filebeat-config.yml and metricbeat-config.yml How do I specify which machine to install the ELK server on versus which to install Filebeat on?_The IP address and port numbers are specified in the config file.

Also updated the hosts files to include the Web-1, Web-2 and Elk Server IPs and python information

Also updated the ansible.cfg to specify the correct remote_user
- _Which URL do you navigate to in order to check that the ELK server is running? 
 http://<public ELK IP address>:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

ansible-playbook filebeat-playbook.yml
ansible-playbook metricbeat-playbook.yml