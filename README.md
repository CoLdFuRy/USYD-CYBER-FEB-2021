# USYD-CYBER-FEB-2021
Homework: GitHub Fundamentals and Project 13 Submission
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _yml_ and _config_ file may be used to install only certain pieces of it, such as Filebeat.

* [Ansible Playbook - pentest](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/pentest.yml)
* [Ansible Hosts](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/hosts)
* [Ansible Configuration](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ansible.cfg)
* [Ansible ELK Installation and VM Configuration](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ELK-Stack/install-elk.yml)
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

| Name          | Function       | IP Address                 | Operating System |
|---------------|----------------|----------------------------|------------------|
| Jump-Box-Prov | Gateway        | 10.0.0.4 / 191.239.176.100 | Linux            |
| Web-1         | Web Server     | 10.0.0.5                   | Linux            |
| Web-2         | Web Server     | 10.0.0.6                   | Linux            |
| ELK           | ELK Server     | 10.1.0.4 / 20.37.244.118   | Linux            |
| Red-Team-LB   | Load Balancer  | 23.101.233.237             | Linux            |
| Workstation   | Access Control | External IP of Public IP   | Linux            |

Server redundency has been set-up for Web-1 and Web-2 Virtual Machines.
This can be confirmed by visiting the DVWA site via <http://{LB-IPAddress/setup.php> and disabling either or both Web servers.


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _Elk Server_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
    * Workstation public IP through TCP 5601

Machines within the network can only be accessed by _Web-3 and Jump-Box-Provisioner_.
    Which machine did you allow to access your ELK VM? What was its IP address?
    * Jump-Box-Provisioner: 10.0.0.4 via SSH port 20
    * Workstation public IP via TCP port 5601

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses              |
|---------------|---------------------|-----------------------------------|
| Jump Box      | No                  | Workstation public IP on SSH 22   |
| Web-1         | No                  | 10.0.0.5 on SSH 22                |
| Web-2         | No                  | 10.0.0.6 on SSH 22                |
| ELK Server    | No                  | Workstation public IP on TCP 5601 |
| Load Balancer | No                  | Workstation public IP on HTTP 80  |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because _Ansible allows you to quickly and easily deploy multitier applications. Their is no need to write code to automate systems, simply list the tasks required to be done by configuring the ansible playbook and the application will figure out how to get your systems to the state desired._

The playbook implements the following tasks:
* Specify a different group of machines as well as a different remote user:

```- name: Config elk VM with Docker
      hosts: elk
      remote_user: sysadmin
      become: true
      tasks:
```
 
* Increase System Memory : 
``` - name: Use more memory
     sysctl:
      name: vm.max_map_count
      value: '262144'
      state: present
      reload: yes`
```

* Install the following services:
```docker.io
   python3-pip
   docker, which is the Docker Python pip module.
```

* Launching and Exposing the container with these published ports:
```    5601:5601 
    9200:9200
    5044:5044
```


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://raw.githubusercontent.com/CoLdFuRy/USYD-CYBER-FEB-2021/main/Diagrams/ELK.JPG?token=AS3LVQRPDHK4HS7DV6BFNWTAVJECW "ELK instance")

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

  * Web1 : 10.0.0.5
  * Web2 : 10.0.0.6

We have installed the following Beats on these machines:
  * ELK Server, Web-1 and Web-2
  * The ELK Stack Installed are: _FileBeat and MetricBeat_

These Beats allow us to collect the following information from each machine:
  * Filebeat: _log events_
  * Metricbeat: _metrics and system statistics_

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
For ELK VM Configuration:
    * Copy the [Ansible ELK Installation](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ELK-Stack/metricbeat-playbook.yml) file to ~/etc/ansible folder within the Ansible docker.
    * Run the playbook using this command: `ansible-playbook install-elk.yml`

For Filebeat:
    * Download Filebeat playboook using the command:
    `curl -L -O https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml`
    * Copy the '/etc/ansible/roles/filebeat-config.yml' file to '/etc/filebeat/filebeat-playbook.yml'
    * Update the filebeat-playbook.yml file to include installer
    `curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb`
    * Update the filebeat-config.yml file root@c1e0a059c0b0:/etc/ansible/files# `nano filebeat-config.yml`
   ```output.elasticsearch:
  #Array of hosts to connect to.
 hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme” 
```
   * Run the playbook using this command `ansible-playbook filebeat-playbook.yml` and navigate to Kibana > Logs : Add log data > System logs > 5:Module Status > Check data to check that the installation worked as expected.

For METRICBEAT:
    * Download Metricbeat playbook using this command:
        `curl -L -O https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/files/metricbeat-config.yml`
    * Copy the /etc/ansible/files/metricbeat file to /etc/metricbeat/metricbeat-playbook.yml
    * Update the filebeat-playbook.yml file to include installer
        `curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb`
    * Update the metricbeat file rename to metricbeat-config.yml
root@c1e0a059c0b0:/etc/ansible/files# `nano metricbeat-config.yml`
```output.elasticsearch:
#Array of hosts to connect to.
hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme"

setup.kibana:
  host: "10.1.0.4:5601"
```
   * Run the playbook, (ansible-playbook metricbeat-playbook.yml) and navigate to Kibana > Add Metric Data > Docker Metrics > Module Status to check that the installation worked as expected.

## ADDITONAL NOTES:
### How to get Filebeat installer :

    Login to Kibana > Logs : Add log data > System logs > DEB > Getting started
    Copy: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb

### How to get the Metricbeat installer:

   Login to Kibana > Add Metric Data > Docker Metrics > DEB > Getting Started
   Copy: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb

   * Which file is the playbook? Where do you copy it?

       * Answer : For Ansible create the pentest.yml as our playbook.

        See [Ansible Playbook](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/pentest.yml)

       * Answer : For Filebeat create filbeat-playbook.yml as our playbook.

        See [Filebeat Playbook](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ELK-Stack/metricbeat-playbook.yml)

       * Answer: For Metricbeat create metricbeat-playbook.yml as our playbook.

        See [Metricbeat Playbook](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ELK-Stack/filebeat-playbook.yml)

   * Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?

### How to Download and Edit the Ansible Configuration file

```- root@4c4f5f3c2523:/etc/ansible# curl -L -O https://ansible.com/  > ansible.cfg
- root@4c4f5f3c2523:/etc/ansible# nano ansible.cfg

- Press CTRL + W (to search > enter remote_user then change `remote_user = azureuser`
```

`Where : `azureadmin` is the remote user that has control over ansible.`

### How to Edit the Ansible Hosts file in this directory /etc/ansible/hosts

```#List the IP Addresses of your webservers
#You should have at least 2 IP addresses

[webservers]
10.0.0.4 ansible_python_interpreter=/usr/bin/python3
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3

#List the IP address of your ELK server
#There should only be one IP address
[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3
```

`Where: [webservers] and [elk] are the group of machines and each group has 1 or more members.`

### How to Create the ELK Installation and VM Configuration in the /etc/ansible/ directory:

See the final solution of the [Ansible ELK Installation.](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/ELK-Stack/install-elk.yml)

    * Specify a different group of machines as well as a different remote user

      ```- name: Config elk VM with Docker
        hosts: elk
        remote_user: sysadmin
        become: true
        tasks:
```

`Where: [elk] is the Virtual Machine hosts or the group of machine targetted for this installation and can only be done by a `sysadmin` remote_user`

### How to Copy the raw Filebeat Module Configuration file from web to the /etc/ansible/files directory:

    ```curl -L -O https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml
```
        * Note : The filebeat-config.yml as our filebeat configuration file.

See the final solution of the [Filebeat Config file](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/filebeat-config.yml)

```hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme" 

setup.kibana:
  host: "10.1.0.4:5601"
```

`Where: hosts: ["10.1.0.4:9200"] is the ELK VM that can install Filebeat`

### How to Copy the raw Metricbeat Module Configuration from web to the /etc/ansible/files/ directory:

     ```curl -L -O https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/files/metricbeat-config.yml
```
        * Note : the metricbeat-config.yml as our metricbeat configuration file.

See the final solution of the [Metricbeat Config file.](https://github.com/CoLdFuRy/USYD-CYBER-FEB-2021/blob/main/Ansible/metricbeat-config.yml)

```hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme" 

setup.kibana:
  host: "10.1.0.4:5601"
```
`Where: hosts: ["10.1.0.4:9200"] is the ELK VM that can install Metricbeat`

    * Which URL do you navigate to in order to check that the ELK server is running?
        * Test Kibana on web : http://[ELK-VM.External.IP]:5601/app/kibana
        * Test Kibana on localhost: azureuser@10.1.0.4: curl localhost:5601/app/kibana

## Activity Commands in Linux:
| ### COMMAND 					                                 | ### EXPLANATION              		             |
|---------------------------------------------------|---------------------------------------------|
| `sudo apt-get update` 		    	                     | this will update all packages		             |
| `sudo apt install docker.io` 		    	              | install docker application		                |
| `sudo service docker start` 		   	                | start the docker application		              |
| `systemctl status docker` 		    	                 | status of the docker application		          |
| `sudo docker pull cyberxsecurity/ansible` 	       | download the docker file			                 |
| `sudo docker run -ti cyberxsecurity/ansible bash` | run and create a docker image	           	  |
| `sudo docker start <docker-name>` 		              | starts the image specified	              	  |
| `sudo docker ps -a`			         	                  | list all active/inactive containers	        |
| `sudo docker attach <docker-name>` 		             | effectively sshing into the ansible	        |
| `ssh-keygen` 					                                | create a ssh key				                        |
| `ansible -m ping all` 			                         | check the connection of ansible containers  |
