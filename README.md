# ansible

## Ansible: A CM Tool and the latest version of 6.0

Ansible 6.0 is python 3 based and installation of python 3 is needed.
```
Installation : https://gitlab.com/thecloudcareers/opensource/-/tree/master/lab-tools 
```


### Inventory File : This is the file which we supply ansible the list of DNS Names or IP's on the machine that you would like to
do that configuration management. The default group in this file is `all` which included all the DNS or IP's that you supplied.


### Ansible can be operated in 2 ways
```
    * Manual way     ( Executing the commands and can work one command at a time )
    * Automated way  ( Using Ansible Playbook )
```

### Sample Ansible Manual Command:

```
ansible all -i inv -e ansible_user=centos -e ansible_password=DevOps321 -m shell -a "df -h"

-i               : Inventory file 
all              : group name 
ansible_user     : Username which ansible uses for authentication 
ansible_password : Password which ansible uses for authentication 
-m               : Module 
-a               : argument
-e               : extra arguments

PS : ansible --help gives you all the latest and greatest option of that time

```


### Pre-Requisites:
    * The very first thing we need to ensure that ANSIBLE works is : SSH. Your Ansible should be able to SSH to the enteries   mentioned in your inventory file

### Playbooks is nothing but your ansible scripts which are writtent on YAML

YAML: This is just a mark up language ( Markup Language is nothing but presentation language )

Abbrevation of YAML : Yet Another Markup Language.


# YAML Basics :
```
    * Dictionary : A Key Value Pair is called as dictionary 
    * List       : A Key with multiple values is called as a list 
    * Map        : A Key with multiple key value pairs is referred as MAP
```

PS : YAML is intendation specific ( spacing matters )


### What is a playbook in ansible ???

```
Playbook is a list of plays.
What is play ? A Play is a list of tasks!!
What is task ? A Task is an action or actions that you wish to do!

```

Ansible playbooks should always ends with .yml or .yaml. Anything apart from that won't be considered.

### How do you run the playbooks ?

```

ansible-playbook -i inv -e ansible_user=centos -e ansible_password=DevOps321 01-sample.yml
ansible-playbook -i inv -e ansible_user=centos -e ansible_password=DevOps321 -e COMPONENT=catalogue roboshop.yml


``` 

# FORLOOP:
```
for i in mongodb catalogue redis cart user mysql shipping frontend; do ansible-playbook -i inv -e ansible_user=centos -e ansible_password=DevOps321 -e COMPONENT=$i roboshop.yml; done

With Environments,

git pull ; for i in mongodb catalogue redis cart user mysql shipping rabbitmq payment frontend; do ansible-playbook -i dev-inv -e ansible_user=centos -e ansible_password=DevOps321 -e ENV=dev -e COMPONENT=$i roboshop.yml; done

```

### Command to encrypt a string in ansible 

```
 ansible-vault encrypt_string abc123
```

### Command to run an encrypted playbook 

```
ansible-playbook --ask-vault-password 12-secret.yml
```



### Ansible-Pull

For ansible pull to work you need to ensure that the machine which executes the pull command has ANSIBLE Installed on the machine.

```
ansible-pull -U https://github.com/b50-clouddevops/ansible.git -e COMPONENT=frontend -e ENV=dev roboshop-pull.yml
```

## Ansible Tags 

```
ansible-playbook 13-tags.yml  --skip-tags  web
ansible-playbook 13-tags.yml  -t web
```


### Test Commits for the ansible-pull 
Ansible pull needs ansible to installed and ensure version6 is the installed version


# How to create an AMI with ANSIBLE ?
1) Launch the machine with our lab image 
2) Install ansible with curl command and also install boto : $ sudo pip3 install boto
3) Once Installed , make an AMI and ensure that comes to available state 
4) Going forward for all the machines that needs needs ansible use this AMI....
