# Lab 1 - Useful Commands

### Without docker-compose containers running

1) Composer Install

       docker run -it  -v $(pwd):/app/ -v ~/.composer/:/root/.composer/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'composer install'

2) ECE-Tools from `vendor/bin/`

       docker run -it  -v $(pwd):/app/ magento/magento-cloud-docker-php:7.3-cli-1.1 bash -c 'vendor/bin/ece-tools'

### After containers are running

1) Composer Install

       docker-compose run deploy 'composer install'

2) bin/magento Command

       docker-compose run deploy 'bin/magento'

3) Get a Bash Shell

       docker-compose run deploy bash

4) Deploy Magento

       docker-compose run deploy cloud-deploy

5) Fix Permissions

       sudo chown -R webuser. . ~/.composer/

6) Get to Log Files

       docker-compose logs -f fpm  # any container name from docker-compose.yaml will do
