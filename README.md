## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

### Elk Diagram

![Diagram](https://github.com/Jessica27sanchez/Fundamentals/blob/main/Diagram/HW-12-Cloud-Security.png)



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

 https://github.com/Jessica27sanchez/Fundamentals/blob/main/Ansible/filebeat-playbook.yml
 
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable, in addition to restricting access to the network. A load balancer intelligently distributes traffic from clients across multiple servers without the clients having to understand how many servers are in use or how they are configured. Because the load balancer sits between the clients and the servers it can enhance the user experience by providing additional security, performance, resilience and simplify scaling your website.

- Security - A load balancer can add additional layers of security to your website without any changes to your application. It protects applications from emerging threats. Also, the Web Application Firewall (WAF) in the load balancer protects your website from hackers and includes daily rule updates just like a virus scanner. Another way is using Authenticate User Access, The load balancer can request a username and password before granting access to your website to protect against unauthorized access. It can protect against DDoS attack; The load balancer can detect and drop distributed denial-of-service (DDoS) traffic before it gets to your website. And lastly but the least, Simplify PCI compliance, If you process credit cards, you need to comply with Payment Card Industry (PCI) regulations. A load balancer simplifies compliance with PCI rules

- Performance - Load balancers can reduce the load on your web servers and optimize traffic for a better user experience. With SSL Offload securing traffic with SSL (Secure Sockets Layer) on the load balancer removes the overhead from web servers resulting in more resources being available for your web application. It can use traffic compression for website traffic giving your users a much better experience with your website. Using Traffic Caching, a load balancer will retain a copy of frequently accessed elements of your website such as images resulting in fewer to your web servers and quicker delivery of content to users. Another feature,
HTTP 2.0 is an enhancement to the HTTP protocol which results in much quicker websites. A load balancer can communicate with clients using HTTP 2.0 even if not supported by your web servers

- Resilience -
Load balancers can transparently accommodate failed and under-performing components to maintain user service. It can continued service if a web server fails, If one of your web servers fails, the load balancer will continue to transparently provide service to the remaining servers with no impact on the user. If a web server is busy, the load balancer will detect this and redirect traffic to less busy web servers. Create a highly available site, load balancers can be deployed in highly available pairs so that if one fails, the other load balancer immediately takes over with no impact on users. Simplify business continuity
If you have an application in multiple sites for disaster recovery, a load balancer can detect a site outage and seamlessly redirect users to the alternate site. 

A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an organization point to connect to other servers or untrusted environments. It is an intermediary host or an SSH gateway to a remote network, through which a connection can be made to another host in a dissimilar security zone, for example a demilitarized zone (DMZ). It bridges two dissimilar security zones and offers controlled access between them.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log and system traffic.


What does Filebeat watch for? Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as: Apache
What does Metricbeat record? Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 52.250.126.157   | Linux            |
| Web-1   | DVWA      | 10.0.0.5         | Linux            |
| Web-2   | DVWA      | 10.0.0.6         |   Linux          |
| Web-3   | ELK       | 10.1.0.7         |     Linux        |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 52.175.253.204

Machines within the network can only be accessed by Jump-Box.
The jump-box is allowed to access the ELK vm, its IP address is 52.250.126.157 and the local machine is IP address is 10.1.0.4. A summary of the access policies in place can be found in the table below.
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 77.199.197.11        |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
The primary benefit of Ansible is it allows IT administrators to automate away the drudgery from their daily tasks. That frees them to focus on efforts that help deliver more value to the business by spending time on more important tasks.

The playbook implements the following tasks:

- Install Python3-pip
- Install Docker using pip
- Install ELK
- Enable docker service on restart

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker ps output](https://github.com/Jessica27sanchez/Fundamentals/blob/main/Diagram/ELK1.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5, 10.0.0.6, 10.0.0.7

We have installed the following Beats on these machines:
- We successfully installed_filebeat and metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

- Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Playbook.yml file to the ansibe container in the Jump-Box.
- Update the Ansible_Playbooks_Solved_ansible_config.yml file to include Web- 1,2,3 machines.
- Run the playbook, and navigate to the ansible container to check that the installation worked as expected.
  Filebeat (https://github.com/Jessica27sanchez/Fundamentals/blob/main/Ansible/filebeat-playbook.yml) and metricbeat (https://github.com/Jessica27sanchez/Fundamentals/blob/main/Ansible/metricbeat-configuration.yml) playbooks which are copied in the abisble container

 ![Successfully logging into Kibana after installing beat files](https://github.com/Jessica27sanchez/Fundamentals/blob/main/Diagram/kibana1.jpg)
