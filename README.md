# USYD-CYBER-FEB-2021
Homework: GitHub Fundamentals and Project 13 Submission
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _yml_ and _config_ file may be used to install only certain pieces of it, such as Filebeat.

* [Ansible Playbook - pentest](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/pentest.yml)
* [Ansible Hosts](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/hosts)
* [Ansible Configuration](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ansible.cfg)
* [Ansible ELK Installation and VM Configuration]()
* [Ansible Filebeat Playbook](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ELK-Stack/metricbeat-playbook.yml)
* [Ansible Filebeat Config file](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/filebeat-config.yml)
* [Ansible Metricbeat Playbook](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ELK-Stack/filebeat-playbook.yml)
* [Ansible Metricbeat Config file](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/metricbeat-config.yml)

Download the ansible.cfg configuration file from <https://ansible.com/> and edit or copy Ansible Configuration to your `/etc/ansible` directory

  * For ansible.cfg edit:

   `cd /etc/ansible/	
    nano ansible.cfg
    CTRL + W > enter remote_user
    change _remote_user = sysadmi_n`

Assign username and SSH Public Key for Web1, Web2, ELK Virtual Machine in Azure GUI

  * Web1 / Web2 / ELK Server > Reset Password > Reset SSH Public Key

     `username: sysadmin
      SSH Key : copy id_rsa.pub from the ansible control node in .ssh/ directory.`

  * To get the SSH Key run this command:
       `~/.ssh# ssh-keygen`
       `~/.ssh# cat id_rsa.pub`


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _available_, in addition to restricting _traffic_ to the network.
* What aspect of security do load balancers protect?
    Answer: _Availability, web traffic and web security._
* What is the advantage of a jump box?
    Answer: _Automation, security, network segmentation and access control._

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _data_ and system _logs_.
* What does Filebeat watch for?
    Answer: _Monitors log files or specified locations, collects log events and forwards them to Elasticsearch or Logstash for indexing._
* What does Metricbeat record?
    Answer: _Gathers the metrics and statistics that it collects and sends them a specified output such as Elasticsearch or Logstash._

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| TODO     |          |            |                  |
| TODO     |          |            |                  |
| TODO     |          |            |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

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
