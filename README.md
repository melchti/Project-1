# Project1
In the first project week, I configured an ELK stack server in order to set up a cloud monitoring system. This project resulted in tangible deliverables that demonstrate my knowledge of cloud, network security, logging and monitoring.

The Scenario for this assignment was as follows:

In this assignment, you will review the concepts and procedures of git and GitHub. You will create a repository that will serve as the location where you can store any scripts, diagrams or other documentation that you have worked on throughout this course. Additionally you will be tasked with uploading the README file, network diagram, and other associated files that you have created during the ELK Stack project. Uploading these files will serve as the official submission of your project.


Background

To understand GitHub, you need to know the basics of version control.

•	Version control is a system that allows users to save all versions of a file while working on it. It's like adding an undo function to any document or file. You create save points as you work, which you can revert to at any time.

•	Git is the most popular software used for version control. It runs on your local computer and allows you create save points (known as commits) for your documents.

•	You can use Git to manage any directory and track every item inside that directory. At any point, you can revert the Git directory (known as a repository) to a previous commit.

GitHub is a website that allows you to sync your local Git repository with a repository in the cloud. This allows you to save your work to the cloud, share your work with others, and easily collaborate on a project.

•	Other users can access your online GitHub repository and sync their own changes. They can also make a copy of your repository to create an entirely new project based on your original project. This is known as forking.

In this activity, you will:

•	Create a new, empty Github repository and sync it to your local machine.

•	Once your repository is up, you will add all of your Ansible scripts, Bash scripts, and network diagrams to the repository, and sync it again with the cloud.

•	When everything is synced, you will update the GitHub README file, which will explain each of the items in the repo, and display a network diagram. You will then have a GitHub repository to present to future employers.

You will also use your GitHub account for other activities in the course.

Required Files

•	Ansible YAML scripts from the Cloud Security Unit.

o	Gather all of your Ansible YAML scripts from your Ansible container on your jump box.

o	Copy and paste these into new documents on your local machine.

•	Bash scripts from the Linux System Administration Unit.

o	Gather all of your system configuration scripts you created during the Linux weeks.

•	Network diagrams from the Cloud Security and Networking Units.

o	Gather all of the network diagrams you created during the weeks on cloud security and networking.


Steps used to complete task:

Day 1: ELK Installation

1.	I used my personal microft Azure account trial to create 3 VM’s
2.	I create a new vNet located in the same resource group I’ve been using located in a new region and not the same region as my other VM's.
3.	I created a Peer connection between my vNets. This allows traffic to pass between my vNets and regions. This peer connection will make both a connection from my first vNet to my Second vNet And a reverse connection from my second vNet back to my first vNet. This will allow traffic to pass in both directions.
4.	I navigated to 'Virtual Network' in the Azure Portal. 
5.	I selected my new vNet to view it's details.
6.	Under 'Settings' on the left side, I select 'Peerings' and clicked the + Add button to create a new Peering.
7.	My new peering had a unique name of the connection from my new vNet to my old vNet.
8.	Choose my original RedTeam vNet in the dropdown labeled 'Virtual Network'. This is the network I was connecting to my new vNet and I only had one option.
9.	I named the resulting connection from my RedTeam Vnet to my Elk vNet “Red-to-ELK”.
10.	I SSHed into my Jump-Box using ssh azadmin@40.71.216.54
11.	I used sudo docker container list -a to display my Ansible container list.
12.	I started and connected to the Ansible container.
13.	I copied the SSH public key from the Ansible container on my jump box and created a new VM with this SSH key.
14.	I added my new VM to the Ansible hosts file.
15.	I created a new Ansible playbook to use for my new ELK virtual machine.
16.	 I created myplaybook.yml file to install docker.io, python3-pip and docker on each VM.
17.	After Docker was installed, I download and ran the sebp/elk:761 container.
18.	On Azure I created an incoming rule for my security group that allows TCP traffic over port 5601 from my IP address.
19.	I loaded ELK stack server from your browser at http://40.71.216.54:5601/app/kibana


Day 2

1.	I went to http://40.71.216.54:5601/app/kibana 
2.	On the ELK server homepage I clicked on add log data > chose system logs > clicked on DEB tab under Getting Started to view the correct Linux Filebeat installation instructions.
3.	I opened a terminal and SSH into my jump box, started my ansible container and SSHed into the Ansible Container. 
4.	I used curl curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat >> /etc/ansible/filebeat-config.yml and modified the filebeat-config.yml file with the correct IP addresses.
5.	I installed dpkg -i filebeat-7.4.0-amd64.deb
6.	I copied the Filebeat configuration file from my Ansible container to my WebVM's where I just installed Filebeat.
7.	I ran the filebeat modules enable system command.
8.	I ran the filebeat setup command.
9.	I ran service filebeat start command to enable the filebeat service to boot.
10.	On kibana I scrolled to the bottom and clicked on Verify Incoming Data.
11.	I followed the same steps to download metricbeat on all of the VM’s as well.


Day 3

1.	I explored Kibana to review the data collected through the ELK stack and Metricbeat.


