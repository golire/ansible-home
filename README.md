### Ansible home automation

Install Ubuntu manually. SSH must be enabled and a user with sudo rights must exist.
Execute `init_user.yaml` to create ansible operations user:
```bash
# execute on host pce-lvm using first_user with and ask for password (for ssh login and sudo)
ansible-playbook init_user.yaml -l pce-lvm -u first_user -k -K
```
