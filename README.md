# Elk-Stack-Project-1
Class Project-1, Elk Stack Deployment 
 Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
https://github.com/khalieq/cloud/blob/f8838379d7c57c25da1e16a15bcadf1e3b3de51b/Diagram.drawio%20(1).png

These are the files used to create the configuration:

       /etc/ansible/install-elk-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machine information
- How to Use the Ansible Build


 Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting traffic to the network.

- What aspect of security do load balancers protect?
   	- Load balancers protect the system from DDoS attacks by moving the traffic to keep a systeem from being overloaded
  	- Load Balancing focus on keeping a service available
 
- What is the advantage of a jump box?
   	- Allows users secure access to the server by adding another layer of security 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the changes to the Logs and system traffic.

- What does Filebeat watch for?
   	- lightweight shipper for shipping and centralizing data
- What does Metricbeat record?
  	- lightweight shipper that collects metric information on the operating system and services running on the server

The configuration details of each machine may be found below.

| Name      |  Function | IP Address | Operating System   |
|------------ |----------  |-------------- |-------------------------|
| JumpBox | Gateway  |  10.0.0.4    |  Linux(ubtntu 18.04)|           
| Web-1     | Server      |  10.0.0.5    |  Linux(ubtntu 18.04)|                     
| Web-2     | Server      |  10.0.0.6  |  Linux(ubtntu 18.04)|                                  
| Elk-VM1 | Elk Server|  10.2.0.4    |  Linux(ubtntu 18.04)|

           
 Access Policies
- Machines are only accessible by whitelisted IPs

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses:- 173.73.222.169
    	

Machines within the network can only be accessed by SSH.

- Which machine did you allow to access your ELK VM? What was its IP address? The Elk machine can only be accessed via Jumpbox-10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses |
|--------------|----------------------- |---------------------------|
| Jump Box  |     NO                    |    10.0.0.4                   |
| Web-1       |     NO                    |     10.0.0.5                  |
| Web-2       |     NO                    |    10.0.0.6                 |
| Elk-VM1   |     NO                    |    10.2.0.4                   |


 Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
  	- Its simplistic, makes applications and systems easier to deploy and maintain.

The playbook implements the following tasks:
- Install docker.io
- Install Python-pip
- Install docker container
- Launch docker container: elk
- Command: sysctl -w vm.max_map_count=262144

Target Machines & Beats

This ELK server is configured to monitor the following machines:

- List the IP addresses of the machines you are monitoring:-
    	- Web-1(10.0.0.5) Web-2(10.0.0.6)

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed:-
    	-  Filebeat
    	-  Metricbeat

These Beats allow us to collect the following information from each machine:

   	- Filebeat monitors log files or locations you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
   	- Metricbeat collects metrics from the operating system and from services running on the server.

 Using the Playbook-install-elk.yml

     In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

   - Copy the playbook file to /etc/ansible.
   - Update the the configuration file to include the webservers and ElkVM (private Ip address. 
   - Run the playbook, and navigate to ElkVM to check that the installation worked as expected.
/etc/ansible/host should include:

[webservers]
[10.0.0.5] ansible_python_interpreter=/usr/bin/python3
[10.0.0.6] ansible_python_interpreter=/usr/bin/python3

[elk]
[10.2.0.4] ansible_python_interpreter=/usr/bin/python3

Run the playbook, and SSH into the Elk vm, then run docker ps to check that the installation worked as expected.
Playbook: install_elk.yml Location: /etc/ansible/install_elk.yml
Navigate to  http://[your.ELK-VM.External.IP]:5601/app/kibana to confirm ELK and kibana are running.  

Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it?
    	 /etc/ansible/file/filebeat-configuration.yml 
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
        add the correct Ip addresses in the ansible host file
- Which URL do you navigate to in order to check that the ELK server is running?
    	 http://[your.ELK-VM.External.IP]:5601/app/kibana

 Using the Playbook-filebeat-playbook.yml

 - Copy the filebeat.yml file to the /etc/ansible/files/ directory.
 - Update the configuration file to include the Private IP of the Elk-Server to the ElasticSearch and Kibana sections of the configuration file.
 - Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the filebeat setup, and start the filebeat service.
- Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the metricbeat setup, and start the metricbeat service. 
 - Run the playbooks, and navigate back to the installation page on the ELk-Server GUI, click the check data on the Module Status
 - Click the verfiy incoming Data to check and see the receiving logs from the DVWA machines.  

 
 
   The commands needed to run the Ansible configuration for the Elk-Server are:

	- ssh azadmin@JumpBox(Public IP)
	- sudo docker container list -a (locate your ansible container)
	- sudo docker start container (name of the container)
	- sudo docker attach container (name of the container)
cd /etc/ansible/
	- ansible-playbook elk.yml (configures Elk-Server and starts the Elk container on the Elk-Server) wait a couple minutes for the implementation of the Elk-Server
	- cd /etc/ansible/roles/
	- ansible-playbook filebeat-playbook.yml (installs Filebeat and Metricbeat)
	- open a new web browser (http://[your.ELK-VM.External.IP]:5601/app/kibana) This will bring up the Kibana Web Portal
	- check the Module status for file beat and metric beat to see their data receiving.




