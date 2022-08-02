# ansible

Ansible is an openSource and free tool to perform configuration management majorly and the latest version of it is 5    .
But we will be using 2.9, which is the 1 level behind latest.

### Sample Usage :

```
[centos@ip-172-31-24-198 Ansible ~]$ ansible -i hosts all -u centos --private-key=~/.ssh/id_rsa -m shell -a "df -h"
    172.31.84.5 | CHANGED | rc=0 >>
    Filesystem      Size  Used Avail Use% Mounted on
    devtmpfs        471M     0  471M   0% /dev
    tmpfs           495M     0  495M   0% /dev/shm
    tmpfs           495M   13M  482M   3% /run
    tmpfs           495M     0  495M   0% /sys/fs/cgroup
    /dev/xvda1       10G  1.6G  8.5G  16% /
    tmpfs            99M     0   99M   0% /run/user/1000
    tmpfs            99M     0   99M   0% /run/user/0
    172.31.82.111 | CHANGED | rc=0 >>
    Filesystem      Size  Used Avail Use% Mounted on
    devtmpfs        471M     0  471M   0% /dev
    tmpfs           495M     0  495M   0% /dev/shm
    tmpfs           495M   13M  482M   3% /run
    tmpfs           495M     0  495M   0% /sys/fs/cgroup
    /dev/xvda1       10G  1.6G  8.5G  16% /
    tmpfs            99M     0   99M   0% /run/user/1000
    tmpfs            99M     0   99M   0% /run/user/0

```

### Important Points :
```
-i  : Inventory file : file with the list of IP Address of the nodes needed configuration Management
all : All is the default group in the hosts file which includes everything 
-u  : User with which account you want to connect 
-m  : module
-a  : argument
```

### Ansible can be utilized in 2 ways :
```
1) Manual Approach        : $ ansible -i hosts all -u centos --private-key=~/.ssh/id_rsa -m shell -a "df -h" :  
                             with manual approach, you can execure one command at a time.
2) Automated Approach     : PLAYBOOK : With playbooks ,we can execute n numbers of tasks on n number of machines in a shot
   ( Suggested )
```

### Ansible Playbook uses YAML as the language :

```
What is YAML ?  YA Markup Language : A presentation language is referred as markup language.

    Ex : XML , HTML  . . ,

Again YAML is declarative , DSL 
```

### We will start with YAML basics from tomorrow.


### YAML Basics

```
YAML is all about , DICTIONARY & LIST 

A Key value part is referred as DISTIONARY or a HASH

name: ManuVerma


A Key, which is having more than one value is referred as list. A Playbook is a list of plays and that's why playbook always start with - 

- name:
    lastName: Verma
    JobLocation: Bangalore

```


### Modules

```
Ansible is all about modules. You name a task it will have an modeule

Ex: yum , service, file , packge, archive

```


### Fact

```
FACT is a property of the remote node. Whenever you run any playbook, `ANSIBLE` gathers the FACTS of all the remote machines, before it executes the tasks.
This ways it comes to know whether it has to do the task or not.

Like if you ask to install some XYZ, it don't have to go and check and then install.
During facts itself it has that info and if that XYZ is alreayd, it will just `SKIP`

# This will show you the list of all the FACTS that ANISBLE is collecting during the PLAYBOOK execution

$ ansible all -m setup
```


In ansible, if any TASK fails, the subsesequent tasks will be failed or the playbook will be aborted in between

### Privilege Escalation 


### As per Ansible, Code should STRUCTURED and should be in a resuable format and this can only be achieved if you ROLES

```
Ansible Roles, helps you to organize the code as per that it does

1) This helps you in organizing the code
2) You can keep the code dry
3) Code can be reused.

```

### Role directory structure :
An Ansible role has a defined directory structure with eight main standard directories. You must include at least one of these directories in each role. You can omit any directories the role does not use. For example:

```
site.yml
webservers.yml
fooservers.yml
roles/
    common/
        tasks/
        handlers/
        library/
        files/
        templates/
        vars/
        defaults/
        meta/
    webservers/
        tasks/
        defaults/
        meta/
```


### Ansible-Pull

```
For pull to work, ensure you have GIT & ANSIBLE installed in the machine where you're running ANSIBLE-PULL.

At the moment, ansible-pull can only pull playbooks from GIT.

```

### Ansible-Vault :
```
This hels you in ensuring a password is been setup to trigger any plabook and restricts the plan text format of the playbook

$ ansible-vault encrypt 13-role-dependencies.yml  # Encrypts the playbook

$ ansible-playbook 13-role-dependencies.yml --ask-vault-pass    # Prompts for the password to run the playbook

$ ansible-vault decrypt 13-role-dependencies.yml   # Decrypt the playbook 

```

### This is to demonstrate git
## This will recorded in the git