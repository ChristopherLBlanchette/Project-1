# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Images/Network%20Topology.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the **yml and config** file may be used to install only certain pieces of it, such as Filebeat.

[Elkstack Playbook](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/elkstack-playbook.yml)  
[Pentest Playbook](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/pentest-playbook.yml)  
[Filebeat Playbook](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/filebeat-playbook.yml)  
[Filebeat Config](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/filebeat-config.yml)  
[Metricbeat Playbook](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/metricbeat-playbook.yml)  
[Metricbeat Config](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/metricbeat-config.yml)  

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

# Description of the Topology  

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly **functional and available**, in addition to restricting **traffic** to the network.

- What aspect of security do load balancers protect?  
  - **Load balancers add resiliency by rerouting live traffic from one server to another if a server falls prey to a DDoS attack or otherwise becomes unavailable.**

- What is the advantage of a jump box?
  - **A Jump Box Provisioner is also important as it prevents Azure VMs from being exposed via a public IP Address. This allows us to do monitoring and logging on a single box. We can also restrict the IP addresses able to communicate with the Jump Box.**

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **network** and system **logs**.

- What does Filebeat watch for?
  - **Filebeat monitors the log files or locations that you specify, collects log events.**

- What does Metricbeat record?  
  - **Metricbeat takes the metrics and statistics that collects and ships them to the output you specify.**

The configuration details of each machine may be found below.

| Name        | Function           | IP Address  | Operating System |
| :- | :- | :- | :- |
| Jump-Box | Gateway | 20.102.71.52 / 10.0.0.6 | Linux |
| Web-1 | UbuntuServer |20.106.225.235 / 10.0.0.7 | Linux |
| Web-2 | UbuntuServer | 20.106.255.235 / 10.0.0.8 | Linux |
| ELK-Server | UbuntuServer | 20.124.23.81 / 10.0.0.9 | Linux |

# Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the **Jump-Box-Provisioner** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- **Workstation Public IP Address using TCP Port 5601**

Machines within the network can only be accessed by **Workstation and Jump-Box-Provisioner**.

- Which machine did you allow to access your ELK VM? What was its IP address? 
  - **Jump-Box-Provisioner: 10.0.0.6 on SSH Port 22**

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
| :- | :- | :- |
| Jump Box | Yes | 20.102.71.52 <Worksation Public IP Address on SSH Port 22> |
| Web-1 | No | 10.0.0.6 on SSH Port 22 |
| We-2 | No | 10.0.0.6 on SSH Port 22 |
| ELK-Server | No | <Workstation Public IP Address> using TCP Port 5601 |

# Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
  - **This allows you to deploy to multiple servers using a single playbook**

The playbook implements the following tasks:  
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.

- Specify a different group of machinges:
```
---
- name: Configure Elk VM with Docker
  hosts: elkservers
  become: true
  tasks:
```   
- Install Docker.io:
```
    - name: Install docker.io
      apt:
        update_cache: yes
        force_apt_get: yes
        name: docker.io
        state: present
```       
- Install Python:
```
    - name: Install python3-pip
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present
```
- Increase Virtual Memory:
```
    - name: Increase virtual memory
      command: sysctl -w vm.max_map_count=262144

    - name: Use more memory
      sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes
```
- Download and Launch ELK Docker Container and Published ports were made available:
```
    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          -  5601:5601
          -  9200:9200
          -  5044:5044
```

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

- Jump-Box-Provisioner
![alt text](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Images/Docker_PS_Output/JumpBox_Docker_PS_Output.png)

- Web-1
![alt text](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Images/Docker_PS_Output/Web_1_Docker_PS_Output.png)

- Web-2
![alt text](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Images/Docker_PS_Output/Web_2_Docker_PS_Output.png)

- ELK-Server
![alt text](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Images/Docker_PS_Output/ELK_Server_Docker_PS_Output.png)

# Target Machines & Beats

This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.7
- Web-2: 10.0.0.8

We have installed the following Beats on these machines:

- Filebeat:

  - [Filebeat Status](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Images/Beats%20Installed/Filebeat_Data_Successful.png)

- Metricbeat

  - [Metricbeat Status](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Images/Beats%20Installed/Metricbeat_Data_Successful.png)

These Beats allow us to collect the following information from each machine:

- Filebeat will be used to collect log files from very specific files such as Apache, Microsft Azure tools and web servers, MySQL databases.
- Metericbeat will be used to monitor VM stats, per CPU core stats, per filesystem stats, memory stats and network stats.

# Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the **yml** file to **ansible folder**.
- Update the **config** file to include **remote users and ports**.
- Run the playbook, and navigate to **Kibana <ELK_Server IP Address:5601>** to check that the installation worked as expected.

Answer the following questions to fill in the blanks:

- Which file is the playbook?
  - For Anisible make [Pentest Playbook](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/pentest-playbook.yml)
  - For Filebeat make [Filebeat Playbook](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/filebeat-playbook.yml)
  - For Metricbeat make [Metricbeat Playbook](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Files/metricbeat-playbook.yml)

- Where do you copy it?
  - /etc/ansible/

- Which file do you update to make Ansible run the playbook on a specific machine?
  - /etc/ansible/hosts file > IP Address of the VMs
  
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
  -I specified in /etc/ansible/hosts file which is a webserver and which is an ELKserver.
  
![alt text](https://github.com/ChristopherLBlanchette/Project-1/blob/main/Images/Docker_PS_Output/ServerSpecification.png)
  
- Which URL do you navigate to in order to check that the ELK server is running?
  - http://20.124.23.81:5601/app/kibana#/home
