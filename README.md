# Docker Base

Docker Base setup with a 
- deployer / sudo user
- ufw firewall
- Docker Engine and Docker Compose

This base is created as an Ansible book so Laradock and the Laravel app of choice can be added to an Ubuntu 18.0.4 image with basic setup done. With this setup you can deploy as a web user with ssh access. You can also use the same user used for deployment as an admin user. You could of course set up a secondary admin user as well, but I have decided to not do that just yet.
