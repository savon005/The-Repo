## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


![image](https://user-images.githubusercontent.com/75633808/117615586-88b3dc00-b12f-11eb-90ff-89b95f460e20.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

 https://github.com/savon005/The-Repo/blob/main/Ansible/elk-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected, in addition to restricting traffic to the network.

- What aspect of security do load balancers protect? What is the advantage of a jump box?

Azure Load Balancer operates at layer four of the Open Systems Interconnection (OSI) model and protects servers from getting overloaded and possibly breaking down. If a single server goes down, the load balancer redirects traffic to the remaining online servers. When a new server is added to the server group, the load balancer automatically starts to send requests to it. In other words, load balancing improves service availability and helps prevent downtimes.

- What is the advantage of a jump box?

Jump box prevents Azure VMs from being exposed to the public. This means that this will be the entry point connecting via Remote Desktop Protocol (RDP) from the on-premise network. It also helps to open only one port instead of several ports to connect different virtual machines present in the Azure cloud.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

- What does Filebeat watch for?

Filebeat watches and monitors the log files or locations that users specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on the server.

- What does Metricbeat record?

Metricbeat is a lightweight shipper that records and periodically collects metrics from the operating system and from services running on the server and takes the metrics and statistics that it collects and ships them to the output that users specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| Web-3    | Server   | 10.0.0.7   | Linux            |
| ELK-Web  | Monitor  | 10.0.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

- Only the Jump box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

5061 Kibana port

- Machines within the network can only be accessed by Jump-Box-Provisioner.

Jump-Box-Provisioner

- What was its IP address?

10.0.0.4 (Jump box Private IP)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes.                | 10.0.0.1 10.0.0.2    |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| Web-3    | No                  | 10.0.0.4             |
| ELK-Web. | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it was protected from vulnersabilities.

- What is the main advantage of automating configuration with Ansible?

Free: Ansible is an open-source tool.
Very simple to set up and use: No special coding skills are necessary to use Ansible's playbooks.
Powerful: Ansible lets user model even highly complex IT workflows.
Flexible: User can orchestrate the entire application environment no matter where it’s deployed. Users can also customize it based on their needs.
Agentless: User don’t need to install any other software or firewall ports on the client systems it want to automate. User also don’t have to set up a separate management structure.
Efficient: Because user don’t need to install any extra software, there’s more room for application resources on the server.


The playbook implements the following tasks:

- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- Download and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/75633808/117618590-cb77b300-b133-11eb-9b75-f1cca1561d85.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

   | Name  	    |   	| IP Address 	|
   |------------|-----|-------------|
   | Web-1 	    |   	| 10.0.0.5   	|
   | Web-2 	    |   	| 10.0.0.6   	|
   | Web-3 	    |   	| 10.0.0.7   	|

We have installed the following Beats on these machines:

- filebeat
- nmetricbeat

These Beats allow us to collect the following information from each machine:

Filebeat - collects data about the file system such as log events, and ships them to the monitoring cluster.

Metricbeat - collects metrics and statistics and ships them to the output that was specified, such as Elasticsearch or Logstash.



### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the Playbook file to Ansible.
- Update the host file to include webserver and ELK.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.


- Which file is the playbook? Where do you copy it?

/etc/ansible/file/filebeat-configuration.yml
 
- Which file do you update to make Ansible run the playbook on a specific machine?  How do I specify which machine to install the ELK server on versus which to install Filebeat on?

/etc/ansible/file/filebeat-configuration.yml

- Which URL do you navigate to in order to check that the ELK server is running?
www.publicip:5601 (Kibana)


-Specific commands the user will need to run to download the playbook

- nano ansible.cfg
- add the machine, its IP, and ansible_python_interpreter=/usr/bin/python3 to the hosts
- Ctrl + x to exit file
- in the folder that install-elk.yml is in, run: cp install-elk.yml /etc/ansible
- nano install-elk.yml /etc/ansible
- name: installing elk hosts: [your_machine]
- Ctrl + x to exit file
- ansible-playbook install-elk.yml
