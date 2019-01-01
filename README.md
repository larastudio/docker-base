# Docker Base

Docker Base setup with: 
- deployer / sudo user
- ufw firewall
- Docker Engine and Docker Compose

## Ubuntu 18.0.4
This base is created as an Ansible book so Laradock and the Laravel app of choice can be added to an Ubuntu 18.0.4 image with basic setup done. This version is also the latest Docker can work with at the moment.

## Deployment User
An extra user for deployment and sudo tasks is setup using the Ansible User module. With this setup you can deploy as a web user with ssh access. You can also use the same user used for deployment as an admin user. You could of course set up a secondary admin user as well, but I have decided to not do that just yet.

## Docker and Docker Compose

Both Docker and Docker Compose are setup with Geerlingguy's Docker role. You can adjust the composer version in the `server.yml` where it currently overrides the default version.

## Variables

Do not forget to add `group_vars/all.yml`. Here are example vars you can adjust:
- upassword: password
- web_user: web
- github_keys: https://github.com/jasperf.keys

