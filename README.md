## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


<br>

![](diagrams/Azure%20Resource%20Group%20Diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

- [filebeat-config](ansible/filebeat-config.yml)
- [filebeat-playbook](ansible/filebeat-playbook.yml)
- [metricbeat-config](ansible/metricbeat-config.yml)
- [metricbeat-playbook](ansible/metricbeat-playbook.yml)<br>


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

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system configuration.
- Filebeat monitors log files and/or specified locations for fowarding to Elasticsearch.
- Metricbeat collects system metrcis and statistics.

The configuration details of each machine may be found below:

| Name       | Function           | IP Address | Operating System |   |
|------------|--------------------|------------|------------------|---|
| Jump Box   | Gateway            | 10.0.0.4   | Ubuntu 18.04     |   |
| Web-1      | Traffic Monitoring | 10.0.0.5   | Ubuntu18.04      |   |
| Web-2      | Traffic Monitoring | 10.0.0.6   | Ubuntu 18.04     |   |
| Elk Server | Data Analytics     | 10.2.0.4   | Ubuntu 18.04     |   |
<br>


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- White Listed public IP Address

Machines within the network can only be accessed by SSH connections from the JumpBox.
- Jump box ansible containers 10.0.0.4

A summary of the access policies in place can be found in the table below:

| Name       | Publicly Accessible | Allowed IP addresses  |
|------------|---------------------|-----------------------|
| Jump Box   | Yes                 | ssh from whitelist IP |
| Web -1     | No                  |                       |
| Web -2     | No                  |                       |
| Elk Server | Yes                 | ssh from whitelist IP |
<br>

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because scripting allows for multiple VMs to be spun up at the same time

The playbook implements the following tasks:
- Install Docker.io
- Install Pip3
- Install Docker Python
- Configure Sysctl modeules
- Enables docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance:

![ELK Docker ps](images/Elk%20docker%20ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeats collects file system data
- Metricbeats collects data related to the system and services

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml files to the ansible container.
- Update the configuration files to include the correct IP address for the Elk Server (10.2.0.4:5601 and 10.2.0.4:9200)
- Run the playbooks and navigate to the GUI of the Elk Server (current public IP) to check that the installation worked as expected.

- The filebeat-playbook.yml and metricbeat-playbook.yml playbook files should both be located in the /etc/ansible/roles directory.
- The filebeat-config.yml and metricbeat-config.yml files can be updated to make Ansible run the playbook on a specific machine. The IP address and port numbers specified in the config file determine which machines ELK and filebeat are installed on.

- Also updated the hosts files to include the Web-1, Web-2 and Elk Server IPs and python information

- Also updated the ansible.cfg to specify the correct remote_user
- Use the following URL to verify the ELK server is running:

       http://<public ELK IP address>:5601/app/kibana#/home

The following commands are used to download and update the files:

- ansible-playbook filebeat-playbook.yml
- ansible-playbook metricbeat-playbook.yml