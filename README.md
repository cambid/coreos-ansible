
# README
## Requirements
- Vagrant
- Ansible
- Vault from https://www.vaultproject.io/

## Setup vault for development
```
vault server -dev
export VAULT_ADDR='http://127.0.0.1:8200'
vault write secret/hello value="TEST"
```
