# Docker Base

Docker Base setup Ansible Playbook to get you quickly up and running with server basics to run your Docker containers on. This Playbook has: 
- deployer / sudo user
- ufw firewall
- Docker Engine and Docker Compose
- Swapfile

## Ubuntu 18.0.4
This base is created as an Ansible book so Laradock and the Laravel app of choice can be added to an Ubuntu 18.0.4 image with basic setup done. This version is also the latest Docker can work with at the moment. We tend to set up a Digital Ocean Droplet with Ubuntu 18.0.4 and attach our own id_rsa public key to it so we have a root user with our SSH key up and running. From there on you can use this playbook.

## Deployment User
An extra user for deployment and sudo tasks is setup using the Ansible User module. With this setup you can deploy as a web user with ssh access. You can also use the same user used for deployment as an admin user. You could of course set up a secondary admin user as well, but I have decided to not do that just yet.

## Docker and Docker Compose

Both Docker and Docker Compose are setup with Geerlingguy's Docker role. You can adjust the composer version in the `server.yml` where it currently overrides the default version.

## Swapfile

We use Oefenweb's Swapfile to add more memory to the server. This way we can keep on using the cheap $5 / month Droplet and run composer and so on without issues.

## Variables

Do not forget to add `group_vars/all.yml`. Here are example vars you can adjust:
- upassword: password
- web_user: web
- github_keys: https://github.com/jasperf.keys

# Deployment

We have added a basic deployment from Github repo as well. You can simply do this using this command `ansible-playbook deploy.yml` This as we could not with ease use deployer for the current setup. Base server does not run PHP, a container does. As Deployer has no solution for this yet we will use Ansible deployment for now.

Post deployment you do need to do a `composer install` and `npm install` inside the Laradock workspace . Access it using `docker-compose -f prod-docker-compose.yml  exec --user=laradock workspace bash`

