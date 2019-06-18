# On the VM / Remote (Ubuntu based but could work on other Debian systems)

Ansible script to get a simple instance of DHIS2 configured on a VM with Nginx (with Letsencrypt), Tomcat, and Postgresql.

## Install Python

```
sudo apt-get install python
```

# On the local machine

## Install ansible

```
brew install ansible
```

or install using pip.

## Install anisble galaxies (open source playbooks from other devs)

```
ansible-galaxy install geerlingguy.postgresql
ansible-galaxy install idealista.tomcat-role
```

## Setup the ansible playbooks

There's a file called `all-playbooks.yml` which basically runs through all the individual playbooks

```
---
- import_playbook: server.yml
- import_playbook: database.yml
- import_playbook: tomcat.yml
- import_playbook: nginx-from-source.yml
- import_playbook: nginx-playbook.yml
```

## Setup your inventory

Define the hostname and user of the server you're deploying to in the your inventory `_dhis2-server-credentials.ini`

## Configure postgresql and tomcat

Review `vars/main.yml` make sure you define postgresql and tomcat passwords.

## Run ansible

You can either run the individual playbooks in the order defined in `all-playbooks.yml` or you can run them all in one go.

```
ansible-playbook -i _dhis2-server-credentials.ini all-playbooks.yml
```

