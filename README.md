# Ansible role to add new user!

Here we create an ansible role for add new user on system!

## Installation

First i have installed ansible

```bash
sudo apt install ansible
```

## Script=>Playbook=>Automation

First create a directory (ansible_user_add). In it, create a directory and name it roles

```bash
mkdir roles
```
After, create a empty directory (role main directory) in roles directory
```bash
cd roles
mkdir add_user
```
Now we can create all the other required folders and files for role
```bash
cd add_user
ansible-galaxy init test-role-1
```
### Scripting
Now we can write playbook!

To do that, first edit the [add_user/tasks/main.yml]() file
```yml
---
# tasks file for create user
- name: create user jongeek
  user:
    name: jongeek
    shell: /bin/bash
    state: present
    group: root
    password: '$6$zRbpHzlSfVAqe2c$KzEX.mTTJXpIggGOvZGv2AH3/lhZj7zFaZZb9wSPqUHj7a.VHuIwkEnZNBuo7wK/zMAVB9L6Kln1c2PSEcLI41'
    createhome: yes
    home: /home/jongeek
```
We use the user ansible to create a user. name parameter is the username, shell is the shell associated to user(For login), password is the encoded password with(mkpasswd)
```bash
sudo apt install whois
mkpassd --method=sha-512
```
To more information, go here [link](https://docs.ansible.com/ansible/latest/modules/user_module.html)
Now go to root project directory and create playbook.yml file wit content
```yml
---
- hosts: desktop
  name: Add user role
  remote_user: geek
  become: true


  roles:
    - add_new_user
```
This is the playbook it will call roles prevouisly created in <roles> directory add_user.

After create a hosts.ini file in the same directory.
```
[desktop]
127.0.0.1 ansible_connection=ssh ansible_user=<remote user> ansible_ssh_pass=<remote_pass>
```
Is the inventory file

Now run our playbook.
```bash
sudo ansible-playbook -i hosts.ini playbook.yml --become 
--ask-become-pass
```
## Tutorial
[Create playbook](https://docs.ansible.com/ansible/latest/network/getting_started/first_playbook.html)
[User module](https://docs.ansible.com/ansible/latest/modules/user_module.html)

[Tutorial user module](https://serversforhackers.com/c/create-user-in-ansible)

[Create role](https://galaxy.ansible.com/docs/contributing/creating_role.html)

[Create inventory file](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
