## Deployment of Jenkins slave with Ansible

### Control machine requirements:

- Requires Ansible 1.2 or newer
- Expects Ubuntu 12.04 Server or Desktop
- Requires 'git'
- Requires 'sshpass'

Currently Ansible can be run from any machine with Python 2.6 installed

### Managed node requirements:

- Expects Ubuntu 12.04 Server x86_64
- Expects Python 2.6 to be installed
- Requires 'openssh-server' installed

### Installing the control machine:

	sudo apt-get install ansible sshpass git

### Deploying Jenkins slave node:


On the control machine - clone this repository from where it is, for example:

	git clone git@github.com:andybondar/ansible-playbook.git
	cd ansible-playbook

Edit the "hosts" inventory file to set up the hostname or/and IP address, SSH user name, SSH user password and sudo user password of the machine on which you want Jenkins slave node environment deployed, for example:

	[jenkins-slave]
	10.0.0.1
	
	[jenkins-slave:vars]
	ansible_ssh_host=10.0.0.1
	ansible_ssh_port=22
	ansible_ssh_user=master
	ansible_ssh_pass=master
	ansible_sudo_pass=master


Finally - run ansible-playbook:

	ansible-playbook -i hosts install.yml

After playbook finish working Jenkins slave node environment is completely deployed. Now you can connect it to Jenkins master as a new node.

P.S. 

### Installing Oracle JDK7 manually on Ubuntu 12.04

	sudo apt-get install python-software-properties
	sudo add-apt-repository ppa:webupd8team/java
	sudo apt-get update
	sudo apt-get install oracle-java7-installer
