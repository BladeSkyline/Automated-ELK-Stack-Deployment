# Automated-ELK-Stack-Deployment-Project-1



Calixto Gonzalez 5/22/2022 Cyber Security Boot Camp


## Automated-Elk-Stack-Deployment


*The files in this repository were used to configure the network depicted below.

![Cloud Security-Page-1](https://user-images.githubusercontent.com/105831725/169916907-68c42054-aa0d-4e9c-bd61-450782085be5.jpg)




These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the *Project 1 Red Team Network Diagram file may be used to install only certain pieces of it, such as Filebeat*.

[Ansible-DVWA-Install.txt](https://github.com/BladeSkyline/Automated-ELK-Stack-Deployment/files/8758486/Ansible-DVWA-Install.txt)

[Ansible-hosts.txt](https://github.com/BladeSkyline/Automated-ELK-Stack-Deployment/files/8758462/Ansible-hosts.txt)

[ansible-configuration.txt](https://github.com/BladeSkyline/Automated-ELK-Stack-Deployment/files/8758454/ansible.txt)

[filebeat-playbook.yml.txt](https://github.com/BladeSkyline/Automated-ELK-Stack-Deployment/files/8749569/filebeat-playbook.yml.txt)

[filebeat-configuration.txt](https://github.com/BladeSkyline/Automated-ELK-Stack-Deployment/files/8749605/filebeat-configuration.txt)

[metricbeat-playbook.txt](https://github.com/BladeSkyline/Automated-ELK-Stack-Deployment/files/8758438/metricbeat-playbook.txt)

[metricbeat-configuration.txt](https://github.com/BladeSkyline/Automated-ELK-Stack-Deployment/files/8758439/metricbeat-configuration.txt)



This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly functioanl, in addition to restricting high-traffic to the network.
-What aspect of security do load balancers protect?
  ..*-It helps prevent overloading servers as well as optimizes productivity and maximizes uptime.
  ..*-It also adds resiliency by rerouting live traffic from one server to another causing it to eliminate single points of failure from attacks such as DDoS attack.
  
-What is the advantage of a jump box?

..*Jump-box are highly secured computers that are never used for non-admin tasks. Throughout the years, jump-box has improved into an even more comprehensive/lock-down secure admin workstation to decrease the chances of hackers/malware infection.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data network and system logs.

-..*What does Filebeat watch for?_  
  ..*Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
-..*What does Metricbeat record?_ 
  ..*Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.6/ Dyanmic IP  | Linux |
| Web Box 1 | Web Server | 10.0.0.4 |  Linux |
| Web Box 2 | Web Server | 10.0.0.5 |  Linux |
| Elk Stack | Elk Server | 10.1.0.4/ Dynamic IP | Linux |
| Workstaion | Access Control |  External or Public IP | Any |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
..*Workstation Public IP through TCP 5601.

Machines within the network can only be accessed by Workstation and Jump Box.
..*

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  |  Workstation Public IP on SSH 22   |
| Web Box 1 | No                 |                      |
| Web Box 2 | No                 |                      |
| Elk Server | No                | Workstation Public IP using TCP 5601 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _Ansible lets you quickly and easily deploy multitier apps. You won't need to write custom code to automate your systems; you list the tasks required to be done by writing a playbook, and Ansible will figure out how to get your systems to the state you want them to be in _

The playbook implements the following tasks:
..*Specify a different group of machines as well as a different remote user 

  - name: Config elk VM with Docker
    hosts: elk
    remote_user: sysadmin
    become: true
    tasks:
    
    
..*Increase System Memory : 

 - name: Use more memory
  sysctl:
    name: vm.max_map_count
    value: '262144'
    state: present
    reload: yes


..*Install the following services: 

   `docker.io`
   `python3-pip`
   `docker`, which is the Docker Python pip module.
   
   
 ..*Launching and Exposing the container with these published ports: 

 `5601:5601` 
 `9200:9200`
 `5044:5044`




The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![Screenshot (45)](https://user-images.githubusercontent.com/105831725/170170762-6101bc47-8dac-42d8-a977-0fab8d52cc6e.png)



![Screenshot (51)](https://user-images.githubusercontent.com/105831725/170170804-564cd30b-5cfe-47f9-bb85-9cfeff6f8378.png)

![Screenshot (52)](https://user-images.githubusercontent.com/105831725/170170812-ccbd6c1c-c3fb-40a8-b125-aa493733a5d8.png)



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- ..*Web Box 1 10.0.0.4_
- ..*Web Box 2 10.0.0.5_

We have installed the following Beats on these machines:

  ..*ELK Server, Web1 and Web2
  ..*The ELK Stack Installed are: FileBeat and MetricBeat


These Beats allow us to collect the following information from each machine:
   ..*Filebeat: log events
   ..*Metricbeat: metrics and system statistics


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
 For Elk VM Configuration
- Copy the Ansible ELK Installation and VM Configuration 
- Run the playbook using this command : ansible-playbook install-elk.yml
 
 For Filebeat:
Download Filebeat playbook usng this command:

    curl -L -O https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml
Copy the '/etc/ansible/filebeat-config.yml' file to '/etc/filebeat/filebeat-playbook.yml'
Update the filebeat-playbook.yml file to include installer

    curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb

output.elasticsearch:
  #Array of hosts to connect to.
 hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme” 

 setup.kibana:
  host: "10.1.0.4:5601"


- Run the playbook using this command ansible-playbook filebeat-playbook.yml and navigate to Kibana > Logs : Add log data > System logs > 5:Module Status > Check data to check that the installation worked as expected.

For Metric beat:

Download Metricbeat playbook using this command:

    curl -L -O https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/files/metricbeat-config.yml

Copy the /etc/ansible/metricbeat file to /etc/metricbeat/metricbeat-playbook.yml

Update the metricbeat-playbook.yml file to include installer

    curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb

output.elasticsearch:
#Array of hosts to connect to.
hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme"

setup.kibana:
  host: "10.1.0.4:5601"




 Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
Copy the elk_install.yml file to /etc/ansible/roles/elk_install.yml

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
Update the /etc/ansible/hosts file to include the elk group and add the target vm's ip address to that group

- _Which URL do you navigate to in order to check that the ELK server is running?

Test Kibana on web : http://[your.ELK-VM.External.IP]:5601/app/kibana


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

curl -L -O https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml'

    Note : The filebeat-config.yml as our filebeat configuration file.


curl -L -O https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/files/metricbeat-config.yml'

    Note : the metricbeat-config.yml as our metricbeat configuration file. ```





| Command  | Purpose  |
|---|---|
| sudo apt-get update | this will update all packages  |
| sudo apt install docker.io| install docker application  |
| sudo service docker start  | start the docker application  |
| systemctl status docker  |status of the docker application   |
| sudo docker pull cyberxsecurity/ansible  | download the docker file  |
| sudo docker run -ti cyberxsecurity/ansible bash  | run and create a docker image  |
| sudo docker start <image-name>  |starts the image specified   |
| sudo docker ps -a  | list all active/inactive containers  |
| sudo docker attach <image-name>  |effectively sshing into the ansible   |
| ssh-keygen  | create a ssh key  |
| ansible -m ping all  |check the connection of ansible containers   |



