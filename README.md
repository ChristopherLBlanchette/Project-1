# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text]...................topology pic

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
- What is the advantage of a jump box?

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- What does Filebeat watch for?  
- What does Metricbeat record?  

The configuration details of each machine may be found below.

| Name        | Function           | IP Address  | Operating System |
| :- | :- | :- | :- |
| Jump-Box-Provisioner| Gateway | 20.102.71.52 / 10.0.0.6 | Linux |
| col 2 is      | centered      |   $12 | Linux |
| zebra stripes | are neat      |    $1 | Linux |
| zebra stripes | are neat      |    $1 | Linux |
