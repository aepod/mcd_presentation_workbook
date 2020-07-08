# Lab 1 - Full Setup Instructions

This is not part of the lab, it is meant to give full reference on how the tgz file was created. 

1)  Create the project 

        docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition magento-ce'

2)  Add the Magento Cloud Docker Repository and ECE Tools

        docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer config repositories.mcd vcs git@github.com:magento/magento-cloud-docker.git'

        docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer config repositories.et vcs git@github.com:magento/ece-tools.git'

        docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer require "magento/magento-cloud-docker:1.1" "magento/ece-tools"'

3)  Copy files from https://github.com/magento/magento-cloud

        .magento/ (entire folder)
        .magento.app.yaml
        magento-vars.php
        php.ini

4)  Create the docker-compose config and bring up instances

        docker run -it -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c "./vendor/bin/ece-docker build:compose --sync-engine=native --mode=developer"
        docker-compose up -d

5)  Optionally, add sample data

        docker-compose run deploy php -dmemory_limit=4G bin/magento sampledata:deploy

6)  Deploy and automatically install

        docker-compose run deploy cloud-deploy
        

## Modification

##### Added database dump

The database was dumped to `.docker/mysql/docker-entrypoint-initdb.d/m2ce-demo.sql`

This is inserted when the database comes up, and is much quicker than a full install from scratch. The database itself is not changed.

The dump was generated using n98-magerun2:

        docker-compose run deploy var/n98-magerun2 db:dump .docker/mysql/docker-entrypoint-initdb.d/m2ce-demo.sql

With this change the app/etc/env.php was left in place as well, for the crypt key.

##### Added n98-magerun2 to var/

This was added for convenience. This can be run easily using `docker-compose run deploy var/n98-magerun2 [cmd]`

##### Fix for magento-vars.php function declared issue

Removed code here, this is just used for multi-store, setting the proper store code is done in this file.
         
