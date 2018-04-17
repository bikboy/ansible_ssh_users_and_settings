# Ansible playbooks for ssh custom settings and adding necessary users
## Prerequisites
### 1. you need to have ansible version >= 1.6
### 2. prepare file vars/creds.yaml with your login and pass to our webdav(pub keys storage) and encrypt it with ansible vault:

`ansible-vault create vars/creds.yml`
and add there:
```
url_user: <username>
url_pass: <password>
url_webdav: <url for webdav server with public keys>
```
### 3. edit users files: `vars/techops.yml` and `vars/users.yml`
add necessary users to "techops_users" if you want to add this user or add necessary username to "disabled_techops_users" to disable this user

## create inventory file with necessary hosts (optional)
in format:
```
all:
  hosts:
    <IP>:
      ansible_user: ubuntu
      ansible_ssh_private_key_file: <path to private key>
```

## Run
### setup SSH (security settings and port change)
`ansible-playbook setup_ssh.yml -i "<inventory_file_name>"`
### add/disable users
`ansible-playbook manage_user.yml -i "<inventory_file_name>" --ask-vault-pass`
