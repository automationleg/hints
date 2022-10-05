# How to use Ansible

## Installation
### Red Hat
1. On host that is going to be used to provision other hosts
```
sudo yum install epel-release
sudo yum install ansible
```

2. Create 'ansible' user on both provisioning host and remote hosts
```
sudo useradd ansible
sudo passwd ansible
```

3. Configure ssh keys on host to login to remote machines
```
sudo -i -u ansible
ssh-keygen (accept default options)
ssh-copy-id remote-host
```
4. Configure permissions on remote hosts so we ansible may sudo without password
On remote hosts
```
sudo visudo
```
Add text at the end
```
ansible ALL=(ALL) NOPASSWD: ALL
```
5. Test with simple playbook if all works
Example playbook
```
--- # install git on target host
- hosts: workstation
    become: yes
    tasks:
    - name: install git
    yum:
        name: git
        state: latest
```
Execute:
```
ansible-playbook -i inventory myfile.yml
```

