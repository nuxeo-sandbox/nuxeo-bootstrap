# Nuxeo project bootstrap

This sample projects aims at providing a full Nuxeo sample project, focusing on QA and DevOps. This project may be a good starting point if you want to build you own Nuxeo Project.

## Targets

### Deployability

When you start your project, you should be able to deploy it, that's why the first thing here is to be able to deploy with [Vagrant](https://www.vagrantup.com/) which is then provisionned with [Ansible](http://www.ansible.com/home).

So to test your project, the only thing you have to do is :

  ansible-galaxy install -r requirements.yml
	vagrant up

After the deployment, you should be able to browse your Nuxeo instance at [http://192.168.33.10]() on a fresh Ubuntu server. The components installed are :

  * Java 8
  * Apache as a reverse proxy
  * PostgreSQL
  * Elasticsearch
  * Redis
  * Nuxeo

For more complex deployment scenario, just have a look at the [documentation](ansible/README.md) in the ansible directory.

TODO: use maven plugin to use vagrant

### Testability

#### Unit Tests

In progress

#### Functionnal Tests

In progress

#### SBE Tests

In progress


