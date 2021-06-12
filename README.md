# project-1
![Cloud_Diagram](https://user-images.githubusercontent.com/85802280/121785582-77ffe700-cb6f-11eb-8036-db4bdeaa52f5.png)
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.
This document contains the following details:

Description of the Topology

Access Policies

ELK Configuration

Beats in Use
Machines Being Monitored
How to Use the Ansible Build

Description of the Topology

The load balancer aids in security by offloading traffic from a corporate server to a public cloud provider. Integrating an ELK (Elasticsearch, Logstash, and Kibana) server allows users to easily monitor the vulnerable VMs for changes to the file names and watch system metrics.
Filebeat monitors the logs in the specified locations. It detects changes to the filesystem. It collects logs and forwards them to Elastisearch or Logstash for indexing

Metricbeat detects changes in system metrics such as CPU usage. was useed to detect SSH login attempts.

![Polices](https://user-images.githubusercontent.com/85802280/121785653-dcbb4180-cb6f-11eb-8a68-6b642506e44c.jpg)

 Policies
The machines on the internal network are not exposed to the public Internet.

Only the Jumpbox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the designated public IP address. This address changes each time the machine is powered down and restarted.

Machines within the network can only be accessed by peer servers. The Jumpbox Provisioner connects via SSH to the Webservers (Web 1, Web 2 & Web 3) and the ELK Server. The Web Server machines send logs to the ELK Server to be forwarded for indexing.

Ansible was used to automate configuration of the ELK Server. No configuration was performed manually, which is advantageous because...

Using Ansible allowed me to quickly install, update, and add the web servers to the network using the same playbooks
The playbook implements the following tasks:

Install docker on all network machines so they will be able to recieve and install containers
Ansible is installed on the Jump Box VM to distribute containers to other VMs on the network
Ansible playbooks are used to install the ELK stack container on the ELK server and a 'Beats' containers on the Web servers

We have installed the following Beats on these machines:

Filebeat
Metricbeat
These Beats allow us to collect the following information from each machine:

Filebeat - Filebeat detects changes to the filesystem. We are using this to monitor our Web Log data.
Metricbeat - Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.
