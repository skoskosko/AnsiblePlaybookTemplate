# Ansible-Playbook Template

This repository is meant to provide very simple working template that can be used for larger ansible projects

You need docker and ansible installled to try all the features.

Either is enough for testing

## Getting started 

- Change ip adrresses in hosts file
- set correct users in hosts file

inventory/hosts and inventory_docker/hosts (docker one is only for docker)

### locally

- install ansible
- check that your ssh key can access all the hosts

run ansible playbook
```bash

ansible-playbook -i inventory/hosts playbook.yml --extra-vars "my_runtime_var=set_at_runtime"

# Test it using remote host

ansible-playbook -i inventory/hosts playbook.yml --extra-vars "my_runtime_var=now_different variable_host=remote"


```

### in docker

- install docker

To run ansible inside docker you need to provide it with ssh keys to your remote servers. 

- Copy your ssh pirvate key file with to your local workdir. Name it id_rsa

```bash
cp ~/.ssh/id_rsa ./id_rsa
```

Rember never to share this container with anyone, or run it in an environment where someone else can access it, at the risk of loosing your private key!

```bash
docker build -t playbook .
docker run playbook
# inventory setting is not needed because your hosts file is enabled globally
docker run playbook ansible-playbook playbook.yml --extra-vars "my_runtime_var=now_different_and_in_docker variable_host=remote"

```



## What is the playbook doing

- Testing connection to your local computer (localhost  is not used to allow usage from  a docker container)
- Debugging my variables
- Listing items in your home directory
- Saving them to array and printing them

## Installing ansible on ubuntu

```bash

sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible

```

## Things to consider

This only gives an template for very basic usage of ansible. 
