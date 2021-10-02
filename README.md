## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](/Linux/Elk-Stack.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate 
the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain 
pieces of it, such as Filebeat.


•Elk install 


•Metricbeat playbook


•Filebeat playbook


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load balancers help ensure environment availability through distribution of incoming data to web servers. Jump boxes allow for more easy administration of multiple systems and provide an additional layer between the outside and internal assets.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system metrics.
 
• Filbeats watch for log directories or specific log files.

• Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System       |
|----------|----------|------------|------------------------|
| Jump Box | Gateway  | 10.0.0.4   |Linux (Ubuntu 18.04 LTS)|
| Web 1    | Server   | 10.0.0.5   |Linux (Ubuntu 18.04 LTS)|
| Web 2    | Server   | 10.0.0.6   |Linux (Ubuntu 18.04 LTS)|
|ELK Server| Server   | 10.1.0.5   |Linux (Ubuntu 18.04 LTS)|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 13.82.216.121

Machines within the network can only be accessed by Jump Box

- _ Which machine did you allow to access your ELK VM? What was its IP address?Jump Box 10.0.0.4


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Personal IP Address  |
|  Web-1   | No                  |      10.0.0.4        |
|  Web-2   | NO                  |      10.0.0.4        |
|ELK Server| No                  |      10.0.0.4        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _ The main advantage of automating the installation process is that we could deploy multiple servers easily and quickly without having to physically touch each server.
    In case we need to configure more machines,we can just run the ansible playbook instead of going to every machine and configuring individually.

The playbook implements the following tasks:

•Installs docker.io, pip3, and the docker module.

•Increases the virtual memory for the virtual machine we will use to run the ELK server

•Download and Configure elk docker container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](/Linux/docker-ps.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

•Web 1 10.0.0.5

•Web 2 10.0.0.6

We have installed the following Beats on these machines:
 
•Filebeat

•Metricbeat

These Beats allow us to collect the following information from each machine:

•Filebeat is a log data shipper for local files. Installed as an agent on your servers, Filebeat monitors the log directories or specific log files, tails the files, and forwards them either to Elasticsearch or Logstash for indexing.
 An examle of such are the logs produced from the MySQL database supporting our application.

•Metricbeat collects metrics and statistics on the system. An example of such is cpu usage, which can be used to monitor the system health.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

•Copy the configuration file from your Ansible container to your Web VM's

•Update the /etc/ansible/hosts file to include the IP address of the Elk Server VM and webservers.

•Run the playbook, and navigate to http://51.143.21.166:5601/app/kibana to check that the installation worked as expected.

•Which file is the playbook? The Filebeat-configuration

•Where do you copy it? copy /etc/ansible/files/filebeat-config.yml to /etc/filebeat/filebeat.yml

•Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? update filebeat-config.yml -- specify which machine to install by updating the host files with ip addresses of web/elk servers and selecting which group to run on in ansible



_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

  -------Filebeat---------

- To create the filebeat-configuration.yml file: nano filebeat-configuration.yml. For this, I used the filebeat configuration file template.

- To create the playbook: nano filebeat-playbook.yml

  ---
 - name: installing and launching filebeat
	   hosts: webservers
       become: true
       tasks:

	   - name: download filebeat deb
  	     command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.7.1-amd64.deb

	   - name: install filebeat deb
  	     command: dpkg -i filebeat-7.7.1-amd64.deb

	   - name: drop in filebeat.yml
  	     copy:
   	       src: ./files/filebeat-configuration.yml
   	       dest: /etc/filebeat/filebeat.yml

	   - name: enable and configure system module
  	     command: filebeat modules enable system

	   - name: setup filebeat
  	     command: filebeat setup

	   - name: start filebeat service
  	    command: service filebeat start
---
-To run the playbook: ansible-playbook filebeat-playbook.yml

* In order to run the playbook, you have to be in the directory the playbook is at, or give the path to it (ansible-playbook /etc/ansible/roles/filebeat-playbook.yml


-------Metricbeat-------

- To create the metricbeat-configuration.yml file: nano metricbeat-configuration.yml. For this, I used the metricbeat configuration file template.

- To create the playbool: nano metricbeat-playbook.yml

---
  - name: installing and lunching metricbeat
    hosts: webservers
    become: true
    tasks:
    
  - name: download metricbeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.7.1-amd64.deb
    
  - name: install metricbeat deb
    command: sudo dpkg -i metricbeat-7.7.1-amd64.deb
    
  - name: drop in metricbeat.yml
    copy:
      src: /etc/ansible/roles/files/metricbeat-configuration.yml
      dest: /etc/metricbeat/metricbeat.yml
      
   - name: enable and configure system module
     command: metricbeat modules enable system
     
   - name: setup metricbeat
     command: metricbeat setup
     
   - name: start metricbeat service
     command: service metricbeat start
     
   ---
   
   - To run the playbook: ansible-playbook metricbeat-playbook.yml
   
   * To order to run the playbook, you have to be in the directory the playbook is at, or give the path to it (ansible-playbook /etc/ansible/roles/metricbeat-playbook.yml


   