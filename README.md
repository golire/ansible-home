### Ansible home automation

Install Ubuntu manually. SSH must be enabled and a user with sudo rights must exist.
Execute `init_user.yaml` to create ansible operations user:
```bash
# execute on host pce-lvm using first_user with and ask for password (for ssh login and sudo)
ansible-playbook init_user.yaml -l pce-lvm -u first_user -k -K
```

Execute `server.yaml` to configure server. Vault password must be available in `vault_pass.txt` file.
```bash
ansible-playbook server.yaml --vault-password-file vault_pass.txt -l unode1
```

#### Secrets
Secrets are stored using ansible-vault. Operations:
- Encrypt
```
ansible-vault encrypt ./group_vars/all/vault.yaml
```
- Decrypt
```
ansible-vault decrypt ./group_vars/all/vault.yaml
```
- Inplace edit
```
ansible-vault edit ./group_vars/all/vault.yaml
```
