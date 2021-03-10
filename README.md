## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](Diagrams/Network-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the config file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available to use, in addition to restricting traffics to the network.
- Load Balancer it does provide the realible traffics to all the VMs that connected to it, for example instad of 1000 traffics goin into one server Load Balancer does split those traffics and send it to each of the VMs at the same time for better connetivities and availabilities.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Logs and system traffics.

- Filebeat is an open-source that you install on your server in order to send the logs data to the Elasticsearch, It can either send to Elasticsearch from Logstack for more friendly output with graphs, diagrams and easy to uderstand or straight to Elasticsearch for indexing.
- Metricbeat is a bit different from Filebeat, Metric is an open-source that you install on your server that you wish to monotor. Metricbeat does collect the metrics form operating system and services that running on the server and send it to Elasticsearch for further process and output.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | Pub: 52.243.72.220 P: 10.0.0.1 | Linux |
| Web 1    | Server   | P: 10.0.0.5 | Linux |
| Web 2    | Server   | P: 10.0.0.6 | Linux |
| Web 3    | Server   | P: 10.0.0.8 | Linux |
| ELK Server    | Monitor   |  Pub: 104.214.140.44 P: 10.1.0.4 | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 124.149.255.70 is my host machine public IP address.

Machines within the network can only be accessed by Jumpbox.
- Web 1, Web 2, and Web 3 can access the ELK server because as the Web 1 and Web 2 installed the containers and DVWA and the Web 3 is a redundancy, it can only be done by using SSH.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 124.149.255.70       |
| Web 1    | No                  | N/A                  |
| Web 2    | No                  | N/A                  |
| Web 3    | No                  | N/A                  |
| ELK server    | No             | N/A                  |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Playbooks are Ansible configuration files and the language write the playbook is YML which is human readablel, the superiority of YAML is like JSON makes better configuration management and automation tool.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install docker through pip
- Increase virtual memory
- Download and launch a elk docker container  

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](Images/elk.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name     | IP Address | 
|----------|------------|
| Web 1    | 10.0.0.5 |
| Web 2    | 10.0.0.6 |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
![](Images/Logs-data.png)
- The picture above is an example of logs data that has been generated from Elasticsearch using Filebeat.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook.yml file to Ansible directory.
- Update the hosts file to include the webservers (eg: 10.0.0.5, 10.0.0.6, 10.0.0.8) ELK (eg: 10.1.0.4)
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.
- Open up the browser and put in http://[your.VM.IP]:5601/app/kibana
- To run a play book run a command ansible-playbook[playbook-name]
- To change the hosts file go to /etc/hosts/