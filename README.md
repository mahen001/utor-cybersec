## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Diagrams/Network Diagram Project1.png]

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _configuration_ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._ Ansible Playbook; Ansible Hosts File; ELK Playbook---Need to check

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
- What aspect of security do load balancers protect? What is the advantage of a jump box?
  Load balancers protect the servers from a denial of service attack. The advantage of a jump box is that it protects the virtual   machines from being exposed from the public internet.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _data_and system _logs.
- What does Filebeat watch for?_Collects log files from very specific files and forwards them either to Elasticsearch or Logstash.
- What does Metricbeat record?_Collects machine metrics such as uptime and send the output to Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name          | Function                  | IP Address   | Operating System   |
|---------------|---------------------------|--------------|--------------------|
| Jump Box      | Jump Box                  | 10.0.0.5     | Linux ubuntu 18.04 |
| Web-1         | VM Server                 | 10.0.0.6     | Linux ubuntu 18.04 |
| Web-2         | VM Server                 | 10.0.0.7     | Linux ubuntu 18.04 |
| Elk VM        | Log Analysis              | 10.2.0.4     | Linux ubuntu 18.04 |
| Load Balancer | Secure/Distribute traffic | 20.120.20.59 | Linux ubuntu 18.04 |
| Workstation   | Access Control            | Public IP    | Windows 10         |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _Jump Box Provisioner__ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:Workstation Public IP through TCP 5601.
-Add whitelisted IP addresses_ : This is the public IP of the local workstation outside the network.

Machines within the network can only be accessed by Workstation and Jump-Box-Provisioner.
- Which machine did you allow to access your ELK VM? What was its IP address?_Jump-Box-Provisioner IP : 10.0.0.4 via SSH port 22
Workstation Public IP via port TCP 5601.. Need to check.
 
A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses                 |
|---------------|:-------------------:|--------------------------------------|
| Jump Box      |          No         | Workstation Public IP SSH on Port 22 |
| Web-1         |          No         | 10.0.0.6 SSH on Port 22              |
| Web-2         |          No         | 10.0.0.7 SSH on Port 22              |
| ELK VM        |          No         | Workstation Public IP on TCP 5601    |
| Load balancer |          No         | Workstation Public IP on HTTP 80     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Diagrams/docker_ps_output.png]

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 : 10.0.0.6
  Web-2 : 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
  Metricbeat
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml/metricbeat-config.yml file to files.
- Update the filebeat-config.yml file to include the private IP address of your ELK machine in lines #1106 and 1806.

output.elasticsearch:
hosts: ["10.1.0.4:9200"]
username: "elastic"
password: "changeme"

setup.kibana:
host: "10.1.0.4:5601"

- Run the playbook "ansible-playbook filebeat-playbook.yml", and navigate to http://public ip elk server:5601/app/kibana--log-add log data-system log-last module Module status--click check data to check that the installation worked as expected.

output.elasticsearch:
#Array of hosts to connect to.
hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme"

setup.kibana:
  host: "10.1.0.4:5601"


_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running? http://public ip elk server:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

