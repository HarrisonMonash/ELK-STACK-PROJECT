# ELK-STACK-PROJECT
Harrison's repository 
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram](/Diagram/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _[Elk Install](Ansible/elk.yml)_
  - _[FileBeat](Ansible/filebeat.yml)_
  - _[MetricBeat](Ansible/metric_playbook.yml)_
  - _[DVWA SETUP](Ansible/dvwa_setup.yml)_

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box?
A load balancer serves as a specific point of access for a the machines on the network. Load balancers protect the servers from an overload of web requests, such as DDOS(Distributed denial-of-service) attacks. It can do this by re-directing the traffic to a public cloud provider.
The advantages of a jump box is that Admins have a secure origin point to connect to the rest of the VM's on the system to complete tasks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log and system resources.

Filebeat is used to monitor for system logs and forward any changes to the Elasticsearch or Logstash.
Metricbeat periodically collects metrics from the system and services running on the sever. This also forwards the data to Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name      | Function | IP Address | Operating System |
|-----------|----------|------------|------------------|
| Jump Box  | Gateway  | 10.0.0.4   | Linux            |
| Web_1     | Server   | 10.0.0.5   | Linux            |
| Web_2     | Server   | 10.0.0.6   | Linux            |
| Web_3     | Server   | 10.0.0.7   | Linux            |
| ELK_Server| Server   | 10.0.1.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

Add whitelisted IP addresses:
My IP: 121.200.7.39

Machines within the network can only be accessed by jumpbox.
Which machine did you allow to access your ELK VM? What was its IP address?
Jumpbox IP: 191.239.178.113
Jumpbox Private IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes via SSH         | 121.200.7.39         |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| Web-3    | No                  | 10.0.0.4             |
| ELK      | No                  | 10.0.0.4             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?
You can implement multiple commands across multiple servers from the single Ansible playbook.

The playbook implements the following tasks:
- Install docker:
- Install Pyhton3_pip
- Docker Module
- Increase the virtual memory. When installing the ELK server in the elk.yml file using the command sysctl -w vm.max_map_count=262144, will assist in the server to launch and stabilise. 
- Launching the docker, ELK and specifying the ports required to access.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker ps output](/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1: 10.0.0.5
Web-2: 10.0.0.6
Web-3:10.0.0.7

We have installed the following Beats on these machines:
Specify which Beats you successfully installed
I have installed Filebeat and Metricbeats onto the ELK server to monitor Web-1, Web-2 and Web-3.

These Beats allow us to collect the following information from each machine:
Filebeat is able to monitor system activity such as logins, failure and accepted.
[Filebeat Example](/Images/Filebeat_example.png)

Metricbeats is able to monitor cpu and memory usage to determine what services could be using too many services or if someone is attempting a malicious attack. 
[Metricbeat Example](/Images/Metricbeat_example.png)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

- Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it?
  The file is elk_install.yml and you copy it to /etc/ansible/elk_install.yml

- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
 Update the hosts file to include the elk server and it's internal IP with the following command: 
[ELK]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- Which URL do you navigate to in order to check that the ELK server is running?
http://20.92.81.58:5601/app/kibana#/home . This URL has the ELK server IP and the open port of 5601 on Kibana.