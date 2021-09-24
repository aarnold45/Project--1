# Project--1

![](/Linux/Elk-Stack.png)

![](/Linux/Bonus-Command-to-install-chkrootkit.png)

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](/Diagrams/Elk-Stack.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate 
the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain 
pieces of it, such as Filebeat.
- _TODO: Enter the playbook file._

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
|ELK Server| Server   | 10.1.0.5  |Linux (Ubuntu 18.04 LTS) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 13.82.216.121

Machines within the network can only be accessed by Jump Box
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Personal IP Address  |
|  Web-1   | No                  |      10.0.0.4        |
|  Web-2   | NO                  |      10.0.0.4        |
|ELK Server| No                  |      10.0.0.4        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: The main advantage of automating the installation process is that we could deploy multiple servers easily and quickly without having to physically touch each server.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

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
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

•Filebeat is a log data shipper for local files. Installed as an agent on your servers, Filebeat monitors the log directories or specific log files, tails the files, and forwards them either to Elasticsearch or Logstash for indexing.
 An examle of such are the logs produced from the MySQL database supporting our application.

•Metricbeat collects metrics and statistics on the system. An example of such is cpu usage, which can be used to monitor the system health.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

