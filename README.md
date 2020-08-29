# Ansible Roles

## Setup
clone all roles to ansible roles
```shell
git clone https://github.com/amir2b/ansible-roles.git /etc/ansible/roles/
```
Or copy any role you want to `/etc/ansible/roles/`

## Example

Show all server details by command
```shell
ansible all -m include_role -a name=details
```
use in playbook.yml
```yaml
- name: Install docker
  hosts: all
  become: true
  roles:
    - update
    - docker_setup
```
