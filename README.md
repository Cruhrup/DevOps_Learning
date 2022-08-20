# Ansible
Agentless, simple python library and very simple Config Mgmt System (CMS), uses SSH for linux, Winrm for Windows and API for Cloud (IMPORTANT for WHERE to install dependencies)\
Ansible simply sends a python script to the machine, executes, and returns the output\
Written in YAML, INI or text format with output being in json\
Inventory - Target machine information (/etc/ansible/hosts) (create one in working dir)\
Modules - Tasks to do\
Playbook - Tie inventory to module for target and send (what do you want to do and where)
NOT ideal for Cloud, use TF instead\
Edit global config file to decline host_key_checking
```
group:children - group of groups [group:children] then name groups below
group:vars - variables for the group such as ansible_user
see inventory file for examples on this

-m - module flag to pass (i.e ping to check inventory availability, yum to install pkg)
-a - arguments to pass to the module
-i - inventory file name/location (if not set in ansible.cfg in working dir)

Ansible-playbook <name of playbook> –syntax-check - do syntax check on playbook
Ansible-playbook -i inventory playbook.yaml - run playbook with this inventory file
```
Basic Playbook Format
```-hosts: name_of_host_in_inventory_file
 Tasks:
    -name: Install Apache or any name you want for this task
      Yum: ←name of module you want to run
        Name: httpd ←args to pass to module
        State: latest
```
There are a LOT of modules, just look up module in doc and learn to use as necessary\
Ansible.cfg is default config file to change how Ansible acts, can create one in working dir to overwrite the settings\
Variables can be set in playbook using ```vars:``` and calling variables via ```“{{variable_name}}”```
- Set in group_vars/all for all hosts, group_vars/groupname or host_vars/hostname paths
- Vars in playbook have highest priority and will be checked FIRST, then host_vars, then group, and then all
- Can store task output into a variable
- Fact variables are run by default on each host with various parameters being returned, you can grab these vars as well

Loops are amazing at doing multiple things in the specified list and can be returned via "{{item}}" variable (see provision.yml for exmaple)\
Multiple values can be used in loops in dictionary format shown below:
```
Name: "{{item.name}}"
Groups: "{{item.group}}"
Loop:
  - { name: 'bob', groups: 'wheel' }
```
Handlers are used to run tasks ONLY when a change is made (i.e only restart service if another task changed) (see provision.yml for example)\
Roles simplify playbook content by distributing it across directories to be used at an org level (see roles dir and provision_roles.yml)\
Galaxy.ansible.com has a lot of pre-defined community roles you can use\

