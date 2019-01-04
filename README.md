# Docker Base

Docker Base setup Ansible Playbook to get you quickly up and running with server basics to run your Docker containers on. This Playbook has: 
- deployer / sudo user
- ufw firewall
- Docker Engine and Docker Compose
- Swapfile
- Deployment

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

## Deployment

We have introduced a new deployment role based on made by Blacklight. This should allow us to mimick Deployer and deploy without interruption using releases.

### Vars

**laravel_root_dir** (Required) - The root directory of the project.

**laravel_repo** (Required) - The URL to the repo containing the application code.

**laravel_branch** (Defaults: master)- The branch that you would like to deploy.

**laravel_strategy** (Defaults: git)- The deployment strategy to use. Available options: git, svb, mercurial, rsync, archive

**laravel_local_root** (Defaults: /) This option is only used when deploying via Rsync. It defines the path to the local folder to upload to the server.

**NB** The path is relative to your playbook file.

**laravel_composer_install:** defaults to true

**laravel_composer_path** (Defaults: false) -The path to an existing composer installation. If set to false, the role will automatically download composer into the projects root directory.

**laravel_composer_options** (Defaults: --no-dev --no-interaction --optimize-autoloader) -Flags to add to the composer install command.

**laravel_php_path** (Defaults: /usr/bin/php) -The path to PHP. This is only used when the role has to download composer.

**laravel_releases** (Defaults: 5) The amount of releases to keep in the releases directory.



## FYIs

Post deployment you do need to do a `composer install` and `npm install` inside the Laradock workspace . Access it using `docker-compose -f prod-docker-compose.yml  exec --user=laradock workspace bash` . We are working on avoiding this altogether with `docker exec` or `docker-compose exec..`

