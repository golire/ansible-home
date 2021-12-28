## Ansible home automation

### Ansible user setup

#### Real server
- Install Ubuntu manually. SSH must be enabled and a user with sudo rights must exist.
- Edit `inventory.ini` - register newly deployed server there
- Execute `init_user.yaml` to create ansible operations user:
    ```bash
    # execute on host pce-lvm using "first_user" with and ask for password (for ssh login and sudo)
    ansible-playbook init_user.yaml -l pce-lvm -u first_user -k -K
    ```

#### Vagrant test instance
- Configure vagant instance so that it has fix IP address assigned
- Spin up test instance using vagrant
- Update `init_inventory.ini`, add/edit vagrant instance, it's fix IP
- Execute `init_user.yaml` to create ansible operations user:
    ```bash
    ansible-playbook -i init_inventory.ini  init_user.yaml -l unode1
    ```

### Server configuration
Execute `server.yaml` to configure server. Vault password must be available in `vault_pass.txt` file.
```bash
ansible-playbook server.yaml --vault-password-file vault_pass.txt -l unode1
```

### Secrets
Secrets are stored using ansible-vault. Operations:
- Encrypt
```bash
ansible-vault encrypt ./group_vars/all/vault.yaml
```
- Decrypt
```bash
ansible-vault decrypt ./group_vars/all/vault.yaml
```
- Inplace edit
```bash
ansible-vault edit ./group_vars/all/vault.yaml
```

### Roles
Initialize a new role structure:
```bash
ansible-galaxy role init --init-path './roles' role_name
```
