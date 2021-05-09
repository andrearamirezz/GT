## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/andrearamirezz/GT/blob/main/README/Images/Graph.jpeg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

The following playbooks were created: 
<a href="https://github.com/andrearamirezz/GT/blob/main/README/Ansible/File-beat.yml 
">Filebeat Playbook</a>

<a href="https://github.com/andrearamirezz/GT/blob/main/README/Ansible/metric-beat.yml
">Metricbeat Playbook</a>

<a href="https://github.com/andrearamirezz/GT/blob/main/README/Ansible/install-elk.yml
">Installing Elk</a>



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



What aspect of security do load balancers protect? What is the advantage of a jump box?
 - Load balancers protects against DDos attacks by distributing the traffic from a private server to the cloud. 

 - Advantage of a jump box:
    - It is a secure admin workstation (SAW)
    - Provides hardened security 
    - Manages other virtual machines in the network

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.


What does Filebeat watch for?
 - Filebeat monitors the log files/locations that is specified, collects log events and forwards them to Elasticsearch or Logstash for indexing. 
          


What does Metricbeat record? 
 - Metricbeat fetches metrics from the Docker server. 


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function  | IP Address | Operating System |
|----------|---------- |------------|------------------|
| Jump Box | Gateway   | 10.0.0.4   | Linux            |
| DVWA-VM1 |Webserver1 | 10.0.0.5   | Linux            |
| DVWA-VM2 |Webserver2 | 10.0.0.6   | Linux            |
|ELK-server|ElkServer  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 - Public: 168.62.190.236
 - Private: 10.0.0.4

Machines within the network can only be accessed by SSH with the private IP address.

 - Which machine did you allow to access your ELK VM? What was its IP address?
    - The only machine allowed access to the ELK VM is the JumpBox Machine. The Private IP address is    10.0.0.4 and the Public IP address is 168.62.190.236. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 10.0.0.4             |
| DVWA-VM1 | No                  | 10.0.0.5             |
| DVWA-VM2 | No                  | 10.0.0.6             | 
|ELK-server| No                  | 10.1.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Administrators do not have to manually configure the machine, therefore saving a lot of their time. 

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
- sudo apt get docker.io 
- sudo docker run -ti cybersecurity/ansible:latest bash 
- sudo docker container list -a 
- sudo docker start [name of container]
- sudo docker ps 
- sudo docker attach [name of container]

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
https://github.com/andrearamirezz/GT/blob/main/README/Images/Documentation%20httpshelp.ubuntu.com.jpeg

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats successfully on these machines:
 - Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeatconfig.yml Metricbeatconfig.yml file to /etc/filebeat/filebeat.yml and /etc/metricbeat/metricbeat.yml
- Update the configuration files to include the private IP address of the ELK Server to the elastic search and Kibana sections. 

- Run the playbook, and navigate to Kibana Website/ELK server's GUI to check that the installation worked as expected.

Answer the following questions to fill in the blanks:

- Which file is the playbook? Where do you copy it?_
    - Filebeat-playbook.yml and you copy it to /etc/filebeat/filebeat.yml 

- Which file do you update to make Ansible run the playbook on a specific machine? 
    - You have to update the host files in the ansible and add the IP addresses of the machines. 


- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
    - You have to specify according to the machine's Private IP addresses 



- Which URL do you navigate to in order to check that the ELK server is running?

   - You have to navigate to http://[ELK Public IP address]/app/kibana#/home

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
  - To run a playbook: ansible-playbook [playbookexample.yml] 
  - To update a file you will have to nano the file, so nano /etc/ansible/playbookexample.yml
